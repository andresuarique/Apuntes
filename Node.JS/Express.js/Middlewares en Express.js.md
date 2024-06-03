# Middleware en Express.js

El [middleware](../../ConceptosGenerales/Middleware.md) en Express.js se refiere a funciones que se ejecutan durante el ciclo de vida de una solicitud [HTTP](../../ConceptosGenerales/HTTP.md) antes de que esta llegue a su manejador final. Los middlewares pueden modificar la solicitud (`req`), la respuesta (`res`) y tomar decisiones sobre si continuar con la cadena de middleware o finalizar la respuesta.

## Tipos de Middleware

1. **Middleware de aplicación**: Se aplica a toda la aplicación y se ejecuta para cada solicitud.
2. **Middleware de router**: Se aplica a un router específico.
3. **Middleware de error**: Maneja errores en la aplicación.
4. **Middleware incorporado**: Incluye funciones integradas como `express.json()` y `express.urlencoded()`.

## Uso Básico de Middleware

### Middleware de Aplicación

```js
const express = require('express');
const app = express();

// Middleware de aplicación
app.use((req, res, next) => {
  console.log(`Request Method: ${req.method}, Request URL: ${req.url}`);
  next(); // Llama al siguiente middleware
});

app.get('/', (req, res) => {
  res.send('Hello World');
});

const port = 3000;
app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

### Middleware Incorporado

Express viene con algunos middlewares integrados que son muy útiles.

```js
app.use(express.json()); // Parsear cuerpos JSON
app.use(express.urlencoded({ extended: true })); // Parsear cuerpos URL-encoded
```

### Middleware de Terceros

Se pueden utilizar middlewares de terceros para ampliar las funcionalidades de la aplicación. Por ejemplo, `morgan` para el registro de solicitudes HTTP.

```js
const morgan = require('morgan');

app.use(morgan('tiny'));
```

### Middleware de Router

```js
const express = require('express');
const router = express.Router();

router.use((req, res, next) => {
  console.log(`Request URL: ${req.url}`);
  next();
});

router.get('/', (req, res) => {
  res.send('Home Page');
});

router.get('/about', (req, res) => {
  res.send('About Page');
});

app.use('/api', router);
```

### Middleware de Manejo de Errores

El middleware de manejo de errores se define con cuatro parámetros: `err`, `req`, `res`, y `next`.

```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

### Captura de Errores desde el Router

Para capturar errores en los routers y pasar esos errores a los manejadores de errores, puedes utilizar el siguiente patrón:

```js
const express = require('express');
const router = express.Router();

router.get('/', (req, res, next) => {
  try {
    // Código que puede lanzar un error
    res.send('Home Page');
  } catch (err) {
    next(err); // Pasa el error al middleware de manejo de errores
  }
});

// Capturar errores asincrónicos
router.get('/async', async (req, res, next) => {
  try {
    // Código asincrónico que puede lanzar un error
    res.send('Async Page');
  } catch (err) {
    next(err); // Pasa el error al middleware de manejo de errores
  }
});

app.use('/api', router);
```

En el manejador de errores:

```js
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

## Creación de Middleware Personalizado

Puedes crear tus propios middlewares para tareas específicas como autenticación, validación, etc.

### Ejemplo de Middleware de Autenticación

```js
const authMiddleware = (req, res, next) => {
  const { headers } = req;
  if (headers.authorization && headers.authorization === 'Bearer token123') {
    next();
  } else {
    res.status(403).send('Forbidden');
  }
};

app.use('/secure-route', authMiddleware, (req, res) => {
  res.send('This is a secure route');
});
```

### Orden de Ejecución del Middleware

El orden en el que defines los middlewares es importante. Se ejecutan en el orden en que se agregan.

```js
app.use(middleware1);
app.use(middleware2);
app.use(middleware3);

// Request -> middleware1 -> middleware2 -> middleware3 -> route handler
```

El middleware es una parte fundamental de Express.js, permitiendo una gran flexibilidad y modularidad en la construcción de aplicaciones web y APIs.