# Instalación de Express.js
Para empezar a usar Express.js en un proyecto, sigue estos pasos:

## Paso 1: Inicializar un Proyecto Node.js

Primero, asegúrate de tener [Node.js](../📌%20Node%20js.md) y [019 - npm](../001%20-%20Fundamentos/019%20-%20npm.md) instalados en tu sistema. Puedes verificar esto ejecutando los siguientes comandos en tu terminal:

```sh
node -v
npm -v
```

A continuación, inicializa un nuevo proyecto Node.js. Abre tu terminal y navega al directorio donde quieres crear tu proyecto. Luego ejecuta:

```sh
npm init
```

Este comando te guiará a través de una serie de preguntas para configurar tu proyecto. Si prefieres usar la configuración predeterminada, puedes ejecutar:

```sh
npm init -y
```

## Paso 2: Instalar Express.js

Una vez que tu proyecto esté inicializado, puedes instalar Express.js usando npm. Ejecuta el siguiente comando en tu terminal:

```sh
npm install express --save
```

El modificador `--save` (o `-S`) asegura que Express se añada como una dependencia en tu archivo `package.json`.

## Paso 3: Verificar la Instalación

Para asegurarte de que Express.js se instaló correctamente, verifica la presencia de la carpeta `node_modules` y el archivo `package.json` en tu directorio de proyecto. Deberías ver algo como esto en tu `package.json`:

```json
"dependencies": {
  "express": "^4.17.1"
}
```

## Paso 4: Crear un Servidor Básico con Express

Ahora que Express.js está instalado, puedes crear un servidor básico. Crea un archivo llamado `app.js` (o cualquier nombre que prefieras) y añade el siguiente código:

```js
const express = require('express');
const app = express();
const PORT = process.env.PORT || 3000;

app.get('/', (req, res) => {
  res.send('Hola, mundo!');
});

app.listen(PORT, () => {
  console.log(`Servidor escuchando en el puerto ${PORT}`);
});
```

Este código hace lo siguiente:
- Importa el módulo Express.
- Crea una aplicación Express.
- Define una ruta para manejar solicitudes GET a la raíz (`/`) y responde con "Hola, mundo!".
- Configura el servidor para que escuche en el puerto 3000 (o cualquier puerto definido en la variable de entorno `PORT`).

## Paso 5: Ejecutar el Servidor

Finalmente, ejecuta tu servidor con el siguiente comando:

```sh
node app.js
```

Si todo está configurado correctamente, deberías ver un mensaje en la terminal indicando que el servidor está escuchando en el puerto 3000. Puedes abrir tu navegador y navegar a `http://localhost:3000` para ver tu mensaje "Hola, mundo!".

¡Y eso es todo! Ahora tienes un servidor básico de Express.js corriendo en tu máquina.