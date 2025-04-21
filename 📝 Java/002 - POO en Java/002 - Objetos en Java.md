
# Objetos en Java
Un **objeto** en Java es una instancia de una [clase](001%20-%20Clases%20en%20Java.md). Cuando se crea un objeto, se reserva espacio en memoria para almacenar su estado y se le asignan comportamientos definidos por su clase.

Los objetos contienen:

- **Atributos**: Almacenan su estado o características.
- **Métodos**: Definen sus comportamientos o acciones.

### Creación de un objeto

Para crear un objeto en Java se utiliza la palabra clave `new`, seguida del constructor de la clase:

```java
Persona persona = new Persona();
````

Esto realiza tres acciones:

1. Reserva memoria para el nuevo objeto.    
2. Llama al constructor correspondiente.    
3. Asigna la referencia del objeto creado a la variable `persona`.    

### Ejemplo completo:

```java
public class Persona {
    String nombre;

    public Persona(String nombre) {
        this.nombre = nombre;
    }

    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}

// En otra clase
Persona p = new Persona("Ana");
p.saludar();  // Salida: Hola, soy Ana
```
