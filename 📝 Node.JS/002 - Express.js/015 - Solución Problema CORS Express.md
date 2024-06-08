# Solución al Problema de CORS en Express

## Habilitar CORS en Express

Para resolver el problema de CORS en una aplicación Express, se utiliza el middleware `cors` que permite configurar de manera flexible las [políticas de CORS](../../🌐%20ConceptosGenerales/CORS.md). Aquí hay una guía paso a paso para habilitar y configurar CORS en Express.

### Habilitar CORS para Todos los Orígenes

Para permitir que cualquier origen acceda a los recursos de tu API, simplemente agrega el middleware `cors` globalmente en tu aplicación Express:

```javascript
const cors = require('cors');
const express = require('express');
const app = express();

app.use(cors());

// Tus rutas y lógica de la aplicación aquí

const port = 3000;
app.listen(port, () => {
  console.log(`Servidor escuchando en el puerto ${port}`);
});
```

### Habilitar CORS para Endpoints Específicos

Si solo quieres permitir CORS en ciertos endpoints de tu API, puedes mover el middleware `cors` justo antes de las rutas correspondientes:

```javascript
const cors = require('cors');
const express = require('express');
const app = express();

// Otras configuraciones y middleware

// Rutas no afectadas por CORS

// Habilitar CORS para rutas de la API
app.use('/api', cors(), require('./routes/api'));

// Rutas adicionales

const port = 3000;
app.listen(port, () => {
  console.log(`Servidor escuchando en el puerto ${port}`);
});
```

### Habilitar CORS para Orígenes Específicos

Para permitir CORS solo desde orígenes específicos, se puede usar una lista blanca (whitelist) que contiene los dominios permitidos. Luego, se configura el middleware `cors` para verificar si el origen de la solicitud está en esta lista:

```javascript
const cors = require('cors');
const express = require('express');
const app = express();

const whitelist = ['http://localhost:3000', 'https://pagina.co'];
const corsOptions = {
  origin: (origin, callback) => {
    if (whitelist.includes(origin) || !origin) {
      callback(null, true);
    } else {
      callback(new Error('No permitido por CORS'));
    }
  }
};

app.use(cors(corsOptions));

// Tus rutas y lógica de la aplicación aquí

const port = 3000;
app.listen(port, () => {
  console.log(`Servidor escuchando en el puerto ${port}`);
});
```

### Desglose de la Configuración

1. **Crear una Whitelist**:
   La whitelist es un array que contiene los dominios que tienen permiso para acceder a los recursos de tu API.

   ```javascript
   const whitelist = ['http://localhost:3000', 'https://pagina.co'];
   ```

2. **Definir Opciones de CORS**:
   Se define una función que verifica si el origen de la solicitud está en la whitelist. Esta función recibe dos parámetros: `origin` y `callback`.

   ```javascript
   const corsOptions = {
     origin: (origin, callback) => {
       if (whitelist.includes(origin) || !origin) {
         callback(null, true);
       } else {
         callback(new Error('No permitido por CORS'));
       }
     }
   };
   ```

   - Si el origen está en la whitelist (o si no hay origen, lo que permite solicitudes de herramientas como Postman), se llama al callback con `null` y `true`.
   - Si el origen no está en la whitelist, se llama al callback con un error.

3. **Usar las Opciones de CORS en la Aplicación**:
   Se pasa las opciones de CORS configuradas al middleware `cors`.

   ```javascript
   app.use(cors(corsOptions));
   ```
