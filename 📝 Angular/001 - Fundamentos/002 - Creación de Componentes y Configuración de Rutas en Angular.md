# Creación de Componentes y Configuración de Rutas en Angular

## Creación de un Nuevo Componente

Para crear un nuevo componente en Angular, utiliza el siguiente comando:

```bash
ng generate component ruta/del/componente
```

Este comando generará un nuevo componente con todos sus archivos necesarios, incluyendo la plantilla HTML, el archivo de estilos CSS, y la lógica del componente en TypeScript.

## Configuración de Rutas (Routing)

En Angular, el archivo de rutas principal es generalmente `app.routes.ts` o `app-routing.module.ts`. En este archivo, puedes importar los componentes y definir las rutas de la aplicación, indicando qué componente se debe renderizar para cada ruta.

```typescript
import { Routes } from '@angular/router';

import { HomeComponent } from './pages/home/home.component';
import { LabsComponent } from './pages/labs/labs.component';

export const routes: Routes = [
  {
    path: '',
    component: HomeComponent
  },
  {
    path: 'labs',
    component: LabsComponent
  }
];
```

En el componente principal (normalmente `app.component.html`), agrega el siguiente marcador para permitir que Angular maneje el enrutamiento y renderice los componentes correspondientes:

```html
<router-outlet></router-outlet>
```

Esto le indica a Angular que, al navegar a diferentes rutas, debe renderizar el componente especificado en la configuración de rutas.

## Configuración de Estilos

El archivo `styles.css` es el archivo de estilos global de la aplicación Angular. Los estilos definidos aquí afectarán a toda la aplicación. Sin embargo, cada componente tiene su propio archivo de estilos específico (por ejemplo, `componente.component.css`), lo que permite encapsular estilos que solo se aplican dentro del alcance de ese componente.

Los estilos locales permiten que los desarrolladores apliquen estilos específicos sin preocuparse por conflictos con otros componentes o con los estilos globales.