# Módulo `child_process`

El [módulo](Modulos.md) `child_process` en Node.js nos permite crear y controlar procesos hijos. Estos procesos hijos pueden ejecutar comandos del sistema, otros programas y scripts, permitiendo que Node.js interactúe con el sistema operativo y otros programas de manera eficiente.

## Características Principales

1. **Ejecución de Comandos del Sistema**: Puedes ejecutar comandos del sistema operativo directamente desde Node.js.
2. **Comunicación Entre Procesos**: Permite la comunicación entre el proceso padre y los procesos hijos mediante flujos estándar (stdin, stdout, stderr).
3. **Manejo de Recursos**: Puedes controlar el uso de recursos de los procesos hijos, como la memoria y la CPU.

## Métodos Principales

### `child_process.exec()`

Este método ejecuta un comando en una shell y búfera la salida. Es útil para comandos que no generan grandes volúmenes de salida.

```javascript
const { exec } = require('child_process');

exec('ls', (error, stdout, stderr) => {
    if (error) {
        console.error(`Error: ${error.message}`);
        return;
    }
    if (stderr) {
        console.error(`stderr: ${stderr}`);
        return;
    }
    console.log(`stdout: ${stdout}`);
});
```

### `child_process.spawn()`

Este método lanza un nuevo proceso utilizando un comando dado. A diferencia de `exec`, no búfera la salida, lo que lo hace más adecuado para procesos que generan grandes volúmenes de datos.

```javascript
const { spawn } = require('child_process');

const ls = spawn('ls', ['-lh', '/usr']);

ls.stdout.on('data', (data) => {
    console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
    console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
    console.log(`Proceso hijo finalizado con el código ${code}`);
});
```

### `child_process.fork()`

Este método es una especialización de `spawn` diseñada específicamente para crear nuevos procesos de Node.js. Crea un nuevo proceso JavaScript V8 con el mismo archivo JavaScript que el proceso padre.

```javascript
const { fork } = require('child_process');

const child = fork('child.js');

child.on('message', (message) => {
    console.log(`Mensaje del hijo: ${message}`);
});

child.send('Hola hijo');
```

## Ventajas del Módulo `child_process`

1. **Paralelismo**: Permite ejecutar múltiples operaciones en paralelo, aprovechando mejor los recursos del sistema.
2. **Separación de Concerns**: Cada proceso puede encargarse de una tarea específica, mejorando la modularidad y mantenibilidad del código.
3. **Integración con el Sistema**: Facilita la interacción con el sistema operativo y otros programas, ampliando las capacidades de Node.js.

El módulo `child_process` es una herramienta poderosa para ejecutar y controlar procesos del sistema desde una aplicación Node.js, permitiendo una mayor flexibilidad y eficiencia en la ejecución de tareas complejas.