# 007 - Método DELETE en Nest.js

## Método DELETE

El método DELETE se utiliza para eliminar recursos en una aplicación. En Nest.js, se utiliza el decorador `@Delete` para definir rutas que manejarán la eliminación de datos.

## Importar Decorador DELETE

```typescript
import { Controller, Delete } from '@nestjs/common';
```

## Crear un End-Point DELETE

```typescript
@Delete('ruta')
remove() {
  return {
    message: 'acción de eliminar',
  };
}
```

## Utilizar Parámetros de Ruta

El método DELETE a menudo necesita un parámetro de ruta que especifica el recurso a eliminar. Para manejar esto en Nest.js, importamos el decorador `@Param` desde `@nestjs/common`.

## Importar Decorador PARAM

```typescript
import { Controller, Delete, Param } from '@nestjs/common';
```

## Usar Param en el Método DELETE

```typescript
@Delete('ruta/:id')
remove(@Param('id') id: string) {
  return {
    message: 'acción de eliminar',
    id,
  };
}
```

## Validación de Parámetros

Para realizar una prevalidación del parámetro, por ejemplo, asegurando que sea un entero, podemos usar pipes. Un ejemplo simple de esto es:

```typescript
import { ParseIntPipe } from '@nestjs/common';

@Delete('ruta/:id')
remove(
  @Param('id', new ParseIntPipe({ errorHttpStatusCode: HttpStatus.NOT_ACCEPTABLE })) id: number,
) {
  return {
    message: 'acción de eliminar',
    id,
  };
}
```
