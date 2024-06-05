# Manejo de Paginación en Sequelize

Para implementar la paginación en Sequelize, se utilizan los conceptos de `limit` y `offset`. Aquí se detalla cómo funcionan y cómo implementarlos en una consulta.

## Conceptos de Limit y Offset

- **Limit**: Es el número de elementos que se desean traer en cada página, es decir, el límite de elementos por página.
- **Offset**: Es un apuntador que indica cuántos elementos se quieren omitir antes de empezar a traer los elementos deseados. 

Por ejemplo, si tenemos una lista de elementos `[1, 2, 3, 4, 5]`, y queremos mostrar solo 2 elementos por página:
- En la primera página, con `limit = 2` y `offset = 0`, obtendríamos `[1, 2]`.
- En la segunda página, con los mismos valores de `limit` y `offset = 2`, obtendríamos `[3, 4]`.
- Y así sucesivamente.

## Implementación en el Método `find()` del Servicio

```javascript
async find(query) {
    const options = {
      include: ['category'],
    };
    const { limit, offset } = query;
    if (limit && offset) {
      options.limit = limit;
      options.offset = offset;
    }
    const products = await models.Product.findAll(options);
    return products;
}
```

En el método `find()` del servicio, se recibe un objeto `query` que puede contener los parámetros `limit` y `offset`. Si estos parámetros están presentes, se agregan a las opciones de la consulta. Esto permite hacer la paginación de forma dinámica.

## Validación del Esquema y Modificaciones en el Routing

Se valida que los parámetros `limit` y `offset` cumplan con ciertas reglas utilizando un esquema Joi. Luego, en el routing, se llama al método `find()` del servicio y se le pasa el objeto `query` que contiene los parámetros de paginación.

Esto asegura que la paginación se maneje correctamente y se puedan obtener los resultados deseados de forma eficiente.