# Modelo Conceptual Formal – Tienda de Repuestos para Motos

## 1. Introducción

Este documento describe el modelo conceptual formal del sistema de gestión
para una tienda física de venta de repuestos para motos.

En este modelo se definen las entidades principales del sistema, sus relaciones
y cardinalidades, sirviendo como base para el modelo lógico y la implementación
de la base de datos.

## 2. Entidades del sistema

### Cliente
Representa a la persona que realiza compras en la tienda.
Un cliente puede realizar uno o varios pedidos.

### Producto
Representa un repuesto para motocicleta disponible para la venta.
Cada producto tiene precio, pertenece a una categoría y a una marca,
y se controla en inventario.

### Categoria
Representa la clasificación de los productos (ej: motor, frenos, eléctricos).
Una categoría puede tener múltiples productos asociados.

### Marca
Representa la marca a la cual pertenece un producto.
Una marca puede tener múltiples productos asociados.

### Pedido
Representa la solicitud de compra realizada por un cliente.
Un pedido contiene uno o varios productos y posee un estado.

### EstadoPedido
Representa el estado del pedido (pendiente, completado, anulado).

### Factura
Representa el comprobante de venta generado a partir de un pedido.
Cada factura tiene un estado.

### EstadoFactura
Representa el estado de la factura (activa, anulada).

### Pago
Representa el registro del pago realizado por una factura.

### MetodoPago
Representa las formas de pago disponibles (efectivo, tarjeta, etc.).

### Inventario
Representa el control de existencias de los productos.

### MovimientoInventario
Registra cada cambio realizado en el inventario de un producto.

### TipoMovimientoInventario
Define el tipo de movimiento (entrada, salida, ajuste, devolución).

## 3. Relaciones entre entidades

- Un cliente realiza pedidos.
- Un pedido pertenece a un cliente.
- Un pedido genera una factura.
- Una factura registra uno o varios pagos.
- Un pago utiliza un método de pago.
- Un pedido tiene un estado.
- Una factura tiene un estado.
- Un pedido incluye productos.
- Un producto pertenece a una marca.
- Un producto pertenece a una categoría.
- Cada producto está controlado por el inventario.
- El inventario registra movimientos.
- Un movimiento inventario tiene un tipo de movimiento.

## 4. Cardinalidades

- Cliente (1) —— (N) Pedido  
  Un cliente puede realizar muchos pedidos, pero un pedido pertenece a un solo cliente.

- Pedido (1) —— (1) Factura  
  Cada pedido genera una única factura.

- Factura (1) —— (N) Pago  
  Una factura puede tener uno o varios pagos.

- MetodoPago (1) —— (N) Pago  
  Un método de pago puede utilizarse en muchos pagos.

- Pedido (N) —— (M) Producto  
  Un pedido puede contener varios productos y un producto puede estar en muchos pedidos.

- Marca (1) —— (N) Producto  
  Una marca puede tener muchos productos, pero un producto pertenece a una sola marca.

- Categoria (1) —— (N) Producto  
  Una categoría puede tener muchos productos, pero un producto pertenece a una sola categoría.

- Pedido (N) —— (1) EstadoPedido  
  Varios pedidos pueden tener el mismo estado.

- Factura (N) —— (1) EstadoFactura  
  Varias facturas pueden tener el mismo estado.

- Producto (1) —— (1) Inventario  
  Cada producto tiene un único registro de inventario.

- Inventario (1) —— (N) MovimientoInventario  
  Un inventario puede tener múltiples movimientos registrados.

- TipoMovimientoInventario (1) —— (N) MovimientoInventario  
  Un tipo de movimiento puede aplicarse a muchos registros.

## 5. Observaciones

Este modelo conceptual formal representa de manera completa la lógica del negocio,
incluyendo clasificación de productos por categoría y marca, gestión de estados,
métodos de pago y trazabilidad del inventario mediante movimientos.

Este modelo servirá como base para el modelo lógico del sistema en la siguiente fase.