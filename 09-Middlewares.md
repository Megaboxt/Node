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

Explicación de los parametros `req`, `res` y `next`:

1. Objeto de solicitud Request (`req`) : Es un objeto que representa todos los datos que el cliente está enviado al servidor. Tiene varias propiedades que se pueden utilizar para obtener diferentes datos

| Propiedad                  | Qué representa ?                                                                                                         |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------|
| `req.method`               | El método HTTP que el cliente realizo al servidor ( `GET`, `POST`, `PUT`, `PATCH`, `DELETE`).                            |
| `req.url`                  | La ruta solicitada (por ej: `/productos/1`).                                                                             |
| `req.headers`              | Los headers HTTP (información adicional como `User-Agent`, `Authorization`, etc).                                        |
| `req.query`                | Los parámetros en la URL (Query String `?`, por ej: `?nombre=megaboxt`).                                                 |
| `req.params`               | Obtiene los parámetros de una ruta dinámica (`/productos/:id`).                                                          |
| `req.body`                 | El cuerpo de la petición (si es `POST`, `PUT`, etc.), se necesita utilizar `express.json()` para que esté disponible.    |

- `res`: Es la respuesta que envia el servidor que creamos

- `next`: Es una función que se encarga de continuar a la siguiente tarea.

