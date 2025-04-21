# Mocking con Jest

El mocking es una técnica utilizada en [pruebas](001%20-%20Testing.md) para suplantar dependencias y controlar el comportamiento de las mismas. En Jest, se puede usar el método `jest.mock` para reemplazar módulos o clases con implementaciones simuladas.

## Suplantando MongoLib

Para suplantar la clase `MongoLib` con un objeto de prueba, se utiliza el método `jest.mock`. Este método toma como argumentos la ruta del módulo a suplantar y una función que devuelve una implementación simulada.

### Implementación

```javascript
jest.mock('../lib/mongo.lib', () => jest.fn().mockImplementation(() => MongoLibStub));
```

Aquí, `MongoLibStub` es un objeto que contiene métodos simulados que reemplazan a los métodos originales de `MongoLib`.

### Creación de MongoLibStub

```javascript
const MongoLibStub = {
  getAll: () => fakeBooks,
  create: () => { },
};
```

`MongoLibStub` es una clase de prueba que simula los métodos `getAll` y `create`. En este caso, `getAll` retorna un arreglo de objetos ficticios de tipo `Book`.

### Definición de Datos Ficticios

```javascript
const fakeBooks = [
  {
    _id: '1',
    name: 'Harry Potter',
  },
  {
    _id: '2',
    name: 'Principito',
  },
];
```

`fakeBooks` es un arreglo de libros ficticios que se utiliza para simular respuestas en las pruebas.

### Limpieza de Mocks

Es una buena práctica limpiar los mocks creados para evitar efectos secundarios entre pruebas. Se puede utilizar el método `clearAllMocks` de Jest para esto:

```javascript
jest.clearAllMocks();
```

Este método asegura que todos los mocks sean limpiados entre las pruebas para evitar resultados inesperados.

*ver: [006 - Doubles en Testing](006%20-%20Doubles%20en%20Testing.md)*