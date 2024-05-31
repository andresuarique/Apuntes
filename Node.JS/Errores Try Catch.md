# Errores (try / catch)

El manejo de errores síncronos y [[Asincronía|asíncronos]] en JavaScript se realiza utilizando `try...catch` para errores síncronos y métodos como `.catch()` o bloques `try catch` con [[Async - Await|async/await]] para errores asíncronos. A continuación, se proporcionan ejemplos de cómo manejar ambos tipos de errores:

### Manejo de Errores Síncronos con `try...catch`

```javascript
try {
    // Código síncrono que puede arrojar un error
    const resultado = funcionSincrona(); 
    // Supongamos que esta función lanza un error
    console.log(resultado); 
    // Esta línea nunca se ejecutará
} catch (error) {
    // Manejo del error síncrono
    console.error('Se produjo un error síncrono:', error.message);
}
```

En este caso, el bloque `try` envuelve el código síncrono que podría arrojar un error. Si ocurre un error en ese bloque, se captura y se pasa al bloque `catch`. Puedes acceder al objeto `error` para obtener información sobre el error.

### Manejo de Errores Asíncronos con `async/await` y `try...catch`

```javascript
async function doSomething() {
    try {
        // Código asíncrono que puede arrojar un error
        const resultado = await funcionAsincrona(); 
        // Supongamos que esta función lanza un error
        console.log(resultado); 
        // Esta línea nunca se ejecutará
    } catch (error) {
        // Manejo del error asíncrono
        console.error('Se produjo un error asíncrono:', error.message);
    }
}
doSomething();
```

En este caso, `async/await` permite que el código asíncrono sea manejado dentro de un bloque `try...catch` como si fuera síncrono. Si ocurre un error en la función asíncrona, se captura y se maneja en el bloque `catch`.

### Manejo de Errores Asíncronos con Promesas y `.catch()`

```javascript
someAsyncFunction()
    .then(result => {
        // Realiza alguna operación con el resultado
    })
    .catch(error => {
        console.error('Error en la promesa:', error);
    });
```

Cuando trabajas con promesas, puedes utilizar el método `.catch()` para manejar errores que ocurran en la ejecución de la promesa. Este método se encargará de atrapar cualquier error lanzado dentro de la promesa o en las promesas encadenadas.

El manejo de errores, ya sean síncronos o asíncronos, es fundamental para desarrollar aplicaciones robustas y detectar problemas en tiempo de ejecución. Debes elegir la estrategia adecuada según el tipo de operación que estés realizando.