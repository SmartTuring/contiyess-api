# Usuarios y Contribuyentes

## Crear Usuario y Empresa

```shell
# tokenMaquina es el token asignado para la comunicación con el sistema externo
curl "https://contable.contiyess.com/api/v1/createUser" \
  -H "Authorization: Bearer tokenMaquina"
```

> El JSON a enviar sería el siguiente:

```json
{
    "user": {
        "name": "Peter Parker",
        "email": "peter@gmail.com",
        "password": "123456"
    },
    "business":{
        "ruc": "1712345678001",
        "business_name": "Empresa ABC",
        "headquarter_address": "La Kennedy",
        "retention_agent": "12345",
        "rimpe": true,
        "account_required": false,
        "ambient": 1
    }
}
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "success": true,
    "data": {
        "user": {
            "email": "peter@gmail.com",
            "name": "Peter Parker",
            "updated_at": "2024-01-05T03:37:48.000000Z",
            "created_at": "2024-01-05T03:37:48.000000Z",
            "id": 37
        },
        "issuing": {
            "ambients_id": 1,
            "id_iva": 2,
            "ruc": "1712345678001",
            "business_name": "Empresa ABC",
            "headquarter_address": "La Kennedy",
            "retention_agent": "12345",
            "rimpe": "SI",
            "account_required": "NO",
            "updated_at": "2024-01-05T03:37:48.000000Z",
            "created_at": "2024-01-05T03:37:48.000000Z",
            "id": 52,
            "establishments": []
        },
        "emission_point_id": 19,
        "token": "tokenUsuario"
    }
}
```

Este endpoint crea un usuario y una empresa. En caso de que el usuario ya exista, solo toma su identificación e ignora la información consiguiente del mismo. En cambio, si el RUC ya existiere, devuelve un error indicando el mismo.

<aside class="success">
De la respuesta, es importante tomar 'emission_point_id' y 'token', ya que los mismos servirán para la creación de nuevos documentos como facturas. Y el uso de todos los endpoints consiguientes, deberá ser con el token generado.
</aside>
<aside class="success">
El token de usuario tiene una duración de 1 hora, en caso de que expire tendrá que generar un nuevo token desde el endpoint <a href='#generar-token-de-usuario-desde-correo-electronico'>Generar token de usuario desde email</a>.
</aside>
<aside class="notice">
Debe reemplazar <code>tokenMaquina</code> con su token generado anteriormente. <a href='#generar-token'>Como generar token</a>
</aside>
<aside class="notice">
* Los valores user.name y user.password solo se toman en caso de que el usuario sea nuevo, y se ignora en caso de que el usuario ya exista.
</aside>

### HTTP Request

`POST https://contable.contiyess.com/api/v1/createUser`

### Parámetros URL

| Campo | Tipo | Descripción |
|-|-|-|  
| user | Objeto | Información del usuario |
| user.name | String | Nombre del usuario * |  
| user.email | String | Email del usuario |
| user.password | String | Contraseña del usuario *|
| business | Objeto | Información del negocio |
| business.ruc | String | RUC del negocio |
| business.business_name | String | Nombre del negocio |
| business.headquarter_address | String | Dirección de la sede |
| business.retention_agent | String | Agente de retención |
| business.rimpe | Boolean | ¿Pertenece al RIMPE? |
| business.account_required | Boolean | ¿Es obligado a llevar contabilidad? |
| business.ambient | Number | Ambiente |

### Respuesta

| Campo                  | Tipo   | Descripción                               |
|------------------------|--------|-------------------------------------------|
| success                | boolean| Indica si la operación fue exitosa o no   |
| data                   | object | Objeto contenedor de los datos            |
| user                   | object | Objeto que contiene datos del usuario     |
| user.email             | string | Correo electrónico del usuario            |
| user.name              | string | Nombre completo del usuario               |
| user.updated_at        | string | Fecha y hora de la última actualización   |
| user.created_at        | string | Fecha y hora de la creación               |
| user.id                | number | Identificador único del usuario           |
| issuing                | object | Objeto que contiene datos de emisión      |
| issuing.ambients_id    | number | Identificador del ambiente                |
| issuing.id_iva         | number | Identificador del IVA                     |
| issuing.ruc            | string | RUC de la empresa emisora                 |
| issuing.business_name  | string | Nombre comercial de la empresa            |
| issuing.headquarter_address | string | Dirección de la sede principal            |
| issuing.retention_agent| string | Agente de retención                       |
| issuing.rimpe          | string | Indicador de Registro de Información de Micro y Pequeña Empresa (RIMPE) |
| issuing.account_required | string | Indica si es obligado a llevar contabilidad |
| issuing.updated_at     | string | Fecha y hora de la última actualización   |
| issuing.created_at     | string | Fecha y hora de la creación               |
| issuing.id             | number | Identificador único de emisión            |
| issuing.establishments | array  | Arreglo de establecimientos               |
| emission_point_id      | number | Identificador del punto de emisión        |
| token                  | string | Token de usuario                          |

