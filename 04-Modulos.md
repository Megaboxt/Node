# Qué son los Módulos ?

Node.js organiza el código en piezas reutilizables llamadas módulos. Estos permiten dividir la funcionalidad en diferentes archivos y aprovechar herramientas externas o integradas.

Node JS utiliza el sistema de módulos llamado CommonJS aunque también se puede utilizar el estándar ESModules. Ambos proporcionan una forma estándar de definir, importar y exportar módulos.  

Cada archivo de JavaScript en Node.js se considera un módulo por defecto, lo que significa que el código dentro de ese archivo está contenido en ese ámbito y no afectará a otros módulos a menos que se exporten específicamente ciertos elementos.  

### Módulos Internos

Son todos los archivos de nuestro proyecto donde disponibilizamos o exportamos código que puede ser importado como módulo desde otro archivo.  

### Módulos Nativos  

Node.js proporciona una amplia gama de módulos internos (core modules) que ofrecen funcionalidades listas para usar, como `http` para la creación de servidores web, `fs` para la manipulación de archivos, `path` para la manipulación de rutas de archivo, entre otros.  

### Módulos Externos  

Además de los módulos nativos, Node JS cuenta con un vasto ecosistema de módulos externos disponibles en el repositorio npm (Node Package Manager) o el gestor de paquetes de nuestra preferencia.  

## Importando, exportando y creando Módulos 

Actualmente, en JavaScript existen dos estándares principales para importar y exportar código, cada uno con características y casos de uso particulares:  

### 1. CommonJS (CJS)

Es el estándar más antiguo y ampliamente utilizado, con soporte nativo tanto en JavaScript como en Node.js. Ha sido el formato predeterminado para la gestión de módulos en Node.js durante muchos años.

Aqui un ejemplo de como **exportar** código con CJS: 

<pre>
  // Archivo math.js
  // Exportando funciones y constantes
  const sumar = (a, b) => a + b;
  const restar = (a, b) => a - b;

  module.exports = { sumar, restar };
</pre>

*Utilizamos la declaración `module.exports` donde seguido al símbolo de igualdad `(=)` le asignamos el código a exportar envuelto entre llaves `{ }`, en este caso será un objeto que contiene las funciones creadas. De ser una sola función simplemente exportaríamos el nombre de la misma.*  


Y aqui ejemplo de como **importar** código con `require`: 

<pre>
  const math = require('./math'); 

  console.log(math.sumar(3, 5)); // 8
  console.log(math.restar(10, 6)); // 4
</pre>

*En el archivo donde necesitemos implementar el código exportado, utilizaremos la sentencia `require(‘./ruta-al-archivo’);` asignándose a una constante.*  

>NOTA: También podemos usar *Desctructuring Operator* cuando importemos un objeto:  
>`const { sumar, restar } = require(‘./ruta-al-archivo’);`


### 2. ES Modules (ESM)  

Introducido en 2015 con la especificación ES6, este estándar, también conocido como EcmaScript Modules, representa una evolución en la forma de trabajar con módulos en JavaScript. ESM ha ganado popularidad por su sintaxis moderna y su integración nativa en navegadores y entornos modernos.  

Aquí un ejemplo de cómo **exportar** mediante la sintaxis de ESM:

<pre>
  // Exportando funciones y constantes

  export const sumar = (a, b) => a + b;
  export const restar = (a, b) => a - b;
</pre>

*A diferencia de CJS donde se exportan todas las funciones como un objeto en conjunto, ahora colocamos la palabra reservada `export` previo a la declaración de cada elemento a exportar.  


Y aqui ejemplo de como **importar** código con `import`: 

<pre>
  // Importando con ESModules
  import { sumar, restar } from './math.js';

  console.log(math.sumar(3, 5)); // 8
  console.log(math.restar(10, 6)); // 4
</pre>

*Luego, al importar utilizamos la palabra reservada `import` seguido del destructuring de las funciones que deseamos utilizar y agregamos la palabra reservada `from` y la ruta donde se encuentra el módulo requerido.*

### Las principales diferencias entre ES Modules y CommonJS son:  

- **Sintaxis:**  ES modules utilizan una sintaxis basada en palabras clave como import y export para importar y exportar elementos. Por otro lado, CommonJS utiliza la asignación de objetos (module.exports y require) para exportar e importar elementos.

- **Comportamiento asincrónico**: los ES modules se cargan de forma asincrónica, lo que significa que las importaciones se resuelven dinámicamente en tiempo de ejecución. En cambio, CommonJS se carga de forma sincrónica, lo que significa que las importaciones se resuelven estáticamente en tiempo de compilación.

- **Ámbito**: Los ES modules tienen un ámbito propio por archivo, lo que significa que las variables y funciones declaradas dentro de un módulo no se filtran al ámbito global. En CommonJS, las variables y funciones declaradas en un módulo están disponibles en el ámbito global.

- **Exportación e importación estática**: ES modules solo permiten exportaciones e importaciones estáticas en la parte superior del archivo. No se pueden realizar exportaciones o importaciones condicionales o dentro de bloques de código. CommonJS permite exportaciones e importaciones dinámicas en cualquier parte del archivo.

>NOTA: Common JS es la sintaxis por defecto para manejo de módulos en Node.js, en caso de querer utilizar la sintaxis de ESModules, es necesario especificar `"type": "module"` en el archivo `package.json` del proyecto.

