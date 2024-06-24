# Crear un Pipe en Nest.js

Crear tus propias validaciones de datos es fundamental para securizar tu aplicación y evitar errores inesperados. Nest.js permite crear custom pipes para implementar lógica personalizada de validación de datos.

## Cómo Crear Custom Pipes

### 1. Crear tu Primer Pipe

Con el CLI de Nest.js, puedes autogenerar un nuevo pipe con el comando `nest generate pipe <pipe-name>` o en su forma corta `nest g p <pipe-name>`. Por defecto, verás un código como el siguiente:

```typescript
import { ArgumentMetadata, Injectable, PipeTransform } from '@nestjs/common';

@Injectable()
export class ParseIntPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    return value;
  }
}
```

### 2. Implementar la Lógica del Pipe

Implementa tu propia lógica de transformación y validación de datos. Si los datos no son válidos, puedes arrojar excepciones para informar al front-end que los datos son erróneos.

```typescript
import { ArgumentMetadata, Injectable, PipeTransform, BadRequestException } from '@nestjs/common';

@Injectable()
export class ParseIntPipe implements PipeTransform {
  transform(value: string, metadata: ArgumentMetadata) {
    const finalValue = parseInt(value, 10);
    if (isNaN(finalValue)) {
      throw new BadRequestException(`${value} no es un número.`);
    }
    return finalValue;
  }
}
```

### 3. Importar y Utilizar el Pipe

Finalmente, implementa tu custom pipe en el controlador.

```typescript
import { Controller, Get, Param } from '@nestjs/common';
import { ParseIntPipe } from './pipes/parse-int.pipe';

@Controller('products')
export class ProductsController {
  @Get('product/:idProduct')
  getProduct(@Param('idProduct', ParseIntPipe) idProduct: number): string {
    // ...
  }
}
```

Puedes desarrollar la lógica para validar y transformar los datos de acuerdo a tus necesidades. Es fundamental no permitir el ingreso de datos erróneos a tus controladores. Por eso, los pipes actúan como una capa previa a los controladores para realizar esta validación.

## Generar un Pipe con Nest CLI

Para generar un pipe con el CLI de Nest, puedes usar el siguiente comando:

```bash
nest g pi common/parse-int
```

El archivo generado tendrá una estructura similar a la siguiente:

```typescript
// src/common/parse-int.pipe.ts

import { ArgumentMetadata, Injectable, PipeTransform, BadRequestException } from '@nestjs/common';

@Injectable()
export class ParseIntPipe implements PipeTransform {
  transform(value: string, metadata: ArgumentMetadata) {
    const val = parseInt(value, 10);
    if (isNaN(val)) {
      throw new BadRequestException(`${value} no es un número`);
    }
    return val;
  }
}
```
