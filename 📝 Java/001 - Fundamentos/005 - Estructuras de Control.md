# **Estructuras de Control**
A continuación se definen las estructuras de control en [[001 - ¿Qué es Java?|Java]]:

## **Estructuras Selectivas**

Permiten tomar decisiones en el flujo del programa basadas en condiciones.

### **`if`**

- Evalúa una condición y ejecuta un bloque de código si esta es verdadera.

```java
if (condición) {
    // Bloque de código si la condición es verdadera
}
```

### **`else`**

- Extiende la estructura `if`. Permite ejecutar un bloque alternativo si la condición es falsa.

```java
if (condición) {
    // Bloque de código si la condición es verdadera
} else {
    // Bloque de código si la condición es falsa
}
```

### **`switch`**

- Permite múltiples caminos posibles basados en el valor de una expresión. Cada caso comienza con la palabra clave `case` y finaliza con `break`. Si ningún caso coincide, se ejecuta el bloque `default`.

```java
switch (expresión) {
    case valor1:
        // Código para valor1
        break;
    case valor2:
        // Código para valor2
        break;
    default:
        // Código si no coincide ningún caso
        break;
}
```

## **Estructuras Repetitivas**

Permiten ejecutar un bloque de código varias veces. Cada repetición se conoce como **bucle**. Los bucles pueden controlarse mediante contadores, condiciones o banderas.

### **`do-while`**

- Evalúa la condición al **final** del bloque, lo que garantiza que el código se ejecute **al menos una vez**.

```java
do {
    // Código a ejecutar
} while (condición);
```

### **`while`**

- Evalúa la condición al **principio** del bloque, por lo que el código solo se ejecuta si la condición es verdadera.

```java
while (condición) {
    // Código a ejecutar
}
```

### **`for`**

- Bucle controlado por un contador. Tiene una variable contadora propia que gestiona el número de repeticiones. Su sintaxis incluye:
    - Inicialización del contador.
    - Condición de terminación.
    - Incremento o decremento del contador.

```java
for (int i = 0; i < límite; i++) {
    // Código a ejecutar
}
```



