# Diferencia entre Autenticación y Autorización

## Autenticación
La autenticación es el proceso de verificar la identidad de una persona o entidad. En términos simples, es como mostrar tu tarjeta de identificación para demostrar que eres realmente tú. Es el primer paso en el proceso de seguridad y se enfoca en confirmar que alguien es quien dice ser.

- **Ejemplo**: Iniciar sesión en una aplicación usando tu nombre de usuario y contraseña.

**Flujo típico de autenticación**:
1. **Solicitud de credenciales**: La aplicación solicita al usuario sus credenciales (por ejemplo, nombre de usuario y contraseña).
2. **Verificación de credenciales**: La aplicación verifica las credenciales contra un sistema de almacenamiento seguro (por ejemplo, una base de datos).
3. **Resultado**: Si las credenciales son correctas, el usuario es autenticado. Si no, se le niega el acceso.

## Autorización
La autorización, por otro lado, es el proceso de determinar qué permisos tiene un usuario una vez que ha sido autenticado. Es como determinar qué acciones puede realizar y qué recursos puede acceder una vez que está dentro. La autorización se lleva a cabo después de la autenticación y define lo que el usuario puede y no puede hacer dentro del sistema.

- **Ejemplo**: Una vez que has iniciado sesión en una aplicación, determinar si tienes permiso para acceder a ciertos datos o ejecutar ciertas acciones.

**Flujo típico de autorización**:
1. **Asignación de roles**: El sistema asigna roles o permisos al usuario autenticado.
2. **Verificación de permisos**: Cada vez que el usuario intenta realizar una acción, el sistema verifica si el usuario tiene los permisos necesarios.
3. **Resultado**: Si el usuario tiene los permisos necesarios, se le permite realizar la acción. Si no, se le deniega el acceso.
