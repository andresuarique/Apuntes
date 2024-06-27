# Interacción entre Módulos en NestJS

Dentro de un módulo, puedes tener la necesidad de utilizar un servicio que pertenece a otro módulo. Importar estos servicios en otros módulos requiere de un paso adicional.

## Importaciones de Servicios Compartidos

Si tienes un Módulo A que posee un Servicio A y un segundo Módulo B requiere hacer uso de este, debes exportar el servicio para que otro módulo pueda utilizarlo.

```typescript
// Módulo A
import { ServiceA } from './service-A.service';

@Module({
  providers: [ServiceA],
  exports: [ServiceA]
})
export class ModuleA {}
```

```typescript
// Módulo B
import { ServiceA } from './module-A/service-A.service';

@Module({
  providers: [ServiceA]
})
export class ModuleB {}
```

Debes indicar en la propiedad `exports` del decorador `@Module()` que un módulo es exportable para que otro módulo pueda importarlo en sus `providers`.

De esta manera, evitas errores de compilación de tu aplicación que ocurren cuando importas servicios de otros módulos que no están siendo exportados correctamente.

## Ejemplo de Interacción entre Módulos

A continuación, podrás ver el código que necesitas para hacer que los módulos interactúen entre sí.

```typescript
// src/users/entities/order.entity.ts
import { User } from './user.entity';
import { Product } from './../../products/entities/product.entity';

export class Order { // 👈 new entity
  date: Date;
  user: User;
  products: Product[];
}
```

```typescript
// src/users/controllers/users.controller.ts
  @Get(':id/orders') //  👈 new endpoint
  getOrders(@Param('id', ParseIntPipe) id: number) {
    return this.usersService.getOrderByUser(id);
  }
```

```typescript
// src/users/services/users.service.ts

import { Injectable } from '@nestjs/common';
import { Order } from '../entities/order.entity';
import { ProductsService } from './../../products/services/products.service';

@Injectable()
export class UsersService {
  constructor(private productsService: ProductsService) {}

  getOrderByUser(id: number): Order { // 👈 new method
    const user = this.findOne(id);
    return {
      date: new Date(),
      user,
      products: this.productsService.findAll(),
    };
  }
}
```

```typescript
// src/products/products.module.ts

import { Module } from '@nestjs/common';
import { ProductsController } from './controllers/products.controller';
import { BrandsController } from './controllers/brands.controller';
import { CategoriesController } from './controllers/categories.controller';
import { ProductsService } from './services/products.service';
import { BrandsService } from './services/brands.service';
import { CategoriesService } from './services/categories.service';

@Module({
  controllers: [ProductsController, CategoriesController, BrandsController],
  providers: [ProductsService, BrandsService, CategoriesService],
  exports: [ProductsService], // 👈 Export ProductsService
})
export class ProductsModule {}
```

```typescript
// src/users/users.module.ts

import { Module } from '@nestjs/common';
import { CustomerController } from './controllers/customers.controller';
import { CustomersService } from './services/customers.service';
import { UsersController } from './controllers/users.controller';
import { UsersService } from './services/users.service';
import { ProductsModule } from '../products/products.module';

@Module({
  imports: [ProductsModule], // 👈 Import ProductsModule
  controllers: [CustomerController, UsersController],
  providers: [CustomersService, UsersService],
})
export class UsersModule {}
```
