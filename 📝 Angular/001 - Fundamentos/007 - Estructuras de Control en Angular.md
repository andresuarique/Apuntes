# Estructuras de Control en Angular

Las estructuras de control en Angular permiten gestionar la lógica en las plantillas de los componentes, facilitando la visualización condicional y la iteración sobre datos. Estas estructuras son fundamentales para construir interfaces dinámicas y reactivas en Angular.

## Directiva *ngIf

La directiva `*ngIf` se utiliza para mostrar u ocultar un elemento del DOM en función de una condición booleana.

### Sintaxis Básica

```html
<div *ngIf="condition">Contenido visible si la condición es verdadera</div>
```

### Ejemplo

```html
<p *ngIf="isLoggedIn">Bienvenido, usuario.</p>
<p *ngIf="!isLoggedIn">Por favor, inicie sesión.</p>
```

### Uso con `else`

Para manejar un caso alternativo cuando la condición es falsa, se puede usar `else`.

```html
<p *ngIf="isLoggedIn; else notLoggedIn">Bienvenido, usuario.</p>
<ng-template #notLoggedIn>Por favor, inicie sesión.</ng-template>
```

## Directiva *ngFor

La directiva `*ngFor` se usa para iterar sobre una colección y renderizar un elemento para cada ítem en la colección.

### Sintaxis Básica

```html
<li *ngFor="let item of items">{{ item }}</li>
```

### Ejemplo

```html
<ul>
  <li *ngFor="let fruit of fruits">{{ fruit }}</li>
</ul>
```

### Uso de Índices

También es posible obtener el índice de cada ítem en la iteración.

```html
<ul>
  <li *ngFor="let fruit of fruits; let i = index">{{ i + 1 }}. {{ fruit }}</li>
</ul>
```

## Directiva *ngSwitch

La directiva `*ngSwitch` permite mostrar un elemento en función del valor de una expresión. Es útil para seleccionar entre varias opciones.

### Sintaxis Básica

```html
<div [ngSwitch]="value">
  <p *ngSwitchCase="'A'">Valor es A</p>
  <p *ngSwitchCase="'B'">Valor es B</p>
  <p *ngSwitchDefault>Valor no reconocido</p>
</div>
```

### Ejemplo

```html
<div [ngSwitch]="currentStatus">
  <p *ngSwitchCase="'active'">Activo</p>
  <p *ngSwitchCase="'inactive'">Inactivo</p>
  <p *ngSwitchDefault>Estado desconocido</p>
</div>
```

## Directiva *ngTemplate

La directiva `*ngTemplate` se usa para definir un bloque de contenido que puede ser reutilizado en la plantilla, generalmente en combinación con otras estructuras de control.

### Sintaxis Básica

```html
<ng-template #templateRef>
  Contenido reutilizable
</ng-template>
```

### Ejemplo de Uso

```html
<ng-container *ngTemplateOutlet="templateRef"></ng-container>
```

## Directiva *ngIf-Else

Combina `*ngIf` con `else` para manejar bloques alternativos de contenido.

### Sintaxis Básica

```html
<p *ngIf="condition; else elseBlock">Contenido visible si la condición es verdadera</p>
<ng-template #elseBlock>Contenido alternativo</ng-template>
```

### Ejemplo

```html
<p *ngIf="isUserLoggedIn; else loginMessage">Bienvenido, usuario.</p>
<ng-template #loginMessage>Por favor, inicie sesión.</ng-template>
```

## Estructuras de Control Anidadas

Las estructuras de control pueden ser anidadas para crear lógicas más complejas. 

### Ejemplo de *ngIf y *ngFor Anidados

```html
<div *ngIf="categories.length > 0">
  <ul>
    <li *ngFor="let category of categories">
      {{ category.name }}
      <ul>
        <li *ngFor="let item of category.items">{{ item }}</li>
      </ul>
    </li>
  </ul>
</div>
```

## Combinación de Estructuras de Control

Puedes combinar múltiples directivas de control en una sola plantilla para manejar lógica más compleja.

### Ejemplo de Combinación

```html
<div *ngIf="isLoggedIn">
  <p>Bienvenido, {{ user.name }}</p>
  <ul>
    <li *ngFor="let item of user.items">{{ item }}</li>
  </ul>
</div>
<div *ngIf="!isLoggedIn">
  <p>Por favor, inicie sesión.</p>
</div>
```

Estas estructuras de control permiten construir aplicaciones Angular dinámicas y adaptativas al renderizar contenido basado en el estado de los datos y la lógica del componente.