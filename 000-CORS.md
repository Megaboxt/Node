## CORS: Solicitudes entre dominios  

Las siglas CORS significan Cross-Origin Resource Sharing (Intercambio de Recursos entre Orígenes).  
El Control de Acceso HTTP (CORS) es un mecanismo que utiliza headers o cabeceras HTTP adicionales para permitir que un navegador web obtenga permiso para acceder a recursos específicos en un servidor que se encuentra en un origen (dominio) diferente al del propio documento, es decir, cuando quieres acceder a los recursos de un servidor desde otro servidor diferente.

Esto ocurre cuando un user agent (como un navegador) realiza una solicitud a un recurso en un dominio, protocolo o puerto diferente al del documento actual.

Un ejemplo de una solicitud de origen cruzado es cuando el código JavaScript de una aplicación web alojada en `http://dominio-a.com` utiliza `XMLHttpRequest` para cargar el recurso `http://api.dominio-b.com/data.json`.

Por razones de seguridad, los navegadores restringen las solicitudes HTTP de origen cruzado iniciadas por scripts. Por ejemplo, las APIs `XMLHttpRequest` y `Fetch` siguen la política de "mismo origen". Esto significa que una aplicación que utiliza estas APIs solo puede hacer solicitudes HTTP a su propio dominio, a menos que se utilicen cabeceras CORS.  



## ¿Qué peticiones utiliza CORS?  

El estándar de intercambio de origen cruzado (CORS) se utiliza para habilitar las siguientes solicitudes HTTP de sitios cruzados:

1. Invocaciones de las APIs XMLHttpRequest o Fetch en un contexto de sitio cruzado.

2. Fuentes web (utilizadas en dominios cruzados con la regla @font-face dentro de CSS), permitiendo que los servidores muestren fuentes TrueType que solo pueden ser cargadas por sitios cruzados y utilizadas por sitios web autorizados.

3. Texturas en WebGL.

4. Imágenes dibujadas en patrones utilizando drawImage.

5. Acceso a hojas de estilo (CSSOM).

6. Ejecución de scripts (para excepciones inmutables).



## ¿Cómo habilitar solicitudes de origen cruzado?  

Hay distintas formas de hacerlo, la primera es manual y para ello vamos a utilizar el header `Access-Control-Allow-Origin` junto a otros similares.

En nuestro archivo `index.js` de nuestro servidor web, vamos a colocar el siguiente middleware:



    app.use((req, res, next) => {
      // // Permitir un dominio
      res.header('Access-Control-Allow-Origin', 'https://example.com');
      
      // Métodos permitidos
      res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
      
      // Encabezados permitidos
      res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
      
      // Permitir cookies/credenciales
      res.header('Access-Control-Allow-Credentials', 'true');
    
      // Funcion next para seguir al siguiente middleware
      next();
    });



El ejemplo anterior nos permite conceder determinados permisos en nuestra aplicación y al hacerlo a través de un `middleware global` nos aseguramos que las validaciones se realicen frente a cada petición.


Sin embargo, este método a veces suele resultar algo verboso y tedioso de escalar, es por ello que podemos utilizar una librería externa llamada cors para manejar estos permisos de forma más sencilla.


#### Instalamos la siguiente dependencia:


    npm install cors


Configuramos un `middleware global` con la implementación de la nueva librería:



    import express from 'express';
    import cors from 'cors';
    const app = express();
    
    // Configuración básica: Permitir todos los orígenes
    app.use(cors());

    
    // Configuración avanzada: Permitir dominios específicos
    const corsOptions = {
      // Dominios permitidos
      origin: ['https://example.com', 'https://anotherdomain.com'],
      
      // Métodos HTTP permitidos
      methods: ['GET', 'POST', 'PUT', 'DELETE'],
      
      // Encabezados permitidos
      allowedHeaders: ['Content-Type', 'Authorization'],
      credentials: true // Permitir cookies o credenciales
    };
    
    app.use(cors(corsOptions));




En el ejemplo anterior tenemos 2 implementaciones de cors, la primera es una implementación básica que permite peticiones de cualquier origen y la otra es una implementación avanzada que determina mayores parámetros de configuración.