## Generar token de usuario desde correo electrónico

```shell
# tokenMaquina es el token asignado para la comunicación con el sistema externo
curl "https://contable.contiyess.com/api/v1/tokenByEmail" \
  -H "Authorization: Bearer tokenMaquina"
```

> El JSON a enviar sería el siguiente:

```json
{
    "email": "peter@gmail.com"
}
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "success": true,
    "token": "tokenUsuario"
}
```

<aside class="success">
El token de usuario tiene una duración de 1 hora, en caso de que expire tendrá que generar un nuevo token desde este mismo endpoint.
</aside>
<aside class="notice">
Debe reemplazar <code>tokenMaquina</code> con su token generado anteriormente. <a href='#generar-token'>Como generar token</a>
</aside>

### HTTP Request

`POST https://contable.contiyess.com/api/v1/tokenByEmail`

### Parámetros URL

| Campo | Tipo | Descripción |
|-|-|-| 
| email | String | Email del usuario |

### Respuesta

| Campo                  | Tipo   | Descripción                               |
|------------------------|--------|-------------------------------------------|
| success                | boolean| Indica si la operación fue exitosa o no   |
| token                  | string | Token de usuario                          |

## Subir Firma Electrónica
```shell
# tokenMaquina es el token asignado para la comunicación con el sistema externo
curl "https://contable.contiyess.com/api/v1/uploadSignature" \
  -H "Authorization: Bearer tokenMaquina" "Content-Type: multipart/form-data"
```

> El JSON a enviar sería el siguiente:

```json
{
    "file": "Archivo de firma electrónica P12 en base 64",
    "issuing_id": "10",
    "password": "Contraseña de firma electrónica"
}
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "success": true,
    "data": {
        "id": 7,
        "ruc": "1712345678001",
        "business_name": "Empresa ABC",
        "tradename": null,
        "headquarter_address": "La Kennedy",
        "special_taxpayer": "0",
        "retention_agent": "12345",
        "account_required": "NO",
        "rimpe": "SI",
        "status": null,
        "signature_key": "NlFUWERBVW1hajVXPMMJYjJSZ0ZGZz09",
        "ambients_id": 1,
        "created_at": "2024-01-04T21:39:22.000000Z",
        "updated_at": "2024-01-04T21:42:27.000000Z",
        "id_iva": 2,
        "info_issuing": null
    }
}
```
<aside class="notice">
En la cabecera de la petición debe enviar Content-Type: multipart/form-data
</aside>
<aside class="notice">
Debe reemplazar <code>tokenMaquina</code> con su token generado anteriormente. <a href='#generar-token'>Como generar token</a>
</aside>

### HTTP Request

`POST https://contable.contiyess.com/api/v1/uploadSignature`

### Parámetros URL

| Campo | Tipo | Descripción |
|-|-|-| 
| file | file | Firma electrónica P12 |
| issuing_id | number | ID de Emisor |
| password | string | Contraseña de firma electrónica |

### Respuesta

| Campo                  | Tipo   | Descripción                               |
|------------------------|--------|-------------------------------------------|
| success                | boolean| Indica si la operación fue exitosa o no   |
| data                   | object | Objeto contenedor de los datos            |
| id                     | number | Identificador único                       |
| ruc                    | string | RUC de la empresa                         |
| business_name          | string | Nombre comercial de la empresa            |
| tradename              | null   | Nombre comercial alternativo              |
| headquarter_address    | string | Dirección de la sede principal            |
| special_taxpayer       | string | Indicador de contribuyente especial       |
| retention_agent        | string | Agente de retención                       |
| account_required       | string | Indica si es obligado a llevar Contabilidad|
| rimpe                  | string | Indicador de Registro de Información de Micro y Pequeña Empresa (RIMPE) |
| status                 | null   | Estado de la empresa |
| signature_key          | string | Clave de firma encriptada                 |
| ambients_id            | number | Identificador del ambiente                |
| created_at             | string | Fecha y hora de la creación               |
| updated_at             | string | Fecha y hora de la última actualización   |
| id_iva                 | number | Identificador del IVA                     |
| info_issuing           | null   | Información adicional de emisión          |

