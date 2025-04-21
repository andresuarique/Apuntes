# Encapsulamiento

El **encapsulamiento** es uno de los pilares de la programación orientada a objetos. Consiste en **ocultar los detalles internos de una [[001 - Clases en Java|clase]]** y exponer solo lo necesario a través de una interfaz pública. De esta manera, se protege el estado del objeto y se promueve un acceso controlado a sus datos.

## Modificadores de acceso en Java

| Modificador    | Acceso desde...                                  |
|----------------|--------------------------------------------------|
| `public`       | Cualquier clase                                   |
| `private`      | Solo dentro de la misma clase                     |
| `protected`    | Mismo paquete y subclases (incluso fuera del paquete) |
| *default* (sin modificador) | Solo dentro del mismo paquete         |
## Setters y Getters

Los **getters** y **setters** son métodos que permiten acceder y modificar los atributos privados de una clase, siguiendo el principio de encapsulamiento.

### Ejemplo:

```java
public class Persona {
    private String nombre;

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }
}
````

> Esto permite cambiar la lógica interna (por ejemplo, agregar validaciones en el `setNombre`) sin afectar a quienes usan la clase.

# Herencia

La **herencia** es otro pilar de la programación orientada a objetos. Permite que una clase (subclase) herede atributos y métodos de otra clase (superclase), reutilizando código y promoviendo una estructura jerárquica.

## Características clave

- Una subclase hereda todos los métodos y atributos **no privados** de su superclase.    
- Puede sobrescribir métodos mediante `@Override`.    
- Puede añadir nuevos métodos y atributos propios.    
- En Java, solo se puede extender una clase a la vez (**herencia simple**).    

## Ejemplo:

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

> En este caso, `Perro` hereda el atributo `nombre` y el método `comer`, y añade su propio método `ladrar`.

