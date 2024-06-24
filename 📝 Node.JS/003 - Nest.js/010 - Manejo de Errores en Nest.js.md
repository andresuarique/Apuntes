#  Manejo de Errores en Nest.js

Nest.js implementa de forma muy sencilla la posibilidad de responder con errores al cliente que realiza las consultas. Esto lo hace con una serie de clases que implementan los [códigos HTTP](../../🌐%20ConceptosGenerales/Códigos%20de%20Estado%20HTTP.md) correctos dependiendo del tipo de error que necesites.

## Ejemplo Básico de Manejo de Errores

Importando `NotFoundException` puedes arrojar un error con la palabra reservada `throw` indicando que un registro no fue encontrado. Esta excepción cambiará el estado HTTP 200 que envía el decorador `@HttpCode(HttpStatus.OK)` por un 404, que es el correspondiente para la ocasión.

```typescript
import { NotFoundException, HttpCode, HttpStatus, Get, Param } from '@nestjs/common';

@Get('product/:idProduct')
@HttpCode(HttpStatus.OK)
async getProduct(@Param('idProduct') idProduct: string): Promise<string> {
  const product = await this.appService.getProducto(idProduct);
  if (!product) {
    throw new NotFoundException(`Producto con ID #${idProduct} no encontrado.`);
  }
  return product;
}
```

## Lanzar Errores de Permisos

También puedes lanzar errores cuando el usuario no tiene permisos para acceder a un recurso.

```typescript
import { ForbiddenException, Get, Param, HttpCode, HttpStatus } from '@nestjs/common';

@Get('product/:idProduct')
@HttpCode(HttpStatus.OK)
async getProduct(@Param('idProduct') idProduct: string): Promise<string> {
  // ...
  throw new ForbiddenException(`Acceso prohibido a este recurso.`);
}
```

## Lanzar Errores del Servidor

O incluso lanzar errores de la familia del 5XX cuando ocurre un error inesperado en el servidor.

```typescript
import { InternalServerErrorException, Get, Param, HttpCode, HttpStatus } from '@nestjs/common';

@Get('product/:idProduct')
@HttpCode(HttpStatus.OK)
async getProduct(@Param('idProduct') idProduct: string): Promise<string> {
  // ...
  throw new InternalServerErrorException(`Ha ocurrido un error inesperado.`);
}
```

## Exploración de Clases de Errores

Nest.js proporciona una amplia gama de clases de excepción para manejar correctamente los errores en tus endpoints de manera profesional. Algunas de estas clases son:
- `BadRequestException`
- `UnauthorizedException`
- `ForbiddenException`
- `NotFoundException`
- `ConflictException`
- `InternalServerErrorException`
- Entre otras.

## Uso en Servicios

Aquí tienes un ejemplo de cómo usar estas excepciones en un servicio:

```typescript
// src/services/products.service.ts
import { Injectable, NotFoundException } from '@nestjs/common';

@Injectable()
export class ProductsService {
  private products = [];

  findOne(id: number) {
    const product = this.products.find((item) => item.id === id);
    if (!product) {
      throw new NotFoundException(`Product #${id} not found`);
    }
    return product;
  }

  update(id: number, payload: any) {
    const product = this.findOne(id);
    const index = this.products.findIndex((item) => item.id === id);
    this.products[index] = {
      ...product,
      ...payload,
    };
    return this.products[index];
  }

  remove(id: number) {
    const index = this.products.findIndex((item) => item.id === id);
    if (index === -1) {
      throw new NotFoundException(`Product #${id} not found`);
    }
    this.products.splice(index, 1);
    return true;
  }
}
```

## Uso en Controladores

Y cómo integrar estas excepciones en un controlador:

```typescript
// src/controllers/products.controller.ts
import { Controller, Delete, Param } from '@nestjs/common';
import { ProductsService } from '../services/products.service';

@Controller('products')
export class ProductsController {
  constructor(private readonly productsService: ProductsService) {}

  @Delete(':id')
  delete(@Param('id') id: string) {
    return this.productsService.remove(+id);
  }
}
```
