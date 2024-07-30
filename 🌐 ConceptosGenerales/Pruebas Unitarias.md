# Pruebas Unitarias (Aisladas)
Las pruebas unitarias se enfocan en probar unidades específicas de código. Estas [pruebas](Testing.md) son muy comunes y tienen como objetivo verificar el comportamiento de componentes individuales de manera aislada.

## Características

- **Pruebas Aisladas:** Se centran en probar una unidad específica, que puede ser una función, un método o una clase. La unidad debe tener una única responsabilidad y no debe depender de otras unidades en el sistema.
  
- **Dependencias:** Aunque las pruebas unitarias pueden incluir dependencias como bases de datos o librerías, estas se suelen emular usando objetos ficticios (dummies) para asegurar que las pruebas se centren únicamente en la unidad en cuestión.

- **Pruebas de Estado o Caja Negra:** Estas pruebas se centran en las entradas y salidas de la unidad probada, sin preocuparse por el funcionamiento interno. Esto se conoce como pruebas de caja negra.

- **Dependencias Reales:** En algunos casos, es posible realizar pruebas unitarias con dependencias reales, aunque generalmente se prefiere el uso de emulaciones para mantener el aislamiento de la unidad.

## Unidad
Una unidad puede ser:
- Una **función**
- Un **método**
- Una **clase**

La elección de la unidad depende del paradigma de desarrollo utilizado, ya sea funcional o de programación orientada a objetos (POO). La unidad debe tener una sola responsabilidad específica para mantener un diseño claro y efectivo.