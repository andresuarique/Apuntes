# Manejo de Asociaciones Uno a Muchos con Sequelize

En las relaciones uno a muchos, un registro en una tabla puede tener múltiples registros asociados en otra tabla. En este ejemplo, una categoría puede tener múltiples productos.

## Servicio de Productos

**product.service.js**

```javascript
const { models } = require('../libs/sequelize');

class ProductService {
  async create(data) {
    const newProduct = await models.Product.create(data);
    return newProduct;
  }

  async find() {
    const products = await models.Product.findAll({
      include: ['category'],
    });
    return products;
  }

  // Otros métodos como update, delete, etc.
}

module.exports = ProductService;
```

## Servicio de Categorías

**category.service.js**

```javascript
const { models } = require('../libs/sequelize');

class CategoryService {
  async create(data) {
    const newCategory = await models.Category.create(data);
    return newCategory;
  }

  async find() {
    const categories = await models.Category.findAll();
    return categories;
  }

  async findOne(id) {
    const category = await models.Category.findByPk(id, {
      include: ['products'],
    });
    return category;
  }

  // Otros métodos como update, delete, etc.
}

module.exports = CategoryService;
```

## Esquema de Producto

**product.schema.js**

```javascript
const Joi = require('joi');

const id = Joi.number().integer();
const name = Joi.string().min(3).max(15);
const price = Joi.number().integer().min(10);
const description = Joi.string().min(10);
const image = Joi.string().uri();
const categoryId = Joi.number().integer();

const createProductSchema = Joi.object({
  name: name.required(),
  price: price.required(),
  description: description.required(),
  image: image.required(),
  categoryId: categoryId.required(),
});

const updateProductSchema = Joi.object({
  name,
  price,
  description,
  image,
  categoryId,
});

module.exports = {
  createProductSchema,
  updateProductSchema,
};
```

En estos servicios, se manejan las operaciones CRUD para productos y categorías, incluyendo la recuperación de productos con sus respectivas categorías asociadas. Además, se asegura que los datos de los productos se ajusten al esquema definido, incluyendo la validación de la categoría.