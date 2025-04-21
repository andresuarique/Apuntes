# Pruebas Unitarias
Las pruebas unitarias son un tipo de [[001 - Testing|prueba]] que se enfoca en verificar el correcto funcionamiento de unidades individuales de código, como funciones, métodos o clases. Estas pruebas se realizan de manera aislada, evitando la interacción con otros componentes del sistema.

## Características

- **Aislamiento**: Se centran en una unidad específica de código. Esta unidad debe tener una única responsabilidad y no depender de otras unidades.
- **Dependencias simuladas**: Para mantener el aislamiento, se emulan las dependencias externas (como bases de datos o servicios) usando objetos ficticios o mocks.
- **Caja negra**: Se prueban las entradas y salidas de la unidad sin importar cómo está implementada internamente.
- **Dependencias reales (excepcional)**: Aunque es posible usar dependencias reales, se evita para no romper el aislamiento de la prueba.

## Unidad
Una unidad puede ser:

- Una **función**
- Un **método**
- Una **clase**

La definición exacta depende del paradigma de desarrollo utilizado (funcional u orientado a objetos). Lo importante es que la unidad tenga una única responsabilidad clara.

## Objetivo
Verificar que los componentes del programa se comportan correctamente de forma individual, comprobando aspectos como:

- Nombre y tipo de los datos
- Valores devueltos
- Flujo de ejecución

## Quién las realiza
Generalmente, las pruebas unitarias son responsabilidad de los desarrolladores, aunque también pueden ser ejecutadas por el equipo de QA.

## Las tres A's del Unit Testing

1. **Arrange (Organizar)**: Preparar los datos, dependencias y el entorno necesarios para ejecutar la prueba.
2. **Act (Actuar)**: Ejecutar la unidad de código bajo prueba.
3. **Assert (Afirmar)**: Verificar que el resultado obtenido es el esperado.

## Principio F.I.R.S.T

- **Fast (Rápidas)**: Deben ejecutarse en pocos segundos.
- **Independent (Independientes)**: No deben depender unas de otras.
- **Repeatable (Repetibles)**: Deben arrojar los mismos resultados en cualquier entorno.
- **Self-validating (Auto-validadas)**: El resultado debe indicar claramente si la prueba pasó o falló.
- **Timely (Oportunas)**: Deben desarrollarse lo antes posible, preferiblemente antes de subir el código a producción.
