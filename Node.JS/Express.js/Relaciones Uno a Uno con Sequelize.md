# Relaciones Uno a Uno con Sequelize

En [Sequelize](Uso%20de%20Sequelize%20ORM%20en%20Express.js.md), las relaciones uno a uno se utilizan para conectar dos tablas donde cada fila de una tabla está asociada a una única fila de la otra tabla. Las relaciones uno a uno se configuran utilizando los métodos `hasOne` y `belongsTo`.

## Tipos de Relaciones

- **`hasOne`**: Define la relación desde el modelo A hacia el modelo B, indicando que el modelo A tiene una relación uno a uno con el modelo B.
- **`belongsTo`**: Define la relación desde el modelo B hacia el modelo A, indicando que el modelo B pertenece a una instancia del modelo A.

# Ejemplo de Relación Uno a Uno

Supongamos que tienes dos modelos: `User` y `Customer`, donde cada `Customer` pertenece a un `User`.

## Definición de Modelos

**models/user.model.js**

```javascript
const { Model, DataTypes, Sequelize } = require('sequelize');
const USER_TABLE = 'users';

const UserSchema = {
  id: {
    allowNull: false,
    autoIncrement: true,
    primaryKey: true,
    type: DataTypes.INTEGER,
  },
  email: {
    allowNull: false,
    type: DataTypes.STRING,
    unique: true,
  },
  password: {
    allowNull: false,
    type: DataTypes.STRING,
  },
  createdAt: {
    allowNull: false,
    type: DataTypes.DATE,
    field: 'created_at',
    defaultValue: Sequelize.NOW,
  },
};

class User extends Model {
  static associate(models) {
    this.hasOne(models.Customer, { as: 'customer', foreignKey: 'userId' });
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

**models/customer.model.js**

```javascript
const { Model, DataTypes, Sequelize } = require('sequelize');
const CUSTOMER_TABLE = 'customers';

const CustomerSchema = {
  id: {
    allowNull: false,
    autoIncrement: true,
    primaryKey: true,
    type: DataTypes.INTEGER,
  },
  name: {
    allowNull: false,
    type: DataTypes.STRING,
  },
  userId: {
    field: 'user_id',
    allowNull: false,
    type: DataTypes.INTEGER,
    references: {
      model: 'users', // Referencia a la tabla users
      key: 'id',
    },
    onUpdate: 'CASCADE',
    onDelete: 'SET NULL',
  },
  createdAt: {
    allowNull: false,
    type: DataTypes.DATE,
    field: 'created_at',
    defaultValue: Sequelize.NOW,
  },
};

class Customer extends Model {
  static associate(models) {
    this.belongsTo(models.User, { as: 'user' });
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

## Configuración de Relaciones en `index.js`

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

## Migración para Crear la Tabla `Customers`

Genera una nueva migración:

```bash
npx sequelize-cli migration:generate --name create-customers-table
```

Modifica el archivo de migración generado:

**migrations/20220106123456-create-customers-table.js**

```javascript
'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.createTable('customers', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER,
      },
      name: {
        allowNull: false,
        type: Sequelize.STRING,
      },
      userId: {
        field: 'user_id',
        allowNull: false,
        type: Sequelize.INTEGER,
        references: {
          model: 'users',
          key: 'id',
        },
        onUpdate: 'CASCADE',
        onDelete: 'SET NULL',
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE,
        field: 'created_at',
        defaultValue: Sequelize.NOW,
      },
    });
  },

  down: async (queryInterface) => {
    await queryInterface.dropTable('customers');
  },
};
```

Aplica la migración:

```bash
npx sequelize-cli db:migrate
```

## Servicio para Consultar Datos

Para realizar consultas, puedes definir un servicio que utilice los modelos y sus asociaciones:

**services/customer.service.js**

```javascript
const { models } = require('../libs/sequelize');

class CustomerService {
  async find() {
    const customers = await models.Customer.findAll({
      include: ['user'],
    });
    return customers;
  }

  // Otros métodos como create, update, delete, etc.
}

module.exports = CustomerService;
```

Con esta configuración, `Customer` está asociado a `User` a través de la clave foránea `userId`, y las asociaciones se han definido utilizando los métodos `hasOne` y `belongsTo`. Las migraciones se utilizan para crear las tablas y definir las relaciones en la base de datos.