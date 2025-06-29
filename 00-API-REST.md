# API REST - (Representational State Transfer) 


Es un Patrón de Arquitectura que se utiliza para desarrollar Aplicaciones Web y Servicios, mediante el uso de URLs específicas y el uso de los verbos HTTP (GET, POST, PUT, PATCH, DELETE). Este enfoque permite a los sistemas interactuar entre sí de manera eficiente, asegurando que las solicitudes y respuestas sean entendidas sin importar la plataforma involucrada en realizar las peticiones.  
*REST establece principios arquitectónicos que te guían para saber cómo diseñar un modelo de Servicios Web.*

Los datos en una API REST se transmiten comúnmente en formato JSON o XML, a veces en lenguaje HTML.




## Cómo diseñar una API REST ?  

Estos serían los pasos a tener en cuenta para armar una API REST:

- Definir los `recursos`: Los recursos se les llama a las entidades como los `usuarios`, `productos` y diferentes "entidades" que sean necesarias para el proyecto.

- Definir la `Estructura de la URL`: Crear URLs descriptivas para cada recurso, separando elementos con barras.

- Utilizar los `verbos HTTP`: Para realizar las peticiones al servidor `GET`, `POST`, etc.

- Utilizar el `formato de datos` correcto: Según el tipo de operación, asegurarse que sea JSON o XML o HTML.

- Utilizar los `códigos de Estado HTTP`: Utilizar los códigos de estado para informar el resultado de la operación, por ejemplo el código `200` para dar "status ok" o el código `404` para un "bad request".

- Utilizar la `Autenticación` y `Autorización`: Proteger la API RESTful mediante la autenticación y la autorización de los usuarios que quieran acceder a los recursos.   

- Utilizar la `Documentación`: Documentar la API REST para que los consumidores puedan entender cómo utilizarla y qué recursos están disponibles.  



## Estructura de Archivos  

La estructura de archivos nos ayuda a que el código esté ordenado según su propósito, en este caso se va a crear una estructura basada en Capas.  

![image](https://github.com/user-attachments/assets/87e874fc-5d9e-4ac7-a417-d5582ff2192f)


En la estructura podemos notar los siguientes directorios: 

- `src`: Es la carpeta principal, que se encarga de separar los archivos principales y de configuración del resto de la aplicación.

- La carpeta `routes`: Donde se configuran las rutas o "entradas" a nuestra API.

- La carpeta `controllers`: Donde se define qué debe pasar cuando alguien usa esas rutas.

- Otra carpeta llamada `models`: Que se encarga de conectar con la Base de Datos y define cómo se van a ver los datos.

- A veces se puede utilizar una carpeta llamada `services`, donde organizamos toda la lógica que no tiene que ver directamente con la Base de Datos o con responder solicitudes.

