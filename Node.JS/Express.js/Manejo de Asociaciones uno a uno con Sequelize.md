# Manejo de Asociaciones uno a uno con Sequelize

## Modificación de Columnas

Para modificar una columna existente en la base de datos, se utiliza el método `changeColumn` en el archivo de migración. Este método permite redefinir los atributos de una columna ya existente.

**Ejemplo de Migración para Modificar una Columna**

**migrations/20220106123456-modify-user-id-column-in-customers.js**

```javascript
'use strict';
const { DataTypes } = require('sequelize');
const { CUSTOMER_TABLE } = require('../models/customer.model');

module.exports = {
  up: async (queryInterface) => {
    await queryInterface.changeColumn(CUSTOMER_TABLE, 'user_id', {
      field: 'user_id',
      allowNull: false,
      type: DataTypes.INTEGER,
      unique: true,
    });
  },

  down: async (queryInterface) => {
    // Revertir los cambios si es necesario
    await queryInterface.changeColumn(CUSTOMER_TABLE, 'user_id', {
      field: 'user_id',
      allowNull: false,
      type: DataTypes.INTEGER,
    });
  },
};
```

Después de modificar la columna, se debe ejecutar la migración nuevamente. Es importante notar que si la columna tiene valores que violarían la nueva restricción (como `unique`), estos deben ser corregidos manualmente en la base de datos antes de ejecutar la migración.

Ejecutar la migración:

```bash
npx sequelize-cli db:migrate
```

## Consultas con Asociaciones

Cuando se realiza una consulta para obtener registros y sus asociaciones, se utiliza el método `findAll` con la opción `include` para incluir las asociaciones definidas en los modelos.

**Consulta con Asociación en `customer.service.js`**

```javascript
const { models } = require('../libs/sequelize');

class CustomerService {
  async find() {
    const rta = await models.Customer.findAll({
      include: ['user'],
    });
    return rta;
  }

  // Otros métodos como create, update, delete, etc.
}

module.exports = CustomerService;
```

## Definición de Asociaciones en los Modelos

Las asociaciones deben estar definidas tanto en el modelo que tiene la relación (`Customer`) como en el modelo al que pertenece (`User`).

**Asociación en `customer.model.js`**

```javascript
class Customer extends Model {
  static associate(models) {
    this.belongsTo(models.User, { as: 'user', foreignKey: 'userId' });
  }

  static config(sequelize) {
    return {
      sequelize,
      tableName: CUSTOMER_TABLE,
      modelName: 'Customer',
      timestamps: false,
    };
  }
}

module.exports = { CUSTOMER_TABLE, CustomerSchema, Customer };
```

**Asociación en `user.model.js`**

```javascript
class User extends Model {
  static associate(models) {
    this.hasOne(models.Customer, {
      as: 'customer',
      foreignKey: 'userId'
    });
  }

  static config(sequelize) {
    return {
      sequelize,
      tableName: USER_TABLE,
      modelName: 'User',
      timestamps: false,
    };
  }
}

module.exports = { USER_TABLE, UserSchema, User };
```

## Configuración de Asociaciones en `index.js`

Las asociaciones se deben configurar después de inicializar los modelos.

**models/index.js**

```javascript
const { User, UserSchema } = require('./user.model');
const { Customer, CustomerSchema } = require('./customer.model');

function setupModels(sequelize) {
  User.init(UserSchema, User.config(sequelize));
  Customer.init(CustomerSchema, Customer.config(sequelize));

  User.associate(sequelize.models);
  Customer.associate(sequelize.models);
}

module.exports = setupModels;
```

## Creación de Registros con Asociaciones

Para crear un registro de `Customer` y su asociado `User`, se debe incluir el modelo asociado en el método `create`.

**Método `create` en `customer.service.js`**

```javascript
class CustomerService {
  async create(data) {
    const newCustomer = await models.Customer.create(data, {
      include: ['user'],
    });
    return newCustomer;
  }

  // Otros métodos como find, update, delete, etc.
}

module.exports = CustomerService;
```

Con esta configuración, cuando se crea un nuevo `Customer`, Sequelize automáticamente incluye los datos asociados del `User` en la operación de creación, gracias a la asociación previamente definida.