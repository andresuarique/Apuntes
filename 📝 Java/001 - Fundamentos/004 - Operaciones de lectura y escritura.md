## **Operaciones de lectura y escritura**

### **Escritura en consola**

En [Java](001%20-%20¿Qué%20es%20Java?), para imprimir información en la consola, se utiliza `System.out.println()`:

```java
System.out.println("Hola");
```

### **Lectura de datos desde la consola**

Para leer datos desde la consola, puedes usar la clase `Scanner`:

```java
Scanner teclado = new Scanner(System.in);
int numero = teclado.nextInt();
```

Esto lee un número entero desde la entrada estándar (teclado).
