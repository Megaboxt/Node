# API REST - (Representational State Transfer) 

Partiendo de la base de que, una API es un conjunto de reglas que permite a dos aplicaciones comunicarse entre sí. REST es un Patrón de Arquitectura que se utiliza para diseñar APIs simples, legibles y escalables.  

Mediante el uso de URLs específicas y el uso de los verbos HTTP (GET, POST, PUT, PATCH, DELETE). Este enfoque permite a los sistemas interactuar entre sí de manera eficiente, asegurando que las solicitudes y respuestas sean entendidas sin importar la plataforma involucrada en realizar las peticiones.  

*REST establece principios arquitectónicos que te guían para saber cómo diseñar un modelo de Servicios Web.*

Los datos en una API REST se transmiten comúnmente en formato JSON o XML, a veces en lenguaje HTML.



### Principios clave de REST:

- Cliente-Servidor: Separación entre la interfaz de usuario y la lógica de datos.

- Sin estado (Stateless): Cada solicitud lleva toda la información necesaria. No se guarda el estado en el servidor entre solicitudes.

- Caché: Las respuestas deben indicar si son cacheables.

- Interfaz uniforme: Todo recurso se accede con una URL y métodos estándar.

- Sistema en capas: Podés tener varios niveles (servidor, base de datos, seguridad).

- Código bajo demanda (opcional): El servidor puede enviar scripts para que el cliente los ejecute.



## Estructura de Archivos  

