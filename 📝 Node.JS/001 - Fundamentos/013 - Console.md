# Console

En Node.js, `console` es un objeto [global](011%20-%20Globals.md) que nos permite imprimir todo tipo de valores en la terminal. Es una herramienta fundamental para la depuración y el seguimiento de la ejecución de programas. A continuación se describen los métodos más comunes del objeto `console`:

## Métodos de `console`

- **`console.log`**: Recibe cualquier tipo de dato y lo muestra en la consola.
  ```javascript
  console.log("Mensaje informativo");
  ```

- **`console.info`**: Es equivalente a `log` pero se usa principalmente para informar.
  ```javascript
  console.info("Mensaje de información");
  ```

- **`console.error`**: Es equivalente a `log` pero se usa para mostrar errores.
  ```javascript
  console.error("Mensaje de error");
  ```

- **`console.warn`**: Es equivalente a `log` pero se usa para mostrar advertencias.
  ```javascript
  console.warn("Mensaje de advertencia");
  ```

- **`console.table`**: Muestra una tabla a partir de un objeto.
  ```javascript
  const usuarios = [
      { nombre: "Alice", edad: 25 },
      { nombre: "Bob", edad: 30 }
  ];
  console.table(usuarios);
  ```

- **`console.count`**: Inicia un contador autoincremental.
  ```javascript
  console.count("contador");
  console.count("contador");
  ```

- **`console.countReset`**: Reinicia el contador a 0.
  ```javascript
  console.countReset("contador");
  console.count("contador");
  ```

- **`console.time`**: Inicia un cronómetro en milisegundos.
  ```javascript
  console.time("cronometro");
  ```

- **`console.timeEnd`**: Finaliza el cronómetro iniciado con `console.time`.
  ```javascript
  console.timeEnd("cronometro");
  ```

- **`console.group`**: Permite agrupar mensajes mediante indentación.
  ```javascript
  console.group("grupo");
  console.log("Mensaje dentro del grupo");
  ```

- **`console.groupEnd`**: Finaliza la agrupación iniciada con `console.group`.
  ```javascript
  console.groupEnd("grupo");
  ```

- **`console.clear`**: Limpia la consola.
  ```javascript
  console.clear();
  ```

