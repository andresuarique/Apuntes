# Relaciones Uno a Muchos con Sequelize

En las relaciones uno a muchos, un registro en una tabla puede tener múltiples registros asociados en otra tabla. En este ejemplo, una categoría puede tener múltiples productos.

## Definición del Modelo Producto

**models/product.model.js**

```javascript
const { Model, DataTypes, Sequelize } = require('sequelize');
const { CATEGORY_TABLE } = require('./category.model');

const PRODUCT_TABLE = 'products'; // nombre de la tabla

const ProductSchema = {
  // El esquema define la estructura de la BD.
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
  image: {
    allowNull: false,
    type: DataTypes.STRING,
  },
  description: {
    allowNull: false,
    type: DataTypes.TEXT,
  },
  price: {
    allowNull: false,
    type: DataTypes.INTEGER,
  },
  createdAt: {
    allowNull: false,
    type: DataTypes.DATE,
    field: 'created_at',
    defaultValue: Sequelize.NOW,
  },
  categoryId: {
    field: 'category_id',
    allowNull: false,
    type: DataTypes.INTEGER,
    references: {
      model: CATEGORY_TABLE,
      key: 'id',
    },
    onUpdate: 'CASCADE',
    onDelete: 'SET NULL',
  },
};

class Product extends Model {
  static associate(models) {
    this.belongsTo(models.Category, { as: 'category' });
  }

  static config(sequelize) {
    return {
      sequelize,
      tableName: PRODUCT_TABLE,
      modelName: 'Product',
      timestamps: false,
    };
  }
}

module.exports = { Product, PRODUCT_TABLE, ProductSchema };
```

## Definición del Modelo Categoría

**models/category.model.js**

```javascript
const { Model, DataTypes, Sequelize } = require('sequelize');

const CATEGORY_TABLE = 'categories'; // nombre de la tabla

const CategorySchema = {
  // El esquema define la estructura de la BD.
  id: {
    allowNull: false,
    autoIncrement: true,
    primaryKey: true,
    type: DataTypes.INTEGER,
  },
  name: {
    allowNull: false,
    type: DataTypes.STRING,
    unique: true,
  },
  image: {
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

class Category extends Model {
  static associate(models) {
    this.hasMany(models.Product, {
      as: 'products',
      foreignKey: 'categoryId',
    });
  }

  static config(sequelize) {
    return {
      sequelize,
      tableName: CATEGORY_TABLE,
      modelName: 'Category',
      timestamps: false,
    };
  }
}

module.exports = { Category, CATEGORY_TABLE, CategorySchema };
```

## Migración para Crear Tablas

**migrations/20220106123456-create-products-and-categories.js**

```javascript
'use strict';

const { CategorySchema, CATEGORY_TABLE } = require('../models/category.model');
const { ProductSchema, PRODUCT_TABLE } = require('../models/product.model');

module.exports = {
  up: async (queryInterface) => {
    await queryInterface.createTable(CATEGORY_TABLE, CategorySchema);
    await queryInterface.createTable(PRODUCT_TABLE, ProductSchema);
  },

  down: async (queryInterface) => {
    await queryInterface.dropTable(CATEGORY_TABLE);
    await queryInterface.dropTable(PRODUCT_TABLE);
  },
};
```

Para aplicar esta migración, ejecuta el siguiente comando:

```bash
npx sequelize-cli db:migrate
```

## Configuración de Modelos y Asociaciones

**models/index.js**

```javascript
const { User, UserSchema } = require('./user.model');
const { Customer, CustomerSchema } = require('./customer.model');
const { Category, CategorySchema } = require('./category.model');
const { Product, ProductSchema } = require('./product.model');

function setupModels(sequelize) {
  User.init(UserSchema, User.config(sequelize));
  Customer.init(CustomerSchema, Customer.config(sequelize));
  Category.init(CategorySchema, Category.config(sequelize));
  Product.init(ProductSchema, Product.config(sequelize));

  User.associate(sequelize.models);
  Customer.associate(sequelize.models);
  Category.associate(sequelize.models);
  Product.associate(sequelize.models);
}

module.exports = setupModels;
```

## Consultas con Asociaciones

Para obtener una categoría y sus productos asociados, puedes utilizar el método `findAll` con `include`.

**category.service.js**

```javascript
const { models } = require('../libs/sequelize');

class CategoryService {
  async find() {
    const rta = await models.Category.findAll({
      include: ['products'],
    });
    return rta;
  }

  async findOne(id) {
    const category = await models.Category.findByPk(id, {
      include: ['products'],
    });
    return category;
  }

  // Otros métodos como create, update, delete, etc.
}

module.exports = CategoryService;
```

Para crear un producto asociado a una categoría, asegúrate de incluir la `categoryId` en los datos del producto.

**product.service.js**

```javascript
const { models } = require('../libs/sequelize');

class ProductService {
  async create(data) {
    const newProduct = await models.Product.create(data);
    return newProduct;
  }

  // Otros métodos como find, update, delete, etc.
}

module.exports = ProductService;
```

Con esta configuración, Sequelize gestiona las relaciones uno a muchos, asegurando que cada producto está correctamente asociado a su categoría correspondiente.