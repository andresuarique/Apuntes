# Control de Roles en Express

La gestión de permisos y roles es crucial para asegurar que solo usuarios autorizados puedan realizar ciertas acciones en una aplicación. A continuación se describe cómo implementar un sistema básico de control de roles en Express, utilizando [JWT](Generar%20JWT%20en%20Servicios%20de%20Express.md) para autenticación y [middleware](Middlewares%20en%20Express.js.md) para autorización.

## 1. Creación del Middleware para Control de Roles

Primero, creamos un middleware que verifica el rol del usuario y decide si puede proceder o no. Empezamos con una función simple que verifica si el usuario es administrador.

**Archivo `auth.handler.js`:**

```javascript
const boom = require('@hapi/boom');

// Middleware que verifica si el usuario es admin
function checkAdminRole(req, res, next) {
  const user = req.user;
  if (user.role === 'admin') {
    next();
  } else {
    next(boom.unauthorized());
  }
}

module.exports = { checkAdminRole };
```

Este middleware se puede mejorar para manejar múltiples roles, creando una función que acepte una lista de roles permitidos.

**Mejora con `checkRoles`:**

```javascript
const boom = require('@hapi/boom');

// Middleware que verifica si el rol del usuario está en la lista de roles permitidos
function checkRoles(...roles) {
  return (req, res, next) => {
    const user = req.user;
    if (roles.includes(user.role)) {
      next();
    } else {
      next(boom.unauthorized());
    }
  };
}

module.exports = { checkAdminRole, checkRoles };
```

## 2. Uso del Middleware en las Rutas

Para proteger una ruta y restringir su acceso según el rol del usuario, se utiliza el middleware en la definición de la ruta. Primero autenticamos al usuario con JWT y luego verificamos su rol.

**Ejemplo en `categories.router.js`:**

```javascript
const express = require('express');
const passport = require('passport');
const validatorHandler = require('../middlewares/validator.handler');
const { createCategorySchema } = require('../schemas/category.schema');
const CategoryService = require('../services/category.service');
const { checkRoles } = require('../middlewares/auth.handler');

const router = express.Router();
const service = new CategoryService();

router.post(
  '/',
  passport.authenticate('jwt', { session: false }),
  checkRoles('admin', 'seller'),  // Solo admin y seller pueden acceder
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

## 3. Configuración de JWT y Autenticación

Para que el middleware de roles funcione, primero necesitamos asegurarnos de que el usuario está autenticado con un token JWT válido. Esto se hace configurando Passport con la estrategia JWT.

**Archivo `jwt.strategy.js`:**

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

**Archivo `utils/auth/index.js`:**

```javascript
const passport = require('passport');

const LocalStrategy = require('./strategies/local.strategy');
const JwtStrategy = require('./strategies/jwt.strategy');

passport.use(LocalStrategy);
passport.use(JwtStrategy);
```

