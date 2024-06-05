# Migraciones con Sequelize en Express.js

Las migraciones de bases de datos son una herramienta esencial para gestionar y versionar los cambios en el esquema de la base de datos a lo largo del tiempo. En el contexto de [Sequelize](Uso%20de%20Sequelize%20ORM%20en%20Express.js.md), las migraciones permiten describir y aplicar estos cambios de manera estructurada y controlada.

## ¿Qué son las Migraciones?

Las migraciones son archivos que contienen instrucciones para modificar el esquema de la base de datos. Estos archivos permiten agregar nuevas tablas, modificar columnas existentes o eliminar restricciones, entre otros cambios. Esto es especialmente útil en entornos donde múltiples instancias de la aplicación pueden estar ejecutándose.

## Configuración de Migraciones en Sequelize

Supongamos que tienes un modelo `User` definido de la siguiente manera:

**models/user.js**

```javascript
const { Sequelize, Model, DataTypes } = require('sequelize');
const sequelize = require('../libs/sequelize'); // Asegúrate de que la instancia de Sequelize esté importada

class User extends Model {}

User.init(
  {
    id: {
      type: DataTypes.INTEGER,
      primaryKey: true,
      autoIncrement: true,
    },
    username: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: true,
    },
    email: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: true,
    },
    password: {
      type: DataTypes.STRING,
      allowNull: false,
    },
  },
  {
    sequelize, // Pasando la instancia de Sequelize
    modelName: 'User',
  }
);

module.exports = User;
```

## Creación de una Migración

Supongamos que necesitas agregar una nueva columna llamada `createdAt` al modelo `User`. Primero, genera una nueva migración ejecutando el siguiente comando:

```bash
npx sequelize-cli migration:generate --name add_createdAt_column_to_users
```

Esto creará un nuevo archivo en el directorio `migrations` con un nombre similar a `20220106123456-add_createdAt_column_to_users.js`. Abre este archivo y define las instrucciones necesarias para realizar el cambio:

**migrations/20220106123456-add_createdAt_column_to_users.js**

```javascript
'use strict';

module.exports = {
  up: async (queryInterface, Sequelize) => {
    await queryInterface.addColumn('Users', 'createdAt', {
      type: Sequelize.DATE,
      allowNull: false,
      defaultValue: Sequelize.literal('CURRENT_TIMESTAMP'),
    });
  },

  down: async (queryInterface, Sequelize) => {
    await queryInterface.removeColumn('Users', 'createdAt');
  },
};
```

La función `up` describe cómo aplicar el cambio (agregar la columna `createdAt`), mientras que la función `down` describe cómo revertir el cambio (eliminar la columna `createdAt`).

## Aplicación de la Migración

Para aplicar la migración, ejecuta:

```bash
npx sequelize-cli db:migrate
```

Esto ejecutará la función `up` de todas las migraciones pendientes y aplicará los cambios en la base de datos.

## Reversión de la Migración

Si necesitas revertir la migración, ejecuta:

```bash
npx sequelize-cli db:migrate:undo
```

Esto ejecutará la función `down` de la migración más reciente, revirtiendo el último cambio.

## Beneficios de las Migraciones

Las migraciones proporcionan una forma estructurada de gestionar la evolución de la base de datos, facilitando la colaboración entre desarrolladores y el despliegue en diferentes entornos. Aseguran que todos los cambios en la base de datos sean reproducibles y reversibles, lo que mejora la consistencia y la integridad de la aplicación.