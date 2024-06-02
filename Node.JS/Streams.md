# Streams

Un stream es el proceso de consumir datos al mismo tiempo que se están recibiendo. En palabras del profesor, es el paso de datos entre un punto y otro.

## Ejemplo de Lectura de un Archivo con Streams

```javascript
const fs = require('fs');

let data = '';

let readableStream = fs.createReadStream(__dirname + '/input.txt');

readableStream.setEncoding('UTF8');
readableStream.on('data', chunk => data += chunk);
readableStream.on('end', () => console.log(data));
```

## Escritura en el Buffer de Salida del Sistema

Podemos escribir en el [buffer](Node.JS/Buffers.md) de salida del sistema. `process.stdout` es un buffer de escritura que empieza a trabajar para generar todo esto.

```javascript
process.stdout.write('hola');
process.stdout.write('que');
process.stdout.write('tal');
```

## Uso de Streams con Transformación

Para usar los streams, podemos transformarlos de la siguiente forma:

```javascript
const stream = require('stream');
const util = require('util');

const Transform = stream.Transform;

function Upper() {
    Transform.call(this);
}

util.inherits(Upper, Transform);

Upper.prototype._transform = function (chunk, encoding, callback) {
    let chunkUpper = chunk.toString().toUpperCase();
    this.push(chunkUpper);
    callback();
};

let upper = new Upper();

readableStream
    .pipe(upper)
    .pipe(process.stdout);
```

En este ejemplo:

- Creamos un stream de lectura (`readableStream`) que lee un archivo de texto (`input.txt`).
- Configuramos el stream para usar la codificación UTF-8 y acumulamos los datos en la variable `data`.
- Cuando termina la lectura (`end`), se imprime el contenido del archivo.
- Usamos `process.stdout.write` para escribir directamente en el buffer de salida.
- Creamos un stream de transformación (`Upper`) que convierte los datos a mayúsculas.
- Conectamos el stream de lectura al stream de transformación y luego al buffer de salida del sistema usando `pipe`.

Esto nos permite procesar y manipular datos en tiempo real a medida que se reciben, sin necesidad de cargar todo en memoria de una sola vez.
