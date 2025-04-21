# Configuración de TypeORM en NestJS

## Paso 1: Instalación de TypeORM y @nestjs/typeorm

Asegúrate de tener instaladas las siguientes dependencias:

```bash
npm install --save @nestjs/typeorm typeorm
```

## Paso 2: Configuración en el módulo de la base de datos

En tu módulo de base de datos (`database.module.ts`), importa `TypeOrmModule` y configúralo utilizando `forRootAsync` para manejar configuraciones asíncronas, como conexiones basadas en configuraciones dinámicas:

```typescript
// src/database/database.module.ts

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { ConfigModule, ConfigService } from '@nestjs/config'; // Importa ConfigModule y ConfigService si las estás utilizando

@Module({
  imports: [
    TypeOrmModule.forRootAsync({
      imports: [ConfigModule], // Importa ConfigModule si usas ConfigService
      inject: [ConfigService], // Especifica las dependencias que necesita la factory
      useFactory: async (configService: ConfigService) => ({
        type: 'postgres', // Tipo de base de datos (en este caso PostgreSQL)
        host: configService.get('POSTGRES_HOST'), // Variables de entorno o configuración
        port: configService.get('POSTGRES_PORT'),
        username: configService.get('POSTGRES_USER'),
        password: configService.get('POSTGRES_PASSWORD'),
        database: configService.get('POSTGRES_DB'),
        entities: [__dirname + '/../**/*.entity{.ts,.js}'], // Ruta donde se encuentran las entidades
        synchronize: true, // Sincroniza las entidades con la base de datos (NO usar en producción)
      }),
      inject: [ConfigService], // Especifica las dependencias que necesita la factory
    }),
  ],
  exports: [TypeOrmModule], // Exporta TypeOrmModule para ser utilizado en otros módulos
})
export class DatabaseModule {}
```

## Detalles a considerar:
- **Configuración dinámica:** Se utiliza `ConfigService` para obtener los datos de configuración de entorno o variables de configuración.
- **Entidades:** Especifica las entidades que deben ser gestionadas por TypeORM. Puedes utilizar el patrón `**/*.entity{.ts,.js}` para incluir todas las entidades en una carpeta.
- **Sincronización:** La opción `synchronize: true` sincroniza automáticamente el esquema de la base de datos con las definiciones de las entidades. Esto es útil en desarrollo, pero no se recomienda en producción debido a posibles pérdidas de datos.

## Paso 3: Uso en otros módulos

Una vez configurado el módulo de base de datos, puedes importarlo en otros módulos donde necesites acceder a TypeORM y sus entidades:

```typescript
// src/app.module.ts

import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { DatabaseModule } from './database/database.module';

@Module({
  imports: [
    TypeOrmModule.forRoot(), // Asegúrate de importar TypeOrmModule.forRoot() si no usas configuración asíncrona
    DatabaseModule,
    // Otros módulos de tu aplicación
  ],
  controllers: [],
  providers: [],
})
export class AppModule {}
```

**ver [[ORM]]**