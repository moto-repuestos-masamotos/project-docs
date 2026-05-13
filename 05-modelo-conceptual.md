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
Un cliente puede realizar uno o varios pedidos a lo largo del tiempo.

### Producto
Representa un repuesto para motocicleta disponible para la venta.
Cada producto cuenta con un precio y es controlado mediante inventario.

### Pedido
Representa la solicitud de compra realizada por un cliente.
Un pedido agrupa uno o varios productos seleccionados.

### Factura
Representa el comprobante de venta generado a partir de un pedido.
Cada factura corresponde a un único pedido.

### Pago
Representa el registro del pago realizado por una factura.
Una factura puede tener uno o varios pagos.

### Inventario
Representa el control de existencias de los productos en la tienda.
Permite conocer la cantidad disponible de cada producto.


## 3. Relaciones entre entidades
- Un cliente realiza pedidos.
- Un pedido pertenece a un cliente.
- Un pedido genera una factura.
- Una factura registra uno o varios pagos.
- Un pedido incluye productos.
- Cada producto está controlado por el inventario.

## 4. Cardinalidades
- Cliente (1) —— (N) Pedido
  Un cliente puede realizar muchos pedidos, pero un pedido pertenece a un solo cliente.

- Pedido (1) —— (1) Factura  
  Cada pedido genera una única factura.

- Factura (1) —— (N) Pago  
  Una factura puede tener uno o varios pagos.

- Pedido (N) —— (M) Producto  
  Un pedido puede incluir varios productos y un producto puede aparecer en muchos pedidos.

- Producto (1) —— (1) Inventario  
  Cada producto tiene un único registro de inventario.

## 5. Observaciones
Este modelo conceptual formal podrá ajustarse en fases posteriores del proyecto
para optimizar la normalización y la implementación física de la base de datos.