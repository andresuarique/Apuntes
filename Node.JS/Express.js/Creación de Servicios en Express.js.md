*ver [Arquitectura de Capas](../../ConceptosGenerales/Arquitectura%20de%20Capas.md)*
# Creación de Servicios en Express.js

Los servicios en una aplicación Express.js se utilizan para encapsular la lógica de negocio. Esto ayuda a mantener el código organizado, modular y fácil de mantener. A continuación, se describe cómo crear y utilizar servicios en Express.js.

## Estructura del Proyecto

Supongamos que tenemos una estructura de proyecto similar a la siguiente:

```
/my-app
|-- /node_modules
|-- /routes
|   |-- product.router.js
|-- /services
|   |-- product.service.js
|-- index.js
|-- package.json
```

## Paso 1: Crear el Servicio

Primero, creamos un archivo de servicio dentro de la carpeta `services`. Este archivo contendrá la lógica de negocio para la entidad correspondiente. Por ejemplo, `product.service.js` podría verse así:

### services/product.service.js

```js
class ProductService {
  constructor() {
    this.products = [];
  }

  create(product) {
    this.products.push(product);
    return product;
  }

  find() {
    return this.products;
  }

  findOne(id) {
    return this.products.find(product => product.id === id);
  }

  update(id, changes) {
    const index = this.products.findIndex(product => product.id === id);
    if (index === -1) {
      throw new Error('Product not found');
    }
    const product = this.products[index];
    this.products[index] = { ...product, ...changes };
    return this.products[index];
  }

  delete(id) {
    const index = this.products.findIndex(product => product.id === id);
    if (index === -1) {
      throw new Error('Product not found');
    }
    this.products.splice(index, 1);
    return { id };
  }
}

module.exports = ProductService;
```

## Paso 2: Utilizar el Servicio en el Router

Luego, utilizamos este servicio en nuestro router. El [router](Uso%20de%20express.Router.md) es responsable de recibir las solicitudes HTTP y delegar la lógica de negocio al servicio correspondiente.

### routes/product.router.js

```js
const express = require('express');
const ProductService = require('../services/product.service');

const router = express.Router();
const service = new ProductService();

router.get('/', (req, res) => {
  const products = service.find();
  res.json(products);
});

router.get('/:id', (req, res) => {
  const { id } = req.params;
  const product = service.findOne(id);
  res.json(product);
});

router.post('/', (req, res) => {
  const body = req.body;
  const newProduct = service.create(body);
  res.status(201).json(newProduct);
});

router.put('/:id', (req, res) => {
  const { id } = req.params;
  const body = req.body;
  const updatedProduct = service.update(id, body);
  res.json(updatedProduct);
});

router.delete('/:id', (req, res) => {
  const { id } = req.params;
  const deletedProduct = service.delete(id);
  res.json(deletedProduct);
});

module.exports = router;
```

## Paso 3: Configurar el Enrutamiento en la Aplicación Principal

Finalmente, configuramos el enrutamiento en la aplicación principal para que las solicitudes a `/api/products` se manejen con nuestro router de productos.

### index.js

```js
const express = require('express');
const productRouter = require('./routes/product.router');

const app = express();
const port = 3000;

app.use(express.json());

app.use('/api/products', productRouter);

app.listen(port, () => {
  console.log(`Listening on port ${port}`);
});
```
