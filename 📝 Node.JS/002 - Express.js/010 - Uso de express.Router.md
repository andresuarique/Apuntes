# Uso de express.Router en Express.js

En Express.js, el uso de `express.Router()` permite modularizar y organizar las rutas de una aplicación de manera eficiente. Esto es útil para seguir el principio de responsabilidad única (SRP), donde cada módulo o clase debe tener responsabilidad sobre una sola parte de la funcionalidad. A continuación, se explica cómo aplicar `express.Router()` en Express.js para gestionar diferentes entidades con sus propias rutas.

## Estructura de Carpetas y Archivos

Se crea una carpeta llamada `routes` en la raíz del proyecto, donde se almacenarán los archivos de enrutador para cada entidad. Cada archivo de enrutador, como `product.router.js`, `category.router.js` y `user.router.js`, contendrá las rutas correspondientes para esa entidad.

## Definición de Rutas

En cada archivo de enrutador, se define un enrutador utilizando `express.Router()`. Se definen las rutas específicas para esa entidad utilizando los [métodos HTTP](../../🌐%20ConceptosGenerales/Métodos%20HTTP.md) correspondientes, como `get()`, `post()`, `put()`, `delete()`, etc.

Por ejemplo, en `product.router.js`:

```javascript
const express = require('express');
const { faker } = require('@faker-js/faker');
const router = express.Router();

router.get('/', (req, res) => {
    // Lógica para obtener productos
});

router.get('/:id', (req, res) => {
    // Lógica para obtener un producto por su ID
});

// Más rutas para operaciones CRUD de productos...

module.exports = router;
```

## Importación en el Archivo de Enrutador Principal

En el archivo `routes/index.js` se deben importar los enrutadores individuales y aplicarlos a la aplicación Express. Aquí tienes cómo debe ser esa implementación:

```javascript
const productsRouter = require('./products.router');
const categoriesRouter = require('./categories.router');
const usersRouter = require('./users.router');

const routerApi = (app) => {
    app.use('/api/products', productsRouter);
    app.use('/api/categories', categoriesRouter);
    app.use('/api/users', usersRouter);
}

module.exports = routerApi;
```

Este archivo se encarga de importar cada enrutador individual y aplicarlos a la aplicación Express utilizando `app.use()`. Así, cada enrutador se monta en una ruta base específica, como `/api/products`, `/api/categories` y `/api/users`, respectivamente.
## Importación en el Archivo Principal

En el archivo principal, como `index.js`, se importan y se utilizan los enrutadores para cada entidad. Se define una función `routerApi` que acepta la aplicación Express como parámetro y utiliza los enrutadores importados para definir las rutas.

```javascript
const express = require('express');
const app = express();

const routerApi = require('./routes');

routerApi(app);

const port = 3000;
app.listen(port, () => {
    console.log(`Listening on port ${port}`);
});
```

## Modularización de la Aplicación

Al modularizar la aplicación de esta manera, cada entidad tiene su propio enrutador con sus propias rutas y es responsable de gestionar solo lo correspondiente a esa entidad. Esto facilita el mantenimiento y la escalabilidad de la aplicación, siguiendo el principio de responsabilidad única.

## Ejemplo de Uso

Al visitar las URL correspondientes, como `/api/products`, `/api/categories` o `/api/users`, la aplicación responderá con los datos correspondientes para cada entidad, siguiendo la estructura definida en los enrutadores.

Con esta estructura, se logra una organización clara y eficiente de las rutas en una aplicación Express.js, lo que facilita su mantenimiento y desarrollo.

## Versionando APIs

Versionar una API es una práctica común en el desarrollo de software para evitar conflictos y problemas de compatibilidad entre diferentes versiones de la misma API. En Express.js, se puede implementar el versionado de la API de manera sencilla utilizando enrutadores (`Router`).


Para versionar una API en Express.js, se puede utilizar un enfoque basado en enrutadores. A continuación, se muestra un ejemplo de cómo se puede versionar una API utilizando enrutadores:

```javascript
const express = require('express');
const app = express();

// Importar enrutadores de cada versión de la API
const v1Router = require('./routes/v1');
const v2Router = require('./routes/v2');

// Asignar enrutadores a las rutas de la API
app.use('/api/v1', v1Router);
app.use('/api/v2', v2Router);

// Iniciar el servidor
const port = 3000;
app.listen(port, () => {
    console.log(`Servidor escuchando en el puerto ${port}`);
});
```

En este ejemplo, se importan dos enrutadores, `v1Router` y `v2Router`, que contienen las rutas y controladores específicos de cada versión de la API. Luego, se asignan estos enrutadores a rutas específicas de la API, como `/api/v1` y `/api/v2`. De esta manera, cada versión de la API tiene su propio conjunto de rutas y controladores, lo que permite introducir cambios y mejoras de manera independiente.