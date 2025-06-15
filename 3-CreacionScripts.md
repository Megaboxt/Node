## Creación de scripts  

Otra de las ventajas que nos aporta el archivo package.json es permitirnos definir o preestablecer determinados scripts que nos permitirán ejecutar distintos procesos de nuestro código.  

Según lo visto anteriormente, sabemos que desde la terminal con el comando `node index.js` podemos ejecutar el código de este archivo sin problema, sin embargo, muchas veces los comandos de ejecución llevan variables de configuración lo que provoca que sean bastante más largos y difíciles de recordar, por eso podemos aprovechar el archivo `package.json` para definir determinados comandos de ejecución:  


<pre>
  {
    "type": "module",
    "scripts": {
      "dev": "nodemon index.js",
      "saludo": "echo ¡Hola desde npm run saludo!"
      "start": "node index.js",
    }
  }
</pre>

## Cómo se ejecuta un Script ? 

Desde la terminal tenemos que ejecutar el comando `npm run` seguido del nombre del Script:

<pre>
  npm run dev
</pre>

<pre>
  npm run saludo
</pre>

<pre>
  npm start
</pre>

*Este último es un caso especial ya que, no necesita la palabra `run`*
