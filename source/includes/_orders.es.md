# Pedidos

## Listar pedidos que no están marcados como facturados


```shell
# Se asume que abcdedghi... es el token
curl "https://app.chicochino.com.ec/api/v1/invoice/orders" \
  -H "Authorization: Bearer abcdedghi..."
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
[
    {
        "id": 100007,
        "user_id": null,
        "order_amount": 42.44,
        "coupon_discount_amount": 0,
        "coupon_discount_title": null,
        "payment_status": "paid",
        "order_status": "delivered",
        "total_tax_amount": 3.19,
        "payment_method": "cash",
        "transaction_reference": null,
        "checked": 1,        
        "delivery_charge": 0,
        "order_note": null,
        "coupon_code": null,
        "order_type": "pos",
        "branch_id": 1,
        "extra_discount": "0.00",
        "invoiced": false,
        "customer": null,
        "details": [
            {
                "id": 9,
                "product_id": 12,
                "order_id": 100007,
                "price": 13.3,
                "product_details": {
                    "id": 12,
                    "name": "Combo Familiar",
                    "description": "1 Pollo entero/ 8 presas, porción de papas fritas, porción de menestra, porción de arroz",
                    "image": "2023-06-08-6480e66929009.png",
                    "price": 20.3,
                    "tax": 12,
                    "discount": 0,
                    "discount_type": "percent",
                    "tax_type": "percent",
                    "branch_id": 1,
                    "translations": []
                },
                "variation": [
                    {
                        "Tamaño": "Medio Combo"
                    }
                ],
                "discount_on_product": 0,
                "discount_type": "discount_on_product",
                "quantity": 2,
                "tax_amount": 1.6,
                "variant": "\"MedioCombo\"",
                "add_ons": [
                    {
                        "id": 1,
                        "name": "Presa de pollo",
                        "price": 2.75,
                        "qty": "1"
                    },
                    {
                        "id": 3,
                        "name": "Porción Ensalada",
                        "price": 3.3,
                        "qty": "3"
                    }
                ]
            }
        ]
    },
    {
        "id": 100008,
        "user_id": 2,
        "order_amount": 42.44,
        "coupon_discount_amount": 0,
        "coupon_discount_title": null,
        "payment_status": "paid",
        "order_status": "delivered",
        "total_tax_amount": 3.19,
        "payment_method": "card",
        "transaction_reference": "AB-1234",
        "checked": 1,
        "delivery_charge": 1.50,
        "order_note": null,
        "coupon_code": null,
        "order_type": "web",
        "branch_id": 1,
        "extra_discount": "0.00",
        "invoiced": false,
        "customer": {
            "id": 2,
            "f_name": "Luis",
            "l_name": "Ortiz",
            "identification": "1712345678",
            "email": "luis@gmail.com",
            "image": null,
            "phone": "+593999905876",
        },
        "details": [
            {
                "id": 10,
                "product_id": 12,
                "order_id": 100008,
                "price": 13.3,
                "product_details": {
                    "id": 12,
                    "name": "Combo Familiar",
                    "description": "1 Pollo entero/ 8 presas, porción de papas fritas, porción de menestra, porción de arroz",
                    "image": "2023-06-08-6480e66929009.png",
                    "price": 20.3,
                    "tax": 12,
                    "discount": 0,
                    "discount_type": "percent",
                    "tax_type": "percent",
                    "branch_id": 1,
                    "translations": []
                },
                "variation": [
                    {
                        "Tamaño": "Medio Combo"
                    }
                ],
                "discount_on_product": 0,
                "discount_type": "discount_on_product",
                "quantity": 2,
                "tax_amount": 1.6,
                "variant": "\"MedioCombo\"",
                "add_ons": [
                    {
                        "id": 1,
                        "name": "Presa de pollo",
                        "price": 2.75,
                        "qty": "1"
                    },
                    {
                        "id": 3,
                        "name": "Porción Ensalada",
                        "price": 3.3,
                        "qty": "3"
                    }
                ]
            }
        ]
    }
]
```

Este endpoint recupera todos los pedidos que no se han marcado como facturados.

<aside class="notice">
Debe reemplazar <code>abcdedghi...</code> con su token generado anteriormente. <a href='#generar-token'>Como generar token</a>
</aside>

### HTTP Request

`GET https://app.chicochino.com.ec/api/v1/invoice/orders`

### Respuesta

