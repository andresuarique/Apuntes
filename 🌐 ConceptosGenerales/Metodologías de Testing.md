# Metodologías de Testing

## TDD (Test Driven Development)
Desarrollo guiado por [pruebas](Testing.md). En esta metodología, se crean primero las pruebas antes de escribir el código. Es decir, se definen las expectativas (expect) antes de implementar la funcionalidad.

## BDD (Behavior Driven Development)
Desarrollo guiado por el comportamiento, basado en los requisitos. En BDD, se definen primero los comportamientos esperados del sistema y luego se escriben las pruebas para verificar estos comportamientos.

## AAA (Arrange-Act-Assert)
Es un mantra para estructurar pruebas:
- **Arrange (Preparar / Given):** Configurar el entorno y los datos necesarios para la prueba.
- **Act (Ejecutar / When):** Ejecutar la acción o el método que se está probando.
- **Assert (Afirmar / Then):** Verificar que los resultados sean los esperados.

## Conceptos Importantes

### Falso Positivo
Ocurre cuando una prueba indica un error, pero en realidad todo está bien. Por ejemplo, si se prueba la función de suma `1 + 1` y se espera `5`, la prueba fallará aunque la función esté correcta. En este caso, la prueba está mal definida.

### Falso Negativo
Más comunes que los falsos positivos, ocurren cuando parece que todo está bien, pero hay errores no identificados. Esto sucede a menudo cuando solo se prueba el "Happy Path" (camino feliz), es decir, las condiciones bajo las cuales sabemos que el sistema funciona. Por ejemplo, si en una prueba de división se omitió la división por cero, puede que el sistema funcione bien en otros casos, pero no detecte este error específico. Para evitar falsos negativos, es recomendable aplicar TDD.

### Sistema Legacy
Sistemas existentes que requieren la adición de pruebas. A menudo, estos sistemas tienen métodos grandes y difíciles de probar. Es importante refactorizar estos métodos en unidades más pequeñas y manejables para realizar pruebas unitarias efectivas. Los sistemas legacy suelen carecer de una buena arquitectura.

### Clean Architecture
Un patrón de diseño que promueve buenas prácticas desde el inicio del desarrollo. En una arquitectura limpia, cada método está bien dividido y tiene responsabilidades claras, lo que facilita la creación y ejecución de pruebas.
