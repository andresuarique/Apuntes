# Configuración y Uso de Sequelize con Queries

Sequelize es un [ORM](../../🌐%20ConceptosGenerales/ORM.md) (Object-Relational Mapping) basado en promesas para Node.js y soporta diferentes bases de datos SQL como MySQL, PostgreSQL, SQLite y MariaDB. Integrar Sequelize con una aplicación Express.js facilita la interacción con bases de datos mediante un enfoque orientado a objetos.
## Instalación

Para empezar a usar Sequelize, primero necesitas instalar Sequelize y el driver de la base de datos que vayas a utilizar. Por ejemplo, para MySQL:

```bash
npm install sequelize mysql2
```

## Configuración

1. **Configuración de Sequelize**: Crea un archivo de configuración `config/database.js` para inicializar Sequelize con la configuración de la base de datos.

   ```javascript
   const { Sequelize } = require('sequelize');

   const sequelize = new Sequelize('database', 'username', 'password', {
     host: 'localhost',
     dialect: 'mysql'
   });

   module.exports = sequelize;
   ```

## Uso de Queries

Puedes ejecutar consultas SQL crudas utilizando Sequelize. Esto es útil cuando necesitas realizar consultas complejas que no se pueden manejar fácilmente con los métodos del ORM.

1. **Consultas Básicas**:

   ```javascript
   const sequelize = require('./config/database');

   // SELECT
   sequelize.query("SELECT * FROM Users", { type: sequelize.QueryTypes.SELECT })
     .then(users => {
       console.log(users);
     });

   // INSERT
   sequelize.query("INSERT INTO Users (firstName, lastName, email) VALUES ('John', 'Doe', 'john.doe@example.com')", { type: sequelize.QueryTypes.INSERT })
     .then(result => {
       console.log(result);
     });
   ```

2. **Uso de Data y Metadata**:

   Sequelize también puede devolver datos y metadatos de las consultas. Los metadatos pueden incluir información adicional como el número de filas afectadas.

   ```javascript
   sequelize.query("SELECT * FROM Users", { raw: true })
     .then(([results, metadata]) => {
       console.log('Results:', results);
       console.log('Metadata:', metadata);
     });
   ```

