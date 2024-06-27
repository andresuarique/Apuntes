# Generar la Documentación con Swagger en NestJS

Una API profesional debe estar documentada. Cuando hablamos de documentación, nos suena a una tarea tediosa que nadie quiere realizar. Afortunadamente, NestJS permite automatizar fácilmente la creación de la misma.

## Cómo hacer la documentación API Rest

Swagger es un reconocido set de herramientas para la documentación de API Rest. Instala las dependencias necesarias con el comando:

```bash
npm install --save @nestjs/swagger swagger-ui-express
```

Configura el archivo `main.ts` con el siguiente código:

```typescript
// main.ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
    
  // Configuración Swagger en NestJS
  const config = new DocumentBuilder()
    .setTitle('Platzi API')
    .setDescription('Documentación Platzi API')
    .setVersion('1.0')
    .build();
  const document = SwaggerModule.createDocument(app, config);
  
  // URL API
  SwaggerModule.setup('docs', app, document);

  await app.listen(process.env.PORT || 3000);
}
bootstrap();
```

Setea el título, descripción y versión de tu documentación. Lo más importante es la URL para acceder a la misma.

Levanta el servidor con `npm run start:dev` y accede a `localhost:3000/docs` para visualizar la documentación autogenerada que mapea automáticamente todos los endpoints de tu aplicación.

## Tipado de la documentación

La documentación autogenerada por Swagger es bastante simple, puedes volverla más completa tipando los datos de entrada y salida de cada endpoint gracias a los DTO.

Busca el archivo `nest-cli.json` en la raíz de tu proyecto y agrega el siguiente plugin:

```json
{
  "$schema": "https://json.schemastore.org/nest-cli",
  "collection": "@nestjs/schematics",
  "sourceRoot": "src",
  "compileOptions": {
    "plugins": ["@nestjs/swagger"]
  }
}
```

A continuación, prepara tus DTO de la siguiente manera:

```typescript
import { IsNotEmpty, IsString, IsNumber } from 'class-validator';
import { ApiProperty, PartialType, OmitType } from '@nestjs/swagger';

export class CreateProductDTO {

  @ApiProperty()
  @IsNotEmpty()
  @IsString()
  readonly name: string;

  @ApiProperty()
  @IsNotEmpty()
  @IsString()
  readonly description: string;

  @ApiProperty()
  @IsNotEmpty()
  @IsNumber()
  readonly price: number;
}

export class UpdateProductDTO extends PartialType(
  OmitType(CreateProductDTO, ['name']),
) {}
```

Lo más relevante aquí es importar `PartialType` y `OmitType` desde `@nestjs/swagger` en lugar de importarlo desde `@nestjs/mapped-types`. Coloca también el decorador `@ApiProperty()` en cada una de las propiedades que el DTO necesita.

![Pasted image 20240627105843](📎%20ANEXOS/Pasted%20image%2020240627105843.png)

De esta manera, observarás en la documentación que indica el tipo de dato que requiere cada uno de tus endpoints.

## Cuadro de código para uso de Swagger

Instala las dependencias necesarias:

```bash
npm install --save @nestjs/swagger swagger-ui-express
```

Configura `main.ts`:

```typescript
// src/main.ts
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  const config = new DocumentBuilder()
    .setTitle('API')
    .setDescription('PLATZI STORE')
    .setVersion('1.0')
    .build();
  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('docs', app, document);
  await app.listen(3000);
}
bootstrap();
```

Actualiza `nest-cli.json`:

```json
{
  "collection": "@nestjs/schematics",
  "sourceRoot": "src",
  "compilerOptions": {
    "plugins": ["@nestjs/swagger/plugin"]
  }
}
```

Ejemplo de DTOs configurados para Swagger:

```typescript
// src/products/dtos/brand.dtos.ts
import { PartialType } from '@nestjs/swagger';

// src/products/dtos/category.dtos.ts
import { PartialType } from '@nestjs/swagger';

// src/products/dtos/products.dtos.ts
import { PartialType } from '@nestjs/swagger;

// src/users/dtos/customer.dto.ts
import { PartialType } from '@nestjs/swagger;

// src/users/dtos/user.dto.ts
import { PartialType } from '@nestjs/swagger;
```
