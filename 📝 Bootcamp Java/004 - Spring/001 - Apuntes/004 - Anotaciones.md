### Diccionario de Anotaciones en Spring Boot

- **@SpringBootApplication**:  
    Marca la clase principal de una aplicación Spring Boot. Combina tres anotaciones:
    
    - **@EnableAutoConfiguration**: Activa la configuración automática.
    - **@ComponentScan**: Busca y registra componentes de la aplicación.
    - **@Configuration**: Define beans de configuración.
- **@RestController**:  
    Define un controlador REST, donde los métodos devuelven datos (normalmente en formato JSON o XML) en lugar de vistas.
    
- **@GetMapping**:  
    Mapea solicitudes HTTP GET a un método controlador.
    
- **@PathVariable**:  
    Captura valores de parámetros en la URL y los asigna a los parámetros del método.