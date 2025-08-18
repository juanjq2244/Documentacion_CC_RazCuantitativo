# Arquitectura de Referencia
![Arquitectura de Referencia](/Imagenes/Arquitectura_Referencia.jpg)

## 1. Interacción del Usuario (User → Web/Http)

### Usuario
Un jugador o administrador inicia la interacción con la aplicación, desde el *Componente Centralizador*, dentro de un **navegador web**.

### Web/Http
Las solicitudes del usuario viajan a través de la web utilizando el protocolo **HTTP(S)**, para alcanzar el punto de entrada de la aplicación.  
Esta capa se encarga de **recibir y enrutar** las peticiones iniciales hacia los componentes adecuados del sistema.

---

## 2. Procesamiento Centralizado (Web/Http → Back End)

### Back End
Este componente actúa como el **cerebro de la aplicación**, recibiendo todos los datos provenientes del *Componente Centralizador*.  
Es responsable de procesar la lógica de autenticación y autorización de las sesiones de entrenamiento existentes.

---

## 3. Persistencia de Datos (Back End → Data Bases)

### Data Bases
Este componente es el **repositorio de información persistente** del sistema.  
El Back End interactúa con él para:

- **Almacenar Datos**:  
  Guarda información como el opcion de respuesta dentro de un sesion de entrenamiento.

- **Asegurar la Integridad**:  
  Garantiza que los datos se almacenen de manera consistente y fiable, manteniendo la coherencia del sistema.

---

## 4. Lógica Especializada (Back End → Front End → Tareas RC)

### Front End
Este componente representa el modulo encargado de visualizar el contenido de la pagina.

El Back End se comunica con este servicio para:

- Enviar datos especificos de entrenamiento.

### Tareas RC
Este componente representa el modulo encargado de visualizar los juegos de la variable.

El Back End/Front End se comunica con este servicio para:

- Recibir datos para luego visualizar el juego en si.

**Línea Punteada de Retorno**:  
Este servicio devuelve los datos o resultados procesados al Back End, que los utiliza para:

- Actualizar la base de datos.
- Formular la respuesta final al usuario.


# Arquetipo de Referencia

![Arquetipo de Referencia](/Imagenes/Arquetipo_Referencia.jpg)

La arquitectura propuesta representa el módulo centralizador de una aplicación de entrenamiento cognitivo enfocada en la sesion entrenamiento. Este componente actúa como el punto de entrada principal para los usuarios y su progreso individual.

# Componentes y su Funcionamiento

## Users (Usuarios)
Representan a los jugadores y administradores que interactúan con la aplicación.  
Son el punto de origen de todas las solicitudes al sistema.

## Http
Este elemento simboliza la capa de comunicación web.  
Las solicitudes de los usuarios (desde el frontend de React en sus navegadores) se envían mediante el protocolo HTTP(S) al servidor de la aplicación.  
Es el estándar para la interacción cliente-servidor en la web.

## React
En esta parte del flujo, se asume que existe una aplicación frontend desarrollada en React.  
Esta aplicación es la que los usuarios finales utilizan para interactuar.

React se encarga de:

- La interfaz de usuario dinámica y reactiva.
- Enviar solicitudes al backend de Node.js.

## Node.js
Este es el backend principal de la variable de *Razonamiento Cuantitativo*.  
Node.js es un entorno de ejecución de JavaScript del lado del servidor que permite construir aplicaciones escalables y de alto rendimiento.  
En esta arquitectura, actúa como el servidor de APIs principal.

## Godot
El motor de juegos que se encarga de visualizar el contenido de la variable.

### Funcionalidades Centrales
Este componente es responsable de:

- **Autenticación y Autorización de Sesion**: Gestiona el inicio de sesión de entranamiento.
- **Guardado de Metricas**: Administra la creación del progreso que a su vez seran enviadas al *Componente Centralizador*.
- **Orquestación de Solicitudes**: Actúa como un proxy o puerta de enlace entre el frontend de React y la base de datos PostgreSQL.

## PostgreSQL
Es la base de datos relacional utilizada para almacenar la información persistente del sistema.

### Datos que Almacena
Principalmente, guardará:

