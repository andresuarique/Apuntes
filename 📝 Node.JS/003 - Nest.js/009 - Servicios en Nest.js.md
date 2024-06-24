# Servicios en Nest.js

Los servicios son una pieza esencial de las aplicaciones realizadas con el framework Nest.js. Están pensados para **proporcionar una capa de acceso a los datos** que necesitan las aplicaciones para funcionar. Un servicio tiene la responsabilidad de gestionar el trabajo con los datos de la aplicación, realizando operaciones para obtener, modificar, y gestionar esos datos.

## Beneficios de los Servicios

- **Aislamiento de la lógica de negocio**: La lógica de negocio se aísla en una clase aparte.
- **Reutilización de código**: Facilita la reutilización del código de trabajo con los datos a lo largo de varios controladores.

## Creación de un Servicio

Para construir un servicio podemos usar el CLI de Nest. Para crear la clase de un servicio, se puede lanzar uno de los siguientes comandos:

```bash
nest generate service products
# o usando la abreviatura
nest g s products
```

Además, este comando realiza automáticamente la modificación del archivo `app.module.ts` para incluir el nuevo servicio.

## Decorador @Injectable

El decorador `@Injectable` permite inyectar el servicio en los controladores. Todo servicio debe tener este decorador antes de la declaración de la clase que lo implementa para poder usar la inyección de dependencias.

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class ProductsService {
  // Aquí se define la lógica del servicio
}
```

## Ejemplo de Uso

Aquí tienes un ejemplo básico de cómo definir y usar un servicio en Nest.js:

```typescript
// products.service.ts
import { Injectable } from '@nestjs/common';

@Injectable()
export class ProductsService {
  private products = [];

  findAll() {
    return this.products;
  }

  create(product) {
    this.products.push(product);
  }
}

// products.controller.ts
import { Controller, Get, Post, Body } from '@nestjs/common';
import { ProductsService } from './products.service';

@Controller('products')
export class ProductsController {
  constructor(private readonly productsService: ProductsService) {}

  @Get()
  findAll() {
    return this.productsService.findAll();
  }

  @Post()
  create(@Body() product: any) {
    this.productsService.create(product);
    return product;
  }
}
```

En este ejemplo, `ProductsService` gestiona una lista de productos y proporciona métodos para obtener y crear productos. El `ProductsController` utiliza este servicio para manejar las solicitudes HTTP.
