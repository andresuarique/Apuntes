# Clases Utilitarias en Java

Las **clases utilitarias** en Java son [[001 - Clases en Java|clases]] que agrupan métodos estáticos para realizar tareas comunes sin necesidad de crear instancias. Su propósito es mejorar la reutilización del código y centralizar lógica de apoyo en un solo lugar.

## Características

- **Métodos estáticos (`static`)**: No requieren instanciar la clase para utilizarlos.
- **Sin estado interno**: No almacenan atributos que cambien durante la ejecución.
- **Final (opcional)**: A veces se declaran como `final` para evitar herencia.
- **Constructores privados**: Para impedir la creación de instancias (opcional pero recomendado).

## Ejemplo clásico: `java.lang.Math`

```java
int mayor = Math.max(10, 20);    // Devuelve 20
double raiz = Math.sqrt(25);     // Devuelve 5.0
double potencia = Math.pow(2, 3); // Devuelve 8.0
````

## Otras clases utilitarias comunes en Java

|Clase|Función Principal|
|---|---|
|`java.util.Arrays`|Métodos para manipular arrays|
|`java.util.Collections`|Métodos para manipular colecciones (`List`, `Set`, etc.)|
|`java.util.Objects`|Métodos para validación de objetos (`requireNonNull`, `equals`, etc.)|
|`java.nio.file.Files`|Operaciones con archivos y directorios|
|`java.time.LocalDate` y `java.time.format.DateTimeFormatter`|Manipulación de fechas y horas|

## Crear una Clase Utilitaria Propia

```java
public final class StringUtil {

    // Constructor privado para evitar instanciación
    private StringUtil() {}

    public static boolean esVacia(String texto) {
        return texto == null || texto.trim().isEmpty();
    }

    public static String capitalizar(String texto) {
        if (esVacia(texto)) return texto;
        return texto.substring(0, 1).toUpperCase() + texto.substring(1).toLowerCase();
    }
}
```

### Uso:

```java
String nombre = "java";
System.out.println(StringUtil.capitalizar(nombre));  // Imprime: Java
```
