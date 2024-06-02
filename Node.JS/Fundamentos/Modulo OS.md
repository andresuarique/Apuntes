# Módulo `os`

El [módulo](Modulos.md) `os` en Node.js proporciona una serie de utilidades relacionadas con el sistema operativo subyacente. Este módulo te permite acceder a información sobre el sistema operativo, el entorno y realizar operaciones específicas del sistema operativo.

## Funciones Comunes del Módulo `os`

1. **`os.platform()`**: Devuelve una cadena que identifica la plataforma del sistema operativo, como "darwin" en macOS, "win32" en Windows o "linux" en sistemas basados en Linux.
```javascript
const os = require('os');
console.log(os.platform()); // Ejemplo: 'linux'
```

2. **`os.arch()`**: Devuelve una cadena que identifica la arquitectura del procesador del sistema, como "x64" o "arm".
```javascript
const os = require('os');
console.log(os.arch()); // Ejemplo: 'x64'
```

3. **`os.cpus()`**: Devuelve un arreglo de objetos que describen cada núcleo de la CPU del sistema, incluyendo información como el modelo, la velocidad y los tiempos de uso.
```javascript
const os = require('os');
console.log(os.cpus()); // Ejemplo: [{ model: 'Intel(R) Core(TM) i7-7700HQ CPU @ 2.80GHz', speed: 2808, ... }]
```

4. **`os.totalmem()`**: Devuelve la cantidad total de memoria del sistema en bytes.
```javascript
const os = require('os');
console.log(os.totalmem()); // Ejemplo: 17179869184 (bytes)
```

5. **`os.freemem()`**: Devuelve la cantidad de memoria libre en el sistema en bytes.
```javascript
const os = require('os');
console.log(os.freemem()); // Ejemplo: 4294967296 (bytes)
```

6. **`os.hostname()`**: Devuelve el nombre de host del sistema.
```javascript
const os = require('os');
console.log(os.hostname()); // Ejemplo: 'mi-computadora'
```

7. **`os.networkInterfaces()`**: Devuelve un objeto que contiene información sobre las interfaces de red disponibles en el sistema, incluyendo direcciones IP y otras propiedades.
```javascript
const os = require('os');
console.log(os.networkInterfaces());
/*
Ejemplo:
{
lo: [
{ address: '127.0.0.1', netmask: '255.0.0.0', family: 'IPv4', ... },
...
],
eth0: [
{ address: '192.168.1.100', netmask: '255.255.255.0', family: 'IPv4', ... },
...
]
}
*/
```

8. **`os.userInfo([options])`**: Devuelve un objeto que contiene información sobre el usuario actual, como el nombre de usuario, el UID y el directorio de inicio.
```javascript
const os = require('os');
console.log(os.userInfo());
/*
Ejemplo:
{
uid: 1000,
gid: 1000,
username: 'usuario',
homedir: '/home/usuario',
shell: '/bin/bash'
}
*/
```

9. **`os.tmpdir()`**: Devuelve el directorio temporal predeterminado para el sistema.
```javascript
const os = require('os');
console.log(os.tmpdir()); // Ejemplo: '/tmp'
```

Estas son solo algunas de las funciones proporcionadas por el módulo `os` en Node.js. Puedes consultar la [documentación oficial de Node.js](https://nodejs.org/dist/latest-v16.x/docs/api/os.html) para obtener más información sobre todas las funciones disponibles y sus usos específicos.
