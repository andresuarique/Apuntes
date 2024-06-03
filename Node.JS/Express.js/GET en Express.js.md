# Creación de Solicitudes GET en Express.js

En Express.js, puedes crear solicitudes GET para manejar tanto rutas sin parámetros como rutas con parámetros, incluyendo parámetros de tipo URL y parámetros de tipo query. A continuación, se explica cómo hacerlo

## Solicitudes GET sin Parámetros

Para manejar solicitudes GET en Express.js sin parámetros, simplemente define una ruta utilizando el método `get()` de tu aplicación y proporciona un manejador de solicitud que se ejecutará cuando se realice una solicitud GET a esa ruta.

```js
// Manejo de una solicitud GET sin parámetros
app.get('/ruta', (req, res) => {
  res.send('Respuesta a una solicitud GET sin parámetros.');
});
```

En este ejemplo, cuando se realiza una solicitud GET a la ruta `/ruta`, se envía una respuesta con el mensaje "Respuesta a una solicitud GET sin parámetros".

## Solicitudes GET con Parámetros de Tipo URL

Los parámetros de tipo URL se incluyen directamente en la URL de la solicitud. Para manejar solicitudes GET con parámetros de tipo URL en Express.js, define una ruta con una parte de la URL que actúe como un marcador de posición para el parámetro, y luego accede a ese parámetro a través del objeto `req.params`.

```js
// Manejo de una solicitud GET con parámetros de tipo URL
app.get('/ruta/:parametro', (req, res) => {
  const parametro = req.params.parametro;
  res.send(`Respuesta a una solicitud GET con parámetro de tipo URL: ${parametro}`);
});
```

En este ejemplo, cuando se realiza una solicitud GET a la ruta `/ruta/valor`, donde `valor` es el parámetro de tipo URL, se envía una respuesta con el mensaje "Respuesta a una solicitud GET con parámetro de tipo URL: valor".

## Solicitudes GET con Parámetros de Tipo Query

Los parámetros de tipo query se incluyen en la URL de la solicitud después del signo de interrogación (`?`). Para manejar solicitudes GET con parámetros de tipo query en Express.js, accede a esos parámetros a través del objeto `req.query`.

```js
// Manejo de una solicitud GET con parámetros de tipo query
app.get('/ruta', (req, res) => {
  const parametro = req.query.parametro;
  res.send(`Respuesta a una solicitud GET con parámetro de tipo query: ${parametro}`);
});
```

En este ejemplo, cuando se realiza una solicitud GET a la ruta `/ruta?parametro=valor`, donde `parametro` es el parámetro de tipo query, se envía una respuesta con el mensaje "Respuesta a una solicitud GET con parámetro de tipo query: valor".