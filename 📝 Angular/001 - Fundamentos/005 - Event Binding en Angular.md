# Event Binding en Angular

**Event binding** es una técnica en Angular que permite manejar eventos que ocurren en elementos HTML, como el clic de un botón, cambios en un campo de entrada, el envío de un formulario, entre otros. Se utiliza la sintaxis de paréntesis `()` para vincular el evento del elemento con un método del componente.

## Ejemplo de Uso

Supongamos que tienes un componente con el siguiente método:

```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  enviarFormulario() {
    // Lógica para enviar el formulario
  }
}
```

Puedes ejecutar el método `enviarFormulario()` cuando se hace clic en un botón de la siguiente manera:

```html
<button (click)="enviarFormulario()">Enviar</button>
```

## Eventos Comunes en Angular

### Eventos de Ratón

- **click:** Se activa cuando se hace clic en un elemento.
  ```html
  <button (click)="onSave()">Guardar</button>
  ```

- **dblclick:** Se activa cuando se hace doble clic en un elemento.
  ```html
  <div (dblclick)="onDoubleClick()">Haz doble clic aquí</div>
  ```

- **mouseover:** Se activa cuando el puntero del ratón entra en un elemento.

- **mouseout:** Se activa cuando el puntero del ratón sale de un elemento.

- **mouseleave:** Similar a `mouseout`, pero no se propaga a los elementos secundarios.
  ```html
  <div (mouseleave)="onMouseLeave()">El ratón se fue</div>
  ```

### Eventos de Teclado

- **keydown:** Se activa cuando se presiona una tecla. Puedes especificar la tecla o el código que deseas enlazar.
  ```html
  <input (keydown.enter)="onKeydown($event)" />
  ```

- **keyup:** Similar a `keydown`, pero se activa cuando se suelta una tecla.

### Eventos de Entrada y Cambio

- **input:** Se activa cuando se introduce texto en un campo de entrada (como un `input` o `textarea`). Útil para detectar cambios en el contenido.
  ```html
  <input (input)="onInput($event.target.value)" />
  ```

- **change:** Se activa cuando cambia el valor de un elemento de entrada (por ejemplo, un `select`).
  ```html
  <select (change)="onSelectionChange($event.target.value)">
    <option value="option1">Opción 1</option>
    <option value="option2">Opción 2</option>
  </select>
  ```

### Eventos de Foco

- **focus:** Se activa cuando un elemento obtiene el foco.

- **blur:** Se activa cuando un elemento pierde el foco.

## Consideraciones

- Event binding en Angular es una herramienta poderosa que permite a los desarrolladores crear aplicaciones interactivas y receptivas al permitir que el DOM reaccione a las acciones del usuario.

- Asegúrate de que los métodos vinculados a eventos sean eficientes y no bloqueen el hilo principal para mantener la aplicación fluida.
