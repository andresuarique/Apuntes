# Creación de Entidades en NestJS con TypeORM

Para crear y utilizar entidades en tu aplicación NestJS con TypeORM, sigue estos pasos:

## Paso 1: Definir una entidad

Una entidad en TypeORM es una clase de TypeScript decorada con `@Entity()` y otros decoradores para definir sus columnas y relaciones. Aquí hay un ejemplo de una entidad `Product`:

```typescript
// src/products/entities/product.entity.ts
import { PrimaryGeneratedColumn, Column, Entity } from 'typeorm';

@Entity()
export class Product {
  @PrimaryGeneratedColumn()
  id: number;

  @Column({ type: 'varchar', length: 255, unique: true })
  name: string;

  @Column({ type: 'text' })
  description: string;

  @Column({ type: 'int' })
  price: number;

  @Column({ type: 'int' })
  stock: number;

  @Column({ type: 'varchar' })
  image: string;
}
```

## Paso 2: Configurar el módulo para incluir la entidad

Para que TypeORM reconozca y gestione la entidad, debes incluirla en el módulo correspondiente utilizando `TypeOrmModule.forFeature()`. Aquí tienes un ejemplo de cómo hacerlo en el módulo `ProductsModule`:

```typescript
// src/products/products.module.ts
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';

import { Product } from './entities/product.entity';
import { ProductsController } from './products.controller';
import { ProductsService } from './products.service';
import { CategoriesController } from './categories.controller';
import { BrandsController } from './brands.controller';
import { BrandsService } from './brands.service';
import { CategoriesService } from './categories.service';

@Module({
  imports: [TypeOrmModule.forFeature([Product])], // 👈 Incluir entidades
  controllers: [ProductsController, CategoriesController, BrandsController],
  providers: [ProductsService, BrandsService, CategoriesService],
  exports: [ProductsService],
})
export class ProductsModule {}
```

## Detalles Importantes:

- **`TypeOrmModule.forFeature([Product])`:** Este método registra la entidad `Product` en el contexto de este módulo, lo que permite a TypeORM trabajar con la base de datos y gestionar las operaciones CRUD para esta entidad.
- **Controllers y Services:** Aunque no son el enfoque principal aquí, es importante incluir tus controladores y servicios en el módulo para asegurar que tu aplicación esté completamente funcional.

### Ejemplo de Uso de la Entidad en un Servicio

Una vez que la entidad está configurada, puedes inyectar el repositorio de TypeORM para la entidad en tu servicio y realizar operaciones de base de datos. Aquí tienes un ejemplo de cómo hacerlo en el servicio `ProductsService`:

```typescript
// src/products/products.service.ts
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { Product } from './entities/product.entity';

@Injectable()
export class ProductsService {
  constructor(
    @InjectRepository(Product)
    private readonly productRepository: Repository<Product>,
  ) {}

  findAll(): Promise<Product[]> {
    return this.productRepository.find();
  }

  findOne(id: number): Promise<Product> {
    return this.productRepository.findOne(id);
  }

  create(product: Product): Promise<Product> {
    return this.productRepository.save(product);
  }

  async update(id: number, product: Partial<Product>): Promise<Product> {
    await this.productRepository.update(id, product);
    return this.productRepository.findOne(id);
  }

  async remove(id: number): Promise<void> {
    await this.productRepository.delete(id);
  }
}
```
