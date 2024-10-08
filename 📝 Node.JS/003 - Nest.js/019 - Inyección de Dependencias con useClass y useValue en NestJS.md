# Inyección de Dependencias con useClass y useValue en NestJS

NestJS posee diferentes formas de [inyectar](018%20-%20Inyección%20de%20Dependencias%20en%20NestJS.md) servicios en un módulo según la necesidad. Exploremos algunas de ellas, sus diferencias y cuándo utilizarlas.

## Cómo hacer la inyección con `useClass`

Cuando realizas un import de un servicio en un módulo:

```typescript
import { AppService } from './app.service';

@Module({
  providers: [AppService],
})
export class AppModule {}
```

Internamente, NestJS realiza lo siguiente:

```typescript
import { AppService } from './app.service';

@Module({
  providers: [
    {
      provide: AppService,
      useClass: AppService
    }
  ]
})
export class AppModule {}
```

Ambas sintaxis son equivalentes; `useClass` es el tipo de inyección por defecto. Básicamente, indica que un servicio debe utilizar una clase específica para funcionar. Si el día de mañana, por algún motivo en tu aplicación, el servicio `AppService` queda obsoleto y tienes que reemplazarlo por uno nuevo, puedes realizar lo siguiente:

```typescript
import { AppService2 } from './app.service';

@Module({
  providers: [
    {
      provide: AppService,
      useClass: AppService2
    }
  ]
})
export class AppModule {}
```

De este modo, no tienes necesidad de cambiar el nombre `AppService` en todos los controladores donde se utiliza, este será reemplazado por la nueva versión del servicio.

## Cómo hacer la inyección con `useValue`

Además de clases, puedes inyectar valores como un string o un número. `useValue` suele utilizarse para inyectar globalmente en tu aplicación la llave secreta de una API o alguna otra variable de entorno que tu app necesita.

Para esto, simplemente inyecta el valor de una constante en el `providers`:

```typescript
const API_KEY = '1324567890';

@Module({
  providers: [
    {
      provide: 'API_KEY',
      useValue: API_KEY
    }
  ],
})
export class AppModule {}
```

Importa este valor en los controladores u otros servicios donde se necesite de la siguiente manera:

```typescript
import { Controller, Inject } from '@nestjs/common';

@Controller()
export class AppController {
  constructor(@Inject('API_KEY') private apiKey: string) {}
}
```

Ahora tienes a disposición el valor de este dato en tu controlador para utilizarlo en lo que necesites.

## Ejemplo de código para inyección de servicios

```typescript
// src/app.module.ts
...

const API_KEY = '12345634';
const API_KEY_PROD = 'PROD1212121SA';

@Module({
  imports: [UsersModule, ProductsModule],
  controllers: [AppController],
  providers: [
    AppService,
    {
      provide: 'API_KEY',
      useValue: process.env.NODE_ENV === 'prod' ? API_KEY_PROD : API_KEY,
    },
  ],
})
export class AppModule {}

// src/app.service.ts
import { Injectable, Inject } from '@nestjs/common';

@Injectable()
export class AppService {
  constructor(@Inject('API_KEY') private apiKey: string) {} // 👈 Inject API_KEY
  getHello(): string {
    return `Hello World! ${this.apiKey}`;
  }
}

// src/app.controller.ts
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string { // 👈 new endpoint
    return this.appService.getHello();
  }
}
```
