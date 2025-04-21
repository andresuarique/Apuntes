# **Collections en Java**

## **Definición**

- Las **Collections** son estructuras dinámicas que permiten almacenar y manipular conjuntos de objetos o elementos en [Java](001%20-%20¿Qué%20es%20Java?).
- Se implementan mediante la interfaz **Collection**, que define métodos comunes para:
    - Añadir elementos.
    - Eliminar elementos.
    - Obtener el tamaño de la colección.
    - Iterar sobre los elementos.

## **Principales Tipos de Collections**

1. **List**: Almacena elementos en forma de lista ordenada.
2. **Set**: Almacena elementos únicos (sin duplicados).
3. **Queue**: Gestiona elementos en una cola (FIFO o LIFO).
4. **Map**: Asocia claves únicas a valores.
## **List**

- Permite agrupar elementos de forma **ordenada** (uno detrás de otro).
- Los elementos pueden estar duplicados.
- Tipos principales:
    - **ArrayList**.
    - **LinkedList**.
    - **Stack**.

### **ArrayList**

- Representa un **array dinámico**.
- Permite elementos duplicados.
- Acceso rápido a los elementos mediante su índice.
- Opera en un modelo **FIFO** (_First In, First Out_) para inserción y lectura.

**Declaración y Uso:**

```java
List<String> lista = new ArrayList<>();
lista.add("Elemento 1");
lista.add("Elemento 2");
System.out.println(lista.get(0)); // Acceso por índice
```

### **LinkedList**

- Estructura dinámica basada en **listas enlazadas** (doble enlace entre nodos).
- Permite:
    - Elementos duplicados.
    - Insertar al inicio o al final de la lista.
    - Tratarse como lista, pila o cola.

**Declaración y Uso:**

```java
List<String> lista = new LinkedList<>();
lista.add("Elemento 1");
lista.add("Elemento 2");
System.out.println(lista.get(0)); // Acceso por índice
```
## **Map (o Diccionarios)**

- Un **Map** almacena pares de **clave-valor**, donde:
    - Cada **clave** debe ser única.
    - Los valores pueden repetirse.

### **HashMap**

- Implementación más común de `Map`.
- No garantiza el orden de los elementos.

**Declaración y Uso:**

```java
Map<Integer, String> mapa = new HashMap<>();
mapa.put(1, "Valor 1"); // Agregar un par clave-valor
mapa.put(2, "Valor 2");

System.out.println(mapa.get(1)); // Acceso mediante la clave
```
