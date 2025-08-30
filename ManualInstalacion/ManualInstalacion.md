# Manual de instalación Razonamiento Cuantitativo

## 1. Introducción

Este manual te guiará paso a paso en la configuración e instalación completa de la aplicación Razonamiento Cuantitativo del proyecto Cognicare. Este proyecto está diseñado para que cualquier desarrollador desde conocimientos básicos hasta avanzados pueda duplicarlo, por lo que cada etapa del proceso se explica de forma clara, sencilla y detallada.

## 2. Arquitectura de Razonamiento Cuantitativo

El proyecto implementa un patrón arquitectónico de capas, con las cuales se les da responsabilidades a cada capa para generar la administración crentralizada de todos los componentes de nuestra variable.

![Arquetipo_Referencia](/Imagenes/Arquitectura_Referencia.png)

### 2.1 Componentes

#### Users (Usuarios):

- ¿Quiénes son? ¡Eres tú y todos los que usarán nuestro sistema!

- ¿Qué hacen? Son las personas que interactúan directamente con la aplicación. Podrían estar usando nuestra página web y cualquier otro modulo de Cognicare.

#### Web/Http (Conexión a Internet):

- ¿Qué es? Es la forma en que los usuarios se conectan a nuestro sistema a través de internet. Piensa en esto como la "autopista" por donde viajan las solicitudes y respuestas cuando usas una página web o una aplicación.

- ¿Qué hace? Permite que tu computador o dispositivo envíe una petición al sistema (por ejemplo, "quiero ver mi información") y reciba una respuesta ("aquí está tu información").

#### Backend (El Cerebro Central / La Oficina de Atención):

- ¿Qué es? Este es el corazón de nuestro sistema, construido con Node.js. Imagina que es una "oficina de atención al cliente" muy eficiente.

- ¿Qué hace? Cuando un usuario hace una solicitud (a través de Http), esta es la primera parada. La pagina recibe la petición, la entiende y decide a qué otra parte del sistema debe enviarla para obtener la información correcta o realizar la acción solicitada. También es el que organiza la respuesta para enviársela de vuelta al usuario.

#### Frontend (El Visualizador):

- ¿Qué es? Este es el encargado de visualizar todo el contenido de la pagina.

- ¿Qué hace? Cuando un usuario entra a la pagina, todo lo que ve se considera un "Frontend, donde se pone cada parte del diseño de un sitio web.

#### Tareas Razonamiento Cuantitativo (El Juego):

- ¿Qué es? Este es el lugar donde se ejecuta el juego en si.

- ¿Qué hace? Permite que el juego se ejecute para que el usuario lo pueda jugar, y cada peticion en cuanto al "cerebro central" se realiza al Backend.

#### Postgresql (La Gran Biblioteca / El Archivador Maestro):

- ¿Qué es? Es una base de datos, específicamente PostgreSQL. Piensa en ella como una biblioteca gigantesca o un archivador muy bien organizado donde guardamos toda la información importante del sistema.

- ¿Qué hace? El Componente Centralizador-api (y a veces el Especialista) la usa para guardar nueva información, buscar datos que necesita o actualizar información existente. Es donde se almacena de forma segura todo lo que el sistema necesita recordar.

## 3. Requisitos Previos y Preparación del Entorno

