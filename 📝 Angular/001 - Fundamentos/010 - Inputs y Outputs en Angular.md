# Inputs y Outputs en Angular
Los inputs y outputs en Angular son mecanismos de comunicación entre componentes. Permiten que un componente padre pase datos a un componente hijo (inputs) y que un componente hijo emita eventos al componente padre (outputs).

## Inputs
Los inputs se utilizan para pasar datos desde un componente padre a un componente hijo. Para definir un input en un componente hijo, se utiliza el decorador `@Input()` en una propiedad de la clase.

### Ejemplo de Uso de Inputs
```typescript
// componente-hijo.ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-componente-hijo',
  template: `<p>{{ datos }}</p>`
})
export class ComponenteHijo {
  @Input() datos: string;
}

// componente-padre.html
<app-componente-hijo [datos]="mensaje"></app-componente-hijo>

// componente-padre.ts
export class ComponentePadre {
  mensaje = 'Hola desde el componente padre';
}
```
En este ejemplo, el componente padre pasa la cadena `mensaje` al componente hijo mediante el input `datos`.

## Outputs
Los outputs permiten que un componente hijo envíe eventos al componente padre. Para definir un output, se utiliza el decorador `@Output()` junto con un `EventEmitter`.

### Ejemplo de Uso de Outputs
```typescript
// componente-hijo.ts
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-componente-hijo',
  template: `<button (click)="enviarDatos()">Enviar Datos</button>`
})
export class ComponenteHijo {
  @Output() datosEnviados = new EventEmitter<string>();

  enviarDatos() {
    this.datosEnviados.emit('Datos enviados desde el hijo');
  }
}

// componente-padre.html
<app-componente-hijo (datosEnviados)="recibirDatos($event)"></app-componente-hijo>

// componente-padre.ts
export class ComponentePadre {
  recibirDatos(mensaje: string) {
    console.log(mensaje);
  }
}
```
En este ejemplo, el componente hijo emite un evento con el mensaje `"Datos enviados desde el hijo"`, que es manejado por el componente padre.

## Comunicación Bidireccional
Aunque los inputs y outputs se utilizan principalmente para la comunicación unidireccional, se pueden combinar para lograr una comunicación bidireccional entre componentes.

```typescript
// componente-hijo.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-componente-hijo',
  template: `
    <input [(ngModel)]="valor" (ngModelChange)="valorCambiado.emit(valor)" />
  `
})
export class ComponenteHijo {
  @Input() valor: string;
  @Output() valorCambiado = new EventEmitter<string>();
}

// componente-padre.html
<app-componente-hijo [(valor)]="mensaje"></app-componente-hijo>

// componente-padre.ts
export class ComponentePadre {
  mensaje = 'Texto inicial';
}
```
En este caso, el componente hijo puede actualizar el valor `mensaje` en el componente padre, creando un enlace bidireccional.
