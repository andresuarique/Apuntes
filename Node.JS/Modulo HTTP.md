# Módulo `http`

Node.js nos ofrece el [módulo](Modulos.md) HTTP, el cual nos permite principalmente crear un servidor en nuestro computador. Este módulo incluye todas las herramientas necesarias para crear un sistema de rutas, definir cómo responderá a cada ruta, gestionar los headers, y más.

## Características del Módulo HTTP

- **Creación de Servidores**: Permite crear servidores HTTP que pueden manejar solicitudes y enviar respuestas.
- **Gestión de Rutas**: Puedes definir diferentes rutas y cómo responderá el servidor a cada una.
- **Manipulación de Headers**: Facilita el envío y la gestión de headers HTTP.

## Método Principal: `createServer`

Uno de los métodos principales de este módulo es `createServer`, el cual nos permite abrir un puerto y crear un servidor.

### Ejemplo de Uso

```javascript
const http = require('http');

http.createServer(theServer).listen(3005);

function theServer(req, res) {
    console.log('Nueva petición');
    console.log(req.url);
    switch (req.url) {
        case '/hola':
            res.write('Bienvenido a hola');
            res.end();
            break;
        case '/node':
            res.write('Comienza a aprender Node.js');
            res.end();
            break;
        default:
            res.write('Error 404: Page Not Found');
            res.end();
            break;
    }
}
```

En este ejemplo, se crea un servidor que escucha en el puerto 3005. La función `theServer` se encarga de gestionar las solicitudes entrantes (`req`) y enviar las respuestas (`res`). Dependiendo de la URL de la solicitud, el servidor responderá de manera diferente:

- **`/hola`**: Responde con el mensaje "Bienvenido a hola".
- **`/node`**: Responde con el mensaje "Comienza a aprender Node.js".
- **Ruta por defecto**: Responde con el mensaje "Error 404: Page Not Found".

Este código muestra cómo crear un servidor básico que puede gestionar diferentes rutas y enviar respuestas adecuadas.

## Ventajas del Módulo HTTP

1. **Flexibilidad**: Permite crear servidores personalizados y gestionar las solicitudes de manera precisa.
2. **Facilidad de Uso**: La API es sencilla y directa, facilitando la creación y configuración de servidores.
3. **Integración**: Se integra fácilmente con otros módulos y frameworks de Node.js, como Express, para extender su funcionalidad.

El módulo HTTP de Node.js es una herramienta poderosa y flexible para crear servidores y gestionar comunicaciones HTTP, esencial para el desarrollo de aplicaciones web.