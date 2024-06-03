# CORS (Cross-Origin Resource Sharing)

## ¿Qué es CORS?

CORS, o Cross-Origin Resource Sharing (Compartir Recursos de Origen Cruzado), es una política de seguridad implementada en los navegadores web que restringe las solicitudes de recursos desde un origen (dominio, protocolo y puerto) hacia otro origen diferente al que pertenece la página web actualmente cargada.

## Importancia de CORS

La política de CORS es fundamental para la seguridad de las aplicaciones web, ya que previene que sitios maliciosos realicen solicitudes no autorizadas en nombre de un usuario autenticado a otro sitio web. Sin CORS, un sitio web podría hacer que el navegador de un usuario envíe solicitudes a un servidor diferente y acceda a sus datos sensibles.

## Funcionamiento de CORS

### Concepto Básico

Cuando una aplicación web en un navegador intenta realizar una solicitud [HTTP](HTTP.md) a un servidor que tiene un origen diferente (diferente dominio, protocolo o puerto) al de la aplicación, el navegador aplica la política de CORS. Dependiendo de cómo esté configurado el servidor, la solicitud será permitida o rechazada.

### Cabeceras HTTP en CORS

Para que un servidor permita solicitudes desde orígenes cruzados, debe incluir ciertas cabeceras HTTP en sus respuestas:

- `Access-Control-Allow-Origin`: Especifica qué orígenes pueden acceder a los recursos. Puede ser un origen específico o un asterisco (`*`) para permitir todos los orígenes.
- `Access-Control-Allow-Methods`: Indica los métodos HTTP permitidos (GET, POST, PUT, DELETE, etc.).
- `Access-Control-Allow-Headers`: Lista las cabeceras permitidas en la solicitud.
- `Access-Control-Allow-Credentials`: Indica si las credenciales (cookies, cabeceras de autenticación) pueden ser incluidas en la solicitud.

### Tipos de Solicitudes CORS

1. **Simple Requests (Solicitudes Simples)**:
   - Métodos permitidos: GET, POST, HEAD.
   - Cabeceras permitidas: `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` (con valores `application/x-www-form-urlencoded`, `multipart/form-data`, o `text/plain`).
   - No se requiere una solicitud previa de verificación (preflight).

2. **Preflight Requests (Solicitudes Previa)**:
   - Métodos distintos a GET, POST, HEAD o si se utilizan cabeceras personalizadas.
   - El navegador envía una solicitud de verificación `OPTIONS` antes de la solicitud real para verificar si está permitida.
   - La solicitud de verificación incluye las cabeceras `Access-Control-Request-Method` y `Access-Control-Request-Headers`.

### Ejemplo de Flujo de CORS

1. **Solicitud Preflight**:
   - El navegador envía una solicitud `OPTIONS`:
```http
OPTIONS /api/resource HTTP/1.1
Host: api.example.com
Origin: https://www.example.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: Content-Type
```

2. **Respuesta del Servidor a la Solicitud Preflight**:
   - El servidor responde con las cabeceras de CORS permitidas:
```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://www.example.com
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: Content-Type
```

3. **Solicitud Real**:
   - Si la solicitud preflight es exitosa, el navegador envía la solicitud real:
```http
POST /api/resource HTTP/1.1
Host: api.example.com
Origin: https://www.example.com
Content-Type: application/json

{ "data": "example" }
```

4. **Respuesta del Servidor a la Solicitud Real**:
   - El servidor responde con los datos solicitados y las cabeceras de CORS permitidas:
```http
HTTP/1.1 200 OK
Content-Type: application/json
Access-Control-Allow-Origin: https://www.example.com

{ "response": "success" }
```
