# Setup / Teardown en Jest
En Jest, se utilizan cláusulas para aislar las [pruebas](001%20-%20Testing.md) y asegurar que un escenario de pruebas no afecte a otro. Esto se logra mediante la agrupación de casos con `describe()` y el uso de hooks para el setup y teardown.

## Describe
Se puede encerrar varios `test()` dentro de `describe()`. Esto ayuda a mejorar la lectura y el encapsulamiento de las pruebas.

```javascript
// Agrupamos varios tests dentro de describe()
describe('conjunto', () => {
  test('case 1', () => {
    expect(1 + 1).toBe(2);
  });

  test('case 2', () => {
    expect(2 + 2).toBe(4);
  });

  // Incluso podemos tener conjuntos de tests dentro de otros conjuntos
  describe('conjunto dentro de conjunto', () => {
    test('case 3', () => {
      expect(3 + 3).toBe(6);
    });

    test('case 4', () => {
      expect(4 + 4).toBe(8);
    });
  });
});
```

## beforeAll
`beforeAll()` es una sentencia que se ejecuta antes de todas las pruebas en el bloque `describe()`. Se utiliza, por ejemplo, para levantar una base de datos antes de ejecutar las pruebas.

```javascript
describe('conjunto', () => {
  beforeAll(() => {
    // Se ejecuta antes de todas las pruebas
  });
  ...
});
```

## afterAll
`afterAll()` se ejecuta después de que se han ejecutado todas las pruebas en el bloque `describe()`. Puede ser útil para realizar acciones de limpieza, como bajar una base de datos después de las pruebas.

```javascript
describe('conjunto', () => {
  afterAll(() => {
    // Se ejecuta después de todas las pruebas
  });
  ...
});
```

## beforeEach
`beforeEach()` se ejecuta antes de cada prueba individual dentro del bloque `describe()`. Se usa para preparar el entorno para cada prueba.

```javascript
describe('conjunto', () => {
  beforeEach(() => {
    // Se ejecuta antes de cada prueba
  });
  ...
});
```

## afterEach
`afterEach()` se ejecuta después de cada prueba individual dentro del bloque `describe()`. Es útil para limpiar o restablecer el estado después de cada prueba.

```javascript
describe('conjunto', () => {
  afterEach(() => {
    // Se ejecuta después de cada prueba
  });
  ...
});
```