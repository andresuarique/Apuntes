# Filtros en Consultas con Sequelize

Los filtros son una parte crucial en la manipulación de datos en cualquier sistema. En Sequelize, podemos utilizar operadores y la instrucción `where` para filtrar datos según ciertos criterios. Aquí te muestro cómo implementar filtros en una consulta de productos.

## Utilización de Operadores

Para realizar filtrados, necesitamos utilizar operadores que nos permitan establecer condiciones como mayor que (>), menor que (<), igual que (=), mayor o igual que (≥), etc. Estos operadores se importan de la siguiente manera:

```javascript
const { Op } = require('sequelize');
```

## Validación en el Esquema

Es importante validar los parámetros de entrada para garantizar que los datos proporcionados cumplan con ciertas reglas. En el esquema, se puede definir cómo deben ser los datos de entrada, por ejemplo, para el precio mínimo y máximo:

```javascript
const queryProductSchema = Joi.object({
  limit,
  offset,
  price,
  price_min,
  price_max: price_max.when('price_min', {
    is: Joi.number().integer().required(),
    then: Joi.required(),
  }),
});
```

## Implementación en el Servicio

En el servicio, se ajustan las opciones de la consulta según los filtros proporcionados. Por ejemplo, si se desea filtrar por precio:

```javascript
async find(query) {
    const options = {
      include: ['category'],
      where: {},
    };
    const { limit, offset } = query;
    if (limit && offset) {
      options.limit = limit;
      options.offset = offset;
    }

    const { price } = query;
    if (price) {
      options.where.price = price;
    }

    const { price_min, price_max } = query;
    if (price_min && price_max) {
      options.where.price = {
        [Op.gte]: price_min,
        [Op.lte]: price_max,
      };
    }

    const products = await models.Product.findAll(options);
    return products;
}
```

Aquí, se establecen las opciones básicas de la consulta. Luego, se verifican los parámetros de filtrado y se ajustan las opciones en consecuencia. Si se proporciona un precio, se filtra por ese precio exacto. Si se proporcionan precio mínimo y máximo, se utilizan los operadores de Sequelize para establecer condiciones de rango.

Con estos pasos, puedes implementar fácilmente filtros en tus consultas Sequelize para adaptarlas a las necesidades específicas de tu aplicación.