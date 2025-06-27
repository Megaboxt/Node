# Middlewares

Un middleware es una función que se ejecuta en el medio del camino entre, un cliente que hace una solicitud (request) y el servidor que devuelve una respuesta (response).  
En simples palabras, es una función intermediaria que puede *revisar, modificar o decidir* qué hacer con la solicitud antes de devolver algo al cliente.  


### Para qué se usan los middlewares ?

En Express se utilizan para: 

- Leer el cuerpo de una petición (`req.body`)

- Leer los cookies, headers o autenticación.

- Validar datos que llegan.

- Registrar Logs o estadísticas.

- Manejar errores.

- Proteger rutas (por ej: usuario logueado o no).

- Servir archivos estáticos.


### Estructura de un middleware 

Un middleware en express siempre tiene esta forma:  

    function ejemploMiddleware( req, res, next ) {
        // Lógica con req y res
        next(); // continuar con el siguiente middleware o ruta
    }




### Explicación de los parametros `req`, `res` y `next`:


#### 1. Objeto de Solicitud (Request - `req`)  

Es un objeto que representa todos los datos que el cliente está enviado al servidor. Tiene varias *Propiedades* que se pueden utilizar para obtener diferentes datos

| Propiedad                  | Qué representa ?                                                                                                         |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `req.method`               | El método HTTP que el cliente realizo al servidor ( `GET`, `POST`, `PUT`, `PATCH`, `DELETE`).                            |
| `req.url`                  | La ruta solicitada (por ej: `/productos/1`).                                                                             |
| `req.headers`              | Los headers HTTP (información adicional como `User-Agent`, `Authorization`, etc).                                        |
| `req.query`                | Los parámetros en la URL (Query String `?`, por ej: `?nombre=megaboxt`).                                                 |
| `req.params`               | Obtiene los parámetros de una ruta dinámica (`/productos/:id`).                                                          |
| `req.body`                 | El cuerpo de la petición (si es `POST`, `PUT`, etc.), se necesita utilizar `express.json()` para que esté disponible.    |



#### 2. Objeto de Respuesta (Response - `res`)

Este objeto se encarga de devolver una respuesta con algún tipo de dato al cliente. A diferencia del Objeto Response, este se maneja con *Métodos* para enviar los datos.

| Métodos                    | Para qué sirve ?                                                                                                         |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `res.send()`               | Envía una respuesta de texto o HTML o JSON.                                                                              |
| `res.json()`               | Envía una respuesta con `Content-Type: application/json`.                                                                |
| `res.status()`             | Cambia el estado de la solicitud HTTP que envió el cliente (por ej: `200`, `404`, `500`, etc.                            |
| `res.redirect()`           | Redirige a otra URL.                                                                                                     |
| `res.set()`                | Modifica los headers de la respuesta.                                                                                    |



#### 3. Función para Continuar al Siguiente Middleware - ( `next` )

Este parámetro es una función callback que lo llamas para decirle a Express *"Ya terminé el proceso, sigue con el siguiente Middleware"*.  

Si esta función *NO* se manda a llamar al final del bloque dentro del Middleware, el flujo se detiene y Express deja de procesar los Middlewares posteriores que hubiera.


    app.use( (req, res, next ) => {
        console.log("Middleware 1");
        next();
    });
    
    
    app.use( (req, res, next ) => {
        console.log("Middleware 2");
        next();
    });
    
    app.get('/', (req, res) => {
        res.send("Proceso de middlewares finalizado.")
    });



Tambien se le puede pasar a la función `next()` un `new Error()` para que Express pueda entender que hubo un error en esa ruta y salta directamente al siguiente Middleware.


    app.use( (req,res, next) => {
        const autorizado = false;
    
        if (!autorizado) {
            return next(new Error("No Autorizado"));
        }
    
        next();
    })




## Ejemplo completo de un caso real *validando los datos de un formulario*


    import express from 'express';
    const app = express();
    
    // Middleware de Express que sirve para leer peticiones con datos JSON en req.body
    app.use(express.json());
    
    // Middleware para validar un formulario 
    function validarFormulario(req, res, next) {
        const { nombre, email, mensaje } = req.body;
    
        if ( !nombre || !email || !mensaje ) {
            return res.status(400).json({
                error: "Faltan campos obligatorios. Se requiere: nombre, email y un mensaje."
            });
        }
    
        next();
    }
    
    // Creamos la ruta para poder hacer la simulación de la petición y envio de datos desde un formulario con POSTMAN o Thunder Client
    app.post('/contacto', validarFormulario, (req, res) => {
        const { nombre, email, mensaje } = req.body;
    
        res.status(200).json({
            mensaje: `Gracias por tu mensaje, ${nombre}. Te responderemos a la brevedad a tu email: ${email}`
        })
    })
    
    // Creando un puerto para escuchar peticiones
    const PORT = 3000;
    app.listen( PORT, () => {
        console.log(`Servidor corriendo en el puerto: http://localhost:${PORT}`);
    });


Construimos un servidor en Express que contiene:

- Una ruta `/contacto` que recibe peticiones HTTP de tipo `POST`.

- Un middleware que verifica que el Objeto enviado por el cliente contenga los datos obligatorios `nombre`, `email` y `mensaje`, si falta alguno, devuelve un mensaje de error.




