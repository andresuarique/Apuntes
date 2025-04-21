## Clases Abstractas

Una **clase abstracta** es similar a una clase común, pero tiene al menos un método abstracto. Los métodos abstractos son aquellos que no tienen implementación (cuerpo) y están diseñados para ser definidos por las clases hijas.

### Características principales:

- Una clase se convierte en **abstracta** si posee al menos un método abstracto.
- Las clases hijas que heredan de una clase abstracta **deben implementar** los métodos abstractos, a menos que también sean abstractas.
- Aunque tienen constructores, las clases abstractas **no pueden ser instanciadas** directamente.
- Son útiles para agrupar comportamientos comunes y definir una plantilla para otras clases con atributos y métodos compartidos.
- Pueden contener:
    - Métodos concretos (con implementación).
    - Métodos abstractos (sin implementación).
    - Atributos (variables de instancia).
    - Constructores.

### Ejemplo:

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

---

## Interfaces

Una **interfaz** define un conjunto de métodos abstractos y, opcionalmente, atributos constantes. Es una forma de especificar un contrato que otras clases deben cumplir.

### Características principales:

- **Definen métodos abstractos** (a partir de Java 8, también pueden tener métodos predeterminados y estáticos con implementación).
- Las clases que implementan una interfaz deben proporcionar implementaciones para todos sus métodos abstractos.
- **Permiten la herencia múltiple**, ya que una clase puede implementar varias interfaces.
- No pueden ser instanciadas.
- A partir de Java 9, pueden contener métodos privados.

### Diferencias con clases abstractas:

|Característica|Clases Abstractas|Interfaces|
|---|---|---|
|**Métodos concretos**|Pueden tener métodos concretos|Solo métodos abstractos (excepto predeterminados y estáticos desde Java 8).|
|**Herencia**|Una clase puede heredar solo una|Una clase puede implementar varias interfaces.|
|**Atributos**|Pueden tener atributos normales|Solo atributos constantes (`static final`).|
|**Instanciación**|No pueden ser instanciadas|No pueden ser instanciadas.|

### Ejemplo:

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