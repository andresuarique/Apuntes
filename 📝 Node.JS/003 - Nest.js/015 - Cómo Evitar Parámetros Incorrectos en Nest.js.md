# Cómo Evitar Parámetros Incorrectos en Nest.js

Los [Data Transfer Objects (DTO)](013%20-%20Data%20Transfer%20Objects%20(DTO)%20en%20Nest.js.md) no solo ayudan con el tipado y la validación de datos, sino que también indican la obligatoriedad de los mismos para que los registros se creen completos. Es fundamental evitar que haya datos que no deben estar en las solicitudes, ya que podrían ser ataques maliciosos.

## Prohibición de Datos Incorrectos

1. **Configuración Global en `main.ts`**

   El archivo `main.ts` contiene el bootstrap de tu aplicación, es decir, el punto inicial de la misma. Aquí se puede agregar la configuración necesaria para prohibir datos incorrectos.

   ```typescript
   // main.ts
   import { NestFactory } from '@nestjs/core';
   import { ValidationPipe } from '@nestjs/common';
   import { AppModule } from './app.module';

   async function bootstrap() {
     const app = await NestFactory.create(AppModule);
     app.useGlobalPipes(
       new ValidationPipe({
         whitelist: true,                    // Ignorar datos que no estén en los DTO
         forbidNonWhitelisted: true,         // Lanzar error si existen datos prohibidos
         disableErrorMessages: true,         // Deshabilitar mensajes de error (producción)
       })
     );
     await app.listen(process.env.PORT || 3000);
   }
   bootstrap();
   ```

2. **Parámetros del `ValidationPipe`**

   - `whitelist: true`: Esta opción hace que Nest.js ignore automáticamente cualquier propiedad que no esté definida en el DTO.
   - `forbidNonWhitelisted: true`: Si se reciben propiedades no definidas en el DTO, Nest.js lanzará una excepción y retornará un error.
   - `disableErrorMessages: true`: Deshabilita los mensajes de error en producción para evitar dar información adicional sobre la estructura interna de la API.

3. **Configuración del `ValidationPipe`**

   Importa `ValidationPipe` desde `@nestjs/common` y configura en `true` las propiedades `whitelist` y `forbidNonWhitelisted`. La propiedad `disableErrorMessages` es recomendable activarla solo en producción para no enviar mensajes de error y no dar información al front-end.

   ```typescript
   // src/main.ts

   app.useGlobalPipes(
     new ValidationPipe({
       whitelist: true,
       forbidNonWhitelisted: true,
       disableErrorMessages: true, // Opcional, solo en producción
     }),
   );
   ```

## Beneficios de Usar `ValidationPipe`

- **Seguridad Mejorada**: Al ignorar propiedades no definidas y lanzar errores para datos no permitidos, se reduce el riesgo de inyecciones y otros ataques maliciosos.
- **Claridad en los Errores**: Proporciona mensajes de error claros y específicos durante el desarrollo, mejorando la experiencia de desarrollo.
- **Conformidad de Datos**: Asegura que los datos recibidos siempre cumplen con la estructura esperada, evitando errores y malfuncionamientos en la aplicación.
