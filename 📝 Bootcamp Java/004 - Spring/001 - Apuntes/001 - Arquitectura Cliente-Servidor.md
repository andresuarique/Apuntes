## Arquitectura Cliente-Servidor

La **arquitectura cliente-servidor** es un modelo de diseño de software en el que las tareas y responsabilidades se dividen entre dos entidades principales:

1. **Clientes**:
    
    - Son los **demandantes** de recursos o servicios.
    - Realizan peticiones al servidor mediante solicitudes (requests).
    - Pueden ser aplicaciones frontend, navegadores, dispositivos móviles, etc.
2. **Servidores**:
    
    - Son los **proveedores** de recursos o servicios.
    - Procesan las solicitudes de los clientes y envían respuestas (responses).
    - Normalmente contienen la lógica de negocio, bases de datos y APIs.

---

## Proceso de Comunicación

1. El cliente realiza una **petición** al servidor.
2. El servidor procesa la petición y retorna una **respuesta** al cliente.
3. Este intercambio ocurre a través de protocolos de red, como **HTTP** o **HTTPS**.

---

## Rol del Backend y Frontend

- **Backend**:
    
    - Se encarga de exponer **APIs** mediante protocolos como **HTTP** o **HTTPS**.
    - Procesa la lógica de negocio, maneja la comunicación con la base de datos y asegura la integridad de la información.
- **Frontend**:
    
    - Consume las APIs del backend.
    - Muestra la información según las necesidades del usuario.
    - Proporciona una interfaz gráfica o de usuario (UI) amigable.

---

## Seguridad en la Comunicación

Hoy en día, se utiliza principalmente el protocolo **HTTPS** (Hypertext Transfer Protocol Secure), que añade seguridad al canal de comunicación mediante **SSL/TLS**.

### Beneficios de HTTPS:

- **Cifrado**: Protege la información transmitida entre el cliente y el servidor.
- **Autenticación**: Garantiza que el servidor al que el cliente se conecta es legítimo.
- **Integridad**: Asegura que los datos no han sido alterados durante su transmisión.
