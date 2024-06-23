# Método GET en Nest.js

## Recibir Parámetro en la Ruta

Para recibir un parámetro en la ruta y hacer una prevalidación del mismo, como asegurarse de que es un entero, se pueden utilizar pipes. Un ejemplo sencillo es el siguiente:

```typescript
@Get('products/:id')
getProduct(
  @Param(
    'id',
    new ParseIntPipe({ errorHttpStatusCode: HttpStatus.NOT_ACCEPTABLE }),
  )
  id: number,
) {
  return `Product ${id}`;
}
```

## Recibir Parámetros Tipo Query

Con el decorador `@Query`, podemos recibir parámetros de consulta (Query Params) de una URL:

```typescript
@Get('products')
getProducts(
  @Query('limit') limit = 100,
  @Query('offset') offset = 0,
  @Query('brand') brand: string,
) {
  return `Products limit => ${limit}, offset => ${offset}, brand => ${brand}`;
}
```
