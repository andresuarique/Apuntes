# Hashing de Contraseñas con bcryptjs

El hashing de contraseñas convierte una contraseña en un [hash](../../ConceptosGenerales/Hash.md) cifrado, asegurando que no se almacene en su forma original en la base de datos, mejorando así la seguridad.

## Instalación de bcryptjs

Para utilizar bcryptjs, primero debes instalar el paquete:

```bash
npm install bcrypt
```

## Hashing de una Contraseña

Para hashear una contraseña, se utiliza la función `bcrypt.hash()`. Esta función recibe la contraseña y un número de salt rounds (el nivel de complejidad del hashing). A continuación, un ejemplo de cómo realizar el hashing:

```javascript
const bcrypt = require('bcrypt');

async function hashPassword() {
  const myPassword = 'admin1.2.3';
  const hash = await bcrypt.hash(myPassword, 10);
  console.log(hash);
}

hashPassword(); // Salida: $2b$10$GiP.RKuC7tdx8pIoWMRkZuyCwbQYs8aBhJLaqwwqa6bJ1LET.Msom
```

En este ejemplo:
- `myPassword` es la contraseña que deseas hashear.
- `10` es el número de salt rounds, que determina la complejidad del hashing. Un valor más alto implica mayor seguridad pero más tiempo de procesamiento.

## Verificación de una Contraseña

Para verificar si una contraseña en crudo coincide con un hash almacenado, se utiliza la función `bcrypt.compare()`. Esta función recibe la contraseña en crudo y el hash, devolviendo un booleano que indica si coinciden:

```javascript
const bcrypt = require('bcrypt');

async function verifyPassword() {
  const myPassword = 'admin1.2.3';
  const hash = '$2b$10$6.K1g7Nu7YrVUbLE1FhSJORhkeOg0.X3LVamYf7aZKssfNAWbOgya';
  const isMatch = await bcrypt.compare(myPassword, hash);
  console.log(isMatch); // Salida: true
}

verifyPassword();
```

En este ejemplo:
- `myPassword` es la contraseña que deseas verificar.
- `hash` es el hash previamente generado que se compara con `myPassword`.
- `isMatch` será `true` si `myPassword` coincide con `hash`, de lo contrario, será `false`.
