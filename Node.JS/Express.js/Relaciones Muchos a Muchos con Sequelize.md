# Relaciones Muchos a Muchos con Sequelize

En las relaciones muchos a muchos, se utiliza una tabla intermedia para conectar dos tablas principales. En este caso, se crea la tabla `orders_products` para conectar órdenes con productos.

## Modelo OrderProduct

**order-product.model.js**

```javascript
const { Model, DataTypes, Sequelize } = require('sequelize');
const { ORDER_TABLE } = require('./order.model');
const { PRODUCT_TABLE } = require('./product.model');

const ORDER_PRODUCT_TABLE = 'orders_products';

const OrderProductSchema = {
  id: {
    allowNull: false,
    autoIncrement: true,
    primaryKey: true,
    type: DataTypes.INTEGER,
  },
  createdAt: {
    allowNull: false,
    type: DataTypes.DATE,
    field: 'created_at',
    defaultValue: Sequelize.NOW,
  },
  amount: {
    type: DataTypes.INTEGER,
    allowNull: false,
  },
  orderId: {
    field: 'order_id',
    allowNull: false,
    type: DataTypes.INTEGER,
    references: {
      model: ORDER_TABLE,
      key: 'id',
    },
  },
  productId: {
    field: 'product_id',
    allowNull: false,
    type: DataTypes.INTEGER,
    references: {
      model: PRODUCT_TABLE,
      key: 'id',
    },
    onUpdate: 'CASCADE',
    onDelete: 'SET NULL',
  },
};

class OrderProduct extends Model {
  static config(sequelize) {
    return {
      sequelize,
      tableName: ORDER_PRODUCT_TABLE,
      modelName: 'OrderProduct',
      timestamps: false,
    };
  }
}

module.exports = { OrderProductSchema, OrderProduct };
```

En este modelo se define la estructura de la tabla intermedia `orders_products`, que contiene las relaciones entre órdenes y productos.

## Configuración de Modelos

**db/models/index.js**

```javascript
const { Order, OrderSchema } = require('./order.model');
const { Product, ProductSchema } = require('./product.model');
const { OrderProduct, OrderProductSchema } = require('./order-product.model');

function setupModels(sequelize) {
  // Inicialización de modelos previa
  // ...

  Order.init(OrderSchema, Order.config(sequelize));
  Product.init(ProductSchema, Product.config(sequelize));
  OrderProduct.init(OrderProductSchema, OrderProduct.config(sequelize));

  // Asociaciones previas
  // ...
}

module.exports = setupModels;
```

Se configuran los modelos de `Order`, `Product` y `OrderProduct`, y se establecen las asociaciones necesarias.

## Asociaciones en el Modelo Order

**order.model.js**

```javascript
class Order extends Model {
  static associate(models) {
    // Otras asociaciones previas
    // ...

    this.belongsToMany(models.Product, {
      as: 'items',
      through: models.OrderProduct,
      foreignKey: 'orderId',
      otherKey: 'productId',
    });
  }
}
```

Se especifica la relación muchos a muchos entre órdenes y productos utilizando `belongsToMany`. La tabla intermedia `OrderProduct` se utiliza como puente, y se especifican las llaves foráneas correspondientes.

Con estas configuraciones, se establece una relación muchos a muchos entre órdenes y productos, lo que permite acceder a los productos asociados a una orden y viceversa de manera eficiente.