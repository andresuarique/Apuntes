# **Arrays y Matrices**

## **Arrays**

- Conjunto de datos almacenados de forma **contigua** en memoria bajo un mismo nombre.
- Cada elemento se identifica mediante un **índice**.
- Son **estáticos**, es decir, su tamaño no puede cambiar después de ser inicializado.
- Solo pueden almacenar **un tipo de dato**.

**Declaración:**

```java
tipoDeDato[] nombreArray = new tipoDeDato[tamaño];
```

**Ejemplo:**

```java
int[] numeros = new int[5];
```

## **Vectores**

- Son **arrays unidimensionales** (filas o columnas).
- Cada posición tiene un índice, comenzando en `0`.

**Ejemplo:**

```java
String[] nombres = {"Juan", "María", "Pedro"};
```

## **Matrices**

- Son **arrays bidimensionales** con dos índices:
    - **Filas**.
    - **Columnas**.

**Declaración:**

```java
tipoDeDato[][] nombreMatriz = new tipoDeDato[filas][columnas];
```

**Ejemplo:**

```java
int[][] matriz = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
```

## **Errores de desbordamiento**

- Ocurren cuando intentamos acceder a una posición de un array que **no existe**.
- Ejemplo de error:

```java
int[] numeros = {1, 2, 3};
System.out.println(numeros[3]); // Error: índice fuera de rango
```
