# Crear un Servidor Web con Node + Express.js  

Express es un framework minimalista y flexible que permite construir servidores web y APIs de forma ráapida y sencilla. Es ampliamente utilizado por su eficiencia en el manejo de rutas y middlewares, facilitando el desarrollo del backend.  

Una vez creados y configurados nuestros archivos `index.js` y `package.json`, tenemos que realizar la instalación del framework para comenzar a utilizarlo.  

>NOTA: recordá colocar la propiedad `"type": "module"` en el archivo `package.json` para poder importar y exportar código.

### Instalación y creación del Server

1. El primer paso es ejecutar el comando que se encarga de instalar Express como una dependencia en nuestro proyecto.

        npm install express

Al finalizar, se crea la carpeta `node_modules` en donde va a estar alojado el paquete de instalación, y en el archivo `package.json` se podrá ver el nombre de la dependencia y su versión.  

2. En el archivo `index.js` hay que importar el módulo de Express.

        import express from 'express';

3. Crear una variable que contenga y devuelva una nueva instancia de Express.

        const app = express();

4. Ahora podemos utilizar un método de express para responder a una solicitud HTTP enviada por el cliente. Por ejemplo el método `.get()` que solicita un recurso del servidor *sin modificarlo*

        app.get('/', (req, res) => {
            res.send('Hola desde el servidor Express !')
        });

5. Una vez definida nuestra ruta, debemos indicarle al servidor que puerto va a estar escuchando las peticiones. Podemos utilizar el método `.listen()` de Express para escucharlas.

        const PORT = 3000;
        
        app.listen( PORT, () => {
            console.log(`El servidor esta ejecutandose en el puerto: http://localhost:${PORT}`);
        })
