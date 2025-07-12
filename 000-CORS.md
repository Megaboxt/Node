## CORS: Solicitudes entre dominios  

Las siglas CORS significan Cross-Origin Resource Sharing (Intercambio de Recursos entre Orígenes).  
El Control de Acceso HTTP (CORS) es un mecanismo que utiliza headers o cabeceras HTTP adicionales para permitir que un navegador web obtenga permiso para acceder a recursos específicos en un servidor que se encuentra en un origen (dominio) diferente al del propio documento, es decir, cuando quieres acceder a los recursos de un servidor desde otro servidor diferente.

Esto ocurre cuando un user agent (como un navegador) realiza una solicitud a un recurso en un dominio, protocolo o puerto diferente al del documento actual.

Un ejemplo de una solicitud de origen cruzado es cuando el código JavaScript de una aplicación web alojada en `http://dominio-a.com` utiliza `XMLHttpRequest` para cargar el recurso `http://api.dominio-b.com/data.json`.

Por razones de seguridad, los navegadores restringen las solicitudes HTTP de origen cruzado iniciadas por scripts. Por ejemplo, las APIs `XMLHttpRequest` y `Fetch` siguen la política de "mismo origen". Esto significa que una aplicación que utiliza estas APIs solo puede hacer solicitudes HTTP a su propio dominio, a menos que se utilicen cabeceras CORS.

