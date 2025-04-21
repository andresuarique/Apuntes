# Excepciones  

En Java, una **excepción** es un evento que interrumpe el flujo normal de un programa cuando ocurre un error. Las excepciones se dividen en diferentes tipos según su origen y manejo.  

## Tipos de Excepciones  

### 1. Excepciones Chequeadas  
Estas excepciones derivan de la clase `Exception` y deben ser manejadas o declaradas obligatoriamente. Requieren el uso del bloque `try-catch` o la declaración en la firma del método con `throws`.  

Ejemplos:  
- `FileNotFoundException`  
- `IOException`  

### 2. Excepciones No Chequeadas  
Derivan de la clase `RuntimeException`. No necesitan ser manejadas o declaradas explícitamente, ya que no requieren el uso obligatorio de `try-catch`.  

Ejemplos:  
- `NullPointerException`  
- `ArrayIndexOutOfBoundsException`  
- `IllegalArgumentException`  

### 3. Errores  
Los errores derivan de la clase `Error` y son generados por la JVM. Representan problemas graves que no pueden ser solucionados por el programa y generalmente causan su terminación abrupta.  

Ejemplos:  
- `ExceptionInInitializerError`  
- `StackOverflowError`  
- `NoClassDefFoundError`  

## Stack Trace  
El **stack trace** es una lista de las llamadas a métodos realizadas en el momento en que se lanzó la excepción. Muestra desde el método más reciente hasta el más antiguo, proporcionando información detallada sobre el origen y la propagación de la excepción.  

![[Pasted image 20241227082041.png]]