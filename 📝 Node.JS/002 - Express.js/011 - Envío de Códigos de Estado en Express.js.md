# Envío de Códigos de Estado en Express.js

En Express.js, puedes enviar[ códigos de estado HTTP](../../🌐%20ConceptosGenerales/Códigos%20de%20Estado%20HTTP.md) en las respuestas a las solicitudes para indicar el resultado de la operación. Aquí tienes cómo hacerlo:

## Usando `res.status()` junto con `res.send()`

Puedes utilizar el método `res.status()` para establecer el código de estado HTTP y luego enviar una respuesta utilizando `res.send()` o `res.json()`:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    // Envío de un código de estado 200 (OK) junto con un mensaje
    res.status(200).send('¡Solicitud exitosa!');
});

app.post('/create', (req, res) => {
    // Envío de un código de estado 201 (Creado) junto con un objeto JSON
    res.status(201).json({ message: 'Recurso creado correctamente' });
});

app.delete('/remove', (req, res) => {
    // Envío de un código de estado 204 (Sin contenido) sin enviar datos
    res.status(204).send();
});

app.listen(3000, () => {
    console.log('Servidor Express escuchando en el puerto 3000');
});
```

En este ejemplo, se utilizan los métodos `res.status()` y `res.send()` para enviar diferentes códigos de estado HTTP en función del tipo de solicitud y el resultado de la operación.

## Utilizando los Métodos de Respuesta Específicos

Express.js también proporciona métodos de respuesta específicos para algunos códigos de estado comunes, como `res.sendStatus()` y `res.status().end()`:

```javascript
const express = require('express');
const app = express();

app.get('/not-found', (req, res) => {
    // Enviar un código de estado 404 (No encontrado) con un mensaje de texto
    res.sendStatus(404);
});

app.put('/update', (req, res) => {
    // Envío de un código de estado 204 (Sin contenido) sin enviar datos
    res.status(204).end();
});

app.listen(3000, () => {
    console.log('Servidor Express escuchando en el puerto 3000');
});
```

Estos métodos proporcionan una forma rápida y sencilla de enviar respuestas con códigos de estado específicos sin necesidad de especificar manualmente el mensaje de respuesta.

## Personalizando los Códigos de Estado

Puedes personalizar los mensajes de estado HTTP utilizando los métodos mencionados anteriormente junto con el método `res.set()` para establecer encabezados adicionales si es necesario:

```javascript
const express = require('express');
const app = express();

app.get('/custom', (req, res) => {
    // Envío de un código de estado personalizado (418 - Soy una tetera) con un mensaje personalizado
    res.status(418).send('Soy una tetera');
});

app.listen(3000, () => {
    console.log('Servidor Express escuchando en el puerto 3000');
});
```

En este ejemplo, se envía un código de estado HTTP personalizado 418 junto con un mensaje personalizado utilizando `res.status().send()`. Esto puede ser útil en situaciones donde necesitas indicar un estado específico que no está cubierto por los códigos de estado HTTP estándar.