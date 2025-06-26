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

4. Ahora podemos utilizar un método de express para crear una ruta y responder a una solicitud HTTP enviada por el cliente. Por ejemplo el método `.get()` que solicita un recurso del servidor *sin modificarlo*

        app.get('/', (req, res) => {
            res.send('Hola desde el servidor Express !')
        });

5. Una vez definida nuestra ruta, debemos indicarle al servidor que puerto va a estar escuchando las peticiones. Podemos utilizar el método `.listen()` de Express para escucharlas.

        const PORT = 3000;
        
        app.listen( PORT, () => {
            console.log(`El servidor esta ejecutandose en el puerto: http://localhost:${PORT}`);
        })


### Ventajas de Utilizar Express

- Simplicidad: Proporciona una API sencilla para manejar rutas y solicitudes HTTP.

- Flexibilidad: Permite integrar `middlewares` y otras librerías con facilidad.

- Ecosistema: Cuenta con una amplia comunidad y multiples extensiones.


# Express Generator  

Express Generator es una herramienta que nos brinda el equipo de Express.js para crear una estructura inicial de un proyecto de manera automática y predeterminada.        
Su objetivo es agilizar la configuracion inicial y crear los archivos y directorios necesarios para comenzar con un proyecto en Express.

La estructura incluye: 

- Estructura de capertas predefinida: `public`, `routes` y `views`.

- Plantillas integradas: Orefece compatibilidad con motores de plantillas como `Pug`, para facilitar la generación de vistas dinámicas.

- Archivos de configuración inicial: Configura mdulos y middlewares esenciales desde el inicio.

### Instalando y Creando un proyecto con Express Generator

1. El primer paso es instalar la herramienta de forma global, de modo que se pueda crear un proyecto desde cualquier sitio de la PC.

        npm install -g express-generator

2. Ahora podemos crear un proyecto desde cualquier directorio o ruta del PC. Para crear un nuevo proyecto hay que ejecutar el siguiente comando:

        express nombre-del-proyecto

3. Esto creará una carpeta con la estructura mencionada anteriormente, asi que accedemos a ella.

        cd nombre-del-proyecto

4. Una vez entramos al directorio donde se encuentra alojado el proyecto, debemos descargar el gestor de paquetes NPM.

        npm install

5. Terminada la instalación y configuración del proyecto, creamos el archivo `index.js` y lo configuramos en este caso, para leer archivos estáticos.

        import express from 'express';
        import { join, dirname } from 'path';
        import { fileURLToPath } from 'url';
        
        const __filename = fileURLToPath(import.meta.url);
        const __dirname = dirname(__filename);
        
        const app = express();
        
        // Configurar middleware para servir archivos estáticos
        app.use( express.static( join(__dirname, 'public')));
        
        const PORT = 3000;
        
        app.listen( PORT, () => {
            console.log(`Servidor corriendo en el puerto: http://localhost:${PORT}`);
            
        });

7. Agregamos contenido en nuestros archivos estáticos, por ejemplo en un archivo `index.html`.

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>Servidor de archivos estaticos</title>
        </head>
        <body>
            <h1>Hola mundo desde mi servidor de archivos estaticos</h1>
        </body>
        </html>

8. Y corremos nuestro servidor en el puerto que tengamos de referencia para poder ver el sitio web estático.

        npm start
