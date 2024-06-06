# JWT (JSON Web Token)

**JWT (JSON Web Token)** es una tecnología utilizada para la [autenticación y autorización](Autenticación%20vs%20Autorización.md) de usuarios en aplicaciones web. Los tokens JWT permiten verificar la identidad de los usuarios y conceder acceso a recursos protegidos.

## Funcionamiento de JWT

Anteriormente, la autenticación se gestionaba a través de sesiones que se almacenaban en cookies y se guardaban en el servidor o en la base de datos. Esto presentaba desafíos, especialmente en sistemas distribuidos, donde la sesión podría perderse si el usuario se conectaba a un servidor diferente.

![Pasted image 20240606172925](ANEXOS/Pasted%20image%2020240606172925.png)

**Ventajas de JWT**:
- **Stateless**: No se almacena en memoria ni en bases de datos. El token en sí contiene toda la información necesaria para verificar la identidad y los permisos del usuario.
- **Escalabilidad**: Facilita la distribución del sistema, permitiendo balancear la carga entre múltiples servidores sin perder la sesión.
- **Soporte para diferentes clientes**: Los JWT pueden ser utilizados en aplicaciones web, móviles y otros clientes sin cambios significativos.

## Estructura de un JWT

Un JWT se compone de tres partes, cada una separada por un punto:

1. **Header**:
   - Contiene información sobre el tipo de token y el algoritmo de encriptación.
   - Ejemplo: `{"alg": "HS256", "typ": "JWT"}`

2. **Payload**:
   - Contiene los datos que se quieren transmitir, como el identificador del usuario (sub), el nombre, y la fecha de emisión (iat).
   - Ejemplo: `{"sub": "1234567890", "name": "John Doe", "iat": 1516239022}`

3. **Signature**:
   - Verifica que el token no ha sido alterado. Combina el header y el payload, y se firma con una clave secreta.
   - Ejemplo: `HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secret)`

Ejemplo de un JWT completo:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

## Beneficios de Utilizar JWT

1. **Seguridad**: Al estar firmados, solo quien posee la clave secreta puede generar y verificar tokens, asegurando que la información no ha sido alterada.
2. **Flexibilidad**: Pueden ser utilizados en diversas aplicaciones y con diferentes clientes, mejorando la interoperabilidad.
3. **Desempeño**: Al no requerir almacenamiento en el servidor, se reducen las cargas en el backend y se mejora la velocidad de las aplicaciones.

## Página Oficial de JWT

Para más información y herramientas relacionadas con JWT, se puede visitar la [página oficial de JWT](https://jwt.io/).