## Modelo-Vista-Controlador (MVC)

El **Modelo-Vista-Controlador (MVC)** es un **patrón de arquitectura de software** que organiza una aplicación en tres componentes principales, separando la lógica de negocio de la lógica de presentación:

1. **Modelo**:
    
    - Gestiona los datos de la aplicación.
    - Usualmente interactúa con la base de datos u otras fuentes de datos.
    - Es responsable de las operaciones CRUD (crear, leer, actualizar y eliminar).
2. **Vista**:
    
    - Representa la interfaz de usuario o presentación visual de los datos.
    - Muestra la información obtenida del modelo al usuario.
    - Recibe las entradas del usuario, como clics o formularios.
3. **Controlador**:
    
    - Actúa como intermediario entre el modelo y la vista.
    - Recibe las órdenes del usuario desde la vista, solicita datos al modelo y actualiza la vista con la información procesada.
    - Contiene la lógica que conecta el flujo de datos entre las otras dos capas.

---

## API REST

### ¿Qué es una API?

Una **API** (Application Programming Interface) es un conjunto de funciones y procedimientos que permite que diferentes aplicaciones se comuniquen entre sí, facilitando la integración y el diseño de software modular.

### REST (Representational State Transfer)

REST es un **estilo arquitectónico** para diseñar APIs que:

- Usa **HTTP** como protocolo de comunicación.
- Es **sin estado** (_stateless_): cada petición es independiente y no guarda información del contexto entre solicitudes.
- Usa formatos estándar como **JSON** o **XML** para transferir datos.

---

### Características de una API REST:

1. **Métodos HTTP**:
    
    - **GET**: Para obtener recursos.
    - **POST**: Para crear recursos.
    - **PUT**: Para actualizar recursos.
    - **DELETE**: Para eliminar recursos.
2. **Estructura basada en recursos**:
    
    - Cada entidad o recurso tiene su propia URL única (por ejemplo, `/usuarios`, `/productos`).
3. **Independencia entre cliente y servidor**:
    
    - El cliente (frontend) y el servidor (backend) son componentes separados que se comunican a través de la API.
4. **Caché**:
    
    - REST puede aprovechar la caché para mejorar el rendimiento.
5. **Escalabilidad y simplicidad**:
    
    - Ideal para aplicaciones modernas debido a su flexibilidad y uso de estándares.
