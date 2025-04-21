### Inyección de Dependencias (DI) en Spring

La **inyección de dependencias** es un patrón de diseño que implementa la **inversión de control (IoC)**. Su objetivo es desacoplar el código para facilitar su mantenimiento y escalabilidad, proporcionando las dependencias necesarias a un objeto sin que este las busque.

- **Proceso**: Los objetos definen sus dependencias a través de constructores, métodos de fábrica o propiedades. El contenedor IoC de Spring se encarga de inyectar esas dependencias cuando crea el bean.
- **Ventajas**:
    - Código más limpio y desacoplado.
    - Mejora la facilidad de prueba al permitir el uso de implementaciones mock, especialmente cuando las dependencias están basadas en interfaces o clases abstractas.

### Tipos de Inyección de Dependencias en Spring

1. **Inyección basada en Constructor**:
    
    - **Descripción**: Las dependencias se inyectan a través del constructor de la clase.
    - **Ventaja**: Es la forma más recomendada para garantizar que las dependencias sean obligatorias e inmutables. No se puede instanciar la clase sin que se proporcionen todas las dependencias requeridas.
    - **Uso común**: Se usa cuando las dependencias son **esenciales** para el funcionamiento de la clase y deben ser proporcionadas al momento de la creación del objeto.
2. **Inyección basada en Setter**:
    
    - **Descripción**: Las dependencias se inyectan a través de métodos setters.
    - **Ventaja**: Ofrece más flexibilidad, permitiendo inyectar dependencias opcionales. Las dependencias pueden ser modificadas después de la creación del objeto.
    - **Uso común**: Se usa cuando las dependencias no son críticas o son **opcionales** y no es necesario proporcionar todas las dependencias en el momento de la creación del objeto.
3. **Inyección con `@Autowired`**:
    
    - **Descripción**: Spring inyecta automáticamente las dependencias utilizando la anotación `@Autowired`, ya sea en un constructor, un setter o un campo.
    - **Ventaja**: Simplifica el código al no tener que especificar explícitamente cómo se inyectan las dependencias. Spring se encarga de resolver las dependencias por tipo.
    - **Uso común**: Es más conveniente cuando se quiere delegar la resolución de dependencias a Spring, y las dependencias son fácilmente resolubles por tipo.

---

**Diferencias clave entre los tipos de inyección**:

- **Constructor**: Asegura que todas las dependencias sean proporcionadas y **obligatorias** al momento de la creación de la clase.
- **Setter**: Permite **dependencias opcionales** y puede modificarse después de la creación del objeto.
- **@Autowired**: Simplifica la inyección automáticamente por tipo, siendo útil en la mayoría de los casos, pero a veces menos explícito.