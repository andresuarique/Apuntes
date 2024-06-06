# JWT (JSON Web Token)

JWT (JSON Web Token) es un estándar para la creación de tokens de acceso que transmiten información entre dos partes de manera segura. Actúa como un pase que llevas contigo una vez que has sido autenticado, conteniendo información sobre tu identidad y tus permisos.

## Características principales:

- **Formato**: Los JWT son compactos y están en formato JSON, lo que los hace fáciles de usar en entornos web.
- **Autocontenido**: Cada token contiene toda la información necesaria para su verificación, incluyendo las credenciales del usuario y los permisos.
- **Stateless**: No requieren que el servidor almacene información de sesión, ya que el token en sí lleva toda la información necesaria. Esto simplifica la gestión de sesiones y mejora la escalabilidad.
- **Seguridad**: Los JWT pueden ser firmados digitalmente (usando algoritmos como HMAC o RSA) para garantizar la integridad y autenticidad de la información que contienen.

## Ventajas:

- [**Autenticación y Autorización**](Autenticación%20vs%20Autorización.md): Útil tanto para autenticar usuarios como para definir y verificar permisos.
- **Escalabilidad**: Ideal para arquitecturas distribuidas y microservicios, ya que cada servicio puede verificar la validez del token de manera autónoma.
- **Rendimiento**: Reduce la carga en el servidor al eliminar la necesidad de almacenar y consultar el estado de la sesión.

En resumen, los JWT son una herramienta eficiente y segura para la autenticación y autorización en aplicaciones web modernas.