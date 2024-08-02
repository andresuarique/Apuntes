# Modelo de Reactividad de Signals en Angular

Angular Signals es un sistema diseñado para rastrear de manera granular cómo y dónde se utiliza el estado en una aplicación. Esto permite que el framework optimice las actualizaciones de renderizado de manera más eficiente.

## ¿Qué son las Signals?

Una **signal** es un contenedor (envoltorio) alrededor de un valor que notifica a los consumidores interesados cuando ese valor cambia. Las signals pueden contener cualquier tipo de valor, desde primitivas simples hasta estructuras de datos complejas.

### Características de las Signals

- **Notificación de cambios:** Cuando el valor de una signal cambia, notifica automáticamente a todos los consumidores interesados, lo que desencadena actualizaciones en la interfaz de usuario según sea necesario.

- **Lectura de valores:** El valor de una signal se lee llamando a su función getter. Esto permite que Angular rastree dónde se utiliza la signal en la aplicación, lo que es crucial para la optimización del renderizado.

- **Tipos de Signals:** Las signals pueden ser de escritura (permiten modificar su valor) o de solo lectura (su valor no puede ser modificado directamente).

### Uso de Signals

Las signals son útiles en aplicaciones donde es importante optimizar las actualizaciones de renderizado y manejar cambios en el estado de manera eficiente. Al utilizar signals, Angular puede minimizar las actualizaciones innecesarias en el DOM, mejorando así el rendimiento general de la aplicación.

### Ejemplo de Signals

Supongamos que tienes una signal que contiene un valor numérico:

```typescript
import { signal } from '@angular/core';

const contador = signal(0);

// Leer el valor
console.log(contador()); // Output: 0

// Actualizar el valor
contador.set(contador() + 1);
console.log(contador()); // Output: 1
```

En este ejemplo, `contador` es una signal que contiene un valor numérico. Puedes leer su valor usando `contador()` y actualizarlo utilizando `contador.set(nuevoValor)`.

## Consideraciones

- El uso de signals facilita la creación de aplicaciones más reactivas y eficientes, ya que Angular puede gestionar automáticamente las dependencias y actualizaciones del estado.

- Asegúrate de comprender cómo las signals interactúan con otros componentes del sistema de reactividad de Angular para aprovechar al máximo sus capacidades.
