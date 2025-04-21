## **Variables y Tipos de Datos**

### **Definición de una variable**

Una **variable** es una posición de memoria que se reserva para almacenar un dato que puede cambiar a lo largo del tiempo. Para poder utilizar una variable, debe ser **declarada** previamente con un tipo de dato específico.

### **Tipos de datos**

Los tipos de datos definen qué tipo de valor puede almacenar una variable y los límites de tamaño a tener en cuenta. En [[001 - ¿Qué es Java?|Java]], existen **tipos de datos primitivos** y **clases** que actúan como tipos de datos.

#### **Tipos numéricos**

- `short`: Entero de 2 bytes.
- `int`: Entero de 4 bytes.
- `long`: Entero de 8 bytes.
- `float`: Número con punto flotante de 4 bytes.
- `double`: Número con punto flotante de 8 bytes.

#### **Tipos de caracteres**

- `char`: Caracter único de 2 bytes.
- `String`: Cadena de caracteres (no es primitivo, es una clase).

#### **Otros tipos**

- `boolean`: Valor lógico (2 bytes).
- `void`: Tipo de dato nulo, usado en funciones que no retornan valor.

### **Declaración de una variable**

La sintaxis para declarar una variable es la siguiente:

```java
tipoDeDato nombreVariable;
```

Ejemplo:

```java
int edad;
String nombre;
```

## **Reglas para nombrar variables**

Las variables deben seguir ciertas reglas para ser nombradas correctamente:

- No puede comenzar con un número.
- No puede contener caracteres especiales (excepto `_` o `$`).
- No puede tener espacios en blanco.
- No puede ser igual a una palabra reservada del lenguaje (como `int`, `for`, `class`, etc.).