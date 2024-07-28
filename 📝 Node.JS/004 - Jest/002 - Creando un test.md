# Tu primer test
Vamos a experimentar un poco con Jest. Crearemos varias funciones matemáticas y sus respectivos tests.

## Creación del archivo math.js
```javascript
// Función para sumar
function sum(a, b) {
  return a + b;
}

// Función para multiplicar
function multiply(a, b) {
  return a * b;
}

// Función para dividir
function divide(a, b) {
  return a / b;
}

// Exportamos nuestras funciones como módulos
module.exports = {
  sum,
  multiply,
  divide
}
```

## Creación del archivo de test math.test.js
Para empezar a testear nuestras funciones, usamos la palabra reservada `test` como función. Dentro de esta función, escribimos, como string, qué esperamos que haga esta función, es decir, una pequeña descripción de lo que se supone debe hacer la función. Luego de esto, tenemos una función que será el manejador del test, en esta estableceremos la lógica de nuestro test.

```javascript
// Importar funciones creadas
const { sum, multiply, divide } = require('./math');

test("añadir 1 + 3 debe dar 4", () => {
  // Ejecutamos nuestra función y le pasamos sus respectivos valores
  const rta = sum(1, 3);

  // Expect tendrá la ejecución de la función y toBe tendrá el resultado que esperamos de la función
  expect(rta).toBe(4);
});
```

Si ejecutamos nuestro comando de test, veremos que tenemos un resultado correcto:
```bash
npm run test # Output = test passed
```

## Creación de tests adicionales
```javascript
const { sum, multiply, divide } = require('./math');

test("añadir 1 + 3 debe dar 4", () => {
  const rta = sum(1, 3);
  expect(rta).toBe(4);
});

test("multiplicar 9 x 2 debe dar 18", () => {
  const rta = multiply(9, 2);
  expect(rta).toBe(18);
});

test("dividir 12 / 3 debe dar 4", () => {
  const rta = divide(12, 3);
  expect(rta).toBe(4);

  // Podemos tener varios escenarios de prueba en nuestros tests
  const rta2 = divide(5, 2);
  expect(rta2).toBe(2.5);
});
```

## Aumentando la complejidad de nuestros tests
```javascript
test('dividir entre 0 nos debe retornar un string que diga "no se puede dividir entre 0"', () => {
  const rta = divide(0, 0);
  expect(rta).toBe("no se puede dividir entre 0");
});
```

## Solucionando el problema con una validación
```javascript
function divide(a, b) {
  if (a === 0 || b === 0) {
    return "no se puede dividir entre 0";
  }
  return a / b;
}
```

Así es como podemos crear nuestras pruebas para nuestros proyectos.
