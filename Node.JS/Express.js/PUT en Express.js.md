# Creación de Solicitudes PUT en Express.js

El método PUT en Express.js se utiliza para actualizar un recurso existente en el servidor. Se puede implementar de la siguiente manera:

```javascript
const express = require('express');
const router = express.Router();

router.put('/:id', (req, res) => {
    const resourceId = req.params.id;
    // Obtener los datos enviados en el cuerpo de la solicitud
    const newData = req.body;
    
    // Realizar la actualización del recurso con el ID proporcionado
    // Ejemplo: actualización en la base de datos
    
    res.json({
        message: 'updated',
        resourceId: resourceId,
        newData: newData
    });
});

module.exports = router;
```

En este ejemplo, el enrutador captura peticiones PUT en una ruta específica que incluye el ID del recurso a actualizar. Luego, extrae los datos enviados en el cuerpo de la solicitud utilizando `req.body`, realiza la actualización del recurso y envía una respuesta JSON que confirma la actualización exitosa junto con los datos actualizados.