Parámetro | Descripción
--------- | -----------
id | Identificador o número de pedido.
user_id | Identificador del cliente en el sistema.
order_amount | Valor total del pedido (Productos + Impuestos + Valor de envío - Descuentos).
coupon_discount_amount | Valor de descuento por cupón.
coupon_discount_title | Título de cupón de descuento.
payment_status | Estado de pago: **paid** o **unpaid**. Por defecto este endpoint solo responderá con los pedidos en estado paid.
order_status | Estado del pedido: **pending**, **out_for_delivery**, **delivered**, **failed**. En este se recibe el estado de **pendiente**, **en camino**, **entregado**, y **falló** respectivamente.
total_tax_amount | Monto de impuesto calculado por el sistema.
payment_method | Método de pago: **cash**, **card**. Los métodos de pagos pueden variar en el tiempo.
transaction_reference | Referencia de transacción. Proveniente del método de pago.
checked | Indica si el pedido ha sido revisado por el operador.
delivery_charge | Costo de envío 
order_note | Nota del pedido
coupon_code | Código de cupón *si aplica* caso contrario retorna null
order_type | Indica el canal por donde se recibió el pedido: **pos** *Recibido por el panel POS del sistema*, **app** *Recibido por medio de la aplicación móvil*, **web** *Recibo por medio de la página web*.
branch_id | Id de la sucursal que recibió el pedido
extra_discount | Descuento extra que haya recibido
invoiced | Booleano **true** o **false**, indica si el pedido ya fue facturado o no.
customer | Objeto **Cliente** contiene la información y detalle del cliente [ver Cliente](#cliente), en caso de no registrar retorna el valor **null**. (En este caso facturar como *Consumidor Final*).
details | Detalle del pedido en **array** donde contiene el o los productos ordenados <a href='#detalle'> ver Detalle</a>.

### Cliente
Respuesta contenida en el json recibido en el Endpoint **invoice/orders** nombrado como **customer**.

Parámetro | Descripción
--------- | -----------
id | Identificador del cliente dentro del sistema.
f_name | Nombre del cliente.
l_name | Apellido del cliente.
identification | Número de identificación del cliente (*Cédula, RUC, o Pasaporte*).
email | Correo electrónico del cliente.
image | Imagen de perfil del cliente.
phone | Número de teléfono/celular del cliente.

### Detalle
Respuesta contenida en el json recibido en el Endpoint **invoice/orders** nombrado como **details**, aquí se explica el detalle individual contenido dentro del **array**.
<aside class="notice">
El atributo <code>details</code> puede contener uno o varios detalles del pedido.
</aside>

Parámetro | Descripción
--------- | -----------
id | Identificador del detalle.
product_id | Identificador del producto.
order_id | Identificador del pedido asociado al detalle.
price | Valor del producto **Tomar este valor al facturar**.
product_details.id | Identificador del producto.
product_details.name | Nombre del producto
product_details.description | Descripción del producto.
product_details.image | URL de la imagen del producto.
product_details.price | Valor *referencial* del producto *(Puede variar al valor cobrado, ya que puede que se haya seleccionado alguna variante del mismo o aplicado algún descuento)*.
product_details.tax | Impuesto aplicado al producto.
product_details.discount | Descuento aplicado al prducto.
product_details.discount_type | Tipo de descuento aplicado **percent** o **plane**, es decir, porcentaje o valor fijo respectivamente.
product_details.tax_type | Tipo de impuesto aplicado **percent** o **plane**, es decir, porcentaje o valor fijo respectivamente.
product_details.branch_id | Identificador de la sucursal aplicada.
product_details.translations | Traducciones del producto en diferentes idiomas *(Si aplica)*.
variation | **Array dinámico** Contiene la variación del producto aplicada.
discount_on_product | Contiene el descuento aplicado en el producto.
discount_type | Contiene el tipo de descuento aplicado en el producto.
quantity | Indica la cantidad del producto aplicado en este detalle.
tax_amount | Valor de impuesto aplicado al producto.
variant | Identificador en el sistema de la variación del producto.
**add_ons** | **Array** que contiene los productos adicionales solicitados, relacionados a este detalle.
add_ons[].id | Identificador del producto adicional.
add_ons[].name | Nombre del producto adicional.
add_ons[].price | Precio del producto adicional.
add_ons[].qty | Cantidad solicitada del producto adicional.

## Marcar pedido como Facturado

```shell
# Se asume que abcdedghi... es el token
curl -k  -L -X POST  -H 'Content-Type: application/json'\
  -H "Authorization: Bearer abcdedghi..." \
  -d '{
      "id": "100001",
      "invoiced":true
  }' 'https://app.chicochino.com.ec/api/v1/invoice/set-order'
```

> Para el request previo, la respuesta es un JSON estructurado como sigue:

```json
{
    "message": {
        "id": 100001,
        "order_amount": 43.6,
        "coupon_discount_amount": 0,
        "coupon_discount_title": null,
        "payment_status": "paid",
        "order_status": "delivered",
        "total_tax_amount": 0,
        "payment_method": "cash_on_delivery",
        "checked": 1,
        "order_type": "delivery",
        "branch_id": 2,
        "extra_discount": "0.00",
        "invoiced": true
    },
    "status": "success"
}
```

> En caso de que falle por algún motivo, tendrá esta respuesta:

```json
{
    "message": "Order not found",
    "status": "failed"
}
```

Este Endpoint marca a un pedido específico como facturado.

### HTTP Request

`POST https://app.chicochino.com.ec/api/v1/invoice/set-order`

<aside class="notice">
Debe reemplazar <code>abcdedghi...</code> con su token generado anteriormente. <a href='#generar-token'>Como generar token</a>
</aside>

### Parámetros URL

Parámetro | Tipo | Descripción
--------- | ---- | -----------
id | String | Identificador o número de pedido.
invoiced | Boolean | Solo aceptará el valor de **true** para confirmar si un pedido fue facturado.

### Respuesta

Parámetro | Descripción
--------- | -----------
**message** | En caso de éxito retornará el detalle resumido del pedido, caso contrario, retornará un *String* con un mensaje acerca del motivo de la falla.
message.id | Identificador o número de pedido.
message.order_amount | Monto del pedido.
message.coupon_discount_amount | Monto de descuento por cupón.
message.coupon_discount_title | Título de cupón de descuento.
message.payment_status | Estado de pago del pedido *paid* o *unpaid*
message.order_status | Estado del pedido
message.total_tax_amount | Monto de impuesto aplicado
message.payment_method | Método de pago
message.checked | Marca *1* si fué verificado por operador o *0* en caso contrario.
message.order_type | Tipo de canal recibido para el pedido.
message.branch_id | Identificado de la sucursal en la que se recibió el pedido.
message.extra_discount | Descuento extra, si aplicara.
message.invoiced | Marcará **true** si se marcó como facturado o **false** en el caso contrario.
status | Contentrá el valor de **success** si se realizó la marca como facturado, o **failed** en caso de alguna falla.