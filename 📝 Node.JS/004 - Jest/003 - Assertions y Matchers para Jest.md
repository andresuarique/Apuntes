# Assertions / Matchers para Jest
Las assertions o afirmaciones se utilizan para verificar el comportamiento del código. Algunas de las más comunes en Jest son:

## Expect
Es la función principal de Jest y se utiliza para especificar la salida esperada de una función o valor.
```javascript
expect(2 + 2).toBe(4);
```

## toBe
Compara dos valores usando el operador `===`.
```javascript
expect(2 + 2).toBe(4);
```

## toEqual
Compara dos valores recursivamente para verificar si son iguales.
```javascript
expect({ a: 1 }).toEqual({ a: 1 });
```

## toMatch
Comprueba si una cadena o expresión regular coincide con una cadena esperada.
```javascript
expect("Hello World").toMatch(/Hello/);
```

## toBeNull
Comprueba si un valor es `null`.
```javascript
expect(null).toBeNull();
```

## toBeUndefined
Comprueba si un valor es `undefined`.
```javascript
expect(undefined).toBeUndefined();
```

## toBeDefined
Comprueba si un valor no es `undefined`.
```javascript
expect("Hello").toBeDefined();
```

## toBeTruthy
Comprueba si un valor es verdadero.
```javascript
expect("Hello").toBeTruthy();
```

## toBeFalsy
Comprueba si un valor es falso.
```javascript
expect("").toBeFalsy();
```

## toThrow
Comprueba si una función lanza una excepción.
```javascript
expect(() => { throw new Error(); }).toThrow();
```
