# Aplicación de Verbos HTTP en Express.js

En Express.js, los[[Métodos HTTP| verbos HTTP]] se utilizan para definir las operaciones que se pueden realizar en diferentes rutas de una aplicación. A continuación, se muestra cómo se aplican los principales verbos HTTP en Express.js:

## GET

El verbo GET se utiliza para solicitar datos de un recurso específico. En Express.js, se define una ruta con el método `get()` y se proporciona un manejador de solicitud que se ejecutará cuando se realice una solicitud GET a esa ruta.

```js
app.get('/ruta', (req, res) => {
  res.send('Respuesta a una solicitud GET.');
});
```

## POST

El verbo POST se utiliza para enviar datos a un servidor para crear un nuevo recurso. En Express.js, se define una ruta con el método `post()` y se proporciona un manejador de solicitud que se ejecutará cuando se realice una solicitud POST a esa ruta.

```js
app.post('/ruta', (req, res) => {
  res.send('Datos enviados a través de una solicitud POST.');
});
```

## PUT

El verbo PUT se utiliza para actualizar un recurso existente en el servidor. En Express.js, se define una ruta con el método `put()` y se proporciona un manejador de solicitud que se ejecutará cuando se realice una solicitud PUT a esa ruta.

```js
app.put('/ruta', (req, res) => {
  res.send('Actualización realizada con una solicitud PUT.');
});
```

## DELETE

El verbo DELETE se utiliza para eliminar un recurso existente en el servidor. En Express.js, se define una ruta con el método `delete()` y se proporciona un manejador de solicitud que se ejecutará cuando se realice una solicitud DELETE a esa ruta.

```js
app.delete('/ruta', (req, res) => {
  res.send('Recurso eliminado con una solicitud DELETE.');
});
```

En resumen, en Express.js, los verbos HTTP se aplican utilizando métodos específicos de enrutamiento (`get()`, `post()`, `put()`, `delete()`) para definir cómo la aplicación debe responder a diferentes tipos de solicitudes HTTP en rutas específicas.