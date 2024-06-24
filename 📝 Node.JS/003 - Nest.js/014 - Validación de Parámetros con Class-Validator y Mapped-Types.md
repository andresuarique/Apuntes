# Validación de Parámetros con Class-Validator y Mapped-Types

Los [Data Transfer Objects (DTO) en Nest.js](013%20-%20Data%20Transfer%20Objects%20(DTO)%20en%20Nest.js.md) no solo sirven para tipar y determinar la estructura de los datos de entrada de un endpoint, también pueden contribuir en la validación de los datos y en la entrega de mensajes al front-end en caso de error en los mismos.

### Validación de Datos con DTO

1. **Instalación de Dependencias**

   Utiliza el comando `npm i class-validator class-transformer` para instalar dos dependencias que nos ayudarán en la validación de los datos. Estas librerías traen un set de decoradores para las propiedades de los DTO y así validar los tipos de datos de entrada.

2. **Decoradores de Validación**

   Importa y usa los decoradores de `class-validator` en tus DTOs:

   ```typescript
   import { IsNotEmpty, IsString, IsNumber, IsUrl } from 'class-validator';

   export class CreateProductDTO {
     @IsNotEmpty()
     @IsString()
     readonly name: string;
     
     @IsNotEmpty()
     @IsString()
     readonly description: string;
     
     @IsNotEmpty()
     @IsNumber()
     readonly price: number;
     
     @IsNotEmpty()
     @IsUrl()
     readonly image: string;
   }
   ```

3. **Respuesta del Servidor en Caso de Error**

   Si los datos enviados en la petición no cumplen con las validaciones, el servidor devolverá un mensaje con los errores:

   ```json
   {
     "statusCode": 400,
     "message": [
       "description should not be empty",
       "description must be a string",
       "image must be an URL address"
     ],
     "error": "Bad Request"
   }
   ```

### Reutilización de Código de los DTO

1. **Instalación de Dependencia**

   Instala la dependencia `@nestjs/mapped-types` con el comando `npm i @nestjs/mapped-types`.

2. **Uso de PartialType y OmitType**

   Importa `PartialType` y `OmitType` desde `@nestjs/mapped-types` para reutilizar y modificar DTOs existentes.

   ```typescript
   import { IsNotEmpty, IsString, IsNumber, IsUrl } from 'class-validator';
   import { PartialType, OmitType } from '@nestjs/mapped-types';

   export class CreateProductDTO {
     @IsNotEmpty()
     @IsString()
     readonly name: string;
     
     @IsNotEmpty()
     @IsString()
     readonly description: string;
     
     @IsNotEmpty()
     @IsNumber()
     readonly price: number;
     
     @IsNotEmpty()
     @IsUrl()
     readonly image: string;
   }

   export class UpdateProductDto extends PartialType(
     OmitType(CreateProductDTO, ['name']),
   ) {}
   ```

3. **Uso de DTOs en el Código**

   ```typescript
   // src/dtos/products.dtos.ts
   import {
     IsString,
     IsNumber,
     IsUrl,
     IsNotEmpty,
     IsPositive,
   } from 'class-validator';
   import { PartialType } from '@nestjs/mapped-types';

   export class CreateProductDto {
     @IsString()
     @IsNotEmpty()
     readonly name: string;

     @IsString()
     @IsNotEmpty()
     readonly description: string;

     @IsNumber()
     @IsNotEmpty()
     @IsPositive()
     readonly price: number;

     @IsNumber()
     @IsNotEmpty()
     @IsPositive()
     readonly stock: number;

     @IsUrl()
     @IsNotEmpty()
     readonly image: string;
   }

   export class UpdateProductDto extends PartialType(CreateProductDto) {}
   ```

4. **Configuración Global de Validación**

   ```typescript
   // src/main.ts
   import { ValidationPipe } from '@nestjs/common';

   async function bootstrap() {
     // ...
     app.useGlobalPipes(new ValidationPipe());
     // ...
   }
   bootstrap();
   ```
