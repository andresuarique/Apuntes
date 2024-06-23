# Método POST en Nest.js

## Método POST

El método POST se utiliza para la creación de datos. Para utilizarlo en Nest.js, debemos importar el decorador `@Post` desde `@nestjs/common`.

## Importar Decorador POST

```typescript
import { Controller, Post } from '@nestjs/common';
```

## Crear un End-Point

```typescript
@Post('ruta')
create() {
  return {
    message: 'acción de crear',
  };
}
```

## Utilizar el Body

El body es donde se envían los datos en una petición POST. Para manejar el body en Nest.js, importamos el decorador `@Body` desde `@nestjs/common`.

## Importar Decorador BODY

```typescript
import { Controller, Post, Body } from '@nestjs/common';
```

## Usar el Body en el Método POST

```typescript
@Post('ruta')
create(@Body() payload: any) {
  return {
    message: 'acción de crear',
    payload,
  };
}
```
