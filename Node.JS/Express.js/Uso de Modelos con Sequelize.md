# Trabajando con Sequelize en Express.js: Modelos y Consultas

## Estructura de Carpeta

Para organizar tu proyecto de [Sequelize](Uso%20de%20Sequelize%20ORM%20en%20Express.js.md) en Express.js, sigue una estructura de carpetas clara:

```
/project-root
  /db
    /models
      user.model.js
      index.js
  /libs
    sequelize.js
  /config
    config.js
  /services
    user.service.js
  index.js
```

## Nomenclatura y Convenciones

Una buena práctica en Sequelize y bases de datos es usar `snake_case` para nombres de campos y tablas en la base de datos, mientras que en JavaScript es común usar `camelCase`. 

Ejemplo de esquema de tabla:

```javascript
createdAt: { // Variable JavaScript
  allowNull: false,
  type: DataTypes.DATE,
  field: 'created_at', // Naming en Sequelize
  defaultValue: Sequelize.NOW // Valor por defecto
}
```

## Definición del Modelo

Define tus modelos extendiendo de `Model`. El archivo del modelo define el esquema de la base de datos y cualquier configuración necesaria.

**user.model.js**:

```javascript
const { Model, DataTypes, Sequelize } = require('sequelize');

const USER_TABLE = 'users'; // Nombre de la tabla

const UserSchema = {
  id: {
    allowNull: false,
    autoIncrement: true,
    primaryKey: true,
    type: DataTypes.INTEGER,
  },
  email: {
    allowNull: false,
    type: DataTypes.STRING,
    unique: true,
  },
  password: {
    allowNull: false,
    type: DataTypes.STRING,
  },
  createdAt: {
    allowNull: false,
    type: DataTypes.DATE,
    field: 'created_at',
    defaultValue: Sequelize.NOW,
  },
};

class User extends Model {
  static associate() {
    // Definir asociaciones si es necesario
  }

  static config(sequelize) {
    return {
      sequelize,
      tableName: USER_TABLE,
      modelName: 'User',
      timestamps: false,
    };
  }
}

module.exports = { USER_TABLE, UserSchema, User };
```

## Configuración de Modelos

Configura tus modelos en un archivo `index.js` dentro de la carpeta `models`.

**index.js**:

```javascript
const { User, UserSchema } = require('./user.model');

function setupModels(sequelize) {
  User.init(UserSchema, User.config(sequelize));
}

module.exports = setupModels;
```

## Inicialización y Sincronización de Sequelize

Inicializa Sequelize y sincroniza los modelos en el archivo `sequelize.js`.

**sequelize.js**:

```javascript
const { Sequelize } = require('sequelize');
const { config } = require('../config/config');
const setupModels = require('../db/models/');

const USER = encodeURIComponent(config.dbUser);
const PASSWORD = encodeURIComponent(config.dbPassword);
const URI = `postgres://${USER}:${PASSWORD}@${config.dbHost}:${config.dbPort}/${config.dbName}`;

const sequelize = new Sequelize(URI, { dialect: 'postgres', logging: true });

setupModels(sequelize);
sequelize.sync();

module.exports = sequelize;
```

## Realizando Consultas

Para realizar consultas, importa el modelo desde el archivo de servicios.

**user.service.js**:

```javascript
const { models } = require('../libs/sequelize');

class UserService {
  async find() {
    const users = await models.User.findAll();
    return users;
  }

  // Otros métodos CRUD pueden ir aquí
}

module.exports = UserService;
```

En este archivo, `models` es un objeto que contiene todas las instancias de los modelos inicializados y sincronizados..