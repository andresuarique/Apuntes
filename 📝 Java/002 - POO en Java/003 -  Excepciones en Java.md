# Excepciones en Java

En Java, una **excepción** es un evento que interrumpe el flujo normal de ejecución de un programa cuando ocurre un error. Java proporciona un sistema robusto para el manejo de errores a través del mecanismo de excepciones.

## Tipos de Excepciones

### 1. Excepciones Chequeadas (Checked Exceptions)

Estas excepciones extienden directamente la clase `Exception` (excluyendo `RuntimeException`). Deben ser **manejadas obligatoriamente** usando `try-catch` o declaradas en la firma del método con `throws`.

**Ejemplos:**

- `FileNotFoundException`
- `IOException`
- `SQLException`

```java
public void leerArchivo() throws IOException {
    BufferedReader reader = new BufferedReader(new FileReader("archivo.txt"));
}
````

### 2. Excepciones No Chequeadas (Unchecked Exceptions)

Derivan de la clase `RuntimeException`. No es obligatorio manejarlas o declararlas, aunque puede ser recomendable hacerlo para evitar fallos inesperados.

**Ejemplos:**

- `NullPointerException`    
- `ArrayIndexOutOfBoundsException`    
- `IllegalArgumentException`    

```java
public void imprimirLongitud(String texto) {
    System.out.println(texto.length()); // Puede lanzar NullPointerException si texto es null
}
```

### 3. Errores (Errors)

Son situaciones más graves que generalmente no deben ser capturadas por aplicaciones. Derivan de la clase `Error` y suelen ser lanzados por la JVM.

**Ejemplos:**

- `StackOverflowError`    
- `OutOfMemoryError
- `NoClassDefFoundError`    

## Stack Trace

El **stack trace** es un registro que muestra la secuencia de llamadas a métodos que condujeron a la excepción. Es útil para diagnosticar y localizar errores en el código.

```text
java.lang.NullPointerException
    at com.ejemplo.MiClase.metodo(MiClase.java:10)
    at com.ejemplo.Main.main(Main.java:5)
```

Cada línea muestra:

- El tipo de excepción    
- El método donde ocurrió    
- El archivo fuente y el número de línea    

> ![Pasted image 20241227082041](../📎%20ANEXOS/Pasted%20image%2020241227082041.png)