- Información de los usuarios (opcion de respuesta, tiempo respuesta, etc.).
- Datos transaccionales y de estado relacionados con el progreso de cada usuario en su sesion de entrenamiento.

Su naturaleza relacional es ideal para modelar estas relaciones complejas y asegurar la integridad de los datos.

# Justificación de las Herramientas Elegidas

Las herramientas seleccionadas son las mejores posibles en el contexto de tus necesidades específicas, ofreciendo un equilibrio entre desarrollo ágil, rendimiento, escalabilidad y gestión de datos confiable.  
Cada elección se ha realizado tras considerar alternativas y evaluar su idoneidad para los requerimientos de la variable de *Razonamiento Cuantitativo*.

---

## Godot

- **Eficiencia**
  Godot es conocido por su buen rendimiento, especialmente en juegos 2D, donde puede manejar grandes cantidades de sprites y elementos de juego con fluidez, incluso en hardware de gama baja.

- **Interfaz Intuitiva**
  Godot tiene una interfaz de usuario clara y organizada, lo que facilita la creacion de juegos y la navegacion por diferentes herramientas.

- **Soporte para multiples plataformas**
  Godot permite exportar a diversas plataformas, como; Windows, MacOS, Linux, Android, IOS, y HTML5.

### Alternativa Considerada: Love2D
Aunque **Love2D** ofrece un lenguaje de programacion facil de aprender (LUA) para construir el juego en si, se prefirió **Godot** por:

- Su eficiencia en cuanto al rendimiento.
- Soporte oficial para la exportacion en HTML5.
- La existencia de un interfaz.

---

## Node.js

- **Rendimiento y Escalabilidad (No Bloqueante)**:  
  Node.js se basa en un modelo de E/S no bloqueante y un bucle de eventos, lo que lo hace extremadamente eficiente para manejar múltiples conexiones concurrentes con poca sobrecarga. Ideal para APIs backend en aplicaciones de juegos.

- **JavaScript End-to-End**:  
  Permite usar JavaScript tanto en frontend (React) como en backend (Node.js), facilitando el intercambio de conocimientos, la reutilización de código y la integración del equipo. Reduce la curva de aprendizaje y acelera el desarrollo.

- **Desarrollo Rápido y Prototipado**:  
  Gracias al ecosistema de `npm` y frameworks como `Express.js`, el desarrollo de APIs es ágil. Node.js acelera el lanzamiento al mercado.

- **Ideal como "Punto de Entrada Centralizador"**:  
  Excelente para gestionar rutas, autenticación y orquestar interacciones entre frontend, microservicios y base de datos.

- **Comunidad y Ecosistema Maduro**:  
  Gran comunidad, soporte constante y librerías robustas que aseguran sostenibilidad a largo plazo.

### Alternativa Considerada: Java con Spring Boot
Aunque **Java y Spring Boot** ofrecen robustez y rendimiento para construir microservicios empresariales, se prefirió **Node.js** por:

- Su rapidez de desarrollo.
- Ecosistema JavaScript unificado.
- Modelo asíncrono ideal para manejar concurrencia en tiempo real.
- Menor curva de aprendizaje y tiempo de configuración para este tipo de proyecto.

---

## React

- **Interfaz de Usuario Reactiva y Dinámica**:  
  Permite construir UIs con componentes reutilizables, brindando una experiencia fluida e interactiva. Perfecto para la dinámica de una app de juegos.

- **Rendimiento (Virtual DOM)**:  
  Optimiza las actualizaciones de la UI, lo que resulta en interfaces rápidas y responsivas.

- **Ecosistema y Herramientas**:  
  Comunidad activa con librerías como React Router, Redux o Zustand que agilizan el desarrollo de funcionalidades complejas.

- **Desarrollo Basado en Componentes**:  
  Favorece la modularidad y el mantenimiento del código. Ideal para apps con interfaces que evolucionan constantemente.

### Alternativa Considerada: Angular
Angular ofrece una arquitectura sólida para grandes aplicaciones empresariales, pero React fue elegido por:

- Su mayor flexibilidad.
- Curva de aprendizaje más accesible.
- Ligereza y rapidez en prototipado.
- Mejor adaptación a los requerimientos interactivos de una aplicación de juego.

