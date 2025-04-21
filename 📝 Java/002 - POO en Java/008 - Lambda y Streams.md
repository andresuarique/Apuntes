## Características Principales de la Programación Funcional:

### 1. **Funciones Puras**

- **Definición**: Una función pura es aquella que siempre devuelve el mismo resultado para los mismos argumentos y no tiene efectos secundarios, lo que significa que no modifica el estado del programa ni interactúa con el mundo exterior (como archivos o bases de datos).    

### 2. **Inmutabilidad**

- **Definición**: Una vez creado un objeto, no se puede cambiar. Esto reduce la posibilidad de errores derivados de la modificación inesperada del estado de un objeto.    

### 3. **Composición de Funciones**

- Permite combinar funciones pequeñas y reutilizables para formar funciones más complejas. Esto se logra usando herramientas como **lambdas** y **streams**.    

### 4. **Ausencia de Estado Mutable**

- Se evita modificar el estado a lo largo del programa, lo que facilita la depuración y mejora la confiabilidad del código.    
## Lambdas y Streams

### **Expresiones Lambda**

Las expresiones lambda permiten definir funciones anónimas (sin nombre) y pasarlas como parámetros. Son una característica clave de la programación funcional en Java.

#### Sintaxis básica:

```java
(parametros) -> { cuerpo }
```

- **Parámetros**: Los valores que se pasan a la función lambda.    
- **Cuerpo**: El bloque de código que realiza la operación.    

#### Ejemplo:

```java
public class LambdaExample {
    public static void main(String[] args) {
        // Lambda que suma dos números
        Calculadora suma = (a, b) -> a + b;
        System.out.println("Resultado: " + suma.operacion(5, 3));
    }

    interface Calculadora {
        int operacion(int a, int b);
    }
}
```

### **Referencias a Métodos**

Las referencias a métodos permiten utilizar un método existente como una expresión lambda.

#### Tipos de referencias a métodos:

1. **Métodos estáticos**: Se referencia a un método estático de una clase.    
    ```java
    Clase::metodoEstatico
    ```
   
2. **Métodos de instancia**: Se refiere a un método de instancia de un objeto específico.    
    ```java
    objeto::metodoDeInstancia
    ```

3. **Constructores**: Se puede utilizar el constructor de una clase como referencia a un método.

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

### **API Stream**

La API Stream es una poderosa herramienta para trabajar con colecciones de manera más declarativa y eficiente. Permite realizar operaciones complejas como filtrado, mapeo, y reducción sin modificar la colección original.

#### Características principales de los Streams:

1. **Inmutabilidad**: Los streams no modifican la colección original; devuelven nuevos streams con los resultados transformados.    
2. **Operaciones Declarativas**: Se especifica lo que se quiere hacer (por ejemplo, filtrar, mapear) sin tener que preocuparse de cómo se realiza.    
3. **Encadenamiento**: Se pueden combinar múltiples operaciones en una sola línea.    

#### Operaciones Comunes:

- **Intermedias**: Devuelven un nuevo stream y permiten transformar o filtrar los datos.    
    - `filter()`: Filtra elementos basados en una condición.        
    - `map()`: Transforma cada elemento del stream.        
    - `sorted()`: Ordena los elementos.        
- **Terminales**: Producen un resultado final.    
    - `forEach()`: Realiza una acción para cada elemento.        
    - `collect()`: Convierte el resultado en una colección.        
    - `reduce()`: Combina los elementos en un solo valor.        

#### Ejemplo de uso con Streams:

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

### **Ventajas de la Programación Funcional**:

- **Reducción de errores**: Al evitar el estado mutable y los efectos secundarios, los programas son más fáciles de entender y depurar.    
- **Mayor legibilidad**: Las expresiones lambda y la API Stream permiten escribir código más limpio y conciso.    
- **Reutilización**: Las funciones pequeñas y las referencias a métodos pueden reutilizarse en diferentes contextos.    