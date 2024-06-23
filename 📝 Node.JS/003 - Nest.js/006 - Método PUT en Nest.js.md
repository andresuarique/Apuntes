# Método PUT en Nest.js

## Método PUT

El método PUT se utiliza para la actualización de datos en una aplicación. En Nest.js, se utiliza el decorador `@Put` para definir rutas que manejarán actualizaciones de datos.

## Importar Decorador PUT

```typescript
import { Controller, Put } from '@nestjs/common';
```

## Crear un End-Point PUT

```typescript
@Put('ruta')
update() {
  return {
    message: 'acción de actualizar',
  };
}
```

## Utilizar el Body y Param

El método PUT a menudo necesita tanto el body, que contiene los datos a actualizar, como un parámetro de ruta que especifica el recurso a actualizar. Para manejar esto en Nest.js, importamos los decoradores `@Body` y `@Param` desde `@nestjs/common`.

## Importar Decoradores BODY y PARAM

```typescript
import { Controller, Put, Body, Param } from '@nestjs/common';
```

## Usar Body y Param en el Método PUT

```typescript
@Put('ruta/:id')
update(@Param('id') id: string, @Body() payload: any) {
  return {
    message: 'acción de actualizar',
    id,
    payload,
  };
}
```

## Validación de Parámetros

Para realizar una prevalidación del parámetro, por ejemplo, asegurando que sea un entero, podemos usar pipes. Un ejemplo simple de esto es:

```typescript
import { ParseIntPipe } from '@nestjs/common';

@Put('ruta/:id')
update(
  @Param('id', new ParseIntPipe({ errorHttpStatusCode: HttpStatus.NOT_ACCEPTABLE })) id: number,
  @Body() payload: any,
) {
  return {
    message: 'acción de actualizar',
    id,
    payload,
  };
}
```
