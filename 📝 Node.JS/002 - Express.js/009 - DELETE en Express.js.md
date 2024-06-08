# Creación de Solicitudes DELETE en Express.js

El método DELETE en Express.js se utiliza para eliminar un recurso existente en el servidor. Se puede implementar de la siguiente manera:

```javascript
const express = require('express');
const router = express.Router();

router.delete('/:id', (req, res) => {
    const resourceId = req.params.id;
    
    // Eliminar el recurso con el ID proporcionado
    // Ejemplo: eliminación en la base de datos
    
    res.json({
        message: 'deleted',
        resourceId: resourceId
    });
});

module.exports = router;
```

En este ejemplo, el enrutador captura peticiones DELETE en una ruta específica que incluye el ID del recurso a eliminar. Luego, elimina el recurso con el ID proporcionado y envía una respuesta JSON que confirma la eliminación exitosa junto con el ID del recurso eliminado.