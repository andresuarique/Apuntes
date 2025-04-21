# Clases Wrapper

Las **[clases](001%20-%20Clases%20en%20Java.md) wrapper** en Java sirven para envolver tipos de datos primitivos y tratarlos como [objetos](002%20-%20Objetos%20en%20Java.md). Esto es útil en situaciones en las que se necesitan características de los objetos, como cuando se almacenan en colecciones que solo aceptan objetos o cuando se necesitan funciones adicionales como la conversión y la validación.

## Características:

- Permiten tratar valores primitivos como objetos.    
- Proveen métodos para convertir entre tipos primitivos y objetos.    
- Ofrecen métodos adicionales para manipular y validar los valores encapsulados.    
- Son equivalentes a tipos de referencia, pero con un vínculo directo a tipos primitivos.    

## Ejemplos de equivalencias entre tipos primitivos y sus wrappers:

|**Primitivo**|**Clase Wrapper**|
|---|---|
|`int`|`Integer`|
|`double`|`Double`|
|`char`|`Character`|
|`boolean`|`Boolean`|

## Ejemplo de uso de clases wrapper:

```java
public class WrapperExample {
    public static void main(String[] args) {
        Integer numero = Integer.valueOf(10);  // Convierte un primitivo a objeto
        int valor = numero.intValue();         // Convierte el objeto wrapper a primitivo

        System.out.println("Número: " + numero);       // Output: Número: 10
        System.out.println("Valor primitivo: " + valor); // Output: Valor primitivo: 10
    }
}
```

# Generics

Los **genéricos** en Java permiten definir clases, interfaces y métodos que funcionan con diferentes tipos de datos sin comprometer la seguridad de tipos en tiempo de compilación. Usando genéricos, se pueden crear componentes reutilizables que acepten distintos tipos de datos sin perder la flexibilidad.
## Características:

- Permiten crear clases y métodos que operan sobre un **tipo de dato parametrizado**.    
- Aumentan la **seguridad de tipos** al evitar la necesidad de casting y el riesgo de errores en tiempo de ejecución.    
- Fomentan la **reutilización de código** con tipos genéricos, facilitando la creación de componentes de propósito general.    

## Sintaxis básica de generics:

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

## Ejemplo de uso con genéricos:

```java
public class GenericsExample {
    public static void main(String[] args) {
        // Usando un genérico para Integer
        ClaseGenerica<Integer> objInt = new ClaseGenerica<>(100);
        System.out.println("Dato: " + objInt.getDato());  // Output: Dato: 100

        // Usando un genérico para String
        ClaseGenerica<String> objStr = new ClaseGenerica<>("Hola");
        System.out.println("Dato: " + objStr.getDato());  // Output: Dato: Hola
    }
}
```

## Uso de genéricos en colecciones

Las colecciones en Java utilizan genéricos para garantizar que los elementos que contienen sean del tipo especificado. Esto ayuda a evitar errores de tipo al agregar o recuperar elementos.

```java
import java.util.ArrayList;

public class GenericsCollectionExample {
    public static void main(String[] args) {
        ArrayList<String> lista = new ArrayList<>();
        lista.add("Elemento 1");
        lista.add("Elemento 2");

        // Iteración con seguridad de tipos
        for (String elemento : lista) {
            System.out.println(elemento);  // Output: Elemento 1, Elemento 2
        }
    }
}
```

**Ventajas de los generics:**

- **Seguridad de tipos**: El compilador verifica el tipo de los datos, evitando errores en tiempo de ejecución.    
- **Reutilización**: El código es más flexible y reutilizable al aceptar diferentes tipos de datos sin modificar su implementación.