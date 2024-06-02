# Métodos HTTP

Los métodos [[HTTP|HTTP]] son verbos que se utilizan para indicar la acción que se desea realizar sobre un recurso en un servidor web. Cada método tiene un significado específico y está diseñado para realizar una tarea particular. Aquí se presentan los métodos HTTP más comunes:

## GET

El método GET se utiliza para solicitar datos de un recurso específico en un servidor. Se utiliza para recuperar información y no debe tener ningún efecto secundario en el servidor.

## POST

El método POST se utiliza para enviar datos al servidor para crear un nuevo recurso. Se utiliza comúnmente para enviar datos de formularios al servidor, pero puede utilizarse para cualquier tipo de datos.

## PUT

El método PUT se utiliza para actualizar un recurso existente en el servidor. Se envía toda la representación del recurso actualizado al servidor.

## PATCH

El método PATCH se utiliza para actualizar parcialmente un recurso existente en el servidor. Se envía solo la parte del recurso que se desea actualizar.

## DELETE

El método DELETE se utiliza para eliminar un recurso específico en el servidor. Se utiliza para eliminar recursos que ya no son necesarios.

## OPTIONS

El método OPTIONS se utiliza para obtener información sobre las opciones de comunicación disponibles para un recurso en el servidor. Se utiliza para determinar qué métodos y encabezados son compatibles con un recurso en el servidor.

## HEAD

El método HEAD es similar al método GET, pero solo solicita los encabezados de respuesta del servidor, sin solicitar el cuerpo del recurso. Se utiliza para obtener información sobre un recurso sin recuperar su contenido completo.

## TRACE

El método TRACE se utiliza para solicitar al servidor que devuelva la solicitud recibida de vuelta al cliente. Se utiliza para probar la cadena de solicitud y respuesta entre el cliente y el servidor.

## CONNECT

El método CONNECT se utiliza para establecer una conexión TCP/IP con un servidor proxy. Se utiliza para establecer una conexión segura con un servidor a través de un proxy.

Estos son algunos de los métodos HTTP más comunes que se utilizan para interactuar con los recursos en un servidor web. Cada método tiene un propósito específico y debe utilizarse de acuerdo con el contexto y los requisitos de la aplicación.