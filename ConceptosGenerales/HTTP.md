# HTTP (Protocolo de Transferencia de Hipertexto)

HTTP, que significa Protocolo de Transferencia de Hipertexto, es un protocolo de comunicación utilizado para la transferencia de datos en la World Wide Web (WWW). Fue desarrollado para facilitar la comunicación entre clientes (navegadores web) y servidores web.

## Características Principales:

1. **Basado en el protocolo de solicitud-respuesta:** HTTP sigue el modelo de solicitud y respuesta, donde el cliente envía una solicitud al servidor y el servidor responde con los datos solicitados.

2. **Sin estado:** HTTP es un protocolo sin estado, lo que significa que cada solicitud se procesa de forma independiente y no se almacena información sobre el estado de la sesión del cliente en el servidor entre las solicitudes.

3. **Protocolo de capa de aplicación:** HTTP opera en la capa de aplicación del modelo de referencia OSI (Open Systems Interconnection), lo que significa que se basa en otros protocolos de capas inferiores, como TCP/IP, para la transferencia de datos.

4. **Basado en texto:** Las solicitudes y respuestas HTTP están formateadas en texto legible por humanos, lo que facilita la depuración y la comprensión de la comunicación entre el cliente y el servidor.

## Funcionamiento Básico:

- **Cliente-Servidor:** En una comunicación HTTP, hay dos entidades principales: el cliente (generalmente un navegador web) y el servidor (que aloja los recursos web). El cliente envía solicitudes HTTP al servidor, y el servidor responde con los recursos solicitados.

- **Métodos HTTP:** HTTP define diferentes [métodos](Métodos%20HTTP.md) de solicitud que indican la acción que se desea realizar sobre un recurso en el servidor, como GET para recuperar datos, POST para enviar datos al servidor, etc.

- **Códigos de Estado:** HTTP utiliza [códigos de estado](Códigos%20de%20Estado%20HTTP.md) para indicar el resultado de una solicitud, como 200 OK para una solicitud exitosa, 404 Not Found para un recurso no encontrado, etc.

## Seguridad:

- **HTTP vs HTTPS:** HTTPS es una versión segura de HTTP que utiliza cifrado SSL/TLS para proteger la comunicación entre el cliente y el servidor. HTTPS es ampliamente utilizado en aplicaciones web para garantizar la seguridad y la privacidad de los datos del usuario.

En resumen, HTTP es un protocolo fundamental en el funcionamiento de la World Wide Web, que permite la transferencia de datos entre clientes y servidores de manera eficiente y segura.
