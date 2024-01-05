# Documentos

## Listar Documentos por ID de Punto de Emisión

```shell
# tokenMaquina es el token asignado para la comunicación con el sistema externo
curl "https://contable.contiyess.com/api/v1/documents/all/{id_punto_emision}" \
  -H "Authorization: Bearer tokenUsuario"
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "success": true,
    "message": "",
    "data": []
}
```

> En caso de no tener permisos para acceder a los documentos, la respuesta es un JSON estructurado como sigue:

```json
{
    "success": false,
    "message": "No tiene permiso para ver los documentos de este punto de emisión"
}
```

<aside class="success">
El token de usuario tiene una duración de 1 hora, en caso de que expire tendrá que generar un nuevo token desde el endpoint <a href='#generar-token-de-usuario-desde-correo-electronico'>Generar token de usuario desde email</a>.
</aside>
<aside class="notice">
Debe reemplazar <code>tokenUsuario</code> con su token generado anteriormente. <a href='#generar-token-de-usuario-desde-correo-electronico'>Como generar token</a>
</aside>

### HTTP Request

`GET https://contable.contiyess.com/api/v1/documents/all/{id_punto_emision}`

### Respuesta

| Campo                  | Tipo   | Descripción                               |
|------------------------|--------|-------------------------------------------|
| success                | boolean| Indica si la operación fue exitosa o no   |
| message                | string | Mensaje o información adicional           |
| data                   | array  | Lista de documentos                       |


## Crear Documento

```shell
# tokenMaquina es el token asignado para la comunicación con el sistema externo
curl "https://contable.contiyess.com/api/v1/documents" \
  -H "Authorization: Bearer tokenUsuario"
```

> El JSON a enviar sería el siguiente:

```json
{
  "emission_point_id": 10,
  "emit_date": "2024-01-04",
  "document_type": 1,
  "ambient": 1,
  "person": {
    "identification": "1234567890",
    "name_people": "John Doe",
    "email": "john.doe@example.com",
    "plate": "ABC123",
    "phone_one": "123456789",
    "phone_two": "",
    "address": "123 Main Street",
    "id_type": "5"
  },
  "sub_total_iva": 100.50,
  "sub_total_iva_cero": 50.25,
  "sub_total_noi": 30.75,
  "sub_total_ei": 20.50,
  "sub_total": 201.00,
  "total_discount": 13.00,
  "total_value_ice": 5.00,
  "total_value_irbpnr": 2.50,
  "total_value_iva": 30.00,
  "tip": 5.00,
  "total_value": 290.50,
  "items": [
    {
      "value": 50.00,
      "description": "Item 1",
      "discount_percentage": 10,
      "discount_type": "percent",
      "discount": 5.00,
      "quantity": 2,
      "irbpnr": 1.00,
      "total": 95.00,
      "net_price": 45.00,
      "product_id": 1,
      "iva_id": 2,
      "iva_percentage": 12,
    //   "ice_id": null,
      "code_products": "P123",
      "is_service": true,
      "tax_base": 45,
      "zero_base": 0,
      "non_taxable_base": 0
    },
    {
      "value": 75.50,
      "description": "Item 2",
      "discount_percentage": 0,
      "discount_type": "fixed",
      "discount": 8.00,
      "quantity": 3,
    //   "irbpnr": "",
      "total": 195.50,
      "net_price": 67.50,
      "product_id": 2,
      "iva_id": 2,
      "iva_percentage": 12,
    //   "ice_id": 1,
      "code_products": "P456",
      "is_service": false,
      "tax_base": 67.50,
      "zero_base": 0,
      "non_taxable_base": 0
    }
  ],
  "method_payments": [
    {
      "method_payment": 1,
      "amount": 150.00
    },
    {
      "method_payment": 2,
      "amount": 140.50
    }
  ]
}
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "success": true,
    "message": "Document created success!",
    "data": {
        "authorization": "0401202401171234567800110012000000000014422123018",
        "emit_date": "2024-01-04",
        "number_receipt": "001-200 000000001",
        "serie_receipt": "000000001",
        "receipt_types_id": 1,
        "issuings_id": 8,
        "ambients_id": 1,
        "people_id": 8,
        "emission_point_id": 11,
        "date_venc": null,
        "date_caduca": null,
        "receipt_total_id": 60,
        "status_id": 4,
        "observation": "",
        "user_id": 12,
        "updated_at": "2024-01-05T20:11:26.000000Z",
        "created_at": "2024-01-05T20:11:26.000000Z",
        "id": 46
    }
}
```

<aside class="success">
El token de usuario tiene una duración de 1 hora, en caso de que expire tendrá que generar un nuevo token desde el endpoint <a href='#generar-token-de-usuario-desde-correo-electronico'>Generar token de usuario desde email</a>.
</aside>
<aside class="notice">
Debe reemplazar <code>tokenUsuario</code> con su token generado anteriormente. <a href='#generar-token-de-usuario-desde-correo-electronico'>Como generar token</a>
</aside>

### HTTP Request

`POST https://contable.contiyess.com/api/v1/documents`

### Parámetros URL Factura