Este manual asume que has realizado los pasos para instalar el [Componente Centralizador](https://github.com/federico1605/Documentacion_Cognicare/blob/main/ManualInstalacion/ManualInstalacion.md), asi que cualquier preparacion que aplique por ese medio tambien aplicara en este, pero, si se necesita tambien editar el proyecto, es necesario instalar **Godot**.

### 3.1. Instalacion de Godot v3.6

Godot es un motor de videojuegos multiplataforma, gratuito y de código abierto para crear juegos y aplicaciones 2D y 3D, que se puede exportar a diversas plataformas como PC, móviles y paginas web. La version 3.6 de Godot es requierido por su buena habilidad de exportar a web.

1. Ingrese a la pagina **https://godotengine.org/download/archive/3.6-stable/**.
2. Descargue la version "Estandar" de "Windows" (o, por causa de la traduccion automatica, "Ventanas")
3. Extraiga el contenido de "Godot_v3.6-stable_win64.exe.zip" en una carpeta de su elección.

## 4. Procedimiento de Clonación y Compilación del Proyecto

### 4.1 Clonación del Repositorio

**Propósito:**
Descargar el código fuente del proyecto desde GitHub a tu máquina local para poder trabajar con él.

**Procedimiento:**
1. Abre una terminal o línea de comandos
2. Navega a la carpeta donde quieres guardar el proyecto
3. Ejecuta el comando de clonación, para el FrontEnd:
   ```bash
   git clone -b develop https://github.com/CognicareUCO/RazonamientoCuantitativoFrontEnd.git
   ```
5. Ejecuta el comando de clonación, para el BackEnd:
   ```bash
   git clone -b develop https://github.com/CognicareUCO/RazonamientoCuantitativoBackEnd.git
   ```

### 4.2. Insercion de Base de Datos a PgAdmin (Docker)

Para añadir los datos exclusivos para esta variable en el PgAdmin, realice estos pasos:
1. Abra el archivo "init.sql" en el directorio de "\RazonamientoCuantitativoBackEnd\export\react" dentro de la carpeta donce clonastes los repositorios en cualquier editor de texto que desees (el mas comun es "Bloc de Notas" que viene preinstalado en Windows), luego copie todo el texto en el archivo (CTRL+A, luego CTRL+C).
1. En el menu de "Containers" en Docker Desktop, ejecute el container en la que esta la imagen de PgAdmin e ingrese a la pagina (**http://localhost:5050/browser/**).
2. En la base de datos que creastes para la base de datos del Componente Centralizador, haga clic derecho, luego seleccione la opcion "Query Tool" (o "Herramienta de Consulta").
3. Dentro del bloque de texto, pegue el texto que antes habias copiado (CTRL+V), despues, haga clic en el icono [▶].
4. Si todo le sale bien, habras insertado los datos sin ningun problema!

Si sale un error al ejecutar la consulta, asegurese de haber copiado bien todo el texto dentro del archivo "init.sql".

### 4.3. Ejecucion del proyecto

Para ejecutar el proyecto, realice estos pasos:
1. Dentro del directorio de "\RazonamientoCuantitativoBackEnd\export" dentro de la carpeta donce clonastes los repositorios, existen dos archivos:
  * **startServer.bat:** Compila el proyecto, instalando cualquier dependencia que se requiere, para luego ejecutarlo.
  * **quickStart.bat:** Simplemente ejecuta el proyecto si y solo si ya se habia compilado previamente.
2. Haga doble clic en el que corresponda a sus necesidades.
3. Despues de verificar que el mensaje "Server listening on port..." aparezca, ya puede ejecutar la variable por medio del *Componente Centralizador*.

## 5. Edicion del Proyecto

### 5.1. Importacion de proyecto

Si, por alguna circumstancia, se desea editar el proyecto, asumiendo que ya tienes experiencia codificando en GDScript (Sintaxis similar a Python) o C#, puedes realizar estos pasos:

1. Abra *Godot v3.6*.
2. En el menu de proyectos, seleccione la opcion "Importar", luego dirigese a la ubicacion en "\RazonamientoCuantitativoFrontEnd\code" dentro de la carpeta donce clonastes los repositorios, y abra "project.godot", luego "Importar y Editar".

<p align="center">
  <img src="/Imagenes/ManualInstalacion/GodotImport.png" alt="Menu de Godot">
</p>

3. Cuando la ventana de Godot le aparezca algo asi despues de un tiempo, ya puedes empezar a editar el proyecto.

<p align="center">
  <img src="/Imagenes/ManualInstalacion/GodotProject.png" alt="Proyecto en Godot">
</p>

### 5.2. Exportacion

Para compilar el proyecto para la web, se pueden realizar estos pasos:

1. Dentro de la ventanilla "Proyecto" en la ventana de Godot, de clic en "Exportar".

<p align="center">
  <img src="/Imagenes/ManualInstalacion/GodotExport.png" alt="Exportar en Godot">
</p>

2. Despues de haber creado el preajuste de "HTML5", haga clic en "Exportar Proyecto..."

<p align="center">
  <img src="/Imagenes/ManualInstalacion/GodotExport2.png" alt="Exportar en Godot, HTML5">
</p>

3. Ubiquese en "\RazonamientoCuantitativoBackEnd\export" dentro de la carpeta donce clonastes los repositorios y haga clic en "Guardar", si le sale un mensaje de sobreescritura, haga clic en "OK".
4. El proyecto ya deberia estar listo para la ejecucion, por medio de la ejecucion de **startServer.bat**.

### 5.3. Edicion del Backend

Todo relacionado al Backend se encuentra en "\RazonamientoCuantitativoBackEnd\export\react", cualquier edicion se puede realizar con el IDE **Visual Studio Code (VS Code)**.