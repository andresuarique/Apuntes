# Clases en Java
Una **clase** en Java es una estructura fundamental de la Programación Orientada a Objetos (POO) que agrupa atributos y métodos en un módulo coherente. Define la forma y el comportamiento de los objetos que se crean a partir de ella.

Una clase puede contener:

- **Atributos**: Variables que representan el estado o las propiedades del objeto.
- **Constructores**: Métodos especiales usados para inicializar objetos.
- **Métodos**: Funciones que definen el comportamiento de los objetos.

En Java, una clase se define con la palabra clave `class`:

```java
public class Persona {
    String nombre;
    int edad;

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}
````

## Métodos

Un **método** en Java es un bloque de código que realiza una tarea específica. Los métodos se definen dentro de las clases y pueden modificar o acceder a los atributos de la instancia.

### Ejemplo:

```java
public int obtenerEdad() {
    return edad;
}
```

### Características:

- Pueden tener parámetros.    
- Deben declarar un tipo de retorno (o `void` si no devuelven nada).    
- Pueden ser públicos (`public`), privados (`private`), protegidos (`protected`) o por defecto (package-private).    

## Constructores

Un **constructor** en Java es un método especial que se ejecuta cuando se crea una nueva instancia de una clase.

### Características:

- Su nombre debe coincidir exactamente con el nombre de la clase.    
- No tiene tipo de retorno, ni siquiera `void`.    
- Puede tener parámetros o no.    
- Se pueden definir varios constructores (sobrecarga).
- Se invoca automáticamente al crear un objeto con `new`.


### Ejemplo:

```java
public class Persona {
    String nombre;

    public Persona() {
        this.nombre = "Sin nombre";
    }

    public Persona(String nombre) {
        this.nombre = nombre;
    }
}
```

## Sobrecarga de Constructores

La **sobrecarga de constructores** en Java permite definir múltiples versiones de un constructor dentro de una misma clase, siempre que tengan diferentes listas de parámetros (tipo, cantidad o ambos).

Esto permite crear objetos de distintas maneras según la información disponible en el momento de la instancia.

### Ejemplo:

```java
Persona p1 = new Persona();          // Usa el constructor sin parámetros
Persona p2 = new Persona("Carlos");  // Usa el constructor con un parámetro
```
