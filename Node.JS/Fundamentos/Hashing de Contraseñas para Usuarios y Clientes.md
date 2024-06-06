# Hashing de Contraseñas para Usuarios y Clientes

Para garantizar la seguridad de las contraseñas en una aplicación, es fundamental [hashear](../../ConceptosGenerales/Hash.md) las contraseñas antes de almacenarlas en la base de datos. Aquí se muestra cómo implementar el hashing de contraseñas en los servicios de usuarios y clientes utilizando bcryptjs.
## Servicio de Usuario (user.service.js)

En el servicio de usuario, el hashing de contraseñas se realiza antes de almacenar los datos en la base de datos. Además, se elimina la contraseña de la respuesta para evitar que se devuelva al cliente.

```javascript
const bcrypt = require('bcrypt');

async create(data) {
  // Hashear la contraseña antes de guardarla
  const hash = await bcrypt.hash(data.password, 10);
  const newUser = await models.User.create({
    ...data,
    password: hash,
  });
  // Eliminar la contraseña de la respuesta
  delete newUser.dataValues.password;
  return newUser;
}
```

## Servicio de Cliente (customer.service.js)

En el servicio de cliente, se clona la información del cliente y del usuario asociado, se hashea la contraseña del usuario y luego se almacena en la base de datos. También se elimina la contraseña de la respuesta.

```javascript
const bcrypt = require('bcrypt');

async create(data) {
  // Hashear la contraseña del usuario asociado al cliente
  const hash = await bcrypt.hash(data.user.password, 10);
  const newData = {
    ...data,
    user: {
      ...data.user,
      password: hash,
    },
  };
  const newCustomer = await models.Customer.create(newData, {
    include: ['user'],
  });
  // Eliminar la contraseña de la respuesta
  delete newCustomer.user.dataValues.password;
  return newCustomer;
}
```

## Explicación

1. **Hashing de la Contraseña**: Utilizamos `bcrypt.hash` para hashear la contraseña antes de guardarla en la base de datos. El método `bcrypt.hash` recibe dos parámetros: la contraseña en texto plano y el número de saltos (en este caso, 10).
2. **Clonación de Datos**: En el caso del cliente, se clonan los datos originales y se sustituye la contraseña en texto plano por su versión hasheada.
3. **Eliminación de Contraseña de la Respuesta**: Para evitar que la contraseña hasheada se devuelva en la respuesta, se elimina de los datos del usuario (`delete newUser.dataValues.password` y `delete newCustomer.user.dataValues.password`).

