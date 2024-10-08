# Uso de Módulos Globales en NestJS

Al desarrollar una aplicación con NestJS, existen necesidades de importar módulos cruzados o de importar un mismo servicio en varios módulos. Lo anterior, hace que la cantidad de imports en cada módulo crezca y se vuelva complicado de escalar.

#### Cómo usar el módulo global

NestJS otorga la posibilidad de crear módulos globales que se importarán automáticamente en todos los otros módulos de la aplicación, sin necesidad de importarlos explícitamente.

```typescript
import { Module, Global } from '@nestjs/common';

@Global()
@Module({
  // ...
})
export class MyCustomModule {}
```

Todos los servicios que importes en este módulo, estarán disponibles para su utilización en cualquier otro módulo.

Es importante no abusar de esta característica y no tener más de un módulo global para controlar las importaciones. Pueden ocurrir errores de dependencias circulares que suceden cuando el Módulo A importa al Módulo B y este a su vez importa al Módulo A. El decorador `@Global()` te ayudará a resolver estos problemas.

#### Ejemplo de uso de módulo global

```typescript
// src/database/database.module.ts
import { Module, Global } from '@nestjs/common';

const API_KEY = '12345634';
const API_KEY_PROD = 'PROD1212121SA';

@Global()
@Module({
  providers: [
    {
      provide: 'API_KEY',
      useValue: process.env.NODE_ENV === 'prod' ? API_KEY_PROD : API_KEY,
    },
  ],
  exports: ['API_KEY'],
})
export class DatabaseModule {}

// src/app.module.ts
import { Module } from '@nestjs/common';
import { HttpModule } from '@nestjs/axios';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { ProductsModule } from './products/products.module';
import { DatabaseModule } from './database/database.module';

@Module({
  imports: [
    HttpModule,
    UsersModule,
    ProductsModule,
    DatabaseModule, // 👈 Use DatabaseModule like global Module
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}

// src/users/services/users.service.ts
import { Injectable, Inject } from '@nestjs/common';
import { ProductsService } from '../../products/services/products.service';

@Injectable()
export class UsersService {
  constructor(
    private productsService: ProductsService,
    @Inject('API_KEY') private apiKey: string, // 👈 Inject API_KEY
  ) {}
}
```
