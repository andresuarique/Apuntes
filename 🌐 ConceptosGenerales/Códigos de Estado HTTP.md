# Códigos de Estado HTTP

Los códigos de estado [HTTP](HTTP.md) son indicadores numéricos que se utilizan en las respuestas HTTP para informar al cliente sobre el resultado de la solicitud que ha realizado al servidor. Estos códigos se dividen en diferentes categorías, cada una con un propósito específico. Aquí tienes una descripción de algunas de las categorías de códigos de estado HTTP más comunes:

## 1xx: Respuestas Informativas

- **100 Continue:** Indica que el servidor ha recibido los encabezados de solicitud y el cliente debería continuar enviando el cuerpo de la solicitud.

## 2xx: Respuestas Exitosas

- **200 OK:** Indica que la solicitud ha sido exitosa.
- **201 Created:** Indica que la solicitud ha tenido éxito y se ha creado un nuevo recurso.
- **204 No Content:** Indica que la solicitud se ha procesado correctamente, pero no hay contenido para devolver.

## 3xx: Redirecciones

- **301 Moved Permanently:** Indica que el recurso solicitado ha sido movido permanentemente a una nueva ubicación.
- **302 Found:** Indica que el recurso solicitado se ha movido temporalmente a una nueva ubicación.
- **304 Not Modified:** Indica que el recurso solicitado no ha sido modificado desde la última vez que fue accedido.

## 4xx: Errores del Cliente

- **400 Bad Request:** Indica que la solicitud del cliente es incorrecta o no puede ser procesada por el servidor.
- **401 Unauthorized:** Indica que el cliente debe autenticarse para acceder al recurso solicitado.
- **404 Not Found:** Indica que el recurso solicitado no ha sido encontrado en el servidor.

## 5xx: Errores del Servidor

- **500 Internal Server Error:** Indica que ha ocurrido un error interno en el servidor que ha impedido que se complete la solicitud.
- **503 Service Unavailable:** Indica que el servidor no está disponible en este momento debido a una sobrecarga o mantenimiento.

Estos son solo algunos ejemplos de los códigos de estado HTTP más comunes. Hay muchos más códigos de estado definidos en la especificación HTTP, cada uno con su propio significado y uso específico.

![Pasted image 20240602172301](📎%20ANEXOS/CódigosEstadoHTTP.png)