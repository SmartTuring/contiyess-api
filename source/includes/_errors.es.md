# Errores

Contiyess API utiliza los siguientes códigos de error:


Código de Error | Explicación
--------------- | ------------
400 | Bad Request -- Su solicitud no es válida.
401 | Unauthorized -- Su clave de API es incorrecta.
403 | Forbidden -- El requerimiento no está disponible.
404 | Not Found -- No se pudo encontrar el endpoint especificado.
405 | Method Not Allowed -- Intentaste acceder a un endpoint con un método no válido.
406 | Not Acceptable -- Solicitó un formato que no es json.
410 | Gone -- El requerimiento solicitado ha sido eliminado de nuestros servidores.
429 | Too Many Requests -- Demasiadas solicitudes: ¡Estás solicitando demasiados peticiones! ¡Tranquilo!
500 | Internal Server Error -- Error interno del servidor: tuvimos un problema con nuestro servidor. Inténtalo de nuevo más tarde.
503 | Service Unavailable -- Servicio no disponible: estamos temporalmente fuera de línea por mantenimiento. Inténtalo de nuevo más tarde.
