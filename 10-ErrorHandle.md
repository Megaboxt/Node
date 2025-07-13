# Error Handling - (Manejo de Errores) 

Es frecuente que un cliente envíe una solicitud a una ruta que nuestro servidor no tiene definida. Esto podría ocurrir por errores en la URL, intentos de acceso a recursos inexistentes o simples exploraciones.  
Para solucionar esto, utilizamos un middleware que se ejecutará ***después de haber evaluado todas las rutas definidas en la aplicación***. 
Este middleware capturará cualquier solicitud no gestionada previamente y responderá con un mensaje estandarizado, indicando que el recurso solicitado no existe.  


    import express from 'express';
    import cors from 'cors';
    
    const app = express();
    
    // Configuración básica: Permitir todos los orígenes
    app.use(cors());
    
    app.get('/item/12345', (req, res) => {
      // lógica para DEVOLVER el item solicitado
    });
    
    app.delete('/item/12345', (req, res) => {
      // lógica para ELIMINAR el item solicitado
    });
    
    // Middleware para manejar errores 404
    app.use((req, res, next) => {
      res.status(404).send('Recurso no encontrado o ruta inválida');
    });


En este código, después de declarar las rutas "válidas", agregamos un middleware que captura cualquier solicitud no manejada previamente. Este middleware utiliza el método app.use() y envía al cliente una respuesta con el código de estado 404, que es el estándar HTTP para indicar que un recurso no fue encontrado.
