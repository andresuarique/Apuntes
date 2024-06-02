
# Creación de Solicitudes PATCH en Express.js

El método PATCH en Express.js se utiliza para aplicar modificaciones parciales a un recurso existente en el servidor. Se puede implementar de manera similar a PUT:

```javascript
const express = require('express');
const router = express.Router();

router.patch('/:id', (req, res) => {
    const resourceId = req.params.id;
    // Obtener los datos enviados en el cuerpo de la solicitud
    const patchData = req.body;
    
    // Aplicar modificaciones parciales al recurso con el ID proporcionado
    // Ejemplo: actualización parcial en la base de datos
    
    res.json({
        message: 'patched',
        resourceId: resourceId,
        patchData: patchData
    });
});

module.exports = router;
```

En este ejemplo, el enrutador captura peticiones PATCH en una ruta específica que incluye el ID del recurso a modificar. Luego, extrae los datos enviados en el cuerpo de la solicitud utilizando `req.body`, aplica las modificaciones parciales al recurso y envía una respuesta JSON que confirma la modificación exitosa junto con los datos modificados.