| Campo                  | Tipo     | Descripción                                         |
|------------------------|----------|-----------------------------------------------------|
| emission_point_id      | number   | Identificador del punto de emisión                  |
| emit_date              | string   | Fecha de emisión del documento en formato "YYYY-MM-DD" |
| document_type          | number   | Tipo de documento [Tipo Comprobantes](#tipo-de-comprobantes)|
| ambient                | number   | Ambiente de emisión [Ambientes](#ambientes)         |
| person                 | object   | Objeto que contiene información sobre la persona    |
| identification         | string   | Número de identificación de la persona              |
| name_people            | string   | Nombre de la persona                                |
| email                  | string   | Correo electrónico de la persona                   |
| plate                  | string   | Placa de vehículo de la persona (Opcional)          |
| phone_one              | string   | Número de teléfono principal de la persona          |
| phone_two              | string   | Número de teléfono secundario de la persona (Opcional) |
| address                | string   | Dirección de la persona                             |
| id_type                | string   | Tipo de identificación de la persona [Tipo de Identificación](#tipo-de-identificacion) |
| sub_total_iva          | number   | Subtotal gravado con IVA                            |
| sub_total_iva_cero     | number   | Subtotal gravado con IVA al 0%                      |
| sub_total_noi          | number   | Subtotal no objeto de impuestos                     |
| sub_total_ei           | number   | Subtotal exento de impuestos                        |
| sub_total              | number   | Subtotal general                                    |
| total_discount         | number   | Total de descuentos                                 |
| total_value_ice        | number   | Total del impuesto ICE                              |
| total_value_irbpnr     | number   | Total del impuesto IRBPNR                           |
| total_value_iva        | number   | Total del impuesto IVA                              |
| tip                    | number   | Monto de la propina                                 |
| total_value            | number   | Total del documento                                 |
| items                  | array    | Arreglo de ítems que contiene detalles de productos o servicios |
| method_payments        | array    | Arreglo de métodos de pago con montos correspondientes |

**Estructura del objeto "items":**

| Campo                  | Tipo     | Descripción                                         |
|------------------------|----------|-----------------------------------------------------|
| value                  | number   | Valor unitario del ítem                             |
| description            | string   | Descripción del ítem                                |
| discount_percentage    | number   | Porcentaje de descuento aplicado al ítem (Se ignora en caso de que "discount_type" sea "fixed")|
| discount_type          | string   | Tipo de descuento ("percent" para porcentaje, "fixed" para monto fijo) |
| discount               | number   | Monto de descuento aplicado al ítem                |
| quantity               | number   | Cantidad del ítem                                  |
| irbpnr                 | number   | Monto del impuesto IRBPNR aplicado al ítem (puede ser nulo) |
| total                  | number   | Total del ítem (valor * cantidad - descuento + IRBPNR) |
| net_price              | number   | Precio neto del ítem (valor - descuento + IRBPNR)   |
| product_id             | number   | Identificador del producto o servicio (Opcional)|
| iva_id                 | number   | Identificador del tipo de IVA aplicado [IVAs](#iva) |
| iva_percentage         | number   | Porcentaje de IVA aplicado al ítem                 |
| ice_id                 | number   | Identificador del impuesto ICE aplicado (Opcional) |
| code_products          | string   | Código del producto (Puede ser un código personalizado) |
| is_service             | boolean  | Indica si el ítem es un servicio (true) o un producto (false) |
| tax_base               | number   | Base imponible para cálculo de impuestos           |
| zero_base              | number   | Base imponible al 0% para cálculo de impuestos     |
| non_taxable_base       | number   | Base imponible no sujeta a impuestos               |

**Estructura del objeto "method_payments":**

| Campo                  | Tipo     | Descripción                                         |
|------------------------|----------|-----------------------------------------------------|
| method_payment         | number   | Método de pago [Métodos de Pago](#metodos-de-pago) |
| amount                 | number   | Monto correspondiente al método de pago             |


### Respuesta Factura

| Campo                  | Tipo     | Descripción                                         |
|------------------------|----------|-----------------------------------------------------|
| success                | boolean  | Indica si la operación fue exitosa o no             |
| message                | string   | Mensaje informativo sobre la creación del documento |
| data                   | object   | Objeto contenedor de los datos de respuesta         |
| authorization          | string   | Número de autorización del documento               |
| emit_date              | string   | Fecha de emisión del documento en formato "YYYY-MM-DD" |
| number_receipt         | string   | Número de comprobante                              |
| serie_receipt          | string   | Serie del comprobante                              |
| receipt_types_id       | number   | Identificador del tipo de comprobante              |
| issuings_id            | number   | Identificador del emisor                           |
| ambients_id            | number   | Identificador del ambiente de emisión              |
| people_id              | number   | Identificador de la persona asociada al documento  |
| emission_point_id      | number   | Identificador del punto de emisión                 |
| date_venc              | null     | Fecha de vencimiento del documento (nulo en este caso) |
| date_caduca            | null     | Fecha de caducidad del documento (nulo en este caso) |
| receipt_total_id       | number   | Identificador del total del recibo                 |
| status_id              | number   | Identificador del estado del documento             |
| observation            | string   | Observaciones asociadas al documento               |
| user_id                | number   | Identificador del usuario que creó el documento     |
| updated_at             | string   | Fecha y hora de la última actualización            |
| created_at             | string   | Fecha y hora de la creación                         |
| id                     | number   | Identificador único del documento                  |
