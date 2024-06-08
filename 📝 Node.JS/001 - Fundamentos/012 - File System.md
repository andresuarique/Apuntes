# File System

El File System (sistema de archivos) es uno de los [módulos](010%20-%20Módulos.md) principales que nos ofrece Node.js. Este módulo nos permite operar directamente con los archivos de nuestro sistema, permitiéndonos crear, leer, editar o eliminar archivos. Es muy importante tener en cuenta que la mayoría de los métodos de este módulo son [asíncronos](005%20-%20Asincronía.md), pero también se ofrecen versiones síncronas. Sin embargo, las versiones síncronas son poco recomendables, ya que pueden bloquear el [event loop](003%20-%20Event%20Loop.md) de Node.js.

Para poder usar este módulo, debemos importarlo con `require` en una constante con el mismo nombre del módulo:

```js
const fs = require('fs');
```

Una vez importado, podremos comenzar a usar los métodos que este módulo nos ofrece:

## Métodos Principales del Módulo File System

### `fs.readFile(path, callback)`

Lee el contenido de un archivo de manera asíncrona. El primer argumento es la ruta del archivo y el segundo es una función [callback](006%20-%20Callbacks.md) que se ejecuta cuando la lectura del archivo se completa.

```js
fs.readFile('ruta/al/archivo.txt', 'utf8', (err, data) => {
    if (err) {
        console.error('Error al leer el archivo:', err);
        return;
    }
    console.log('Contenido del archivo:', data);
});
```

### `fs.writeFile(path, content, callback)`

Escribe contenido en un archivo de manera asíncrona. Si el archivo no existe, se crea. El primer argumento es la ruta del archivo, el segundo es el contenido a escribir y el tercero es una función callback que se ejecuta cuando la escritura se completa.

```js
fs.writeFile('ruta/al/archivo.txt', 'Contenido a escribir', (err) => {
    if (err) {
        console.error('Error al escribir el archivo:', err);
        return;
    }
    console.log('Archivo escrito con éxito');
});
```

### `fs.unlink(path, callback)`

Elimina un archivo de manera asíncrona. El primer argumento es la ruta del archivo y el segundo es una función callback que se ejecuta cuando el archivo se elimina.

```js
fs.unlink('ruta/al/archivo.txt', (err) => {
    if (err) {
        console.error('Error al eliminar el archivo:', err);
        return;
    }
    console.log('Archivo eliminado con éxito');
});
```

## Métodos Síncronos (No Recomendados)

Node.js también proporciona versiones síncronas de estos métodos, como `fs.readFileSync`, `fs.writeFileSync` y `fs.unlinkSync`. Sin embargo, el uso de estos métodos no es recomendable en la mayoría de los casos, ya que pueden bloquear el event loop, lo que afecta negativamente el rendimiento de la aplicación.

```js
try {
    const data = fs.readFileSync('ruta/al/archivo.txt', 'utf8');
    console.log('Contenido del archivo:', data);
} catch (err) {
    console.error('Error al leer el archivo:', err);
}
```
