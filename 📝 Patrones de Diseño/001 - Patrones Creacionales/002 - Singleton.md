# Singleton
El patrón Singleton es un [[001 - Patrones de Diseño|patrón]] creacional que asegura que una clase tenga una única instancia y proporciona un punto de acceso global a ella. Este patrón es útil cuando se necesita controlar el acceso a recursos compartidos, como configuraciones, conexiones a bases de datos o registros de logging.

## Concepto
El patrón Singleton restringe la instanciación de una clase a un único objeto. Esto es especialmente importante en situaciones donde es necesario garantizar que solo exista una instancia, como en la gestión de recursos.

## Implementación en Java

### Ejemplo

```java
// Clase Singleton
public class Singleton {
    // Instancia privada y estática
    private static Singleton instancia;

    // Constructor privado para evitar instanciación externa
    private Singleton() {}

    // Método público para obtener la instancia
    public static Singleton getInstancia() {
        if (instancia == null) {
            instancia = new Singleton();
        }
        return instancia;
    }

    public void mostrarMensaje() {
        System.out.println("Soy una instancia única de Singleton.");
    }
}

// Uso del Singleton
public class Main {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstancia();
        singleton1.mostrarMensaje(); // Salida: Soy una instancia única de Singleton.

        Singleton singleton2 = Singleton.getInstancia();
        System.out.println(singleton1 == singleton2); // Salida: true
    }
}
```

## Ventajas
- **Control de acceso**: Garantiza que solo haya una instancia de la clase.
- **Facilidad de uso**: Proporciona un punto de acceso global, simplificando el uso de la instancia.
- **Ahorro de recursos**: Evita la creación innecesaria de objetos.

## Desventajas
- **Dificultad en las pruebas**: Puede complicar las pruebas unitarias debido a su naturaleza global.
- **Uso indebido**: Si no se usa con cuidado, puede convertirse en un anti-patrón al promover un diseño rígido.

## Conclusión
El patrón Singleton es útil en situaciones donde se requiere una única instancia de una clase. Sin embargo, es importante emplearlo con precaución para evitar problemas en la mantenibilidad y la escalabilidad del código.