# Gestores de Paquetes  

Un gestor de paquetes funciona como una biblioteca de módulos o paquetes de código de programación donde a su vez eliminan la necesidad de descargar e integrar manualmente estas bibliotecas, lo que simplifica el desarrollo y asegura que las dependencias estén organizadas y actualizadas.  

Estas herramientas facilitan la instalación, actualización y gestión de bibliotecas o dependencias en un proyecto. Estas dependencias son piezas de código que otros desarrolladores han creado para resolver problemas comunes, como conectarse a una base de datos, realizar peticiones HTTP o manejar archivos.  


## Para qué sirven los Gestores de Paquetes ?  

- Instalar dependencias de terceros.  

- Gestionar versiones de esas dependencias.  

- Actualizar y eliminar dependencias de forma sencilla.  

- Resolver la integración e interacción entre las distintas dependencias y las versiones de las subdependencias que tengan instaladas.  

El concepto de dependencias, paquetes o módulos es propio de la programación en general, incluso existen gestores de paquetes para instalar programas en los distintos sistemas operativos. Los más conocidos son: 

- NPM (Node Package Manager).

- HomeBrew: Permite manejar programas del sistema operativo Mac OS integrado en las computadoras marca Apple.  

- Composer: Usado en proyectos que utilizan el lenguaje de programación **PHP**

- Chocolatey: El gestor de paquetes del sistema operativo Microsoft. Nos permite instalar infinidad de programas desde la terminal sin tener que descargar los ejecutables

- Pip: Gestor de paquetes para el lenguaje Python.  

## NPM - Node Package Manager  

En este caso, nos vamos a enfocar en el Gestor de Paquetes NPM, que además de gestionar paquetes, NPM se encarga de listar y establecer el orden en el que se instala cada dependencia y a su vez cuando estas dependencias utilizan subdependencias, es decir, que el código de origen también utilizó NPM para instalar paquetes, el gestor se encarga de decidir qué versión de cada una de ellas debe utilizar para no entrar en conflictos.

Una vez instaladas todas las dependencias necesarias, crea de forma automática un archivo llamado `package-lock.json` con el detalle minucioso de esta organización de paquetes y también otro archivo llamado `package.json` donde tenemos un detalle directo de las dependencias que nosotros instalamos en el proyecto pero a su vez permite declarar: nombre del proyecto, versión, archivo de inicio, autor, licencia y scripts de ejecución del proyecto, entre otras cosas.  


## Paquetes Base del Proyecto

Por lo general para crear un servidor en Node con Express ya hay una serie de paquetes y comandos a declarar en consola para crear los archivos iniciales y la estructura del proyecto.

En la consola ejecutar los siguientes comandos, siempre hay que fijarse la ruta o el path desde donde estas ubicado, para intarlar adecuadamente las dependencias y/o diferentes paquetes que sean necesarios

    // Crea el archivo package.json
    npm init -y 
    
    // Instala la dependencia para crear un servidor Express
    npm install express 
    
    // Es un watcher de cambios en tiempo real de tu proyecto
    npm install nodemon 
    
    // Instala la dependencia para habilitar solicitudes HTTP de sitios cruzados
    npm install cors 

