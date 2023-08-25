# Autenticación

Chico Chino utiliza API keys para permitir el acceso a la API. Para obtener la misma, se requiere que con anterioridad Ud. tenga su ID y Clave Secreta de Cliente entregado por el equipo de Desarrollo.

## Generar Token

```shell
curl -k  -L -X POST -H 'Content-Type: application/json'
-d '{
    "grant_type": "client_credentials",
    "client_id": "123",
    "client_secret": "abcdefghijklmnopqrstuvwxyz"
}' 'https://app.chicochino.com.ec/oauth/token'
```

```php
$url = 'https://app.chicochino.com.ec/oauth/token';

$data = array(
    "grant_type" => "client_credentials",
    "client_id" => "123",
    "client_secret" => "abcdefghijklmnopqrstuvwxyz"
);

$options = array(
    CURLOPT_URL => $url,
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_POST => true,
    CURLOPT_POSTFIELDS => json_encode($data),
    CURLOPT_HTTPHEADER => array('Content-Type: application/json')
);

$ch = curl_init();
curl_setopt_array($ch, $options);
$response = curl_exec($ch);
curl_close($ch);

echo $response;
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "token_type": "Bearer",
    "expires_in": 31622400,
    "access_token": "your_token"
}
```

Para generar su API key debe hacer una petición al servidor con la ID y clave, luego recibirá una API key única, con validez de un (1) año, debe almacenar la misma en un lugar NO público, ya que la misma adicional de dar acceso al uso de los diferentes Endpoint, le identificará a Ud. para las diferentes transacciones.

### HTTP Request

`POST https://app.chicochino.com.ec/oauth/token`

### Parámetros URL

Parámetro | Descripción
--------- | -----------
grant_type | Tipo de concesión
client_id | Es el identificador público de la aplicación. Una aplicación es el resultado de registrar un nuevo cliente en nuestro servidor OAuth. El mismo que usamos en la primera petición.
client_secret | es una contraseña o secreto que generaremos en el servidor de OAuth en relación con el cliente (la aplicación).

### Respuesta

Parámetro | Descripción
--------- | -----------
token_type | Indicará el tipo de token generado, por defecto "Bearer"
expires_in | Contiene el número de segundos hasta que expire el token de acceso
access_token | Este será su `token` que tendrá que incluir en adelante en todas las peticiones en la cabecera `Header`

> Para consumir los endpoints, use este código:

```shell
# Con Shell, puede simplemente pasar el 
# encabezado correcto con cada solicitud.
curl "api_endpoint_here" \
  -H "Authorization: Bearer token"
```

```php
$apiEndpoint = "api_endpoint_here";
$accessToken = "your_bearer_token";

$ch = curl_init($apiEndpoint);

$options = array(
    CURLOPT_RETURNTRANSFER => true,
    CURLOPT_HTTPHEADER => array(
        'Authorization: Bearer ' . $accessToken
    )
);

curl_setopt_array($ch, $options);
$response = curl_exec($ch);
curl_close($ch);

echo $response;
```

> Asegúrese de reemplazar `token` con su token generado anteriormente.

Chico Chino espera que el `token` se incluya en todas las solicitudes de API al servidor en un encabezado similar al siguiente:

`Authorization: Bearer 'token'`

<aside class="notice">
Debe reemplazar <code>'token'</code> con el su token generado anteriormente.
</aside>