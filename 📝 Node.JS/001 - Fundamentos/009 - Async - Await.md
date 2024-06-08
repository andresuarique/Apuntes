# Async/Await

## ¿Qué es Async/Await?

`async` y `await` son palabras clave introducidas en ECMAScript 2017 (ES8) que permiten escribir código [asíncrono](005%20-%20Asincronía.md) de una manera más legible y manejable. Utilizan [promesas](008%20-%20Promesas.md) en el fondo, pero proporcionan una sintaxis más limpia y directa para manejar operaciones asíncronas, evitando el [callback hell](007%20-%20Callback%20Hell.md) y facilitando la lectura y escritura del código.

## Funciones Async

Una función declarada con la palabra clave `async` devuelve una promesa. Dentro de una función `async`, puedes usar la palabra clave `await` antes de una expresión que devuelve una promesa. La ejecución de la función `async` se pausa hasta que la promesa se resuelve o se rechaza, y luego reanuda con el valor resuelto de la promesa.

### Sintaxis de una Función Async

```js
async function nombreDeLaFuncion() {
    // Código asíncrono
}
```

## La Palabra Clave Await

La palabra clave `await` solo puede usarse dentro de una función `async`. `await` pausa la ejecución de la función `async` y espera a que la promesa se resuelva. Luego, devuelve el valor resuelto de la promesa. Si la promesa es rechazada, `await` lanza el error, que puede ser manejado usando un bloque `try/catch`.

### Sintaxis de Await
```js
let resultado = await promesa;
```

## Ejemplo de Async/Await

```js
const fs = require('fs').promises;

// Función asíncrona para leer un archivo
async function leerArchivo(ruta) {
    try {
        const datos = await fs.readFile(ruta, 'utf8');
        return datos;
    } catch (error) {
        throw new Error(`Error al leer el archivo ${ruta}: ${error.message}`);
    }
}

// Función principal que usa async/await
async function leerArchivosSecuencialmente() {
    try {
        const datos1 = await leerArchivo('archivo1.txt');
        console.log('Contenido de archivo1:', datos1);
        
        const datos2 = await leerArchivo('archivo2.txt');
        console.log('Contenido de archivo2:', datos2);
        
        const datos3 = await leerArchivo('archivo3.txt');
        console.log('Contenido de archivo3:', datos3);
    } catch (error) {
        console.error(error);
    } finally {
        console.log('Lectura de archivos completa.');
    }
}

// Llamar a la función principal
leerArchivosSecuencialmente();

```

### Explicación del Ejemplo

1. **Función `leerArchivo`**:
    
    - Esta función es asíncrona y utiliza `await` para leer un archivo.
    - Si ocurre un error durante la lectura, se lanza un error con un mensaje descriptivo.
2. **Función `leerArchivosSecuencialmente`**:
    
    - Es la función principal que llama a `leerArchivo` de manera secuencial para leer tres archivos.
    - Utiliza `try/catch` para manejar errores que puedan ocurrir durante la lectura de los archivos.
    - El bloque `finally` se ejecuta al final, independientemente de si las operaciones fueron exitosas o no, y notifica que la lectura de archivos ha terminado.

## Ventajas de Async/Await

- **Legibilidad**: El código es más fácil de leer y escribir comparado con el uso de promesas y [callbacks](006%20-%20Callbacks.md) anidados.
- **Manejo de Errores**: El manejo de errores se simplifica usando `try/catch`.
- **Flujo Secuencial**: Facilita la escritura de código asíncrono que se comporta de manera secuencial, similar al código síncrono.

`async` y `await` son herramientas poderosas para manejar la programación asíncrona en JavaScript, haciendo que el código sea más claro y manejable.