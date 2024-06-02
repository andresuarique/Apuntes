# Aplicación del Routing en Express.js

En Express.js, el [routing](../../ConceptosGenerales/Routing%20en%20Aplicaciones%20Web.md) se implementa mediante el uso de [métodos de solicitud HTTP](../../ConceptosGenerales/Métodos%20HTTP.md) para definir cómo la aplicación responde a las solicitudes de los clientes en puntos finales específicos. A continuación, se muestra cómo se aplica el routing en Express:

1. **Definición de Rutas:**
   - Las rutas se definen utilizando métodos de solicitud HTTP como `get`, `post`, `put`, `delete`, etc., en una instancia de Express (normalmente llamada `app`).

   ```js
   app.get(PATH, HANDLER);
   ```

   ```js
   app.post(PATH, HANDLER);
   ```

   ```js
   app.put(PATH, HANDLER);
   ```

   ```js
   app.delete(PATH, HANDLER);
   ```

   Donde `PATH` es la ruta en el servidor y `HANDLER` es la función que se ejecuta cuando la ruta coincide con la solicitud entrante.

2. **Manejadores de Rutas:**
   - Los manejadores de rutas son funciones que se ejecutan cuando una solicitud coincide con la ruta especificada. Estas funciones pueden realizar diversas acciones, como enviar una respuesta al cliente, acceder a bases de datos, procesar datos, etc.

   ```js
   app.get('/ruta', (req, res) => {
       // Manejador de la ruta para el método GET en la ruta '/ruta'
       // Aquí se pueden realizar diversas acciones
       res.send('Respuesta de la ruta GET');
   });
   ```

   ```js
   app.post('/ruta', (req, res) => {
       // Manejador de la ruta para el método POST en la ruta '/ruta'
       // Aquí se pueden realizar diversas acciones
       res.send('Respuesta de la ruta POST');
   });
   ```

3. **Middleware de Rutas:**
   - Express permite utilizar [middleware](../../ConceptosGenerales/Middleware.md) de rutas para realizar acciones específicas antes o después de que se ejecute el manejador de la ruta. Esto proporciona flexibilidad para agregar funcionalidades adicionales a las rutas, como la autenticación, la validación de datos, el registro de solicitudes, etc.

   ```js
   app.get('/ruta', middleware, (req, res) => {
       // Manejador de la ruta con middleware
       // El middleware se ejecuta antes de que llegue aquí
       // Aquí se pueden realizar diversas acciones
   });
   ```

   ```js
   app.post('/ruta', middleware, (req, res) => {
       // Manejador de la ruta con middleware
       // El middleware se ejecuta antes de que llegue aquí
       // Aquí se pueden realizar diversas acciones
   });
   ```

El enrutamiento en Express.js ofrece una forma estructurada y flexible de definir cómo se manejan las solicitudes entrantes, lo que permite construir aplicaciones web dinámicas y escalables.