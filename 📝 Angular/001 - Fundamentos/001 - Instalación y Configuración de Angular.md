# Instalación y Configuración de Angular

Para instalar Angular, utilizamos el siguiente comando en la terminal:

```bash
npm install -g @angular/cli
```

Este comando instalará Angular CLI de manera global en tu sistema, permitiéndote crear y gestionar aplicaciones Angular.

## Creación de una Aplicación Angular

Para crear una nueva aplicación Angular, ejecuta el siguiente comando:

```bash
ng new my-application --skip-tests
```

**Nota:** La opción `--skip-tests` se utiliza para omitir la configuración de pruebas unitarias.

Durante el proceso de creación, se te preguntará si deseas usar un preprocesador de CSS y si quieres configurar Server-Side Rendering (SSR). Esto configurará una aplicación Angular con la configuración predeterminada.

## Ejecutar el Proyecto

Para ejecutar el proyecto, navega a la carpeta raíz del proyecto y ejecuta el siguiente comando:

```bash
ng serve
```

Este comando iniciará el servidor de desarrollo y ejecutará la aplicación en el puerto por defecto, que es el 4200.

# Estructura de un Componente Angular

Un componente en Angular es una pieza fundamental de la aplicación y está compuesto por varios archivos:

## HTML (Template)

El archivo HTML define la estructura visual del componente. Contiene la plantilla que se renderiza en la vista. Puedes usar directivas y bindings de Angular para interactuar con los datos del componente.

```html
<!-- ejemplo.component.html -->
<div>
  <h1>{{ title }}</h1>
  <button (click)="handleClick()">Haz clic aquí</button>
</div>
```

## TypeScript (Clase del Componente)

El archivo TypeScript contiene la lógica del componente. Aquí defines propiedades, métodos y el ciclo de vida del componente.

```typescript
// ejemplo.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-ejemplo',
  templateUrl: './ejemplo.component.html',
  styleUrls: ['./ejemplo.component.css']
})
export class EjemploComponent {
  title: string = 'Mi Componente Angular';

  handleClick() {
    console.log('El botón fue clicado.');
  }
}
```

## CSS (Estilos)

El archivo CSS contiene los estilos específicos para el componente. Angular permite el encapsulamiento de estilos para que no afecten a otros componentes.

```css
/* ejemplo.component.css */
h1 {
  color: blue;
}

button {
  background-color: lightblue;
}
```

### Funcionamiento de un Componente Angular

1. **Selector:** El `selector` es una cadena que especifica un elemento HTML personalizado, que Angular sustituirá por la plantilla del componente.

2. **Plantilla:** La plantilla HTML se renderiza en el lugar del selector y se utiliza para definir el diseño del componente.

3. **Clase:** La clase TypeScript contiene la lógica del componente, definiendo cómo responde el componente a las acciones del usuario y cómo interactúa con el modelo de datos.

4. **Estilos:** Los estilos CSS definen la apariencia del componente, y Angular asegura que sean aplicados de manera encapsulada.

Con esta estructura modular, Angular facilita el desarrollo de aplicaciones complejas al dividirlas en componentes reutilizables y mantenibles.