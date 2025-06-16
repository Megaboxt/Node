# `__dirname`

En Node.js, __dirname es una variable global que representa la ruta absoluta del directorio donde se encuentra el archivo actualmente en ejecución. Es particularmente útil para gestionar rutas y trabajar con archivos en proyectos donde las ubicaciones pueden variar entre entornos de desarrollo y producción.  

## Por qué usar `__dirname`?

Cuando trabajás con archivos y directorios en Node.js, necesitás proporcionar rutas exactas. Sin embargo, estas rutas pueden ser relativas al archivo que ejecuta el código. Esto puede generar problemas si cambias de directorio o despliegas tu aplicación en un servidor ya que dependiendo el entorno de ejecución, las referencias a ciertos archivos pueden verse modificadas.

Usar `__dirname` garantiza que las rutas sean absolutas, eliminando la dependencia de la ubicación actual desde donde se ejecuta el script.


## Uso de `__dirname` en CJS

Supongamos que tenemos la siguiente estructura de directorios y archivos: 

<pre>
  /proyecto
    |-- index.js
    |-- data
         |-- ejemplo.txt
</pre>

Ahora queremos desde el archivo `index.js` acceder a la información dentro del archivo `ejemplo.txt`, para ello podemos utilizar el método (función) llamado `readFileSync` del módulo nativo llamado `fs` (abreviación de file system) que nos brinda métodos para acceder, escribir, crear y eliminar archivos de la PC o servidor con Node JS.  

En este caso `readFileSync` recibe como primer parámetro la ruta absoluta al archivo deseamos leer, donde lo más lógico sería lo siguiente:  
   
   
     const fs = require('fs');

    // Indicamos la ruta en el primer parámetro
    fs.readFile('c:/user-pc/node-project/proyecto/data/ejemplo.txt', 'utf8', (err, data) => {
    if (err) {
      console.error('Error al leer el siguiente archivo: ', err);
      return
    }
    console.log('Contenido del archivo: ', data);
    });


Si bien esto podría funcionar, existen casos donde por el contexto donde se esté ejecutando el código (por ejemplo un servidor cuya estructura de carpetas podría no estar controlada por nosotros) la ruta indicada no apunte correctamente al archivo.  

Por fortuna, gracias a la existencia de __dirname podemos saber en tiempo de ejecución la posición absoluta del archivo actual dentro del servidor, entonces utilizando esta variable global junto con fs y la ayuda de path, otro módulo nativo de Node que nos provee de métodos para trabajar con rutas de archivos de forma sencilla, podremos crear una referencia que nunca se vea corrompida, de la siguiente manera:



    const path = require('path');
    const fs = require('fs');

    /* Obtenemos la ruta absoluta del archivo ejemplo.txt utilizando __dirname */ 
    const filePath = path.join(__dirname, 'data', 'ejemplo.txt');

    // Leemos el archivo ejemplo.txt
    fs.readFile(filePath, 'utf8', (err, data) => {
      if (err) {
        console.error('Error al leer el siguiente archivo: ', err);
        return
      }
      console.log('Contenido del archivo: ', data);
    });


En el ejemplo, `path.join()` combina el resultado de `__dirname` (supongamos que es algo como C:/server/node-project/) junto con el nombre de la carpeta y el nombre del archivo donde se encuentra `ejemplo.txt` para crear una referencia exacta dentro del contexto donde se está ejecutando el proyecto.

Analicemos este código paso a paso:  

  - `__dirname` proporciona la ruta completa del directorio donde se encuentra index.js.  
    
  - `path.join` combina __dirname con los subdirectorios y el nombre del archivo para formar una ruta absoluta.  
    
  - `fs.readFile` usa esa ruta absoluta para acceder al archivo, asegurándose de que funcione sin importar desde dónde ejecutes el script.  


## Uso de `__dirname` en ESM

En proyectos que usan ES Modules, `__dirname` no está disponible. En su lugar, puedes usar `import.meta.url` para obtener una ruta absoluta.

    import { fileURLToPath } from 'url';
    import path from 'path';

    // Obtener el directorio actual
    const __filename = fileURLToPath(import.meta.url);
    const __dirname = path.dirname(__filename);

    console.log('Ruta absoluta: ', __dirname);

    // Leemos el archivo ejemplo.txt
    fs.readFile(__dirname, 'utf8', (err, data) => {
      if (err) {
        console.error('Error al leer el siguiente archivo: ', err);
        return
      }
      console.log('Contenido del archivo: ', data);
    });


En esta ocasión aprovechamos el método `fileURLToPath` del módulo nativo `url`, el cual recibirá y formateará el valor de `import.meta.url` para devolvernos la posición actual de nuestro archivo y mediante el método `path.dirname()` tomaremos sólo la ruta (quitando el nombre del archivo) logrando el mismo resultado que en CJS.  

## Conclusión:  

`__dirname` es una herramienta esencial en Node.js para trabajar con rutas absolutas de manera confiable. Junto con módulos como `path`, facilita la manipulación de rutas y archivos en tus aplicaciones, asegurando que funcionen sin importar el entorno o ubicación desde donde se ejecuten.
