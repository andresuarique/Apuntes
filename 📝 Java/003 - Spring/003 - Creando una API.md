## Crear una API en Spring Boot

### Crear un Controlador

1. **Crear una clase controladora**:
    
    - La clase se debe anotar con `@RestController` para indicar que manejará solicitudes HTTP y responderá con datos.
2. **Definir un método controlador**:
    
    - Crear un método, como `sayHello()`, que responderá a las solicitudes HTTP.
    - Este método puede devolver tipos simples como `String` o tipos más complejos (objetos o listas).
3. **Asignar un endpoint al método**:
    
    - Usar la anotación `@GetMapping` para especificar la ruta HTTP que activará el método.
    - Por ejemplo, para responder a `/hello`, usar:
        
        ```java
        @GetMapping("/hello")
        public String sayHello() {
            return "Hello World";
        }
        ```
        

---

### Recibir Parámetros

Los métodos controladores pueden aceptar parámetros de las solicitudes HTTP, por ejemplo, mediante:

#### 1. **@PathVariable**

- Permite capturar valores desde la URL.
- Ejemplo:
    
    ```java
    @GetMapping("/hello/{name}")
    public String sayHello(@PathVariable String name) {
        return "Hello, " + name + "!";
    }
    ```
    
    Si se accede a `/hello/John`, la respuesta será:
    
    ```
    Hello, John!
    ```
    

#### 2. **@RequestParam**

- Permite capturar parámetros query en la URL.
- Ejemplo:
    
    ```java
    @GetMapping("/greet")
    public String greet(@RequestParam String name) {
        return "Greetings, " + name + "!";
    }
    ```
    
    Si se accede a `/greet?name=Alice`, la respuesta será:
    
    ```
    Greetings, Alice!
    ```
    

---

### Ejemplo Completo

```java
@RestController
public class HelloRestController {

    // Endpoint simple
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello World";
    }

    // Con @PathVariable
    @GetMapping("/hello/{name}")
    public String sayHelloToUser(@PathVariable String name) {
        return "Hello, " + name + "!";
    }

    // Con @RequestParam
    @GetMapping("/greet")
    public String greetUser(@RequestParam String name) {
        return "Greetings, " + name + "!";
    }
}
```