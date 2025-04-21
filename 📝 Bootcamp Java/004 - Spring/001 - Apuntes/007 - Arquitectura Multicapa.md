### Arquitectura Multicapa

La estructura de un proyecto debe seguir una arquitectura multicapa, con cada capa en su propio paquete para facilitar la organización y la ubicación de clases.

- **Repository (DAO)**: Capa de persistencia de datos, trabaja con tecnologías como JDBC o JPA. Marcada con `@Repository`.
- **Entity (Model)**: Representa una tabla de base de datos. Cada instancia corresponde a una fila en la tabla, marcada con `@Entity`.
- **DTO**: Objetos de transferencia de datos, proporcionan vistas del modelo.
- **Service**: Capa intermedia que contiene la lógica de negocio, entre el repositorio y el controlador.
- **Controller**: Gestiona las solicitudes desde la interceptación hasta la respuesta.