# Adapter
El patrón Adapter es un [[001 - Patrones de Diseño|patrón]] estructural que permite que dos interfaces incompatibles trabajen juntas. Este patrón actúa como un puente entre las interfaces, adaptando una interfaz existente a la que se espera.

## Concepto
El patrón Adapter es útil cuando se desea reutilizar código existente, pero las interfaces no son compatibles. Proporciona una forma de adaptar la interfaz de una clase a la interfaz que el cliente espera.

## Implementación en Java

### Ejemplo

```java
// Interfaz objetivo
interface Target {
    void realizarOperacion();
}

// Clase que necesita ser adaptada
class Adaptee {
    public void operacionEspecifica() {
        System.out.println("Operación específica de Adaptee.");
    }
}

// Clase Adapter que implementa la interfaz Target
class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void realizarOperacion() {
        adaptee.operacionEspecifica(); // Adaptando la llamada
    }
}

// Uso del Adapter
public class Main {
    public static void main(String[] args) {
        Adaptee adaptee = new Adaptee();
        Target target = new Adapter(adaptee);
        target.realizarOperacion(); // Salida: Operación específica de Adaptee.
    }
}
```

## Ventajas
- **Reutilización de código**: Permite utilizar clases existentes sin modificar su código.
- **Flexibilidad**: Facilita la integración de nuevas clases en sistemas existentes.
- **Desacoplamiento**: Reduce el acoplamiento entre clases al proporcionar una interfaz común.

## Desventajas
- **Complejidad**: Puede añadir un nivel adicional de complejidad al sistema, especialmente si se utilizan múltiples adaptadores.
- **Dificultad de mantenimiento**: Puede ser más difícil de entender y mantener en comparación con un diseño más directo.

## Conclusión
El patrón Adapter es una solución efectiva para problemas de incompatibilidad de interfaces, permitiendo que clases con interfaces diferentes colaboren. Su uso adecuado puede mejorar la flexibilidad y la reutilización del código en aplicaciones de software.