---

## PostgreSQL

- **Fiabilidad y Consistencia (ACID)**:  
  Garantiza integridad en los datos transaccionales como el progreso y los puntajes de los jugadores.

- **Integridad de Datos**:  
  Soporte para claves primarias/foráneas, esquemas robustos e integridad referencial entre usuarios y sesiones de entrenamiento.

- **Escalabilidad Horizontal y Vertical**:  
  Soporta tanto aumento de recursos en un solo servidor como técnicas como sharding o réplicas para escalar horizontalmente.

- **Flexibilidad (JSONB)**:  
  Al ser relacional pero con soporte para JSONB, permite almacenar datos semi-estructurados sin perder el control relacional.

- **Comunidad y Ecosistema**:  
  Herramientas maduras, extensiones útiles y amplia documentación para facilitar su operación y crecimiento.

### Alternativa Considerada: MongoDB
MongoDB, como base de datos NoSQL, es ideal para esquemas flexibles y escalabilidad horizontal.  
Sin embargo, PostgreSQL fue preferido por:

- Su consistencia transaccional.
- Su solidez en relaciones entre entidades clave.
- La necesidad crítica de integridad en los datos del usuario y su progreso.



# Plataforma Tecnológica

La elección de las herramientas tecnológicas para este proyecto se fundamenta en la búsqueda de eficiencia en el desarrollo, rendimiento óptimo, escalabilidad y robustez en la gestión de datos y seguridad.

---

## Front End: React / Godot

Se ha optado por el framework de JavaScript **React** con **Godot** para la construcción de la capa visual de la aplicación.

- React es una librería de código abierto mantenida por Facebook y una vasta comunidad.
- (React) Ideal para construir interfaces de usuario (UI) dinámicas y de alto rendimiento.
- (React) Su enfoque en el desarrollo basado en componentes permite:
  - Crear módulos reutilizables.
  - Gestionar eficientemente el estado de la aplicación.
  - Facilitar la mantenibilidad del código.
- (React) Utiliza un **Virtual DOM** que optimiza las actualizaciones de la UI, brindando una experiencia fluida y reactiva.
- (React) Su amplio ecosistema y herramientas de desarrollo contribuyen a la eficiencia y calidad del producto final.
- Godot es un motor de juego de código abierto y gratuito.
- (Godot) Es diseñado para trabajar en equipo.
- (Godot) Es la mejor opcion para juegos en HTML5.

---

## Back End: Node.js

La lógica de negocio del proyecto se implementará utilizando **Node.js**, un entorno de ejecución de JavaScript del lado del servidor.

- Se destaca por su arquitectura asíncrona y no bloqueante.
- Eficiente para manejar un gran número de conexiones concurrentes con baja latencia.
- Ideal para construir APIs que sirven a múltiples usuarios simultáneamente (por ejemplo, en una aplicación de juegos).
- Permite mantener un **stack tecnológico homogéneo** (JavaScript/TypeScript) entre frontend y backend:
  - Reutilización de conocimientos.
  - Agilidad en el equipo de desarrollo.
- Junto con frameworks como **Express.js**:
  - Optimiza y acelera el desarrollo de APIs robustas.
  - Fomenta prácticas de código limpio.
  - Promueve estructuras modulares para una mejor mantenibilidad.

---

## Fuente de Datos: PostgreSQL

Se ha seleccionado **PostgreSQL** como la base de datos relacional principal para el almacenamiento de datos del proyecto.

- Garantiza la **integridad de los datos** mediante las propiedades **ACID**:
  - Atomicidad.
  - Consistencia.
  - Aislamiento.
  - Durabilidad.
- Ideal para gestionar información transaccional como:
  - Usuarios.
  - Progreso de los usuarios en el juego.
- Ofrece:
  - Manejo robusto de esquemas.
  - Soporte para claves primarias y foráneas.
  - Índices avanzados para optimizar las consultas.
- Asegura la **fiabilidad y consistencia a largo plazo**, clave para el uso continuo de la aplicación.

[Volver](https://github.com/juanjq2244/Documentacion_CC_RazCuantitativo/tree/main)
