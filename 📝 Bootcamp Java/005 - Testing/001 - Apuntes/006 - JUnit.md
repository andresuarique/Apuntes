### JUnit

- **Definición**: Framework para realizar pruebas unitarias.
- **Spring Boot**: La dependencia `spring-boot-starter-test` incluye JUnit junto con otras librerías para testing.

---

### Anotaciones de JUnit

- **@Test**: Indica un método de prueba.
- **@ParametrizedTest**: Permite realizar pruebas con múltiples argumentos.
- **@DisplayName**: Define un nombre descriptivo para el test.
- **@Tag**: Declara etiquetas para filtrar pruebas.
- **@Disabled**: Desactiva un test.
- **@BeforeEach**: Se ejecuta antes de cada prueba individual.
- **@AfterEach**: Se ejecuta después de cada prueba individual.
- **@BeforeAll**: Se ejecuta antes de todas las pruebas de la clase.
- **@AfterAll**: Se ejecuta después de todas las pruebas de la clase.

---

### Aserciones de JUnit

Utilizadas para verificar condiciones en los tests:

- **assertArrayEquals**: Verifica si dos arrays son iguales.
- **assertEquals**: Comprueba si dos valores son iguales.
- **assertTrue**: Verifica que una condición sea verdadera.
- **assertNull**: Comprueba que un objeto sea nulo.
- **assertSame**: Verifica si dos referencias apuntan al mismo objeto.
- **assertAll**: Agrupa múltiples aserciones.
- **assertIterableEquals**: Comprueba si dos iterables son iguales.
- **assertThrows**: Verifica que se lance una excepción específica.
- **assertTimeout**: Asegura que un método se complete dentro de un tiempo límite.
- **assertLinesMatch**: Compara líneas de texto de forma detallada.

---

### Doubles o Fakes

Término genérico para reemplazar objetos reales en tests:

- **Dummy**: Objetos que solo existen para cumplir requisitos de un método, pero no se usan.
- **Stubs**: Proporcionan respuestas predefinidas para pruebas.
- **Spy**: Solo ciertos métodos son falsificados; los demás son reales.
- **Mocks**: Configurados para verificar llamadas y comportamientos específicos. Permiten comprobar si un método fue llamado o cómo fue utilizado.