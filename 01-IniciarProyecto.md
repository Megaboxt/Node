# Iniciar Proyecto con Node.js y NPM

Comenzar un nuevo proyecto en Node.js es relativamente fácil, basta con asegurarse
de ejecutar los siguientes comandos:


1. Verifica que tengas instalado Node JS y NPM usando los siguientes comandos:

<pre>
  node -v
</pre>

<pre>
  npm -v
</pre>

>En caso de no estar instalados, ir a la página de Node.js e instalarlo.  

2. Crea un nuevo directorio o carpeta para tu proyecto.  

3. Abrí VS Code o el Editor de Código que tengas y arrojá la carpeta o ingresa a la ubicación del proyecto desde la terminal  

4. Ejecuta el comando `npm init` donde la terminal comenzará a pedirnos que
completemos determinada información o `npm init -y` para realizar un inicio
rápido que nos permita configurar nuestro entorno de trabajo luego.  

>En caso de utilizar el flag `npm init -y` salteamos todas las preguntas y se crea directamente un archivo llamado `package.json` en donde podremos *configurar* los
valores por defecto de cada una de las propiedades que tiene el archivo por default.

Este archivo llamado `package.json` se ve de la siguiente manera:

<pre>
  {
    "name": "techlab-proyect",
    "version": "1.0.0",
    "description": "",
    "main": "index.js",
    "scripts": {
      "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC"
  }
</pre>


- name: define el nombre del proyecto. No puede contener mayúsculas o caracteres especiales.

- version: establece el número de versión según la convención X.Y.Z donde X
representa las versiones “major” donde existen cambios importantes de nuestro
proyecto, la Y las versiones “minor” con cambios menores y la Z las versiones
“patch” con parches de seguridad o arreglos de errores.

- main: indica el “entry point” o archivo de entrada de nuestra aplicación.

- scripts: propiedad de suma importancia donde podremos crear diferentes scripts
para ejecutar nuestro código.

- keywords: array de strings donde se colocan palabras clave que definen al
proyecto.

- author: responsable/s del proyecto.
 
- license: tipo de licencia de uso y explotación del código fuente y/o del proyecto.  

- description: cadena de texto que describe el proyecto.  
