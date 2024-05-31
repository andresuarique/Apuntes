
# Promesas

Una Promise o promesa es un objeto que representa la terminación o el fracaso de una operación asíncrona. Esencialmente, una promesa es un objeto devuelto al cual se adjuntan funciones [[Callbacks|callback]], en lugar de pasar callbacks a una función.

Las promesas en JavaScript se representan a través de un objeto, y cada promesa estará en uno de los siguientes estados:
- **Pendiente (pending)**: La promesa se está ejecutando y aún no se ha resuelto ni rechazado.
- **Aceptada (fulfilled)**: La promesa se ha resuelto exitosamente.
- **Rechazada (rejected)**: La promesa se ha rechazado debido a un error.

## Métodos de las Promesas

Cada promesa tiene los siguientes métodos, que podemos utilizar para gestionarla:

1. **then(onFulfilled, onRejected)**: Se ejecuta cuando la promesa se resuelve exitosamente (onFulfilled) o cuando se rechaza (onRejected).
2. **catch(onRejected)**: Se ejecuta cuando la promesa es rechazada.
3. **finally(onFinally)**: Se ejecuta independientemente de si la promesa se resolvió o se rechazó, para realizar una acción una vez que la promesa ha concluido.

![[Pasted image 20240530191452.png]]
## Ejemplo de Promesas

A continuación, se muestra un ejemplo de cómo utilizar promesas en JavaScript para realizar una operación asíncrona, como la lectura de un archivo:

```javascript
const fs = require('fs').promises;

// Función que devuelve una promesa para leer un archivo
function leerArchivo(ruta) {
    return fs.readFile(ruta, 'utf8');
}

// Uso de la función leerArchivo con promesas
leerArchivo('archivo1.txt')
    .then((datos1) => {
        console.log('Contenido de archivo1:', datos1);
        return leerArchivo('archivo2.txt');
    })
    .then((datos2) => {
        console.log('Contenido de archivo2:', datos2);
        return leerArchivo('archivo3.txt');
    })
    .then((datos3) => {
        console.log('Contenido de archivo3:', datos3);
    })
    .catch((error) => {
        console.error('Error al leer un archivo:', error);
    })
    .finally(() => {
        console.log('Lectura de archivos completa.');
    });
```

En este ejemplo, la función `leerArchivo` devuelve una promesa que se resuelve cuando se completa la operación de lectura de un archivo. Utilizamos el método `then` para encadenar las operaciones de lectura de varios archivos de forma secuencial. Si ocurre un error en cualquiera de las operaciones, se captura en el bloque `catch`, y el bloque `finally` se ejecuta al final, independientemente de si la promesa se resolvió o se rechazó.