La estructura de archivos nos ayuda a que el código esté ordenado según su propósito, en este caso se va a crear una estructura basada en `Capas`.  

  ![image](https://github.com/user-attachments/assets/87e874fc-5d9e-4ac7-a417-d5582ff2192f)


En la estructura podemos notar los siguientes directorios:  

- `src`: Es la carpeta principal, que se encarga de separar los archivos principales y de configuración del resto de la aplicación.

- La carpeta `routes`: Donde se configuran las rutas o "entradas" a nuestra API.

- La carpeta `controllers`: Donde se define qué debe pasar cuando alguien usa esas rutas.

- Otra carpeta llamada `models`: Que se encarga de conectar con la Base de Datos y define cómo se van a ver los datos.

- A veces se puede utilizar una carpeta llamada `services`, donde organizamos toda la lógica que no tiene que ver directamente con la Base de Datos o con responder solicitudes.



## Capas de la Aplicación  

Cuando hablamos de las capas de una aplicación, nos referimos a cómo dividimos las responsabilidades dentro del sistema para que cada parte se encargue de algo específico.  
En el caso de una API Rest, dividirla en capas nos ayuda a manejar mejor el código, hacer cambios sin romper todo y trabajar en equipo más fácilmente.  
Las capas se forman en los directorios anteriormente creados.

## Rutas  

Cuando hablamos de rutas en una API Rest, nos referimos a los "puntos de entrada" también conocidos como `endpoints`, que los clientes (como aplicaciones o navegadores) usan para interactuar con nuestra aplicación. Cada ruta es como una dirección que lleva a un recurso específico dentro de la API y define qué se puede hacer con ese recurso.  
Por ejemplo, podrías tener una ruta para listar todos los usuarios, otra para crear uno nuevo y otra para eliminarlo.  

Las rutas se construyen combinando una URL específica con un método HTTP. Los métodos más comunes son:

- GET, para obtener información (como listar usuarios).
- POST, para crear algo nuevo (como registrar un usuario).
- PUT o PATCH, para actualizar información (como cambiar el correo de un usuario).
- DELETE, para eliminar recursos (como borrar un usuario). 


En la práctica, las rutas suelen organizarse en un archivo específico dentro de una carpeta llamada `routes` o similar.  
Por ejemplo, podrías tener un archivo `users.routes.js` que agrupe todas las rutas relacionadas con usuarios.  
Esto no solo mantiene el código más organizado, sino que también hace que sea más fácil encontrar y modificar rutas en el futuro.


## Controladores

Los controladores son como el "centro de comando" de las solicitudes. Es decir, son los responsables es procesar, delegar y responder, la lógica que conecta las rutas con el resto de la aplicación, actuando como un puente entre las solicitudes del cliente y los datos o servicios que necesitamos usar.

Por ejemplo, si tienes una API que maneja usuarios, podrías tener un controlador llamado `users.controller.js` con funciones como estas:

- getAllUsers(req, res): Maneja la solicitud para obtener una lista de usuarios y devuelve una respuesta con esa información.

- getUserById(req, res): Busca un usuario específico basado en un parámetro como el id que llega en la solicitud.

- createUser(req, res): Procesa los datos enviados en la solicitud para crear un nuevo usuario.

- updateUser(req, res): Recibe datos actualizados y los aplica a un usuario existente.

- deleteUser(req, res): Se encarga de eliminar un usuario específico.



## Modelos  

En una API, los modelos son como los planos de una máquina: describen cómo deben verse los datos y cómo deben comportarse al interactuar con la base de datos. Actúan como un “esquema” o “molde” que define la estructura de una entidad, permitiéndonos trabajar de forma ordenada y predecible con la información.

Por ejemplo, si estamos desarrollando una tienda en línea, podríamos tener un modelo llamado Product que represente cómo se ve un objeto producto. Este modelo incluiría propiedades como el nombre del producto, su precio, descripción, y categorías, además de especificar el tipo de datos que se espera para cada propiedad.

Los modelos no solo definen la estructura de los datos, sino que también nos facilitan el acceso y manipulación de información almacenada en bases de datos, ya sean relacionales(SQL) o no relacionales (NoSQL).


Ejemplo de modelo utilizando MongoDB con librería Mongoose:

    const userSchema = new mongoose.Schema({
      name: { type: String, required: true },
      email: { type: String, required: true, unique: true },
      password: { type: String, required: true },
      createdAt: { type: Date, default: Date.now }
    });

Este esquema define cómo lucirá un objeto usuario cada vez que accedamos a los datos de uno o más usuarios en la base de datos.  



## Servicios  

Los servicios son una parte clave de la arquitectura de una API Rest y actúan como los “motores” que realizan las operaciones necesarias para cumplir con las solicitudes que llegan a la API. Su función principal es manejar la lógica de negocio de la aplicación, es decir, todas las reglas y procesos que determinan cómo los datos deben ser tratados.


Los servicios se encuentran entre los `controladores` y los `modelos`:

- Desde el controlador, reciben las solicitudes para ejecutar tareas específicas.

- Hacia los modelos, envían solicitudes para obtener o modificar datos en la base de datos, o en otros casos, procesan datos externos.

Al estructurar la lógica de negocio en los servicios, evitamos que los controladores o los modelos se vuelvan demasiado complejos o cargados de responsabilidades. Esto facilita el mantenimiento y la escalabilidad del código.


Ejemplo de un servicio en una API Rest

Supongamos que estamos trabajando en una API para gestionar productos, y queremos implementar una lógica para obtener todos los productos que están en stock:


    // product.service.js  
    
    const productModel = require('./product.model');
    
    async function getProductsInStock() {
      const products = await productModel.getAllProducts();
      return products.filter( product => product.stock > 0);
    }
    
    async function addNewProduct(productData) {
      if (!productData.name || !productData.price) {
        throw new Error("El nombre y el precio del producto son obligatorios.");
      }
    
      if (productData <= 0) {
        throw new Error("El precio debe ser mayor que cero.");
      }
    
      return await productModel.createProduct(productData);
    }
    
    
    module.exports = {
      getProductsInStock,
      addNewProduct
    }


## Explicación del ejemplo

1. getProductsInStock: El servicio solicita todos los productos al modelo y luego filtra los que tienen stock disponible. La lógica de filtrado se queda aquí, separada del controlador y del modelo.

2. addNewProduct: Antes de crear un nuevo producto, este servicio valida que los datos cumplan con ciertas reglas de negocio, como asegurarse de que el precio sea mayor que cero y que los campos esenciales estén presentes. Si las reglas no se cumplen, lanza un error.

La capa de servicios es esencial para manejar la lógica de negocio de manera organizada y eficiente. Su implementación no solo mejora la claridad y el mantenimiento del código, sino que también prepara a tu API para ser más flexible y escalable, permitiendo que puedas adaptarla fácilmente a nuevas necesidades o requisitos futuros.
