# Manejo de Excepciones en Java

En Java, el manejo de excepciones permite controlar errores durante la ejecución de un programa, evitando su terminación abrupta. Esto se logra mediante la estructura `try-catch-finally` y el uso del operador `throw`.

---

## Estructura `try-catch-finally`

### Componentes:

- **`try`**: Bloque que contiene el código susceptible a lanzar excepciones.
- **`catch`**: Captura y maneja la excepción lanzada desde el bloque `try`. Se puede usar múltiples bloques `catch` para manejar diferentes tipos de excepciones.
- **`finally`**: Contiene código que **siempre se ejecuta**, sin importar si se lanzó una excepción o no. Útil para cerrar recursos (archivos, conexiones, etc.).

### Ejemplo:

```java
try {
    int resultado = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: División por cero.");
} finally {
    System.out.println("Bloque finally ejecutado.");
}
````

---

## `throw`

El operador **`throw`** se utiliza para lanzar manualmente una excepción. Es útil cuando queremos forzar que se cumpla una condición.

### Ejemplo:

```java
public void verificarEdad(int edad) {
    if (edad < 18) {
        throw new IllegalArgumentException("La edad debe ser mayor o igual a 18.");
    }
    System.out.println("Edad válida.");
}
```

> ⚠️ Solo se puede lanzar **una excepción a la vez** con `throw`.

---

## `throws`

La palabra clave **`throws`** se utiliza en la **firma de un método** para indicar que este podría lanzar una o varias excepciones. Es obligatoria en el caso de excepciones chequeadas.

### Ejemplo:

```java
public void leerArchivo(String ruta) throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader(ruta));
}
```

> ✅ Puedes declarar múltiples excepciones separadas por comas:  
> `throws IOException, SQLException`
