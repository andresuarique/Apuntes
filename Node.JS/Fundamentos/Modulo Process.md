# Módulo `process`

El [módulo](Modulos.md) `process` en Node.js nos permite interactuar con el proceso actual de Node.js. Podemos escuchar señales, gestionar eventos y realizar diversas acciones en función del estado del proceso.

Aunque puedes hacer `require` para obtener `process`, no es necesario porque `process` es una variable global disponible en todos los entornos de Node.js.

```javascript
const process = require('process'); // No es necesario
```

## Eventos del Proceso

- **`beforeExit`**: Se dispara cuando Node.js está a punto de finalizar el proceso, pero hay trabajos pendientes en el [bucle de eventos](Event%20Loop.md) que deben completarse.
    ```javascript
    process.on('beforeExit', (code) => {
        console.log('El proceso está a punto de finalizar con el código:', code);
    });
    ```

- **`exit`**: Se dispara cuando el proceso está a punto de terminar, una vez que no queda trabajo pendiente en el bucle de eventos.
    ```javascript
    process.on('exit', (code) => {
        console.log('El proceso ha terminado con el código:', code);
    });
    ```

- **`uncaughtException`**: Permite capturar cualquier error que no fue capturado previamente.
    ```javascript
    process.on('uncaughtException', (err, origen) => {
        console.error('Se nos ha olvidado capturar un error');
        console.error(err);
    });

    // Generar un error no capturado
    funNoExiste();
    ```

- **`unhandledRejection`**: Permite capturar cualquier error de promesas que se han rechazado y no han sido manejadas.
    ```javascript
    process.on('unhandledRejection', (reason, promise) => {
        console.error('Promesa rechazada sin manejar:', promise, 'razón:', reason);
    });

    // Generar una promesa rechazada no manejada
    Promise.reject(new Error('Promesa rechazada sin manejar'));
    ```

## Uso del Módulo `process`

El módulo `process` es esencial para manejar eventos relacionados con el ciclo de vida de la aplicación y para capturar errores inesperados que podrían detener el proceso. A continuación, algunos de los eventos más utilizados:

### Ejemplo de Manejo de `uncaughtException`

```javascript
process.on('uncaughtException', (err, origen) => {
    console.error('Se nos ha olvidado capturar un error');
    console.error(err);
});

// Generar un error no capturado
funNoExiste();
```

En este ejemplo, se captura un error no manejado utilizando el evento `uncaughtException`. Esto permite que el proceso no se detenga abruptamente y que se pueda realizar una acción específica (como registrar el error) antes de finalizar.

El módulo `process` es una herramienta poderosa para gestionar eventos y errores en una aplicación Node.js, proporcionando mayor control sobre el ciclo de vida del proceso y mejor manejo de excepciones.