## Java
### Colecciones
- Son conjuntos de objetos (Set, Collection, Map)
### Garbage Colector
- Se encarga de limpiar memoria, se peude llamar (System.gc())
- Limpia la memoria cuando un variable, objeto o instancia se queda sin referencia
### Static
Define metodos o atributos propios de la clase, es decir no se instacian, el main es static

### Tipos primitivos vs Wrapper

| Primitivo                   | Wrapper                  |
| --------------------------- | ------------------------ |
| Ocupan menos memoria        | Ocupan mas meoria        |
| No pueden recibir null      | Pueden recibir nulos     |
| No tienen metodos asociados | Tienen metodos asociados |

## Spring
### Spring framework vs Spring Boot

| Framework                                                                             | Boot                                                                                                  |
| ------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Es un framework que proporciona funcionalidades para desarrollar aplicaciones en java | Es un proyecto que se basa en Spring framework para facilitar el desarrollo de aplicaciones en spring |
| Requiere configuracion manual                                                         | Tiene configuracion autoamatica                                                                       |
| Es el marco completo para desarrollo de aplicaciones                                  | Es una extension del framework que simplifica el desarrollo                                           |

### Estereotipos
Son anotaciones que definen el rol de un componente
@Service @Controller @Repository @Component

### Bean
Es un objeto que son instancias de clases son creado y gestionados por el framework

### Scopes
- *SINGLETON*: solo crea una instancia
- *PROTOTYPE*: crea una nueva instancia cada que se requiere el bean

### @SpringBootApplication
- Es la anotacion que se usa para inicializar la aplicacion de spring, esta contiene tres anotaciones *@EnableAutoConfigurations* *@ComponentScan* *@Configuration*
### @RestController
- Anotacion para definir controladores REST, contiene 2 anotaciones *@Controller* *@ResquestMapping*

## Patrones
Conceptos de soluciones frecuentes
### Patrones Creacionales
Enfocados en creación de objetos
- **Singleton**: Asegura que una clase tenga una única instancia y proporciona un punto de acceso global a ella.
- **Factory Method**: Define una interfaz para crear un objeto, pero permite a las subclases decidir qué clase instanciar.

### Patrones Estructurales
Enfocados en como se componen las clases
- **Adapter**: Permite que interfaces incompatibles colaboren al convertir la interfaz de una clase en otra que el cliente espera.
- **Decorator**: Permite agregar comportamiento a objetos de manera dinámica sin modificar su estructura.

### Patrones de Comportamiento
Enfocado en como se comportan las clases
- **Observer**: Permite a un objeto notificar a otros cuando su estado cambia, promoviendo un sistema de suscripción y publicación.
- **Strategy**: Define una familia de algoritmos, encapsulándolos y haciéndolos intercambiables. Permite que el algoritmo varíe independientemente de los clientes que lo utilizan.

## Arquitectura
### Hexagonal
Son capas
- *Dominio* (Logica de negocio) Modelos, Servicios
- *Puertos* (Conectan dominio con el exterior) Controladores
- *Adaptadores* conectan con servicios externos
- *Infraestrcutura* (servicios transversales)Bases de datos, auditoria, seguridad
   ![Pasted image 20241023222339](../📎%20ANEXOS/Pasted%20image%2020241023222339.png)

## POO
### Polimorfismo
- Capacidad de que una funcion se comporte diferente dependiendo de quien la implemente, ejemplo clases hijas

### Sobrecarga de metodos
- Metodo con el mismo nombre en la misma clase pero con diferentes parametros, permite adaptar el comportamiento segun los parametros
- Cosntructores

### Sobreescritura de metodos
- Cambiar la implementacion de un metodo ya implementado *@Override*

### Clase asbtracta vs interface

| Abstracta                                            | Interface                                          |
| ---------------------------------------------------- | -------------------------------------------------- |
| No puede ser instanciada directametne                | Puede ser instanciada directamente                 |
| puede contener metodos implementados                 | No tiene metodos implementados                     |
| Una clase solo puede extender de una clase abstracta | Una clase solo puede extender de varias interfaces |
| Es una plantilla                                     | Es un conjunto de reglas                           |


## REST
### HATEOAS

Es un principio que los usuarios pueden itneracutar con los recursos de la api por medio de URLs que los servicios de esta regresa

### Codigos de estado
#### Tipos
- 100 INFORMACION
- 200 SUCCESS
- 300 REDIRECCION
- 400 CLIENT ERROR
- 500 SERVER ERROR
#### Comunes
- 200 ok
- 201 created
- 204 no content
- 400 bad request
- 401 unathorized
- 403 forbidden
- 404 not found
- 500 internal server error
- 502 bad gateway
- 503 service unavaliable

### URL
- Sustanticos, no acciones (para eso estan los verbos http)
- Filtrado con query params
- versionado (v1, v2)

## PRINCIPIOS
### SOLID
- *SINGLE RESPONSABILITY*: Solo una responsabilidad, mas facil de mantener
- *OPEN / CLOSED*: Abiertas a extension, pero cerradas a modificacion, agregar codigo pero no cambiarlo
- *LISKOV*: las subclases deben poderse reemplazar por la clase base
- *INTERFACE SEGREGATION*: Tener muchas interfaces en lugar de una general, las clases solo deben implementar interfaces que usa
- *DEPENDENCY INVERSION*: las dependencias deben ser abstractas, todo depende de abstracciones (como interfaces) ayuda a desaclopar, y facilita las pruebas y matenimineto

### ACID
Para base de datos
- *ATOMICIDAD*: transacciobnes, toda la operacion se debe completar, si no re hace rollback
- *CONSISTENCIA*: una transaccion debe llevar de un estado valido a otro, es decir respeta la integridad (FK, restricciones), si no se regresa
- *ISOALTION (ASILAMIENTO)*: Las transacciones no debe ser visibles para otras transacciones.
- *DURABILIDAD*: Cuando la transaccion se completa sus efectos son permantentes en la abse de datos