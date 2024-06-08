# Error First Callbacks

Un patrón comúnmente seguido en cualquier lenguaje y programa de desarrollo es el **Error First Callbacks**. Esto significa que siempre que tengamos un [callback](006%20-%20Callbacks.md), el primer parámetro debería ser el error. Este patrón se utiliza debido a la convención de que todo puede fallar.

Otro patrón típico es tener el callback como la última función que se pasa, aunque esto puede depender del caso específico.

## Ejemplo de Error First Callback

```javascript
function asincrona(callback) {
    setTimeout(() => {
        try {
            let a = 3 + w;  // Esto generará un error ya que 'w' no está definido
            callback(null, a);
        } catch (error) {
            callback(error);
        }
    }, 1000);
}

asincrona((err, dato) => {
    if (err) {
        console.error('Tenemos un error');
        console.error(err);
        return false;
        // throw err
    }

    console.log(`Todo ha ido bien, mi dato es ${dato}`);
});
```

En este ejemplo:

1. **Definición de la función asincrónica**:
   - `asincrona(callback)` es una función que simula una operación [asíncrona](005%20-%20Asincronía.md) usando `setTimeout`.
   - Dentro del `setTimeout`, se intenta realizar una operación que genera un error (`3 + w` donde `w` no está definido).
   - Si ocurre un error, se pasa como el primer argumento del `callback`.
   - Si no hay errores, el resultado se pasa como el segundo argumento del `callback`.

2. **Uso del Error First Callback**:
   - La función `asincrona` se llama con un callback que maneja el error como el primer parámetro (`err`).
   - Si hay un error (`if (err)`), se registra en la consola y se devuelve `false` para detener la ejecución.
   - Si no hay error, se registra el dato en la consola.

Este patrón es esencial para manejar errores de manera consistente en funciones asíncronas, asegurando que los errores se capturen y manejen adecuadamente antes de proceder con el procesamiento de datos.