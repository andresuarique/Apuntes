# Ciclo de Vida de los Componentes en Angular
El ciclo de vida de un componente en Angular es una serie de eventos o etapas que atraviesa un componente desde su creación hasta su destrucción. Angular proporciona varios métodos de ciclo de vida que permiten a los desarrolladores ejecutar código en diferentes momentos del ciclo de vida de un componente.

![Pasted image 20240808200402](📎%20ANEXOS/Pasted%20image%2020240808200402.png)

## Fases del Ciclo de Vida

### 1. Creación
Durante esta fase, el componente se inicializa, se configuran las dependencias y se inicializan las propiedades de entrada.

- **ngOnChanges()**: Se llama cuando una de las propiedades de entrada (`@Input`) cambia. Se ejecuta inmediatamente después de que el valor de entrada cambie, antes de `ngOnInit`.

- **ngOnInit()**: Se invoca una sola vez después de que Angular haya inicializado todas las propiedades de entrada del componente. Ideal para inicializar datos del componente.

### 2. Renderizado
En esta fase, Angular verifica y actualiza la vista y el modelo de datos del componente.

- **ngDoCheck()**: Se llama en cada ciclo de detección de cambios. Se puede usar para detectar y responder a los cambios que Angular no detecta automáticamente.

- **ngAfterContentInit()**: Se invoca después de que Angular haya proyectado el contenido en el componente.

- **ngAfterContentChecked()**: Se llama después de cada verificación de contenido proyectado en el componente.

- **ngAfterViewInit()**: Se invoca después de que Angular haya inicializado las vistas y sub-vistas del componente.

- **ngAfterViewChecked()**: Se llama después de cada verificación de la vista y sub-vistas del componente.

### 3. Destrucción
En esta fase, se limpia y destruye el componente, liberando recursos.

- **ngOnDestroy()**: Se invoca inmediatamente antes de que Angular destruya el componente. Útil para limpiar recursos, desuscribir observables, y detener temporizadores.

## Ejemplo de Implementación
```typescript
import { Component, OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy, Input } from '@angular/core';

@Component({
  selector: 'app-ejemplo-ciclo-vida',
  template: `<p>{{ data }}</p>`
})
export class EjemploCicloVidaComponent implements OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {
  
  @Input() data: string;

  constructor() {
    console.log('Constructor');
  }

  ngOnChanges() {
    console.log('ngOnChanges');
  }

  ngOnInit() {
    console.log('ngOnInit');
  }

  ngDoCheck() {
    console.log('ngDoCheck');
  }

  ngAfterContentInit() {
    console.log('ngAfterContentInit');
  }

  ngAfterContentChecked() {
    console.log('ngAfterContentChecked');
  }

  ngAfterViewInit() {
    console.log('ngAfterViewInit');
  }

  ngAfterViewChecked() {
    console.log('ngAfterViewChecked');
  }

  ngOnDestroy() {
    console.log('ngOnDestroy');
  }
}
```

En este ejemplo, cada método de ciclo de vida imprime un mensaje en la consola cuando es llamado, lo que ayuda a visualizar el flujo del ciclo de vida de un componente Angular.