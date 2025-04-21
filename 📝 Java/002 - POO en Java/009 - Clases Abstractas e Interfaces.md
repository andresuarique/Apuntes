## Clases Abstractas y Interfaces en Java

Las **clases abstractas** y **interfaces** son dos conceptos fundamentales en la programación orientada a objetos en Java. Aunque ambos permiten definir contratos para las clases que los implementan o heredan, tienen características y comportamientos distintos. A continuación, detallo las diferencias y ejemplos para ilustrar cómo se usan en la práctica.
## **Clases Abstractas**

Una **clase abstracta** es una [[001 - Clases en Java|clase]] que no puede ser instanciada directamente. Se utiliza como una clase base para otras clases. Puede contener tanto métodos abstractos (sin implementación) como métodos concretos (con implementación). Las clases hijas deben implementar los métodos abstractos a menos que también sean abstractas.

### **Características principales:**

- **Métodos abstractos**: Son métodos que no tienen implementación en la clase abstracta, y deben ser implementados por las clases hijas.    
- **Métodos concretos**: Métodos con implementación en la clase abstracta. Las clases hijas pueden usar estos métodos o sobrescribirlos.    
- **No se pueden instanciar**: No se puede crear un objeto de una clase abstracta directamente.    
- **Herencia**: Las clases hijas heredan de la clase abstracta y pueden acceder a los métodos concretos y deben implementar los métodos abstractos.    

### **Ejemplo de clase abstracta:**

```java
// Clase abstracta
abstract class Animal {
    String nombre;

    public Animal(String nombre) {
        this.nombre = nombre;
    }

    // Método abstracto
    public abstract void hacerSonido();

    // Método concreto
    public void dormir() {
        System.out.println(nombre + " está durmiendo.");
    }
}

// Clase hija
class Perro extends Animal {
    public Perro(String nombre) {
        super(nombre);
    }

    @Override
    public void hacerSonido() {
        System.out.println("Guau Guau");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal perro = new Perro("Fido");
        perro.hacerSonido();
        perro.dormir();
    }
}
```

### **Explicación**:

- La clase `Animal` es abstracta y tiene un método abstracto `hacerSonido()` que debe ser implementado por las clases hijas.    
- La clase `Perro` extiende `Animal` e implementa el método `hacerSonido()`.    
- Aunque `Animal` tiene un método concreto `dormir()`, las clases hijas pueden usarlo tal cual o sobreescribirlo.    
## **Interfaces**

Una **interfaz** en Java define un conjunto de métodos abstractos (en Java 8 y versiones posteriores, puede incluir métodos predeterminados y estáticos con implementación). Es una forma de definir un contrato que las clases deben cumplir. Las interfaces no pueden ser instanciadas directamente, y una clase puede implementar varias interfaces.

### **Características principales:**

- **Métodos abstractos**: A partir de Java 8, las interfaces pueden contener métodos con implementación (predeterminados y estáticos).    
- **Métodos predeterminados y estáticos**: A partir de Java 8, las interfaces pueden tener métodos con implementación mediante la palabra clave `default` o `static`.    
- **No pueden ser instanciadas**: No se puede crear un objeto de una interfaz directamente.    
- **Herencia múltiple**: Una clase puede implementar varias interfaces.    
- **Solo atributos constantes**: Las interfaces solo pueden contener variables `static final`.    

### **Diferencias clave con las clases abstractas**:

|**Característica**|**Clases Abstractas**|**Interfaces**|
|---|---|---|
|**Métodos concretos**|Pueden tener métodos concretos con implementación|Solo métodos abstractos (excepto predeterminados y estáticos en Java 8).|
|**Herencia**|Solo pueden extender de una clase abstracta|Pueden implementar varias interfaces.|
|**Atributos**|Pueden tener atributos normales|Solo atributos constantes (`static final`).|
|**Instanciación**|No pueden ser instanciadas|No pueden ser instanciadas.|

### **Ejemplo de interfaz:**

```java
// Interfaz
interface Volador {
    void volar();
}

// Clase que implementa la interfaz
class Pajaro implements Volador {
    @Override
    public void volar() {
        System.out.println("El pájaro está volando.");
    }
}

// Clase que implementa varias interfaces
interface Nadador {
    void nadar();
}

class Pato implements Volador, Nadador {
    @Override
    public void volar() {
        System.out.println("El pato vuela ocasionalmente.");
    }

    @Override
    public void nadar() {
        System.out.println("El pato nada en el lago.");
    }
}

public class Main {
    public static void main(String[] args) {
        Pajaro pajaro = new Pajaro();
        pajaro.volar();

        Pato pato = new Pato();
        pato.volar();
        pato.nadar();
    }
}
```

### **Explicación**:

- La interfaz `Volador` define un contrato con el método `volar()`, que debe ser implementado por cualquier clase que la implemente.    
- La clase `Pajaro` implementa `Volador` y proporciona una implementación del método `volar()`.    
- La clase `Pato` implementa tanto `Volador` como `Nadador`, por lo que debe implementar ambos métodos (`volar()` y `nadar()`).    
## **Cuándo usar una clase abstracta y cuándo usar una interfaz:**

- **Usa una clase abstracta** cuando:    
    - Quieras proporcionar implementación común para las clases hijas.        
    - Necesites definir atributos y métodos concretos además de los abstractos.        
    - La herencia simple es suficiente (solo una clase hija).        
- **Usa una interfaz** cuando:    
    - Quieras que las clases puedan heredar múltiples comportamientos.        
    - No necesites proporcionar implementación, solo un contrato de métodos.        
    - Estés definiendo una relación de "capacidad" (por ejemplo, `Volador`, `Nadador`) que no necesariamente tiene que estar vinculada a una jerarquía de clases.        
