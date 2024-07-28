# Testing
En el mundo actual, las tecnologías con las que vivimos necesitan código, lo que ha hecho que el desarrollo de software se haya industrializado. Este proceso cuenta con herramientas como el testing, que nos permiten entregar proyectos de calidad a nuestros clientes más rápidamente, reduciendo el riesgo de errores en producción.

## ¿Por qué hacer testing?
Normalmente hay cuatro fases en el desarrollo de software para crear un producto:

Diseño ⇒ Desarrollo ⇒ Pruebas ⇒ Producción

En estas fases, detectar un error se vuelve cada vez más costoso a medida que avanzamos. Ahí es donde implementamos técnicas para prevenir estas situaciones. El testing es la manera en la que gestionamos el riesgo y tratamos de evitar, en la medida de lo posible, los errores en el sistema.

## Gestionar riesgos como Google
- **Análisis de código estático**: Mientras desarrollamos, vamos viendo nuestros resultados.
- **Pruebas unitarias**: Nos aseguramos de que el código funciona como queremos.
- **Pruebas de integración**: Verificamos que varios elementos funcionan bien trabajando juntos.
- **Revisión de código**: Un equipo o persona encargada de revisar el código de los demás.
- **QA (Quality Assurance)**: Equipos que crean pruebas automáticas o manuales.

# La pirámide del testing
La pirámide del testing es un modelo que sugiere una proporción adecuada de diferentes tipos de pruebas en el desarrollo de software.

![[Pasted image 20240727182038.png]]
## Unit Test
- Aplicado al código de producción.
- Pruebas estáticas.

## Integration Test
- Se prueba la comunicación entre los módulos o unidades para saber cómo se está transportando la información.

## End to End Test
- Pruebas punto a punto aplicadas a bases de datos de terceros, como APIs.
- Aquí se prueba todo el flujo del programa.

## UI Test
- Emular el funcionamiento entero del programa.
- Incluye las pruebas manuales.

## Enfoques en la pirámide del testing
En la pirámide del testing, se pueden encontrar dos enfoques principales:

### Tecnología
Desde el integration testing hacia el unit testing, las pruebas están enfocadas en la tecnología. Estas pruebas buscan responder: **¿Estamos construyendo el sistema correctamente?** El enfoque principal aquí es la tecnología.

### Negocio
La mitad superior de la pirámide está orientada hacia las pruebas de negocio. Estas pruebas buscan responder: **¿Estamos construyendo el sistema correcto?** El enfoque principal aquí es el negocio.
