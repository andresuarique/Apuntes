# Instalación de Nest.js y Creación de un Proyecto

## Nest CLI: Herramienta de Línea de Comandos para Nest.js

Nest CLI es la Command Line Interface (CLI) de Nest.js. Nos proporciona comandos personalizados para inicializar, trabajar y darle mantenimiento a nuestras aplicaciones de Nest.js.

## Instalación de Nest CLI

Para instalar Nest CLI, necesitas tener un gestor de paquetes como [NPM](../001%20-%20Fundamentos/019%20-%20npm.md) o Yarn. Puedes instalarlo globalmente usando el siguiente comando:

```bash
npm install -g @nestjs/cli
```

## Creación de un Proyecto con Nest CLI

Un ejemplo de cómo usar la CLI es la creación de un nuevo proyecto. Utiliza el siguiente comando para inicializar tu proyecto:

```bash
nest new nombre-de-proyecto
```

Este comando inicializa tu proyecto, instalando los paquetes necesarios con el gestor de tu preferencia y con una configuración predefinida, incluyendo:

- Linter (herramienta de análisis estático de código)
- Prettier (formateador de código)
- Configuración de TypeScript
- Gitignore
- Estructura de carpetas predefinida