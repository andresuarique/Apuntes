# Doubles en Testing

Los doubles son objetos utilizados en [pruebas](Testing.md) para reemplazar dependencias reales y simular diferentes comportamientos en el sistema. Los tipos de doubles incluyen:

## Dummy
Datos ficticios utilizados para llenar información requerida por las pruebas. No tienen comportamiento ni lógica y solo sirven para cumplir con los requisitos de los métodos o funciones.

## Fake
Objetos que simulan comportamientos o datos. Por ejemplo, un usuario ficticio que actúa como si fuera un usuario real para probar ciertas funcionalidades.

## Stubs
Proveedores o APIs de datos preparados que proporcionan respuestas predefinidas. Por ejemplo, una base de datos simulada que devuelve datos del clima para pruebas.

## Spies
Objetos similares a los stubs, pero con la capacidad de espiar su comportamiento, comunicación e invocación. Permiten verificar cómo se interactúa con ellos durante las pruebas.

## Mocks
Una combinación de stubs y spies. Los mocks no solo simulan comportamientos y datos, sino que también pueden estar pre-programados para enviar respuestas específicas. Son útiles para verificar interacciones y comportamientos esperados durante las pruebas.
