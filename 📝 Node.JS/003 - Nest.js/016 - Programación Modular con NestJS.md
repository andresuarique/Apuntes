# Programación Modular con NestJS

Las aplicaciones profesionales que se desarrollan con NestJS se realizan de forma [modularizada](../../🌐%20ConceptosGenerales/Programación%20Modular.md) para dividir el código fuente de forma lógica y que el proyecto sea más escalable y comprensible.

#### Cómo hacer la modularización de un proyecto en NestJS

Para modularizar una aplicación, el CLI de NestJS trae consigo la posibilidad de autogenerar módulos con el comando `nest generate module <module-name>` o en su forma corta `nest g mo <module-name>`.

Los módulos son simples clases que utilizan el decorador `@Module()` para importar todo lo que construyan al mismo.

```typescript
import { Module } from '@nestjs/common';

@Module({
  imports: [],             // Importación de otros módulos
  controllers: [],         // Importación de controladores
  providers: [],           // Importación de servicios
})
export class PruebaModule {}
```

De esta manera, un módulo agrupará un conjunto de controladores y servicios, además de importar otros módulos.

A partir de aquí, tu aplicación podría tener un módulo para usuarios, otro para productos, otro para comentarios, etc. Crea tantos módulos como tu aplicación necesite.

#### Ejemplo de modularización de una aplicación

En las siguientes imágenes te mostramos cómo debería quedar organizada la aplicación:

![Pasted image 20240627101452](📎%20ANEXOS/Pasted%20image%2020240627101452.png)

Donde los módulos deberían quedar así:

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
  exports: [ProductsService],
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
  imports: [ProductsModule],
  controllers: [CustomerController, UsersController],
  providers: [CustomersService, UsersService],
})
export class UsersModule {}
```

```typescript
// src/app.module.ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { ProductsModule } from './products/products.module';

@Module({
  imports: [UsersModule, ProductsModule],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```
