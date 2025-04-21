# Manejo de Excepciones  

En Java, el manejo de excepciones permite controlar errores para que el programa pueda continuar su ejecución, incluso cuando ocurre una excepción. Para esto, se utiliza la estructura `try-catch-finally`.  

## Estructura `try-catch-finally`  

- **`try`**: Contiene el código que puede generar una excepción. Java intentará ejecutar este bloque y capturar cualquier excepción que ocurra.  
- **`catch`**: Define el tratamiento del problema en caso de que se capture una excepción. Aquí se especifica el tipo de excepción a manejar.  
- **`finally`**: Contiene instrucciones que se ejecutarán siempre, independientemente de si se capturó o no una excepción. Es útil para liberar recursos como cerrar archivos o conexiones de base de datos.  

### Ejemplo:  

```java
try {
    // Código que puede lanzar una excepción
    int resultado = 10 / 0;
} catch (ArithmeticException e) {
    // Manejo de la excepción
    System.out.println("Error: División por cero.");
} finally {
    // Código que siempre se ejecuta
    System.out.println("Bloque finally ejecutado.");
}
````

## `throw`

El operador **`throw`** permite lanzar manualmente una excepción. Debe estar seguido del operador `new` y el tipo de excepción que se desea lanzar.

### Ejemplo:

```java
public void verificarEdad(int edad) {
    if (edad < 18) {
        throw new IllegalArgumentException("La edad debe ser mayor o igual a 18.");
    }
    System.out.println("Edad válida.");
}
```
