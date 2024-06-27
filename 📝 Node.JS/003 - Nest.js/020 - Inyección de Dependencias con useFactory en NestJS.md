# Inyección de Dependencias con useFactory en NestJS

NestJS permite inyecciones de servicios o datos que necesiten de alguna petición HTTP o algún proceso asíncrono.

## Inyecciones Asíncronas

El tipo de inyección `useFactory` permite que realices un proceso asíncrono para inyectar un servicio o datos provenientes de una API.

A partir de NestJS v8, el servicio `HttpService` importado desde `@nestjs/common` fue deprecado. Instala la dependencia `@nestjs/axios` e impórtalo desde ahí. No deberás realizar ningún otro cambio en tu código. También debes asegurarte de importar el módulo `HttpModule` desde la misma dependencia.

```typescript
import { HttpService } from '@nestjs/axios';

@Module({
  providers: [
    {
      provide: 'DATA',
      useFactory: async (http: HttpService) => {
        return await http.get('').toPromise();
      },
      inject: [HttpService],
    },
  ],
})
export class AppModule {}
```

La propiedad `inject` permite que inyectes dentro de esta función asíncrona del `useFactory` otros servicios que este pueda necesitar. En el ejemplo anterior, se está haciendo una llamada a un request para obtener datos.

Importa estos datos en el controlador que lo necesite de la siguiente manera:

```typescript
import { Controller, Inject } from '@nestjs/common';

@Controller()
export class AppController {
  constructor(@Inject('DATA') private data: any[]) {}
}
```

Así podrás hacer uso de estos datos que fueron cargados de forma asíncrona.

Ten en cuenta que, al realizar una solicitud asíncrona, el controlador dependerá de la finalización de este proceso para estar disponible, pudiendo retrasar el inicio de tu aplicación. Esta funcionalidad suele utilizarse para conexiones de base de datos o procesos asíncronos similares.

## Ejemplo de código para inyección de servicios `useFactory`

```typescript
// src/app.module.ts
import { Module } from '@nestjs/common';
import { HttpModule, HttpService } from '@nestjs/axios';  // 👈 imports
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UsersModule } from './users/users.module';
import { ProductsModule } from './products/products.module';

@Module({
  imports: [HttpModule, UsersModule, ProductsModule], // 👈 add HttpModule
  controllers: [AppController],
  providers: [
    AppService,
    {
      provide: 'TASKS',
      useFactory: async (http: HttpService) => { // 👈 implement useFactory
        const tasks = await http
          .get('https://jsonplaceholder.typicode.com/todos')
          .toPromise();
        return tasks.data;
      },
      inject: [HttpService],
    },
  ],
})
export class AppModule {}

// src/app.service.ts
import { Injectable, Inject } from '@nestjs/common';

@Injectable()
export class AppService {
  constructor(
    @Inject('API_KEY') private apiKey: string,
    @Inject('TASKS') private tasks: any[], // 👈 inject TASKS
  ) {}
  getHello(): string {
    console.log(this.tasks); // 👈 print TASKS
    return `Hello World! ${this.apiKey}`;
  }
}
```
