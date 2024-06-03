# Routing en Aplicaciones Web

El routing, o enrutamiento, es un concepto fundamental en el desarrollo de aplicaciones web. Se refiere al proceso de determinar cómo una aplicación responde a una solicitud de cliente a un punto final específico en particular, identificado por una URL y un [método de solicitud HTTP](Métodos%20HTTP.md) específico.

## Función del Routing

El routing permite que una aplicación web maneje diferentes tipos de solicitudes de manera dinámica y las dirija hacia la funcionalidad adecuada en el servidor. Esto se logra mediante la definición de rutas, que mapean una URL y un método HTTP a una función controladora que maneja la solicitud y genera una respuesta.

## Componentes del Routing

El routing consta de varios componentes clave:

1. **URL (Uniform Resource Locator):** Es una cadena de caracteres que identifica de manera única la ubicación de un recurso en la web. En el contexto del routing, la URL se utiliza para determinar qué recurso o funcionalidad de la aplicación se está solicitando.

2. **Método HTTP:** Es un verbo que especifica la acción que se debe realizar en el recurso identificado por la URL. Algunos de los métodos HTTP más comunes son GET, POST, PUT, DELETE, etc. Cada método tiene un significado y un propósito específicos.

3. **Función Controladora (Handler):** Es una función que se ejecuta cuando se recibe una solicitud que coincide con una determinada ruta y método HTTP. La función controladora procesa la solicitud, realiza las operaciones necesarias en el servidor y genera una respuesta que se envía de vuelta al cliente.