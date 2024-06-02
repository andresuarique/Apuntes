# Monohilo: implicaciones en diseño y seguridad

Node, al ejecutar o procesar código en un solo hilo, presenta tanto ventajas como desafíos en términos de diseño y seguridad.

### _Buenas prácticas_

Cuando estamos en la consola y ejecutamos un archivo .js con Node, por ejemplo, `node ejemplo.js`, primero se abre un nuevo proceso que es un proceso de Node que interpretará el archivo. Convierte el código a código máquina, prepara todo lo necesario para ejecutar el código, lo ejecuta, muestra el resultado en pantalla y, finalmente, cierra el proceso, lo que hace que Node termine.

Existe la opción de ejecutar algo que esté siempre activo, y lo podemos lograr de la siguiente manera:

```js
setInterval(() => {   
    console.log("Estoy activo"), 1000; 
}); 
// 0 // 1 // 2 // 3 // 4...
```

En el código anterior, le estamos indicando a Node que muestre en la consola el texto 'Estoy activo' cada segundo, y esto se ejecutará infinitamente. Sin embargo, si algo fallara, mostrará inmediatamente el error y Node terminará todos los procesos.

```js
let contadorDeNumeros = 0; 
setInterval(() => {   
    console.log(contadorDeNumeros);
    if (contadorDeNumeros === 5) {
        console.log(contadorDeNumeros + numeroNoexistente);
    }   
    contadorDeNumeros += 1; 
}, 1000); 
console.log(contadorDeNumeros); 
// 0 // 1 // 2 // 3 // 4 // 5 
// /home/mooenz/mis-apuntes/Curso-de-Fundamentos-de-Node-js/tempCodeRunnerFile.js:7 
//     console.log(contadorDeNumeros + numeroNoexistente); 
//                                     ^ 
// ReferenceError: numeroNoexistente is not defined 
//     at Timeout._onTimeout (/home/mooenz/mis-apuntes/Curso-de-Fundamentos-de-Node-js/tempCodeRunnerFile.js:7:37) 
//     at listOnTimeout (internal/timers.js:555:17) 
//     at processTimers (internal/timers.js:498:7)

```

Es importante estar pendiente de todo lo que sucede en nuestra aplicación o programa y si hay alguna probabilidad de que algo falle, entonces fallará.

También debemos tener presente que se pueden mitigar estos errores o controlarlos, ya que Node, al detectar un error, detendrá todos los hilos en ejecución, finalizando así nuestro programa. Por lo tanto, es crucial tener un plan en caso de que esto suceda para evitar la terminación completa del programa.

En conclusión, es fundamental cuidar nuestro programa y el hilo principal. Todo lo que se pueda ejecutar de forma asíncrona, ejecutémoslo. Como dice la ley de Murphy: "si algo tiene una probabilidad de fallar, fallará".