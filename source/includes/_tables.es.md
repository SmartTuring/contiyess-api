# Tablas

## Ambientes

| Tipo de ambiente | Código | Requisito
|-|:-:|-|
| Pruebas | 1 | Obligatorio
| Producción | 2 | Obligatorio

## Tipo de Comprobantes
<aside class="notice">
Actualmente solo funciona la generación de Facturas.
</aside>

| Nombre Comprobante | Código | Requisito
|-|:-:|-|
| Factura | 1 | Obligatorio
| Liquidación de compra de bienes y prestación de servicios | 3 | Obligatorio
| Nota de Crédito | 4 | Obligatorio
| Nota de Débito | 5 | Obligatorio
| Guía de Remisión | 6 | Obligatorio
| Comprobante de Retención | 7 | Obligatorio

## Tipo de Identificación

| Identificación Receptor | Código 
|-|:-:|
| RUC | 4
| Cédula de Ciudadanía | 5
| Pasaporte | 6
| Venta a consumidor final* | 7
| Identificación del exterior* | 8

*Venta a consumidor final: se consignará 13 dígitos de nueve en la identificación del cliente (9999999999999).

*Identificación del exterior: corresponderá al número de Identificación otorgado por la Administración Tributaria (AT) del país que es residente fiscal.

* En el caso de emisión de liquidaciones de compra de bienes y prestación de servicios no se encuentra habilitado el uso del tipo de identificación venta a consumidor final.

* En el caso de emisión de notas de crédito, notas de débito y comprobantes de retención, se debe obligatoriamente identificar al receptor o sujeto retenido con el tipo de identificación correspondiente (RUC, cédula, pasaporte o identificación del exterior).

## Tipo de Descuento

| Tipo de descuento | Código 
|-|:-:|
| Porcentaje | percent
| Valor fijo | fixed

<aside class="notice">
En caso de marcar un descuento con valor fijo, se omitirá el valor de porcentaje de descuento.
</aside>

## IVA

| Porcentaje de IVA | Código 
|-|:-:|
| 0% | 0
| 12% | 2
| 14% | 3
| No Objeto de Impuesto | 6
| Excento de IVA | 7
| IVA Diferenciado* | 8

*Mediante decreto ejecutivo el presidente de la República podrá aplicar una tarifa de IVA diferenciada entre el 8% al 12% para el sector turístico hasta 12 días al año. El código deberá utilizarse para registrar las tarifas de IVA iguales o mayores a 8% y menores a 12% según se establezca en el respectivo decreto, para el resto de los porcentajes y casos se deberán utilizar los códigos específicos previstos en la misma tabla.

## Métodos de Pago

| Nombre Métodos de Pago  | Código |
|-------------------------|:------:|
| Efectivo                |   1    |
| Tarjeta de débito       |   2    |
| Tarjeta de crédito      |   3    |
| Cheque                  |   4    |
| Transferencia           |   5    |
| Cuentas por Cobrar      |   6    |
| Facturación Interna     |   7    |
| Prepago                 |   8    |
| Nota de Crédito         |   9    |

