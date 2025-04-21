# Uso de Repositorios en TypeORM con NestJS

Para utilizar repositorios en TypeORM con NestJS, necesitas inyectar el repositorio correspondiente a tu entidad y usarlo para realizar operaciones CRUD. Aquí te muestro cómo hacerlo paso a paso:

## Paso 1: Configurar TypeORM en el Módulo de Base de Datos

Primero, asegúrate de que tu módulo de base de datos esté configurado correctamente para usar TypeORM. Puedes hacerlo en el archivo `database.module.ts`:

```typescript
// src/database/database.module.ts
import { Module, Global } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { ConfigType } from '@nestjs/config';
import config from '../config';

@Global()
@Module({
  imports: [
    TypeOrmModule.forRootAsync({
      inject: [config.KEY],
      useFactory: (configService: ConfigType<typeof config>) => {
        const { user, host, dbName, password, port } = configService.postgres;
        return {
          type: 'postgres',
          host,
          port,
          username: user,
          password,
          database: dbName,
          synchronize: true, // 👈 Sincronizar entidades automáticamente
          autoLoadEntities: true, // 👈 Cargar entidades automáticamente
        };
      },
    }),
  ],
  exports: [TypeOrmModule],
})
export class DatabaseModule {}
```

## Paso 2: Inyectar el Repositorio en tu Servicio

Luego, inyecta el repositorio en tu servicio y usa los métodos del repositorio para realizar operaciones CRUD. Aquí tienes un ejemplo de cómo hacerlo en el servicio `ProductsService`:

```typescript
// src/products/services/products.service.ts
import { Injectable, NotFoundException } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';

import { Product } from './../entities/product.entity';
import { CreateProductDto, UpdateProductDto } from './../dtos/products.dtos';

@Injectable()
export class ProductsService {
  constructor(
    @InjectRepository(Product) private productRepo: Repository<Product>, // 👈 Inyectar Repositorio
  ) {}

  findAll() {
    return this.productRepo.find();  // 👈 Usar Repositorio
  }

  async findOne(id: number) {
    const product = await this.productRepo.findOne(id);  // 👈 Usar Repositorio
    if (!product) {
      throw new NotFoundException(`Product #${id} not found`);
    }
    return product;
  }

  async create(data: CreateProductDto) {
    const newProduct = this.productRepo.create(data);
    return this.productRepo.save(newProduct);
  }

  async update(id: number, changes: UpdateProductDto) {
    const product = await this.findOne(id);
    this.productRepo.merge(product, changes);
    return this.productRepo.save(product);
  }

  async remove(id: number) {
    const product = await this.findOne(id);
    return this.productRepo.remove(product);
  }
}
```

## Paso 3: Usar el Servicio en Otro Servicio

Puedes inyectar y usar el servicio `ProductsService` en otros servicios para realizar operaciones complejas. Aquí tienes un ejemplo de cómo hacerlo en el servicio `UsersService`:

```typescript
// src/users/services/users.service.ts
import { Injectable } from '@nestjs/common';
import { ProductsService } from '../products/services/products.service';

@Injectable()
export class UsersService {
  constructor(private productsService: ProductsService) {}

  async getOrderByUser(id: number) {
    const user = await this.findOne(id);
    return {
      date: new Date(),
      user,
      products: await this.productsService.findAll(),
    };
  }
}
```

### Resumen

1. **Configurar TypeORM:** Asegúrate de que tu módulo de base de datos esté configurado correctamente para usar TypeORM.
2. **Inyectar el Repositorio:** Inyecta el repositorio correspondiente en tu servicio utilizando `@InjectRepository`.
3. **Usar el Repositorio:** Usa los métodos del repositorio para realizar operaciones CRUD.
4. **Usar Servicios en Otros Servicios:** Inyecta y usa servicios en otros servicios para realizar operaciones complejas.
