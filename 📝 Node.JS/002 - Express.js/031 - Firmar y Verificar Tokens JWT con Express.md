# Firmar y Verificar Tokens JWT con Express

## Instalación de la Librería JSON Web Token

Para trabajar con [JWT](JWT%20(JSON%20Web%20Token).md) en Express, se utiliza la librería `jsonwebtoken`. Se instala con el siguiente comando:

```sh
npm install jsonwebtoken
```

## Firmar un Token

Firmar un token implica generar un token que contiene un payload (información sobre el usuario) y una firma generada con una clave secreta.

**Ejemplo de Firma de un Token (token-sign.js):**

```javascript
const jwt = require('jsonwebtoken');

const secret = 'myCat'; // La clave secreta debe estar en variables de entorno
const payload = {
  sub: 1, // Identificador del usuario
  role: 'customer', // Rol del usuario
};

function signToken(payload, secret) {
  return jwt.sign(payload, secret);
}

const token = signToken(payload, secret);
console.log(token); // Ejemplo de salida: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjEsInJvbGUiOiJjdXN0b21lciIsImlhdCI6MTY0Mzk0NDgxM30.Z3MKuevzXLt0bixve06-Awn3OWYsqxU61NYtLrYq2Zg
```

**Importante:**
- La clave secreta (`secret`) debe almacenarse en una variable de entorno y no en el código fuente para asegurar su confidencialidad.
- El `payload` contiene la información que se quiere incluir en el token.

## Verificar un Token

Verificar un token implica comprobar que el token no ha sido modificado y que es válido, utilizando la misma clave secreta con la que fue firmado.

**Ejemplo de Verificación de un Token (token-verify.js):**

```javascript
const jwt = require('jsonwebtoken');

const secret = 'myCat';
const token =
  'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOjEsInJvbGUiOiJjdXN0b21lciIsImlhdCI6MTY0Mzk0NDgxM30.Z3MKuevzXLt0bixve06-Awn3OWYsqxU61NYtLrYq2Zg';

function verifyToken(token, secret) {
  return jwt.verify(token, secret);
}

const payload = verifyToken(token, secret);
console.log(payload); // Ejemplo de salida: { sub: 1, role: 'customer', iat: 1643944813 }
```

**Importante:**
- Cualquier persona que tenga el token puede ver la información del payload, por lo tanto, no se debe incluir información sensible como contraseñas o datos personales.
- La seguridad del token depende de la confidencialidad de la clave secreta.

## Uso del Refresh Token

Para manejar la expiración de los tokens y asegurar que los usuarios no tengan que autenticarse repetidamente, se puede utilizar un refresh token. Un refresh token es un token especial que se utiliza para obtener nuevos tokens de acceso.

1. **Acceso inicial**: Al autenticarse, el servidor genera un token de acceso (con una vida corta) y un refresh token (con una vida más larga).
2. **Expiración del token de acceso**: Cuando el token de acceso expira, el cliente usa el refresh token para solicitar un nuevo token de acceso.
3. **Expiración del refresh token**: Requiere que el usuario se vuelva a autenticar completamente.
