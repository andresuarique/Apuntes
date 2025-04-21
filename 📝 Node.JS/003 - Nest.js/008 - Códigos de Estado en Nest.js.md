# Códigos de Estado en Nest.js

### Códigos de Estado

En el contexto de una API, los [códigos de estado HTTP](Códigos%20de%20Estado%20HTTP.md) son cruciales para indicar el resultado de una solicitud. Nest.js permite configurar y utilizar códigos de estado personalizados.

### Recurso Recomendado

Para familiarizarte con los códigos de estado HTTP, te recomiendo la siguiente página: [HTTP Cats](https://http.cat/)

### Importar Decoradores Necesarios

Nest.js proporciona el decorador `@HttpCode` para definir códigos de estado personalizados. También puedes importar `HttpStatus` para usar códigos de estado predefinidos.

```typescript
import { Controller, Post, HttpStatus, HttpCode } from '@nestjs/common';
```

### Definir Código de Estado

Puedes definir el código de estado de una respuesta utilizando el decorador `@HttpCode` antes del método del controlador.

```typescript
@Post('ruta')
@HttpCode(201) // Código de estado definido como número
create(@Body() payload: any) {
  return {
    message: 'acción de crear',
    payload,
  };
}
```

### Usar HttpStatus

Aunque `HttpStatus` es opcional, proporciona una manera legible y semántica de definir códigos de estado.

```typescript
@Post('ruta')
@HttpCode(HttpStatus.CREATED) // Código de estado definido usando HttpStatus
create(@Body() payload: any) {
  return {
    message: 'acción de crear',
    payload,
  };
}
```
