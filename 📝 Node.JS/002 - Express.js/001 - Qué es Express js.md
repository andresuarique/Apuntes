# ¿Qué es Express?

**Express** es el framework web más popular de [Node.js](../📌%20Node%20js.md) y es la librería subyacente para un gran número de otros frameworks web populares de Node. Proporciona mecanismos para facilitar el desarrollo de aplicaciones web y APIs.

## Características de Express

1. **Manejadores de Peticiones**:
   - Permite la escritura de manejadores de peticiones utilizando diferentes [verbos HTTP](../../🌐%20ConceptosGenerales/Métodos%20HTTP.md) (GET, POST, PUT, DELETE, etc.) en diferentes caminos URL (rutas).

2. **Motor de Renderización de Vistas**:
   - Facilita la integración con motores de renderización de "vistas" para generar respuestas mediante la introducción de datos en plantillas. Esto permite crear contenido dinámico basado en datos del servidor.

3. **Ajustes de Aplicaciones Web**:
   - Permite establecer configuraciones de la aplicación web, como el puerto a utilizar para conectar y la localización de las plantillas que se utilizan para renderizar las respuestas.

4. **Middleware**:
   - Añade procesamiento de peticiones "[middleware](../../🌐%20ConceptosGenerales/Middleware.md)" adicional en cualquier punto dentro de la tubería de manejo de la petición. Esto permite la manipulación de solicitudes y respuestas, la adición de funcionalidades y el manejo de errores de manera modular y flexible.

Express se destaca por su simplicidad y flexibilidad, permitiendo a los desarrolladores crear aplicaciones web robustas y escalables con facilidad. Al proporcionar una estructura básica sin imponer una arquitectura rígida, permite a los desarrolladores decidir cómo organizar su aplicación según sus necesidades específicas.
