# Passport.js en Express.js

[029 - Passport.js](029%20-%20Passport.js.md) es una serie de librerías y estrategias que proporcionan una capa de autenticación flexible y extensible para aplicaciones Node.js. Permite implementar diversas estrategias de autenticación como Twitter, GitHub, Facebook, y autenticación básica con nombre de usuario y contraseña.

## Instalación y Configuración Básica

1. **Instalar Passport.js**:
   ```bash
   npm install passport
   npm install passport-local
   ```

2. **Estrategias de Autenticación**:
   - Passport-local permite autenticación básica usando nombre de usuario y contraseña.

## Creación de la Estrategia Local

1. **Definir la Estrategia Local**:
   - Crear una carpeta `utils/auth/strategies` y el archivo `local.strategy.js`.
   - En `local.strategy.js`, definir la estrategia utilizando `passport-local`.

```javascript
const { Strategy } = require('passport-local');
const bcrypt = require('bcrypt');
const boom = require('@hapi/boom');

const UserService = require('../../../services/user.service');
const service = new UserService();

const LocalStrategy = new Strategy(
  {
    usernameField: 'email',
    passwordField: 'password',
  },
  async (email, password, done) => {
    try {
      const user = await service.findByEmail(email);
      if (!user) {
        done(boom.unauthorized(), false);
      }

      const isMatch = await bcrypt.compare(password, user.password);
      if (!isMatch) {
        done(boom.unauthorized(), false);
      }
      delete user.dataValues.password;
      done(null, user);
    } catch (error) {
      done(error, false);
    }
  }
);

module.exports = LocalStrategy;
```

2. **Registrar la Estrategia**:
   - En `utils/auth/index.js`, definir las estrategias a usar y registrar la estrategia local con Passport.

```javascript
const passport = require('passport');
const LocalStrategy = require('./strategies/local.strategy');

passport.use(LocalStrategy);
```

3. **Modificar el Servicio de Usuario**:
   - Añadir el método `findByEmail` en `user.service.js` para buscar usuarios por email.

```javascript
async findByEmail(email) {
    const rta = await models.User.findOne({
      where: { email },
    });
    return rta;
}
```

## Implementación de la Estrategia en Routing

1. **Crear el Routing para Autenticación**:
   - Crear un nuevo archivo `auth.router.js`.

```javascript
const express = require('express');
const passport = require('passport');

const router = express.Router();

router.post(
  '/login',
  passport.authenticate('local', { session: false }),
  async (req, res, next) => {
    try {
      res.json(req.user);
    } catch (error) {
      next(error);
    }
  }
);

module.exports = router;
```

2. **Integrar el Routing en la Aplicación**:
   - Modificar `routes/index.js` para incluir el nuevo router de autenticación.

```javascript
const express = require('express');

const productsRouter = require('./api/products.route');
const usersRouter = require('./api/users.router');
const categoriesRouter = require('./api/categories.route');
const orderRouter = require('./api/orders.router');
const customerRouter = require('./api/customer.route');
const authRouter = require('./api/auth.route');

function routerApi(app) {
  const router = express.Router();
  app.use('/api', router);
  router.use('/products', productsRouter);
  router.use('/users', usersRouter);
  router.use('/categories', categoriesRouter);
  router.use('/orders', orderRouter);
  router.use('/customers', customerRouter);
  router.use('/auth', authRouter);
}

module.exports = routerApi;
```
