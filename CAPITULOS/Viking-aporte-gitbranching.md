# Herramientas de Aprendizaje: Learn Git Branching

En el desarrollo de software, dominar el control de versiones con Git no es opcional, es una necesidad. Sin embargo, los conceptos de ramas, fusiones y movimientos de cabeza (`HEAD`) pueden resultar abstractos y confusos al principio. 

Para facilitar este proceso, utilizamos **[Learn Git Branching](https://learngitbranching.js.org/?locale=es_ES)**, una herramienta interactiva y visual diseñada para dominar Git de forma práctica.

---

## ¿Qué es Learn Git Branching?

Es una aplicación web educativa que funciona como un **simulador visual de Git**. A diferencia de una terminal tradicional donde los cambios son invisibles hasta que tirás un comando de estado, esta plataforma renderiza en tiempo real un árbol de confirmaciones (*commits*) a medida que ejecutas los comandos.

Dispone de una serie de niveles guiados en forma de juego, donde se te plantean desafíos lógicos que debes resolver utilizando comandos reales de Git.

---

## ¿Para qué sirve?

* **Visualizar la teoría:** Permite ver exactamente cómo se comportan las ramas (`branches`), cómo se mueven los punteros y qué estructura toma el historial del proyecto.
* **Perder el miedo a experimentar:** Al ser un entorno de simulación, podés probar comandos complejos (como `rebase` o `cherry-pick`) sin temor a romper un repositorio real o perder código.
* **Construir intuición mental:** Ayuda a desarrollar un mapa mental sólido de cómo viaja la información entre ramas, fundamental para resolver conflictos en equipos de trabajo.

---

## ¿Qué vas a aprender con ella?

La herramienta está estructurada para llevarte desde los conceptos más básicos hasta flujos de trabajo avanzados de nivel profesional:

### 1. Conceptos Básicos de Git
* Creación de confirmaciones (`git commit`).
* Gestión y ramificación (`git branch`).
* Fusión de historias de desarrollo (`git merge`).

### 2. Flujos de Trabajo Avanzados
* Reorganización de historias mediante `git rebase` (una alternativa limpia al merge).
* Desplazamiento libre del puntero `HEAD`.
* Modificación y reversión de commits anteriores (`git reset` y `git revert`).

### 3. Técnicas de Precisión
* Copia selectiva de confirmaciones específicas con `git cherry-pick`.
* Malabarismos con commits (reordenar, modificar y descartar cambios específicos).
* Uso de etiquetas (`git tag`) y marcas de seguimiento.

### 4. Repositorios Remotos (Git Avanzado)
* Clonación (`git clone`) y gestión de repositorios remotos.
* Sincronización de cambios mediante `git fetch`, `git pull` y `git push`.
* Resolución de divergencias entre el repositorio local y el remoto.

---

## Consejos para aprovecharla al máximo

> 💡 **Tip de oro:** No te limites a resolver los niveles al azar. Prestá atención a la animación del árbol de nodos cada vez que ejecutas un comando. Entender *hacia dónde se mueve la flecha* es el verdadero superpoder que te dará esta herramienta.

Podés ingresar al simulador completamente gratis y en español desde el siguiente enlace:
🔗 [Aprende Git Branchado Interactivamente](https://learngitbranching.js.org/?locale=es_ES)