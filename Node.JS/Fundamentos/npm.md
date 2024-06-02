# npm (Node Package Manager)

npm es el administrador de paquetes de Node.js que permite ejecutar funciones ya realizadas y validadas, acelerando y asegurando la calidad de nuestro proceso de desarrollo.

Podemos buscar [módulos](Modulos.md) para casi cualquier propósito en el sitio oficial de [npm](https://www.npmjs.com/).

## Uso Básico de npm

### Instalación de Módulos

Para instalar un módulo de npm en nuestro proyecto, utilizamos el siguiente comando:

```sh
$ npm install is-odd
```

### Requerir un Módulo

Una vez instalado, podemos requerir el módulo en nuestro código:

```javascript
const isOdd = require('is-odd');
console.log(isOdd(3)); // true
```

## Comandos Más Usados de npm

### Iniciar un Proyecto

- Iniciar un proyecto
```sh
npm init
```

- Iniciar un proyecto con configuración automática
```sh
npm init -y
```

### Instalación de Dependencias

- Instalar dependencias para producción
```sh
npm install nombreDelPaquete --save 
# Alternativa
npm i nombreDelPaquete -S 
```

- Instalar dependencias para desarrollo
```sh
npm install nombreDelPaquete --save-dev 
# Alternativa
npm i nombreDelPaquete -D
```

- Instalar dependencias de manera global
```sh
npm install -g nombreDelPaquete 
# Alternativa
npm i -g nombreDelPaquete
```

- Instalar una versión específica de una dependencia
```sh
npm install nombreDelPaquete@1.0.0
```

### Desinstalar Dependencias

- Desinstalar dependencias
```sh
npm uninstall nombreDelPaquete
```

### Actualización de Dependencias

- Ver dependencias desactualizadas
```sh
npm outdated
```

- Actualizar las dependencias desactualizadas
```sh
npm update
```

## Comandos Útiles

- **Revisar Paquetes Desactualizados a Nivel Global**: Para revisar qué paquetes no están actualizados a nivel global dentro de nuestro proyecto, usamos el comando `npm outdated` con las opciones `-g --depth=0`.

```sh
npm outdated -g --depth=0
```

Esto imprimirá algo así:

```
Package Current  Wanted  Latest  Location
firebase-tools8.0.1   8.0.2   8.0.2  global
npm  6.13.7  6.14.4  6.14.4  global
```

- **Actualizar Todos los Paquetes a Nivel Global**: Para actualizar todos los paquetes a nivel global dentro del proyecto, usamos el comando `npm update` con la opción `-g`.

```sh
npm update -g
```

## Ventajas de Usar npm

- **Aceleración del Desarrollo**: Permite reutilizar código ya validado y probado por la comunidad, reduciendo el tiempo de desarrollo.
- **Calidad Asegurada**: Al usar módulos populares y bien mantenidos, podemos asegurar un nivel de calidad en nuestras aplicaciones.
- **Amplia Biblioteca de Módulos**: Con una enorme cantidad de paquetes disponibles, es posible encontrar módulos para casi cualquier necesidad.

npm es una herramienta esencial para cualquier desarrollador de Node.js, facilitando la gestión de dependencias y la integración de funcionalidades de terceros en nuestros proyectos.