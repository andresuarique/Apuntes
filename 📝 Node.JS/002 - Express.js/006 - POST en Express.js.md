# Creación de Solicitudes POST en Express.js

Para crear un endpoint que maneje peticiones de tipo POST en Express.js, es importante configurar el servidor para que pueda procesar los datos enviados desde el cliente. A continuación, se muestra cómo se puede implementar esta funcionalidad:

## Configuración del Servidor

En el archivo principal de tu aplicación, generalmente llamado `index.js` o `app.js`, asegúrate de configurar Express para que pueda procesar los datos enviados en formato JSON. Esto se puede lograr utilizando el [middleware](../../🌐%20ConceptosGenerales/Middleware.md) `express.json()` proporcionado por Express. Asegúrate de agregar esta configuración antes de definir tus rutas:

```javascript
const express = require('express');
const app = express();

// Configuración para procesar datos JSON
app.use(express.json());

// Define tus rutas después de configurar el middleware
// Ejemplo: app.use('/api/products', productsRouter);

// Inicia el servidor
const port = 3000;
app.listen(port, () => {
    console.log(`Servidor escuchando en el puerto ${port}`);
});
```

## Manejo de Peticiones POST en una Ruta Específica

Una vez configurado el servidor para procesar datos JSON, puedes definir tus rutas para manejar peticiones POST. Por ejemplo, aquí hay un enrutador que maneja peticiones POST en el endpoint `/api/products`:

```javascript
const express = require('express');
const router = express.Router();

router.post('/', (req, res) => {
    // Obtén los datos enviados en el cuerpo de la solicitud
    const body = req.body;
    
    // Realiza cualquier procesamiento necesario con los datos
    // En este caso, simplemente los devolvemos en la respuesta
    res.json({
        message: 'created',
        data: body
    });
});

module.exports = router;
```

En este ejemplo, el enrutador captura peticiones POST en la ruta `/api/products` y extrae los datos enviados en el cuerpo de la solicitud utilizando `req.body`. Luego, realiza cualquier procesamiento necesario con los datos y envía una respuesta JSON que confirma la creación exitosa junto con los datos enviados.

## Probando el Endpoint POST

Para probar el endpoint POST que has creado, puedes utilizar herramientas como Insomnia o Postman. Envía una solicitud POST a la ruta especificada (`/api/products` en este caso) con los datos que deseas enviar en el cuerpo de la solicitud. Luego, verifica la respuesta recibida del servidor para asegurarte de que se haya procesado correctamente.