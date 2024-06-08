# ¿Qué es un Hash?

Un hash es una representación matemática de datos en una cadena de longitud fija. Se utiliza para convertir entradas de cualquier tamaño en una salida de longitud fija a través de una función de hash. Las propiedades clave de un hash incluyen:

1. **Determinismo**: Una misma entrada siempre producirá la misma salida.
2. **Uniformidad**: Las salidas de la función de hash deben estar distribuidas uniformemente.
3. **Eficiencia**: El cálculo de un hash debe ser rápido y eficiente.
4. **Preimagen Resistencia**: Dado un hash, debe ser computacionalmente inviable encontrar la entrada original.
5. **Resistencia a Colisiones**: Debe ser difícil encontrar dos entradas diferentes que produzcan el mismo hash.

## Usos Comunes de los Hashes

1. **Seguridad**: Los hashes se utilizan para almacenar contraseñas de manera segura, ya que permiten verificar una contraseña sin almacenar la original.
2. **Integridad de Datos**: Los hashes se usan para verificar la integridad de los datos, asegurando que no han sido alterados durante la transmisión o el almacenamiento.
3. **Funciones de Hash en Criptografía**: Los hashes son fundamentales en algoritmos criptográficos y protocolos de seguridad, como SSL/TLS.
4. **Sistemas de Indexación**: Los hashes se utilizan en estructuras de datos como tablas hash para acelerar la búsqueda y recuperación de datos.

## Ejemplos de Algoritmos de Hash

1. **MD5 (Message-Digest Algorithm 5)**: Produce un hash de 128 bits. No se recomienda para aplicaciones de seguridad debido a vulnerabilidades conocidas.
2. **SHA-1 (Secure Hash Algorithm 1)**: Produce un hash de 160 bits. Al igual que MD5, ya no se considera seguro para muchas aplicaciones.
3. **SHA-256 (Secure Hash Algorithm 256 bits)**: Parte de la familia SHA-2, produce un hash de 256 bits y se considera seguro para muchas aplicaciones.
4. **SHA-3**: Un estándar más reciente que ofrece una alternativa a la familia SHA-2.

## Ejemplo de Funcionamiento de un Hash

```plaintext
Entrada: "Hola Mundo"
Hash (SHA-256): a591a6d40bf420404a011733cfb7b190d62c65bf0bcda32b2b02d84a15841e9b
```

En este ejemplo, la cadena de texto "Hola Mundo" se convierte en un hash de 64 caracteres usando el algoritmo SHA-256.

## Propiedades de Seguridad de los Hashes

1. **No Reversibilidad**: Es prácticamente imposible revertir un hash para obtener la entrada original.
2. **Avalancha**: Un pequeño cambio en la entrada produce un cambio significativo e impredecible en la salida del hash.
3. **Resistencia a Preimagen**: Dificultad en encontrar una entrada que coincida con un hash dado.
4. **Resistencia a Colisiones**: Dificultad en encontrar dos entradas diferentes que produzcan el mismo hash.
