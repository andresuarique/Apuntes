# Data Transfer Objects (DTO) en Nest.js

Nest.js utiliza el concepto de Objetos de Transferencia de Datos (DTO, por sus siglas en inglés) para el tipado de datos y su segurización.

## Qué son los Objetos de Transferencia de Datos

Los DTO son clases personalizadas que puedes crear para indicar la estructura que tendrán los objetos de entrada en una solicitud. Ayudan a asegurar que los datos recibidos en las peticiones HTTP tengan el formato y los tipos esperados.

## 1. Creando DTO

Crea un nuevo archivo con la extensión `.dto.ts` para indicar que se trata de un DTO.

```typescript
// src/dtos/products.dto.ts
export class CreateProductDTO {
  readonly name: string;
  readonly description: string;
  readonly price: number;
  readonly image: string;
}
```

La palabra reservada `readonly` es propia de TypeScript y asegura que dichos datos no sean modificados.

Crea tantos atributos como necesites para tu clase `CreateProductDTO`.

## 2. Importando DTO

Importa la clase en tu controlador para tipar el `Body` del endpoint `POST` para la creación de un producto.

```typescript
import { Controller, Post, Body } from '@nestjs/common';
import { CreateProductDTO } from 'src/dtos/products.dto.ts';

@Controller('products')
export class ProductsController {
  @Post('product')
  createProducto(@Body() body: CreateProductDTO): any {
    // ...
  }
}
```

De esta forma, ya conoces la estructura de datos que tendrá el parámetro `body` previo a la creación de un producto.

## Ejemplo Completo

### Definición de DTOs

```typescript
// src/dtos/products.dto.ts
export class CreateProductDto {
  readonly name: string;
  readonly description: string;
  readonly price: number;
  readonly stock: number;
  readonly image: string;
}

export class UpdateProductDto {
  readonly name?: string;
  readonly description?: string;
  readonly price?: number;
  readonly stock?: number;
  readonly image?: string;
}
```

### Uso de DTOs en el Controlador

```typescript
// src/controllers/products.controller.ts
import { Controller, Post, Put, Param, Body } from '@nestjs/common';
import { CreateProductDto, UpdateProductDto } from 'src/dtos/products.dto.ts';
import { ProductsService } from 'src/services/products.service.ts';

@Controller('products')
export class ProductsController {
  constructor(private readonly productsService: ProductsService) {}

  @Post()
  create(@Body() payload: CreateProductDto) {
    return this.productsService.create(payload);
  }

  @Put(':id')
  update(
    @Param('id') id: string,
    @Body() payload: UpdateProductDto,
  ) {
    return this.productsService.update(+id, payload);
  }
}
```

### Uso de DTOs en el Servicio

```typescript
// src/services/products.service.ts
import { Injectable } from '@nestjs/common';
import { CreateProductDto, UpdateProductDto } from 'src/dtos/products.dto.ts';

@Injectable()
export class ProductsService {
  private products = [];

  create(payload: CreateProductDto) {
    const newProduct = { id: Date.now(), ...payload };
    this.products.push(newProduct);
    return newProduct;
  }

  update(id: number, payload: UpdateProductDto) {
    const productIndex = this.products.findIndex(p => p.id === id);
    if (productIndex > -1) {
      const updatedProduct = { ...this.products[productIndex], ...payload };
      this.products[productIndex] = updatedProduct;
      return updatedProduct;
    }
    return null;
  }
}
```
