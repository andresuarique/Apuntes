# Pipes en Nest.js

Nest.js utiliza el concepto de **Pipes** para la validación y transformación de los datos antes del ingreso de estos a un controlador.

## Casos de Uso de Pipes

Los pipes tienen dos casos de uso típicos:

1. **Transformación**: Transforma los datos de entrada a la forma deseada (por ejemplo, de cadena a entero).
2. **Validación**: Evalúa los datos de entrada y, si son válidos, simplemente los pasa sin cambios; de lo contrario, lanza una excepción cuando los datos son incorrectos.

## Implementando tu Primer Pipe

Nest.js ya trae consigo una serie de pipes que puedes utilizar para la manipulación de datos. Puedes importarlos desde `@nestjs/common` y usarlos de la siguiente manera.

## Ejemplo de Transformación

Utiliza el `ParseIntPipe` para transformar el parámetro `idProduct` y asegurar que este sea un número entero.

```typescript
import { Controller, Get, Param, ParseIntPipe } from '@nestjs/common';

@Controller('products')
export class ProductsController {
  @Get('product/:idProduct')
  getProduct(@Param('idProduct', ParseIntPipe) idProduct: number): string {
    // ...
  }
}
```

El pipe `ParseIntPipe` se agrega como segundo parámetro del decorador `@Param` para transformar el parámetro `idProduct`. Si el parámetro no es un entero, arrojará un error, protegiendo así tu aplicación de datos erróneos o maliciosos.

## Exploración de Pipes

Nest.js proporciona una amplia gama de pipes ya preparados para diversas necesidades de validación y transformación. Explora todos los pipes disponibles para aprovechar al máximo las capacidades de Nest.js.

## Ejemplo Completo en un Controlador

```typescript
// src/controllers/products.controller.ts
import { Controller, Get, Param, ParseIntPipe } from '@nestjs/common';
import { ProductsService } from '../services/products.service';

@Controller('products')
export class ProductsController {
  constructor(private readonly productsService: ProductsService) {}

  @Get(':id')
  get(@Param('id', ParseIntPipe) id: number) {
    return this.productsService.findOne(id);
  }
}
```

En este ejemplo, el pipe `ParseIntPipe` se utiliza para asegurar que el parámetro `id` es un número entero antes de pasar los datos al servicio correspondiente.
