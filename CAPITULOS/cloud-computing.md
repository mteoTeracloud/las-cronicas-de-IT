# **Capítulo: Introducción a Cloud Computing y el Ecosistema de AWS**

## 1. ¿Qué es Cloud Computing?

En lugar de comprar, poseer y mantener servidores físicos y centros de datos, el **Cloud Computing** (Computación en la Nube) es la entrega bajo demanda de potencia de cómputo, almacenamiento de bases de datos, aplicaciones y otros recursos de TI a través de Internet, con un modelo de precios de pago por uso.

Pasamos de un modelo **On-Premise** (donde eres dueño de la infraestructura y te encargas del hardware, la luz, la refrigeración y el mantenimiento) a un modelo flexible donde delegas esa carga operativa al proveedor.

---

## 2. Los Modelos de Servicio: IaaS, PaaS y SaaS

La nube se divide principalmente en tres modelos de servicio. La diferencia clave entre ellos es **quién administra qué**: ¿lo haces tú o lo hace el proveedor de la nube?

### 🏢 IaaS (Infrastructure as a Service - Infraestructura como Servicio)

Te proporciona los bloques de construcción básicos para la TI en la nube. Te da acceso a funciones de red, computadoras (virtuales o en hardware dedicado) y espacio de almacenamiento.
* **Tu responsabilidad:** Instalar y mantener el sistema operativo, configurar bases de datos, gestionar el software, los parches de seguridad y el código de tu aplicación.
* **Responsabilidad del proveedor:** El hardware físico, la red subyacente, el almacenamiento físico y la capa de virtualización.
* **Ejemplo ideal:** Una máquina virtual vacía (como una instancia EC2).

### 🛠️ PaaS (Platform as a Service - Plataforma como Servicio)

Elimina la necesidad de que administres la infraestructura subyacente (normalmente hardware y sistemas operativos) y te permite centrarte exclusivamente en la implementación y administración de tus aplicaciones.
* **Tu responsabilidad:** Solo tu código, los datos y la configuración específica de tu aplicación.
* **Responsabilidad del proveedor:** El sistema operativo, el servidor web o entorno de ejecución, el mantenimiento de los servidores, el escalado automático y los parches del sistema.
* **Ejemplo ideal:** Un entorno donde subes un archivo comprimido con tu código y la plataforma lo despliega automáticamente.

### 💻 SaaS (Software as a Service - Software como Servicio)

Te proporciona un producto completo que el proveedor de servicios ejecuta, aloja y administra de extremo a extremo. En la mayoría de los casos, se refiere a aplicaciones finales listas para el usuario.
* **Tu responsabilidad:** Configurar tus preferencias de usuario, gestionar tus credenciales y utilizar el sistema.
* **Responsabilidad del proveedor:** Absolutamente todo, desde el código de la aplicación hasta el mantenimiento de los servidores y el hardware.
* **Ejemplo ideal:** Herramientas de correo electrónico web, plataformas de streaming o suites de oficina online.

> 🍕 **La Analogía de la Pizza (Para entenderlo de un vistazo):**
> * **On-Premise (Hecha en casa):** Tú pones los ingredientes, la masa, el horno, el gas, los platos y la mesa.
> * **IaaS (Pizza congelada):** Compras la pizza ya armada en el supermercado, pero tú pones el horno, el gas, los platos y la mesa en tu casa.
> * **PaaS (Delivery de pizza):** Te traen la pizza cocinada a tu casa; tú solo pones los platos, la mesa y la bebida.
> * **SaaS (Comer en un restaurante):** Vas al lugar, te sirven, comes, pagas y te vas. No te preocupas por cocinar ni por limpiar la mesa.

---

## 3. Catálogo de Servicios Esenciales de AWS

Amazon Web Services (AWS) es la plataforma de nube más adoptado del mundo. Para estructurar tu aprendizaje, aquí tienes una lista de sus servicios principales clasificados por su función tecnológica:

### 💻 Cómputo (Compute)

* **Amazon EC2 (Elastic Compute Cloud):** Máquinas virtuales en la nube. Es el ejemplo puro de **IaaS**. Puedes elegir el sistema operativo, memoria, almacenamiento y CPU que necesites de forma flexible.
* **AWS Lambda:** Servicio "Serverless" (sin servidor). Ejecuta tu código solo cuando se activa por un evento específico (un click, la subida de un archivo, un cambio en la base de datos) y pagas estrictamente por los milisegundos que corre.
* **Amazon ECS / EKS:** Servicios administrados para gestionar, desplegar y orquestar contenedores de Docker (EKS utiliza Kubernetes para la orquestación a gran escala).

### 📦 Almacenamiento (Storage)

* **Amazon S3 (Simple Storage Service):** Almacenamiento de objetos (archivos). Ideal para guardar imágenes, videos, copias de seguridad (backups) o archivos estáticos de una aplicación web. Es virtualmente ilimitado y altamente disponible.
* **Amazon EBS (Elastic Block Store):** Discos duros virtuales de alto rendimiento que se conectan directamente a tus instancias de EC2 (actúan como el disco local del sistema operativo).

### 🗄️ Bases de Datos (Databases)

* **Amazon RDS (Relational Database Service):** Servicio administrado para bases de datos relacionales (SQL). Soporta motores populares como MySQL, PostgreSQL, MariaDB y SQL Server, facilitando tareas como los backups automáticos y la alta disponibilidad.
* **Amazon DynamoDB:** Base de datos NoSQL de tipo clave-valor. Ofrece un rendimiento ultra rápido con respuestas en milisegundos de un solo dígito y es totalmente administrada a cualquier escala.

### 🌐 Redes y Seguridad (Networking & Security)

* **Amazon VPC (Virtual Private Cloud):** Te permite definir y lanzar recursos de AWS en una red virtual lógicamente aislada. Aquí configuras tus propias subredes, tablas de ruteo, gateways de internet y firewalls (Security Groups).
* **Amazon Route 53:** El servicio de sistema de nombres de dominio (DNS) de AWS, altamente disponible y escalable, encargado de traducir nombres de dominio legibles (como `tuweb.com`) en direcciones IP.

---

🔗 **Enlace oficial:** Para explorar más servicios y documentación, puedes visitar la página oficial de [Amazon Web Services (AWS)](https://aws.amazon.com/es/).