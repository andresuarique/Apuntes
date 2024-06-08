# Globals en Node.js

## ¿Qué son los Globals?

En Node.js, los globals son objetos y funciones que están disponibles en todo el entorno de ejecución de Node.js sin necesidad de importarlos o requerirlos explícitamente. Estos objetos globales pueden ser utilizados en cualquier parte de la aplicación.

## Objetos y Funciones Globales Comunes

1. **`global`**:
   - Es el objeto global en Node.js, similar a `window` en los navegadores web.
   - Todas las variables globales definidas en el contexto de Node.js se adjuntan a este objeto.

    ```javascript
    global.miVariableGlobal = "Hola, Mundo";
    console.log(global.miVariableGlobal); // Salida: Hola, Mundo
    ```

2. **`process`**:
   - Proporciona información y control sobre el proceso de Node.js en ejecución.
   - Permite acceder a los argumentos de la línea de comandos, salir del proceso, trabajar con stdin y stdout, entre otros.

    ```javascript
    console.log(`Argumentos de la línea de comandos: ${process.argv}`);
    console.log(`ID del proceso: ${process.pid}`);
    console.log(`Directorio de trabajo actual: ${process.cwd()}`);
    ```

3. **`__dirname`**:
   - Contiene la ruta absoluta del directorio en el que se encuentra el archivo en ejecución.

    ```javascript
    console.log(`Directorio del archivo actual: ${__dirname}`);
    ```

4. **`__filename`**:
   - Contiene la ruta absoluta del archivo en ejecución.

    ```javascript
    console.log(`Ruta del archivo actual: ${__filename}`);
    ```

5. **`module`**:
   - Representa el módulo actual y permite exportar e importar funcionalidades entre módulos.

    ```javascript
    // archivo: miModulo.js
    module.exports.saludar = function() {
        return "Hola desde el módulo";
    };

    // archivo: app.js
    const miModulo = require('./miModulo');
    console.log(miModulo.saludar()); // Salida: Hola desde el módulo
    ```

6. **`require`**:
   - Función utilizada para cargar módulos nativos, de terceros o propios en una aplicación de Node.js.

    ```javascript
    const fs = require('fs'); // Módulo nativo
    const express = require('express'); // Módulo de terceros (requiere instalación previa)
    const miModulo = require('./miModulo'); // Módulo propio
    ```

7. **`console`**:
   - Proporciona métodos para imprimir mensajes en la consola, como `console.log`, `console.error`, `console.warn`, entre otros.

    ```javascript
    console.log('Mensaje informativo');
    console.error('Mensaje de error');
    console.warn('Mensaje de advertencia');
    ```

## Usos Comunes de Globals

### `global`

Permite definir variables globales que pueden ser accedidas desde cualquier parte del código, aunque su uso se desaconseja para evitar conflictos de nombres y problemas de mantenimiento.

### `process`

Se utiliza para:
- Obtener argumentos de la línea de comandos (`process.argv`).
- Salir del proceso (`process.exit()`).
- Escuchar eventos del proceso como `exit`, `uncaughtException`, entre otros.

    ```javascript
    process.on('exit', (code) => {
        console.log(`El proceso terminó con el código: ${code}`);
    });

    // Finalizar el proceso con un código de salida
    process.exit(1);
    ```

### `__dirname` y `__filename`

Se utilizan para:
- Construir rutas absolutas para acceder a archivos y directorios en el sistema de archivos.
- Facilitar el manejo de archivos relativos al directorio del script en ejecución.

    ```javascript
    const path = require('path');

    const archivoRuta = path.join(__dirname, 'archivo.txt');
    console.log(`Ruta del archivo: ${archivoRuta}`);
    ```

### `module` y `require`

Son fundamentales para:
- Modularizar el código y dividirlo en diferentes archivos.
- Reutilizar y organizar el código de manera más eficiente.

### `console`

Se usa para:
- Depuración y registro de información durante la ejecución de la aplicación.
- Mostrar mensajes de error, advertencias e información general.


Los objetos globales en Node.js facilitan el acceso a información y funcionalidades críticas sin necesidad de importaciones adicionales. Sin embargo, es importante usarlos con cuidado para mantener la claridad y el mantenimiento del código.
