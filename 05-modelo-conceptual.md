## Modelo Conceptual Formal – Tienda de Repuestos para Motos

### 1. Introducción

Este documento describe el modelo conceptual formal del sistema de gestión para una tienda física de venta de repuestos para motos.

Este modelo conceptual se construye a partir de los requerimientos funcionales y las reglas de negocio previamente definidas, garantizando que las entidades y relaciones representen correctamente los procesos del dominio como la venta, facturación, pagos y control de inventario.

---

### 2. Entidades del sistema

#### Cliente
Representa a la persona que realiza compras en la tienda.
Un cliente puede realizar uno o varios pedidos.

#### Producto
Representa un repuesto disponible para la venta.
Cada producto tiene precio, pertenece a una categoría y a una marca, y se controla en inventario.

#### Categoria
Representa la clasificación de los productos.
Una categoría puede tener múltiples productos asociados.

#### Marca
Representa la marca de los productos.
Una marca puede tener múltiples productos asociados.

#### Pedido
Representa la solicitud de compra realizada por un cliente.
Un pedido contiene uno o varios productos y posee un estado.

#### EstadoPedido
Representa el estado del pedido (pendiente, completado, anulado).

#### Factura
Representa el comprobante de venta generado a partir de un pedido.

#### EstadoFactura
Representa el estado de la factura (activa, anulada).

#### Pago
Representa el registro del pago de una factura.

#### MetodoPago
Representa los tipos de pago disponibles.

#### Inventario
Representa el control de existencias de los productos.

#### MovimientoInventario
Registra los cambios en el inventario.

#### TipoMovimientoInventario
Define el tipo de movimiento aplicado.

---

### 3. Relaciones entre entidades

- Un cliente realiza pedidos.
- Un pedido pertenece a un cliente.
- Un pedido genera una factura.
- Una factura tiene uno o varios pagos.
- Un pago utiliza un método de pago.
- Un pedido tiene un estado.
- Una factura tiene un estado.
- Un pedido incluye productos.
- Un producto pertenece a una marca.
- Un producto pertenece a una categoría.
- Cada producto tiene inventario.
- El inventario registra movimientos.
- Cada movimiento tiene un tipo de movimiento.

---

### 4. Cardinalidades

- Cliente (1) —— (N) Pedido  
- Pedido (1) —— (1) Factura  
- Factura (1) —— (N) Pago  
- MetodoPago (1) —— (N) Pago  
- Pedido (N) —— (M) Producto  
- Marca (1) —— (N) Producto  
- Categoria (1) —— (N) Producto  
- Pedido (N) —— (1) EstadoPedido  
- Factura (N) —— (1) EstadoFactura  
- Producto (1) —— (1) Inventario  
- Inventario (1) —— (N) MovimientoInventario  
- TipoMovimientoInventario (1) —— (N) MovimientoInventario  

---

### 5. Observaciones

El modelo conceptual representa la lógica completa del dominio, incluyendo clasificación de productos, control de estados, métodos de pago y trazabilidad del inventario.

---

### 6. Relación con otros documentos

El modelo conceptual presentado se basa en:

- Los requerimientos funcionales definidos en el sistema.
- Las reglas de negocio que establecen las restricciones del dominio.

Este modelo servirá como base para el diseño del modelo lógico y la posterior implementación física de la base de datos.