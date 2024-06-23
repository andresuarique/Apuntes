# Controladores en Nest.js

### Función de los Controladores

Los controladores en Nest.js son los encargados de recibir los requests de nuestra aplicación. Estas requests son las peticiones que llegan a nuestra aplicación desde un cliente web, móvil, etc., a través del [protocolo HTTP](../../🌐%20ConceptosGenerales/HTTP.md).

### Responsabilidades de los Controladores

- Validar los requests, asegurando que sus permisos y datos sean correctos.
- Permitir el acceso a la capa de servicios según el resultado de la validación.
- Manejar los [verbos HTTP](../../🌐%20ConceptosGenerales/Métodos%20HTTP.md) para interactuar con los recursos.

### Verbos HTTP Utilizados

- **GET**: Obtener recursos.
- **PUT**: Actualizar recursos.
- **POST**: Crear recursos.
- **DELETE**: Eliminar recursos.

### Definición de Controladores

Los controladores se definen con una clase acompañada de un decorador, que indica el comportamiento de dicho controlador.

### Decoradores Comunes

- `@Controller()`: Define que la clase es un controlador.
- `@Get('nuevo-endpoint')`: Crea un nuevo endpoint.

### Ejemplo de Uso de Decoradores

Para declarar un nuevo endpoint en el controlador:

```typescript
@Controller('example')
export class ExampleController {
  @Get('nuevo-endpoint')
  newEndpoint() {
    return 'I am new endpoint';
  }
}
```
