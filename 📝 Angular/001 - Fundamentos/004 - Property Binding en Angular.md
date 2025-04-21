# Property Binding en Angular

**Property binding** es una técnica en Angular que permite controlar y modificar las propiedades de los elementos HTML de manera dinámica desde el componente. Para ello, se utilizan corchetes `[]` alrededor del nombre de la propiedad HTML que se desea enlazar.

## Utilidades

Property binding se utiliza para:

- **Modificar el atributo `src` de una etiqueta `<img>`:** Permite cambiar dinámicamente la imagen mostrada.

- **Modificar el atributo `href` de un enlace `<a>`:** Cambia dinámicamente el destino de un enlace.

- **Modificar el atributo `value` de un campo `<input>`:** Autocompleta un valor en un formulario.

- **Modificar el atributo `disabled` de un campo `<input>`:** Habilita o deshabilita un campo de formulario.

## Ejemplo de Uso

A continuación, se muestra un ejemplo de cómo usar property binding en Angular:

```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  empresa = 'Platzi';
  habilitado = true;
}
```

### Modificación del Valor y Estado de un Campo de Formulario

Puedes modificar el valor y el estado de un campo de formulario de la siguiente manera:

```html
<input [value]="empresa" [disabled]="habilitado" />
```

En este ejemplo:

- El valor de la propiedad `empresa` se utiliza como el valor del campo `<input>`.

- La variable `habilitado` controla si el campo está habilitado o deshabilitado. Si `habilitado` es `true`, el campo estará deshabilitado, impidiendo su edición.

### Consideraciones

- Property binding es una herramienta poderosa para crear aplicaciones interactivas y dinámicas en Angular, permitiendo a los desarrolladores actualizar el DOM de manera eficiente en respuesta a cambios en el estado de la aplicación.

- Asegúrate de que los valores utilizados en el property binding estén siempre actualizados para reflejar el estado actual de la aplicación.
