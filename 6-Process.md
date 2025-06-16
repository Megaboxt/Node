# Process  

El módulo `process` es uno de los módulos nativos más importantes de Node.js, ya que permite interactuar con el proceso en ejecución. Una de sus propiedades clave es `process.argv`, un array que contiene los argumentos pasados al script desde la línea de comandos.  

## Qué es `process.argv` ?

Es un array que incluye:  

  - La ruta absoluta del ejecutable de Node.js.  
  
  - La ruta del archivo ejecutado.  
  
  - Los argumentos adicionales proporcionados por el usuario.  

Por ejemplo, si ejecutamos:

<pre>
  node index.js argumento1 argumento2
</pre>

El contenido de `process.argv` será:


    [
      '/ruta/node',
      '/ruta/index.js',
      'argumento1',
      'argumento2'
    ]


A partir del índice 2 vienen los argumentos personalizados que se pasaron en la terminal.

De esta manera, podemos aprovechar `process.argv` para crear scripts interactivos que respondan a diferentes argumentos. Veamos un ejemplo simple:

    const args = process.argv.slice(2); // Ignora los 2 primeros elementos del array con slice()

    if (args[0] === 'saludar') {
      console.log(`Hola, ${args[1] || mundo}!`);
    } else if (args[0] === 'despedir') {
      console.log(`Chau ${args[1] || mundo}!`);
    } else {
      console.log("Comando no reconocido, intenta con 'saludar' o 'despedir'. ");
    }

Ahora lo probamos en la terminal

    node index.js saludar Megaboxt


En el ejemplo tenemos un programa que lee los `2 argumentos` siguientes a las instrucciones `node script.js` que ejecutan el programa. 
En función de los valores ingresados retorna un resultado:

- Si el primer argumento es “saludar” o “despedir” enviará un mensaje de bienvenida o despedida, caso contrario informa que el comando no es el apropiado.  

- Si existe un segundo argumento entonces el mensaje irá dirigido al nombre ingresado, caso contrario usará la palabra “mundo” para formular el saludo.  


## Consejos al utilizar `process.argv`  

1. Validar los argumentos: Asegúrate de manejar casos en los que no se pasen suficientes argumentos o se usen comandos inválidos.

2. Parámetros dinámicos: Puedes usar los argumentos para realizar tareas específicas, como leer archivos, realizar cálculos, o manejar interacciones más complejas.
