## Clases Wrapper

Las **clases wrapper** son clases que actúan como un envoltorio para los tipos de datos primitivos, permitiendo tratarlos como objetos.

### Características:

- Representan un dato primitivo en forma de objeto.
- **Anidan** un valor primitivo, proporcionando métodos adicionales para manipularlo.
- **Proveen métodos de conversión** entre tipos compatibles (por ejemplo, de `String` a primitivo).
- Incluyen métodos para **validación y manipulación**.
- Son equivalentes a un tipo de referencia o clase, pero relacionadas con un primitivo específico.
- Cada tipo primitivo tiene una clase `Wrapper` equivalente.

### Ejemplos de equivalencias:

|Primitivo|Clase Wrapper|
|---|---|
|`int`|`Integer`|
|`double`|`Double`|
|`char`|`Character`|
|`boolean`|`Boolean`|

### Ejemplo de uso:

```java
public class WrapperExample {
    public static void main(String[] args) {
        Integer numero = Integer.valueOf(10); // Convierte un valor primitivo a objeto
        int valor = numero.intValue();       // Convierte un objeto wrapper a primitivo

        System.out.println("Número: " + numero);
        System.out.println("Valor primitivo: " + valor);
    }
}
```

---

## Generics

Los **genéricos** son una característica de Java que permite definir clases, interfaces y métodos que operan sobre un tipo específico que se proporciona como parámetro.

### Características:

- Permiten tratar objetos de manera homogénea, sin conocer su tipo concreto en tiempo de compilación.
- El término **genéricos** hace referencia a **tipos parametrizados**, es decir, el tipo de dato se especifica como un parámetro.
- Al definir una clase o interfaz genérica, se crea una plantilla para generar clases e interfaces específicas en el futuro.
- Mejoran la **seguridad de tipos** y evitan la necesidad de realizar conversiones explícitas.

### Ventajas:

- **Seguridad en tiempo de compilación**: Previenen errores de tipo.
- **Reutilización de código**: Permiten usar la misma clase o método con diferentes tipos.

### Sintaxis básica:

```java
public class ClaseGenerica<T> {
    private T dato;

    public ClaseGenerica(T dato) {
        this.dato = dato;
    }

    public T getDato() {
        return dato;
    }

    public void setDato(T dato) {
        this.dato = dato;
    }
}
```

### Ejemplo de uso:

```java
public class GenericsExample {
    public static void main(String[] args) {
        ClaseGenerica<Integer> objInt = new ClaseGenerica<>(100);
        System.out.println("Dato: " + objInt.getDato());

        ClaseGenerica<String> objStr = new ClaseGenerica<>("Hola");
        System.out.println("Dato: " + objStr.getDato());
    }
}
```

### Uso en colecciones:

Los genéricos se utilizan ampliamente en las colecciones de Java:

```java
import java.util.ArrayList;

public class GenericsCollectionExample {
    public static void main(String[] args) {
        ArrayList<String> lista = new ArrayList<>();
        lista.add("Elemento 1");
        lista.add("Elemento 2");

        for (String elemento : lista) {
            System.out.println(elemento);
        }
    }
}
```
