# String interpolation en Angular

**String interpolation** es una técnica utilizada en Angular para enviar datos desde el componente hacia la vista. Utilizando el doble símbolo de llaves `{{ }}`, también conocidos como brackets, puedes mostrar el valor de una variable, realizar operaciones matemáticas, o llamar a una función directamente dentro del código HTML.

### Ejemplos de Interpolación

```html
<h2>{{ 'Hola Platzi' }}</h2>
<h3>1 + 1 = {{ 1 + 1 }}</h3>
<h4>{{ myFunction() }}</h4>
```

- **Mostrar texto:** En el primer ejemplo, la cadena de texto `'Hola Platzi'` se muestra directamente en la vista.
  
- **Operaciones matemáticas:** En el segundo ejemplo, la expresión matemática `1 + 1` se evalúa y el resultado (`2`) se muestra en la vista.

- **Llamada a funciones:** En el tercer ejemplo, se llama a `myFunction()` desde el componente. Es importante que la función retorne un valor para que se muestre en la vista.

### Consideraciones

- La interpolación de cadenas se utiliza principalmente para mostrar datos dinámicos que provienen del componente.

- Es importante recordar que las funciones utilizadas dentro de la interpolación deben ser rápidas de ejecutar, ya que se evaluarán cada vez que Angular detecte cambios en el modelo de datos.

- Para mostrar contenido HTML o valores complejos, considera el uso de enlaces de propiedad o directivas adicionales para mejorar la eficiencia y seguridad de la aplicación.
