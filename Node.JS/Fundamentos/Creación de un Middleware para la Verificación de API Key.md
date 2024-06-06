# Creación de un Middleware para la Verificación de API Key

Un [middleware](../Express.js/Middlewares%20en%20Express.js.md) de verificación de API Key actúa como una capa de [autenticación](../../ConceptosGenerales/Autenticación%20vs%20Autorización.md) en una aplicación web. Su función es verificar si la solicitud entrante contiene una API Key válida en los headers y, dependiendo de la validación, permitir o denegar el acceso a los recursos de la aplicación.

## Pasos para Implementar el Middleware

1. **Instalación de Dependencias**:
   Asegúrate de tener las siguientes dependencias instaladas:
   - `@hapi/boom`: Para manejar errores [HTTP](../../ConceptosGenerales/HTTP.md) de forma elegante.
   - `dotenv`: Para manejar variables de entorno.

2. **Crear el Middleware**:
   El middleware verificará si la API Key en los headers coincide con la clave configurada en las variables de entorno. Si coincide, se permitirá el acceso mediante `next()`. De lo contrario, se retornará un error de autorización.

   ```javascript
   // auth.handler.js
   const boom = require('@hapi/boom');
   const { config } = require('./../config/config');

   function checkApiKey(req, res, next) {
     const apiKey = req.headers['api'];
     if (apiKey === config.apiKey) {
       next();
     } else {
       next(boom.unauthorized());
     }
   }

   module.exports = { checkApiKey };
   ```

3. **Configurar Variables de Entorno**:
   Define la API Key en un archivo `.env` para mantener las configuraciones sensibles fuera del código fuente.

   ```plaintext
   // .env
   PORT=3000
   DATABASE_URL='postgres://john:admin123@localhost:5432/my_store'
   API_KEY=321456
   ```

4. **Cargar Variables de Entorno**:
   Usa `dotenv` para cargar las variables de entorno definidas en `.env`.

   ```javascript
   // config/config.js
   require('dotenv').config();

   const config = {
     env: process.env.NODE_ENV || 'dev',
     isProd: process.env.NODE_ENV === 'production',
     port: process.env.PORT || 3000,
     dbUrl: process.env.DATABASE_URL,
     apiKey: process.env.API_KEY,
   };

   module.exports = { config };
   ```

5. **Integrar el Middleware en la Aplicación**:
   Usa el middleware en las rutas donde desees aplicar la verificación de la API Key.

   ```javascript
   // app.js (o el archivo principal de la aplicación)
   const express = require('express');
   const { checkApiKey } = require('./middlewares/auth.handler');

   const app = express();

   // Usa el middleware globalmente o en rutas específicas
   app.use(checkApiKey);

   // Define tus rutas aquí
   app.get('/protected-route', (req, res) => {
     res.json({ message: 'Access granted' });
   });

   // Manejo de errores
   app.use((err, req, res, next) => {
     if (err.isBoom) {
       const { output } = err;
       res.status(output.statusCode).json(output.payload);
     } else {
       res.status(500).json({ message: err.message });
     }
   });

   app.listen(config.port, () => {
     console.log(`Server running on port ${config.port}`);
   });
   ```

