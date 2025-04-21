### Inversión de Control (IoC) en Spring

El contenedor de IoC en Spring está basado en la interfaz `ApplicationContext` y gestiona la creación y administración de objetos llamados **Beans**. Estos beans, como conexiones de bases de datos o clientes HTTP, son instanciados y administrados por Spring, y pueden ser referenciados y utilizados más tarde mediante inyección de dependencias.

- **Bean**: Es un objeto gestionado por Spring en tiempo de ejecución. Se crea, configura y agrega al repositorio de objetos del contenedor IoC para su reutilización.
- **Contenedor IoC**: Representado por `ApplicationContext`, se encarga de crear, configurar y ensamblar los beans.
- **Inyección de Dependencias (DI)**: Técnica que permite que los beans sean inyectados automáticamente en otras clases, configurada a través de XML o anotaciones.
- **Inversión de Control (IoC)**: El control de los objetos se cede al contenedor, quien se encarga de gestionarlos, lo que reduce el acoplamiento en el código. Es conocido como el principio de "No nos llames, nosotros te llamamos".