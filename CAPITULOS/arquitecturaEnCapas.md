> Les comparto un apunte que redacté originalmente como parte de mi ayudantía para la materia **Desarrollo de Software en la UTN FRBA**.
>
> Es una guía breve y práctica sobre cómo estructurar nuestro código para que sea más mantenible. Básicamente, trata sobre cómo identificar y desarmar el anti-patrón del _"Endpoint Omnipotente"_, repasando conceptos clave de diseño limpio (como Responsabilidad Única e Inversión de Dependencias) para finalmente refactorizar hacia una clásica **Arquitectura en Capas (Controller, Service, Repository)** con ejemplos reales. Espero les sea util!

---

# Arquitectura en Capas: De Código Acoplado a Sistemas Escalables

## Tabla de contenidos

- [El anti-patrón del Endpoint Omnipotente](#el-anti-patrón-del-endpoint-omnipotente)
- [Los tres pilares del diseño limpio](#los-tres-pilares-del-diseño-limpio)
  - [Separación de Responsabilidades (SRP)](#separación-de-responsabilidades-srp)
  - [Acoplamiento y Cohesión](#acoplamiento-y-cohesión)
  - [Inversión de Dependencias](#inversión-de-dependencias)
- [¿Qué define a una arquitectura en capas?](#qué-define-a-una-arquitectura-en-capas)
- [Anatomía del Sistema: Controller, Service y Repository](#anatomía-del-sistema-controller-service-y-repository)
- [De la teoría a la práctica](#de-la-teoría-a-la-práctica)
- [El valor de organizar la complejidad](#el-valor-de-organizar-la-complejidad)

---

## El anti-patrón del Endpoint Omnipotente

Muchos proyectos comienzan con una premisa simple: **"Necesito un endpoint que reciba datos, los guarde y responda"**. En JavaScript, esto es bastante sencillo de lograr gracias a frameworks como Express.

Pensemos en el requerimiento clásico de cualquier e-commerce:

> _"Como Vendedor de la plataforma, quiero poder dar de alta un producto para que esté disponible en mi catálogo"._

Una solución inicial sería algo como esto:

```javascript
app.post("/productos", async (req, res) => {
  try {
    const datos = req.body;
    const nuevoProducto = new Producto(datos);
    productos.push(nuevoProducto); // Simulamos bdd como array de objetos
    res.status(201).json(nuevoProducto);
  } catch (error) {
    res.status(500).json({ error: "Hubo un fallo al guardar" });
  }
});
```

A simple vista, el problema está solucionado. El código se despliega, los usuarios empiezan a crear productos y todo parece funcionar correctamente. Sin embargo, a los pocos días, empezamos a notar un catálogo descuidado: productos con precios negativos, stock incoherente o incluso artículos sin nombre. Ante esto, el cliente nos exige un nuevo requerimiento:

> _"Como Vendedor, quiero dar de alta un producto validando que el precio sea mayor a cero, el stock sea positivo y el nombre sea obligatorio"._

La respuesta inmediata del desarrollador suele ser arreglar el código existente:

```javascript
app.post("/productos", (req, res) => {
  try {
    const datos = req.body;

    // 1. Validamos que el título exista y no sea solo espacios
    if (!datos.titulo || !datos.titulo.trim() === "") {
      return res
        .status(400)
        .json({ error: "El producto debe tener un título válido" });
    }

    // 2. Validamos que el precio sea un número positivo
    if (datos.precio <= 0) {
      return res
        .status(400)
        .json({ error: "El precio debe ser un número mayor a cero" });
    }

    // 3. Validamos que el stock no sea un número negativo
    if (datos.stock < 0) {
      return res
        .status(400)
        .json({ error: "El stock inicial no puede ser negativo" });
    }

    // 4. Normalizamos el título
    const productoProcesado = {
      titulo: datos.titulo.trim(),
      precio: datos.precio,
      stock: datos.stock,
      fechaCreacion: new Date(),
    };

    productos.push(productoProcesado);
    res.status(201).json(productoProcesado);
  } catch (error) {
    res.status(500).json({ error: "No pudimos procesar tu alta" });
  }
});
```

Si comparamos esta versión con la anterior, empezamos a notar que la estructura está mutando. Lo que antes era un simple punto de entrada, ahora es un **Endpoint Todopoderoso**.

Sin darnos cuenta, nuestro endpoint empezó a "adueñarse" de responsabilidades que no le pertenecen:

- **Es un Validador:** Conoce las reglas del negocio (qué es un precio válido).
- **Es un Editor:** Se encarga de limpiar y normalizar los datos (como quitar espacios en los títulos).
- **Es un Gestor de Datos:** Sabe cómo manejar identidades y cómo persistir la información (actualmente en memoria).
- **Es un Comunicador:** Decide qué códigos de error HTTP devolver ante cada fallo técnico o de negocio.

Justo cuando creemos que tenemos todo bajo control, llega un requerimiento más:

> _"Si el stock inicial es mayor a 100 unidades, el producto debe marcarse automáticamente como 'Destacado' para resaltarlo en la tienda"._

```javascript
app.post("/productos", (req, res) => {
  try {
    const datos = req.body;

    // 1. Validaciones de integridad (Siguen acá...)
    if (!datos.titulo || !datos.titulo.trim() === "") {
      return res
        .status(400)
        .json({ error: "El producto debe tener un título" });
    }
    if (datos.precio <= 0) {
      return res.status(400).json({ error: "El precio debe ser mayor a cero" });
    }
    if (datos.stock < 0) {
      return res.status(400).json({ error: "El stock no puede ser negativo" });
    }

    // 2. NUEVA LÓGICA: Regla de "Destacado"
    // El controlador ahora decide el "marketing" del producto
    let esDestacado = false;
    if (datos.stock > 100) {
      esDestacado = true;
    }

    // 3. Procesamiento y creación del objeto
    const productoProcesado = {
      id: productos.length + 1,
      titulo: datos.titulo.trim(),
      precio: datos.precio,
      stock: datos.stock,
      destacado: esDestacado, // Guardamos la decisión tomada arriba
      fechaCreacion: new Date(),
    };

    productos.push(productoProcesado);
    res.status(201).json(productoProcesado);
  } catch (error) {
    res.status(500).json({ error: "Fallo crítico en el alta" });
  }
});
```

Aquí es donde el código se vuelve insostenible y la **deuda técnica** empieza a generar intereses. Antes de continuar con la solución, vale la pena frenar y analizar algunos conceptos concretos que explican por qué ese estilo de código se vuelve insostenible, y conocerlos nos va a permitir tomar mejores decisiones de diseño a futuro.

---

## Los tres pilares del diseño limpio

### Separación de Responsabilidades (SRP)

El **Principio de Responsabilidad Única**, conocido como SRP por sus siglas en inglés (_Single Responsibility Principle_), establece que un módulo debería tener una única razón para cambiar. Dicho de otra forma: cada pieza de código debería ocuparse de una sola cosa.

Cuando miramos nuestro endpoint, podemos identificar al menos cuatro razones por las que podría necesitar modificarse: cambia una regla de validación, cambia la forma en que se guarda el dato, cambia el criterio para marcar un producto como destacado, o cambia el código de error que debe devolverse ante cierto fallo. Cuatro razones de cambio en un solo archivo es una señal clara de que ese archivo tiene **demasiadas** responsabilidades.

La ventaja de respetar el SRP es directa: **cuando algo cambia, sabemos exactamente dónde ir**. No hay que leer cien líneas de código mezclado para encontrar el lugar correcto. Cada módulo tiene un propósito claro, y ese propósito no se mezcla con el de ningún otro.

### Acoplamiento y Cohesión

Estos dos conceptos funcionan mejor juntos porque son, en cierta forma, las dos caras de la misma moneda.

El **acoplamiento** mide cuánto depende un módulo de los detalles internos de otro. Un acoplamiento alto significa que un cambio en un lugar obliga a hacer cambios en otros lugares. En nuestro endpoint, la lógica de negocio está entrelazada con el manejo del protocolo HTTP y con la forma de persistir los datos. Si quisiéramos cambiar la base de datos, tendríamos que tocar el mismo archivo donde vive la regla del producto destacado. Eso genera un acoplamiento alto, y es exactamente lo que buscamos evitar.

La **cohesión**, en cambio, mide qué tan relacionadas entre sí están las responsabilidades de un módulo. Un módulo cohesivo es aquel donde todo lo que contiene tiene sentido junto. Un módulo con baja cohesión es un conjunto de funcionalidades sin un hilo conductor claro.

Lo que buscamos es siempre lo mismo: **bajo acoplamiento y alta cohesión**. Módulos que se ocupen de una cosa y la hagan bien, sin saber más de lo necesario sobre el resto del sistema. La arquitectura en capas es, en buena medida, una estrategia para lograr exactamente eso: cada capa tiene alta cohesión interna y se comunica con las demás a través de interfaces bien definidas, minimizando el acoplamiento.

### Inversión de Dependencias

Este es quizás el concepto más sutil de los tres, pero también uno de los más poderosos. El **Principio de Inversión de Dependencias** (_Dependency Inversion Principle_, o DIP) establece que los módulos de alto nivel no deberían depender de los módulos de bajo nivel. Ambos deberían depender de **abstracciones**.

Traducido a nuestro contexto: la lógica de negocio (alto nivel) no debería saber nada sobre cómo se persisten los datos (bajo nivel). No debería importarle si usamos una base de datos en memoria, MongoDB o PostgreSQL. Lo único que debería conocer es que existe algo capaz de guardar y recuperar productos, sin importar cómo lo hace por dentro.

Esto tiene una ventaja concreta y muy tangible: **podemos cambiar la implementación de una capa sin tocar las demás**. Si el día de mañana el cliente decide migrar de una base de datos a otra, el cambio queda completamente contenido en el Repository. El Service no se entera, el Controller no se entera, y las reglas de negocio permanecen intactas.

---

## ¿Qué define a una arquitectura en capas?

Con estos tres principios sobre la mesa, la arquitectura en capas empieza a tener mucho sentido. No es un patrón arbitrario ni una convención que alguien inventó por capricho: es la consecuencia natural de aplicar SRP, bajo acoplamiento y DIP a la organización de un sistema web.

La idea central es organizar el código en **grupos horizontales de módulos**, donde cada grupo —cada capa— agrupa responsabilidades afines y se comunica con el resto del sistema de manera controlada. Pero para que esto funcione, una capa tiene que cumplir tres condiciones:

- **Responsabilidad única y clara:** todo lo que vive dentro de esa capa comparte el mismo tipo de preocupación. Una capa no mezcla lógica de negocio con acceso a datos, de la misma forma que en un restaurante la cocina no atiende las mesas.

- **Interfaz definida:** una capa no expone sus entrañas. Ofrece un contrato claro hacia afuera: un conjunto de operaciones que las capas adyacentes pueden invocar, sin necesidad de saber cómo están implementadas por dentro.

- **Ignorancia hacia arriba:** una capa conoce únicamente a la capa inmediatamente inferior, pero es completamente ajena a todo lo que está por encima de ella. Esa ignorancia no es un descuido; es una decisión de diseño deliberada, y es la base del bajo acoplamiento que buscamos.

---

## Anatomía del Sistema: Controller, Service y Repository

Hasta acá definimos qué es una capa y qué condiciones tiene que cumplir. Ahora toca aterrizar eso en el ejemplo concreto. Para hacerlo, primero necesitamos conocer las tres capas que vamos a usar y entender el rol específico de cada una.

**Controller** es la puerta de entrada al sistema. Su única responsabilidad es recibir la petición HTTP, extraer los datos que vienen en ella y pasárselos a la capa siguiente. No sabe nada de reglas de negocio ni de cómo se guardan los datos. Habla el idioma del protocolo HTTP y solo ese.

**Service** es el corazón del sistema. Acá vive toda la lógica de negocio: las validaciones, las reglas, las decisiones. Es quien determina si un precio es válido, si un nombre es obligatorio o si un producto merece ser marcado como destacado. No sabe nada de HTTP ni de bases de datos. Su existencia radica en las reglas del negocio. Puede pensarse como un director de orquesta: no toca los instrumentos (no accede a la base de datos ni maneja el protocolo de comunicación), pero conoce la partitura completa y coordina a los músicos (el resto de componentes) para que la obra se ejecute correctamente. Es decir, conoce todos los pasos necesarios para cumplir con cierto requerimiento y se encarga de que se ejecuten en orden.

**Repository** es el único que sabe cómo persistir y recuperar datos. No conoce las reglas de negocio ni el protocolo por el que llegó la petición. Si mañana decidimos migrar de una base de datos en memoria a PostgreSQL, este es el único lugar del sistema que tiene que cambiar.

Ninguna capa puede saltarse a otra, y ninguna capa de nivel inferior conoce a las que están por encima de ella. Esa restricción no es burocracia: es lo que garantiza que el sistema pueda crecer sin convertirse en un nudo.

---

## De la teoría a la práctica

Volvamos a todo lo que nuestro endpoint hacía solo y distribuyámoslo donde corresponde.

El **Controller** se queda con lo mínimo indispensable: recibir el request HTTP, extraer los datos del body y pasárselos al Service. Cuando el Service termina, el Controller toma el resultado y decide qué código HTTP devolver: 201 si todo salió bien, 400 si hubo un error de validación, 500 si algo falló de forma inesperada. Nada más.

```javascript
export const postProducto = async (req, res) => {
  try {
    const datos = req.body;

    // El Controller le pide al Service que haga su trabajo
    const nuevoProducto = productoService.crearProducto(datos);

    // Todo bien -> 201 Created
    return res.status(201).json(nuevoProducto);
  } catch (error) {
    // Diferenciamos errores de negocio (400) de errores técnicos (500)
    if (error.message.startsWith("VALIDATION_ERROR")) {
      return res
        .status(400)
        .json({ error: error.message.replace("VALIDATION_ERROR: ", "") });
    }

    console.error(error);
    res.status(500).json({ error: "Fallo crítico en el servidor" });
  }
};
```

El **Service** hereda todo lo que antes estaba mezclado con el código de rutas. Es quien valida que el nombre no esté vacío, que el precio sea mayor a cero y que el stock sea un número positivo. Es quien decide si un producto con más de 100 unidades iniciales merece el flag de destacado. Es quien normaliza el nombre quitándole los espacios sobrantes. Toda esa lógica, que antes estaba dispersa entre condiciones y comentarios, ahora tiene un hogar fijo y predecible.

```javascript
export const productoService = {
  crearProducto: (datos) => {
    // 1. Validaciones
    if (!datos.titulo || !datos.titulo.trim()) {
      throw new Error("VALIDATION_ERROR: El producto debe tener un título válido");
    }
    if (datos.precio <= 0) {
      throw new Error("El precio debe ser un número mayor a cero");
    }
    if (datos.stock < 0) {
      throw new Error("El stock inicial no puede ser negativo");
    }

    // 2. Lógica de Marketing (asignación de 'destacado')
    let esDestacado = false;
    if (datos.stock > 100) {
      esDestacado = true;
    }

    // 3. Normalización y preparación del objeto
    const productoParaGuardar = {
      titulo: datos.titulo.trim(),
      precio: datos.precio,
      stock: datos.stock,
      destacado: esDestacado
    };

    // 4. Delegamos la persistencia al Repository
    return await productoRepository.save(productoParaGuardar);
  }
};
```

El **Repository** hace una sola cosa: toma el producto que el Service ya validó y procesó y lo persiste. No sabe si el producto es destacado por regla de negocio o por capricho del cliente. No sabe si vino de un endpoint HTTP, de un proceso batch o de una consola de administración. Eso no es su problema, y está bien que no lo sea.

```javascript
export const productoRepository = {
  save: async (datosProducto) => {
    const nuevoProducto = new ProductoModel(datosProducto);
    return await nuevoProducto.save();
  },
};
```

---

## El valor de organizar la complejidad

Si miramos hacia atrás y retomamos los tres problemas que identificamos al principio, podemos ver cómo la arquitectura los resuelve uno a uno.

**La lógica ya no es invisible.** Antes, las reglas de negocio estaban sepultadas entre código de rutas y queries a la base de datos. Ahora tienen un hogar fijo: el Service. Cualquier desarrollador que se incorpore al proyecto sabe que si necesita entender o modificar una regla, tiene que ir ahí. No hay que buscar un `if` perdido entre cien líneas de código mezclado.

**El testing se vuelve posible.** Al estar la lógica de negocio aislada en el Service, podemos probarla de forma independiente sin necesidad de levantar un servidor ni simular peticiones HTTP. Alcanza con instanciar el Service, pasarle datos directamente y verificar el resultado. Cada capa puede testearse por separado, con la complejidad que le corresponde y sin arrastrar la de las demás.

**El acoplamiento desapareció.** El Service no sabe si los datos se guardan en memoria, en MongoDB o en un archivo de texto. El Controller no sabe qué reglas aplica el Service. Esa ignorancia mutua es lo que nos permite cambiar partes del sistema sin efecto dominó. Si el cliente decide migrar de base de datos, el cambio queda completamente contenido en el Repository. Las reglas de negocio no se enteran, y el código HTTP tampoco.

La arquitectura en capas no elimina la complejidad inherente a un sistema. Lo que hace es **organizarla**. Y un sistema bien organizado es un sistema que puede crecer, que puede cambiar y que puede ser entendido por alguien que no lo escribió.

Volviendo al endpoint con el que arrancamos: el código original funcionaba. El cliente podía crear productos, el servidor respondía, todo parecía estar bien. El problema no era que no funcionara, sino que cualquier cambio futuro iba a ser cada vez más costoso, más riesgoso y más difícil de razonar. La arquitectura en capas no es la solución a un sistema roto; es la forma de evitar que un sistema sano se rompa con el tiempo.

Separar responsabilidades, reducir el acoplamiento y respetar el flujo entre capas no son reglas arbitrarias. Son decisiones de diseño que se pagan a futuro, cada vez que alguien tiene que modificar una regla de negocio sin miedo a romper la base de datos, o migrar de tecnología sin tocar la lógica del sistema.

---

> _"The art of programming is the art of organizing complexity."_ — Edsger W. Dijkstra
