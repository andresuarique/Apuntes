### Manejo de Excepciones en Spring Boot

El manejo adecuado de excepciones es esencial para construir aplicaciones robustas en Spring Boot. Spring proporciona diversas herramientas para gestionar excepciones más allá del uso de bloques `try-catch`.

1. **`@ResponseStatus`**:
    
    - **Descripción**: Vincula una excepción a un **código de estado HTTP** específico.
    - **Uso**: Cuando Spring detecta esa excepción, devuelve automáticamente una respuesta HTTP con el código de estado configurado en la anotación.
    - **Ejemplo**:
        
        ```java
        @ResponseStatus(HttpStatus.NOT_FOUND)
        public class ResourceNotFoundException extends RuntimeException { }
        ```
        
2. **`@ExceptionHandler`**:
    
    - **Descripción**: Permite definir **métodos** en un controlador específico para manejar excepciones lanzadas por los métodos de ese controlador.
    - **Uso**: Es útil cuando quieres manejar excepciones de manera local dentro de un controlador.
    - **Ejemplo**:
        
        ```java
        @ExceptionHandler(ResourceNotFoundException.class)
        public ResponseEntity<String> handleResourceNotFound(ResourceNotFoundException ex) {
            return new ResponseEntity<>("Resource not found", HttpStatus.NOT_FOUND);
        }
        ```
        
3. **`@ControllerAdvice`**:
    
    - **Descripción**: Proporciona una forma de manejar excepciones globalmente para toda la aplicación.
    - **Uso**: Consolidar todos los manejos de excepciones en un único componente centralizado.
    - **Ejemplo**:
        
        ```java
        @ControllerAdvice
        public class GlobalExceptionHandler {
            @ExceptionHandler(Exception.class)
            public ResponseEntity<String> handleException(Exception ex) {
                return new ResponseEntity<>("Internal server error", HttpStatus.INTERNAL_SERVER_ERROR);
            }
        }
        ```
        

---

**Resumen**:

- **`@ResponseStatus`**: Vincula excepciones a códigos de estado HTTP específicos.
- **`@ExceptionHandler`**: Maneja excepciones dentro de controladores específicos.
- **`@ControllerAdvice`**: Gestiona excepciones globalmente a nivel de la aplicación.