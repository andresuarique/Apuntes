## Programación Funcional

La **programación funcional** es un paradigma que se centra en la evaluación de expresiones y funciones matemáticas en lugar de modificar el estado del programa o ejecutar instrucciones imperativas.

### Características principales:

1. **Funciones puras**:
    
    - Siempre producen el mismo resultado para los mismos argumentos de entrada.
    - No tienen efectos secundarios en el estado del programa.
2. **Inmutabilidad**:
    
    - Una vez que se crea un objeto, su estado no puede ser modificado.
3. **Composición de funciones**:
    
    - Permite combinar funciones pequeñas para crear operaciones más complejas.
4. **Ausencia de estado mutable**:
    
    - Reduce los errores derivados del cambio de estado.

---

## Lambdas y Streams

### Expresiones Lambda

Una **lambda** es una forma concisa de definir una función anónima y pasarla como argumento a otro método o función.

#### Sintaxis básica:

```java
(parametros) -> { cuerpo }
```

- Los **parámetros** son los valores que recibe la función.
- El **cuerpo** define lo que la función debe hacer.
- Si el cuerpo tiene una única instrucción, las llaves (`{}`) son opcionales.

#### Ejemplo de uso:

```java
public class LambdaExample {
    public static void main(String[] args) {
        // Expresión lambda que suma dos números
        Calculadora suma = (a, b) -> a + b;
        System.out.println("Resultado: " + suma.operacion(5, 3));
    }

    interface Calculadora {
        int operacion(int a, int b);
    }
}
```

### Referencias a Métodos

Permiten utilizar un método como una expresión lambda. Se usa el operador `::`.

Tipos de referencias a métodos:

1. **Métodos estáticos**:
    
    ```java
    Clase::metodoEstatico
    ```
    
2. **Métodos de instancia**:
    
    ```java
    objeto::metodoDeInstancia
    ```
    
3. **Constructores**:
    
    ```java
    Clase::new
    ```
    

#### Ejemplo de referencia a método:

```java
import java.util.function.Consumer;

public class MethodReferenceExample {
    public static void main(String[] args) {
        Consumer<String> imprimir = System.out::println;
        imprimir.accept("Hola desde una referencia a método");
    }
}
```

---

### API Stream

La **API Stream** permite procesar colecciones de datos de forma más sencilla y eficiente, facilitando operaciones como filtrar, mapear, ordenar y reducir.

#### Características principales:

1. **Inmutabilidad**:
    - Los streams no modifican las colecciones originales; generan nuevos resultados.
2. **Operaciones declarativas**:
    - Expresan _qué_ se quiere hacer, no _cómo_.
3. **Encadenamiento**:
    - Permiten combinar varias operaciones en una sola línea de código.

#### Operaciones comunes:

- **Intermedias**: Transforman o filtran los datos (devuelven un nuevo stream).
    - `filter()`: Filtra elementos según una condición.
    - `map()`: Transforma cada elemento del stream.
    - `sorted()`: Ordena los elementos.
- **Terminales**: Producen un resultado o efecto final (devuelven un valor o colecciones).
    - `forEach()`: Itera sobre cada elemento.
    - `collect()`: Convierte el resultado a una colección.
    - `reduce()`: Combina los elementos en un único valor.

#### Ejemplo de uso:

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<String> nombres = Arrays.asList("Ana", "Luis", "Pedro", "Juan");

        // Filtrar nombres que empiezan con "P" y convertirlos a mayúsculas
        List<String> resultado = nombres.stream()
                                        .filter(nombre -> nombre.startsWith("P"))
                                        .map(String::toUpperCase)
                                        .collect(Collectors.toList());

        System.out.println(resultado); // [PEDRO]
    }
}
```
