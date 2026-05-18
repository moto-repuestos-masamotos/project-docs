# Modelo Lógico – Tienda de Repuestos para Motos

## 1. Introducción
El modelo lógico representa la estructura de la base de datos a partir del modelo conceptual, definiendo tablas, atributos, llaves primarias y relaciones mediante llaves foráneas.

Este modelo servirá como base para la implementación física en PostgreSQL utilizando Liquibase.

## 2. Tablas del sistema

### Cliente
cliente(
- id_cliente (PK)
- nombre
- correo
- telefono
)

### Categoria
categoria(
- id_categoria (PK)
- nombre
)

### Marca
marca(
- id_marca (PK)
- nombre
)

### Producto
producto(
- id_producto (PK)
- categoria_id (FK)
- marca_id (FK)
- nombre
- precio
)

### Inventario
inventario(
- id_inventario (PK)
- producto_id (FK)
- cantidad
)

### TipoMovimientoInventario
tipo_movimiento_inventario(
- id_tipo (PK)
- nombre
)

### MovimientoInventario
movimiento_inventario(
- id_movimiento (PK)
- inventario_id (FK)
- tipo_movimiento_id (FK)
- cantidad
- fecha
)

### EstadoPedido
estado_pedido(
- id_estado (PK)
- nombre
)

### Pedido
pedido(
- id_pedido (PK)
- cliente_id (FK)
- estado_pedido_id (FK)
- fecha
)

### DetallePedido
detalle_pedido(
- id_detalle (PK)
- pedido_id (FK)
- producto_id (FK)
- cantidad
- precio_unitario
)

### EstadoFactura
estado_factura(
- id_estado (PK)
- nombre
)

### Factura
factura(
- id_factura (PK)
- pedido_id (FK)
- estado_factura_id (FK)
- total
- fecha
)

### MetodoPago
metodo_pago(
- id_metodo (PK)
- nombre
)

### Pago
pago(
- id_pago (PK)
- factura_id (FK)
- metodo_pago_id (FK)
- valor
- fecha_pago
)

## 3. Relaciones entre tablas
- Un cliente tiene muchos pedidos (1:N)
- Un pedido pertenece a un cliente

- Un pedido tiene un estado (N:1)
- Un estado_pedido puede estar en muchos pedidos

- Un pedido genera una factura (1:1)

- Una factura tiene un estado (N:1)

- Una factura puede tener varios pagos (1:N)

- Un pago usa un método de pago (N:1)

- Un pedido tiene muchos detalles (1:N)

- Un detalle_pedido pertenece a un producto (N:1)

- Un producto pertenece a una categoría (N:1)

- Un producto pertenece a una marca (N:1)

- Un producto tiene un inventario (1:1)

- Un inventario tiene muchos movimientos (1:N)

- Un movimiento tiene un tipo (N:1)

## 4. Consideraciones de diseño
El modelo lógico se diseñó siguiendo principios de normalización,
evitando redundancia de datos y asegurando la integridad referencial
mediante el uso de llaves foráneas.

Se implementaron tablas de catálogo como categoria, marca, estado_pedido,
estado_factura y metodo_pago para mantener consistencia en los datos.
