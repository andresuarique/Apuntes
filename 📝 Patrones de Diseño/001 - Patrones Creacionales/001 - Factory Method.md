# Factory Method
El patrón Factory Method es un patrón creacional que proporciona una interfaz para crear objetos en una superclase, pero permite que las subclases decidan qué clase instanciar. Este patrón ayuda a delegar la responsabilidad de creación de objetos, promoviendo la flexibilidad y la extensibilidad del código.

## Concepto
El patrón Factory Method permite que las clases instanciadas sean determinadas en tiempo de ejecución, lo que facilita el uso de nuevas clases sin modificar el código existente.

## Implementación en Java

### Ejemplo

```java
// Producto
interface Producto {
    void usar();
}

// Implementaciones de Producto
class ProductoA implements Producto {
    public void usar() {
        System.out.println("Usando Producto A");
    }
}

class ProductoB implements Producto {
    public void usar() {
        System.out.println("Usando Producto B");
    }
}

// Creator
abstract class Creator {
    public abstract Producto crearProducto();
}

// Implementaciones de Creator
class CreatorA extends Creator {
    public Producto crearProducto() {
        return new ProductoA();
    }
}

class CreatorB extends Creator {
    public Producto crearProducto() {
        return new ProductoB();
    }
}

// Uso del Factory Method
public class Main {
    public static void main(String[] args) {
        Creator creator = new CreatorA();
        Producto producto = creator.crearProducto();
        producto.usar(); // Salida: Usando Producto A

        creator = new CreatorB();
        producto = creator.crearProducto();
        producto.usar(); // Salida: Usando Producto B
    }
}
```

## Ventajas
- **Desacoplamiento**: Separa la creación de objetos de su uso.
- **Flexibilidad**: Permite agregar nuevas variantes de productos sin modificar el código existente.
- **Reutilización**: Facilita el uso de código común para la creación de objetos.

## Desventajas
- **Complejidad**: Puede aumentar la complejidad del código si se utiliza en exceso.
- **Dificultad de comprensión**: Los nuevos desarrolladores pueden tener problemas para entender la arquitectura si no están familiarizados con el patrón.

## Conclusión
El patrón Factory Method es una herramienta poderosa en el desarrollo de software, especialmente útil en sistemas que requieren una alta flexibilidad y escalabilidad. Su correcta implementación puede mejorar significativamente la calidad y mantenibilidad del código.
