# Procesos y Requerimientos del Sistema

## 1. Procesos del dominio
### Proceso de venta
El proceso de venta inicia cuando un cliente selecciona uno o varios repuestos
en la tienda. El vendedor registra la información de la venta en el sistema,
lo que da origen a un pedido y posteriormente a una factura.

### Proceso de pedido
El pedido representa la solicitud de compra realizada por un cliente.
En este proceso se asocian los productos seleccionados, las cantidades
y el cliente que realiza la compra.

### Proceso de facturación
La facturación se genera a partir de un pedido registrado.
Este proceso permite calcular el total de la venta y generar el comprobante
correspondiente.

### Proceso de inventario
El proceso de inventario controla las existencias de los productos.
Cada vez que se realiza una venta, el sistema debe actualizar las cantidades
disponibles de los repuestos.

## 2. Requerimientos funcionales (RF)
RF-01 El sistema debe permitir registrar clientes.
RF-02 El sistema debe permitir registrar productos con su información básica.
RF-03 El sistema debe permitir registrar pedidos realizados por los clientes.
RF-04 El sistema debe permitir asociar uno o varios productos a un pedido.
RF-05 El sistema debe permitir generar una factura a partir de un pedido.
RF-06 El sistema debe permitir registrar pagos asociados a una factura.
RF-07 El sistema debe permitir consultar pedidos, facturas y pagos registrados.
RF-08 El sistema debe actualizar el inventario al registrarse una venta.

## 3. Requerimientos no funcionales (RNF)
RNF-01 La base de datos debe garantizar integridad referencial entre las entidades.
RNF-02 La base de datos debe evitar la duplicidad de información.
RNF-03 La base de datos debe permitir consultas eficientes sobre ventas y productos.
RNF-04 La estructura de la base de datos debe estar normalizada.
RNF-05 La base de datos debe soportar control de inventario por cantidad.
RNF-06 La base de datos debe permitir auditoría básica de registros (fechas).