# Proteger Rutas con JWT en Express

Para asegurar rutas en una aplicación Express, se puede usar `passport-jwt` para manejar la autenticación basada en tokens [JWT](JWT%20(JSON%20Web%20Token).md). Esto garantiza que solo los usuarios con tokens válidos pueden acceder a ciertas rutas.

## Instalación de `passport-jwt`

Primero, se instala la estrategia `passport-jwt` con el siguiente comando:

```bash
npm install passport-jwt
```

## Creación de la Estrategia JWT

1. **Archivo `jwt.strategy.js`**:

Se requiere la `Strategy` y `ExtractJwt` del paquete `passport-jwt`. La estrategia se configura con opciones para extraer el token del header y verificarlo con una clave secreta.

**Código de Ejemplo:**

```javascript
const { Strategy, ExtractJwt } = require('passport-jwt');
const { config } = require('../../../config/config');

const options = {
  jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
  secretOrKey: config.jwtSecret,
};

const JwtStrategy = new Strategy(options, (payload, done) => {
  return done(null, payload);
});

module.exports = JwtStrategy;
```

2. **Archivo `utils/auth/index.js`**:

Se agrega la nueva estrategia JWT a Passport junto con cualquier otra estrategia que ya esté en uso (como la estrategia local).

**Código de Ejemplo:**

```javascript
const passport = require('passport');

const LocalStrategy = require('./strategies/local.strategy');
const JwtStrategy = require('./strategies/jwt.strategy');

passport.use(LocalStrategy);
passport.use(JwtStrategy);
```

## Protegiendo Rutas con JWT

Para proteger una ruta, se usa `passport.authenticate` con la estrategia JWT y la opción `session: false` para no manejar sesiones de servidor.

**Ejemplo de Implementación en `categories.router.js`**:

```javascript
const express = require('express');
const passport = require('passport');
const validatorHandler = require('../middlewares/validator.handler');
const { createCategorySchema } = require('../schemas/category.schema');
const CategoryService = require('../services/category.service');

const router = express.Router();
const service = new CategoryService();

router.post(
  '/',
  passport.authenticate('jwt', { session: false }),
  validatorHandler(createCategorySchema, 'body'),
  async (req, res, next) => {
    try {
      const body = req.body;
      const newCategory = await service.create(body);
      res.status(201).json(newCategory);
    } catch (error) {
      next(error);
    }
  }
);

module.exports = router;
```

## Configuración del Secret en Variables de Entorno

El secreto (`secret`) utilizado para [firmar y verificar tokens](031%20-%20Firmar%20y%20Verificar%20Tokens%20JWT%20con%20Express.md) debe estar en las variables de entorno (`.env`). Asegúrate de no incluir esta clave directamente en el código fuente.

**Ejemplo de Archivo `.env`:**

```env
PORT=3000
DATABASE_URL='postgres://john:admin123@localhost:5432/my_store'
API_KEY=321456
JWT_SECRET='D8T1LkIMVTA8yYSuNgbadlFJ9yGU7cjD'
```

**Configuración en `config/config.js`**:

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
