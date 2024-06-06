# Generar JWT en Servicios de Express

## Introducción

En una aplicación Express, [JWT (JSON Web Tokens)](../../ConceptosGenerales/JWT%20(JSON%20Web%20Token).md) se utiliza para [autenticar y autorizar](../../ConceptosGenerales/Autenticación%20vs%20Autorización.md) usuarios. Una vez autenticados, se genera un token que el cliente puede usar para acceder a recursos protegidos. Este proceso implica la autenticación inicial del usuario, la creación de un payload con los datos del usuario, y la firma de un token con una clave secreta.

## Implementación del JWT en el Archivo `auth.route.js`

En el archivo `auth.route.js`, se implementa la lógica para autenticar al usuario usando la estrategia local de [Passport.js](Passport.js%20en%20Express.js.md) y generar un JWT.

1. **Autenticación con Estrategia Local**: Primero, se autentica al usuario con la estrategia local y se obtiene el usuario autenticado (`req.user`).

2. **Creación del Payload**: Se crea un payload con los datos relevantes del usuario, como su ID y rol.

3. **Firma del Token**: Se firma el token usando el método `.sign()` de la librería `jsonwebtoken` y la clave secreta almacenada en las variables de entorno.

4. **Respuesta con el Token**: Se responde con un JSON que contiene el usuario y el token.

**Código de Ejemplo (auth.route.js):**

```javascript
const express = require('express');
const passport = require('passport');
const jwt = require('jsonwebtoken');

const { config } = require('../../config/config');

const router = express.Router();

router.post(
  '/login',
  passport.authenticate('local', { session: false }),
  async (req, res, next) => {
    try {
      const user = req.user;
      const payload = {
        sub: user.id,
        role: user.role,
      };

      const token = jwt.sign(payload, config.jwtSecret);
      res.json({ user, token });
    } catch (error) {
      next(error);
    }
  }
);

module.exports = router;
```

## Configuración del Secret en Variables de Entorno

Para firmar el token, se necesita una clave secreta (`secret`). Esta clave se debe almacenar en una variable de entorno para mantenerla segura y fuera del código fuente. 

1. **Archivo `.env`**: Aquí se definen las variables de entorno, incluida la clave secreta para JWT.

**Ejemplo de Archivo `.env`:**

```env
PORT=3000
DATABASE_URL='postgres://john:admin123@localhost:5432/my_store'
API_KEY=321456
JWT_SECRET='D8T1LkIMVTA8yYSuNgbadlFJ9yGU7cjD'
```

2. **Archivo `config.js`**: Se actualiza la configuración para incluir la nueva variable de entorno.

**Código de Ejemplo (config/config.js):**

```javascript
require('dotenv').config();

const config = {
  env: process.env.NODE_ENV || 'dev',
  isProd: process.env.NODE_ENV === 'production',
  port: process.env.PORT || 3000,
  dbUser: process.env.DB_USER,
  dbPassword: process.env.DB_PASSWORD,
  dbHost: process.env.DB_HOST,
  dbName: process.env.DB_NAME,
  dbPort: process.env.DB_PORT,
  dbUrl: process.env.DATABASE_URL,
  apiKey: process.env.API_KEY,
  jwtSecret: process.env.JWT_SECRET,
};

module.exports = { config };
```

## Resumen

1. **Instalación de Librerías**: Instalar `jsonwebtoken` y `passport-local`.
2. **Configuración de Clave Secreta**: Definir `JWT_SECRET` en el archivo `.env` y agregarlo a la configuración.
3. **Implementación de Autenticación y Generación de Token**: En `auth.route.js`, autenticar al usuario y generar un JWT que se envía en la respuesta.

Estos pasos permiten la autenticación de usuarios y la generación de tokens JWT en una aplicación Express, facilitando un sistema de autenticación seguro y escalable.