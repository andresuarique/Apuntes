# Encapsulamiento  

El **encapsulamiento** consiste en controlar el acceso a los datos de un objeto o instancia de una clase. Esto implica decidir qué métodos y atributos serán accesibles desde fuera de la clase y cuáles permanecerán ocultos, utilizando los **modificadores de acceso** de Java.  

## Modificadores de acceso  
- **`public`**: Permite que el atributo o método sea accesible desde cualquier lugar.  
- **`private`**: Restringe el acceso, permitiendo que solo sea visible dentro de la misma clase.  
- **`protected`**: Permite el acceso desde clases del mismo paquete y desde subclases.  
- **Sin modificador** (*default*): Accesible solo dentro del mismo paquete.  

---

# Setters y Getters  

Los **setters** y **getters** son métodos utilizados para acceder y modificar atributos privados de una clase.  

## Características:  
- **Setters**: Permiten asignar valores a las variables de instancia.  
- **Getters**: Permiten obtener los valores de las variables de instancia.  
- Generalmente, las variables de instancia se definen como **`private`**, mientras que los setters y getters se definen como **`public`**, ofreciendo un acceso controlado.  

### Ejemplo:  
```java
public class Persona {
    private String nombre;

    // Getter
    public String getNombre() {
        return nombre;
    }

    // Setter
    public void setNombre(String nombre) {
        this.nombre = nombre;
    }
}
````

---

# Herencia

La **herencia** permite crear una nueva clase basada en una clase existente, heredando sus atributos y métodos públicos o protegidos.

## Características:

- La clase que hereda se llama **subclase** (o clase hija).
- La clase de la que se hereda se llama **superclase** (o clase padre).
- Java solo soporta **herencia simple**, es decir, una clase puede heredar de una única clase padre.

### Sintaxis básica:

```java
public class ClaseHija extends ClasePadre {
    // Métodos y atributos adicionales
}
```

### Ejemplo:

```java
public class Animal {
    protected String nombre;

    public void comer() {
        System.out.println("El animal está comiendo.");
    }
}

public class Perro extends Animal {
    public void ladrar() {
        System.out.println("El perro está ladrando.");
    }
}
```

En el ejemplo anterior, la clase `Perro` hereda el atributo `nombre` y el método `comer` de la clase `Animal`.