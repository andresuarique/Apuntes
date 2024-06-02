# Importar y Exportar Módulos con ES6 Modules

Los ES6 Modules son una forma moderna y estándar de organizar y estructurar el código en proyectos de JavaScript. Permiten la importación y exportación de funciones, variables y clases entre diferentes archivos dentro de un proyecto.

## Exportar desde un Módulo

Para exportar contenido desde un [módulo](Modulos.md), utilizamos la palabra clave `export`. Hay varias formas de exportar:

- **Exportar por Defecto (`export default`)**: Permite exportar una sola entidad por defecto desde un módulo.

  ```javascript
  // en un archivo llamado utils.js
  const sumar = (a, b) => a + b;
  export default sumar;
  ```

- **Exportar Varias Entidades (`export`)**: Permite exportar múltiples entidades desde un módulo.

  ```javascript
  // en un archivo llamado utils.js
  export const sumar = (a, b) => a + b;
  export const restar = (a, b) => a - b;
  ```

## Importar en otro Módulo

Para importar contenido desde un módulo, utilizamos la palabra clave `import`. También hay varias formas de importar:

- **Importar Todo (`import * as nombre from 'ruta'`)**: Importa todas las entidades exportadas de un módulo.

  ```javascript
  // en un archivo llamado app.js
  import * as utils from './utils.js';
  console.log(utils.sumar(3, 5)); // 8
  console.log(utils.restar(10, 4)); // 6
  ```

- **Importar Entidades Individuales (`import { entidad } from 'ruta'`)**: Importa entidades específicas de un módulo.

  ```javascript
  // en un archivo llamado app.js
  import { sumar, restar } from './utils.js';
  console.log(sumar(3, 5)); // 8
  console.log(restar(10, 4)); // 6
  ```

- **Importar Entidad por Defecto (`import nombre from 'ruta'`)**: Importa la entidad por defecto de un módulo.

  ```javascript
  // en un archivo llamado app.js
  import sumar from './utils.js';
  console.log(sumar(3, 5)); // 8
  ```

## Consideraciones Importantes

- **Extensiones de Archivos**: Cuando importas un archivo de un módulo, generalmente debes incluir la extensión de archivo `.js` si estás trabajando con archivos JavaScript.

- **Rutas Relativas**: Las rutas en las importaciones deben ser relativas a la ubicación actual del archivo.

- **Soporte del Navegador**: Los ES6 Modules son ampliamente compatibles con los navegadores modernos, pero es posible que necesites configurar herramientas de construcción (como webpack o babel) para que funcionen correctamente en entornos de producción.

Los ES6 Modules proporcionan una manera limpia y eficiente de organizar y compartir código en proyectos de JavaScript, facilitando el desarrollo y mantenimiento de aplicaciones escalables y modulares.