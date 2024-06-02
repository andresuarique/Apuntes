# ¿Qué es Node.js?

**Node.js es un entorno de ejecución de JavaScript fuera del navegador**. Se creó en 2009 con un enfoque orientado a servidores. Su importancia radica en que no requiere un navegador web para ejecutar código JavaScript.

Características principales de Node.js:

- **Concurrencia**: Es [monohilo](Node.JS/Monohilo%20-%20implicaciones%20en%20diseño%20y%20seguridad.md), con operaciones de entrada/salida asíncronas.

- **Motor V8**: Desarrollado por Google en 2008 para Chrome, escrito en C++. Convierte JavaScript en código máquina en lugar de interpretarlo en tiempo real.

- Todo se organiza en base a **módulos**, que son pequeñas piezas de código que modularizan los sistemas y mejoran la comprensión del código.

- **Orientación a Eventos**: Node.js emplea un [bucle de eventos](Node.JS/Event%20Loop.md) que se ejecuta de manera constante. Esto nos permite programar de forma reactiva, lo que implica que podemos desarrollar con la lógica de "cuando ocurre algo, ejecuta esta parte de mi código y, a su vez, dispara otra parte".
