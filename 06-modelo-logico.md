# Modelo Lógico – Tienda de Repuestos para Motos

## 1. Introducción

El modelo lógico representa la transición entre el modelo conceptual y el modelo físico,
definiendo la estructura de la base de datos mediante tablas, atributos, tipos de datos,
restricciones y relaciones.

En esta fase se incorporan detalles técnicos como claves primarias, llaves foráneas,
restricciones de integridad (NOT NULL, UNIQUE) y la definición de relaciones,
garantizando consistencia de los datos y preparando la implementación en PostgreSQL
mediante Liquibase.

---

## 2. Tablas del sistema

### cliente
cliente(
- id_cliente INT (PK)
- nombre VARCHAR(100) NOT NULL
- correo VARCHAR(100) UNIQUE NOT NULL
- telefono VARCHAR(20)
)

---

### categoria
categoria(
- id_categoria INT (PK)
- nombre VARCHAR(100) NOT NULL UNIQUE
)

---

### marca
marca(
- id_marca INT (PK)
- nombre VARCHAR(100) NOT NULL UNIQUE
)

---

### producto
producto(
- id_producto INT (PK)
- categoria_id INT (FK → categoria.id_categoria) NOT NULL
- marca_id INT (FK → marca.id_marca) NOT NULL
- nombre VARCHAR(100) NOT NULL
- descripcion TEXT
- precio DECIMAL(10,2) NOT NULL
)

---

### inventario
inventario(
- id_inventario INT (PK)
- producto_id INT (FK → producto.id_producto) UNIQUE NOT NULL
- cantidad INT NOT NULL
)

---

### tipo_movimiento_inventario
tipo_movimiento_inventario(
- id_tipo_movimiento INT (PK)
- nombre VARCHAR(50) NOT NULL UNIQUE
)

---

### movimiento_inventario
movimiento_inventario(
- id_movimiento INT (PK)
- inventario_id INT (FK → inventario.id_inventario) NOT NULL
- tipo_movimiento_id INT (FK → tipo_movimiento_inventario.id_tipo_movimiento) NOT NULL
- cantidad INT NOT NULL
- fecha DATE NOT NULL
)

---

### estado_pedido
estado_pedido(
- id_estado_pedido INT (PK)
- nombre VARCHAR(50) NOT NULL UNIQUE
)

---

### pedido
pedido(
- id_pedido INT (PK)
- cliente_id INT (FK → cliente.id_cliente) NOT NULL
- estado_pedido_id INT (FK → estado_pedido.id_estado_pedido) NOT NULL
- fecha_pedido DATE NOT NULL
)

---

### detalle_pedido
detalle_pedido(
- id_detalle INT (PK)
- pedido_id INT (FK → pedido.id_pedido) NOT NULL
- producto_id INT (FK → producto.id_producto) NOT NULL
- cantidad INT NOT NULL
- precio_unitario DECIMAL(10,2) NOT NULL
)

---

### estado_factura
estado_factura(
- id_estado_factura INT (PK)
- nombre VARCHAR(50) NOT NULL UNIQUE
)

---

### factura
factura(
- id_factura INT (PK)
- pedido_id INT (FK → pedido.id_pedido) UNIQUE NOT NULL
- estado_factura_id INT (FK → estado_factura.id_estado_factura) NOT NULL
- numero_factura VARCHAR(20) UNIQUE NOT NULL
- total DECIMAL(10,2) NOT NULL
- fecha_factura DATE NOT NULL
)

---

### metodo_pago
metodo_pago(
- id_metodo_pago INT (PK)
- nombre VARCHAR(50) NOT NULL UNIQUE
)

---

### pago
pago(
- id_pago INT (PK)
- factura_id INT (FK → factura.id_factura) NOT NULL
- metodo_pago_id INT (FK → metodo_pago.id_metodo_pago) NOT NULL
- valor DECIMAL(10,2) NOT NULL
- fecha_pago DATE NOT NULL
)

---

## 3. Relaciones entre tablas

- Cliente (1) —— (N) Pedido  
- Pedido (N) —— (1) EstadoPedido  
- Pedido (1) —— (1) Factura  
- Factura (N) —— (1) EstadoFactura  
- Factura (1) —— (N) Pago  
- Pago (N) —— (1) MetodoPago  
- Producto (N) —— (1) Categoria  
- Producto (N) —— (1) Marca  
- Producto (1) —— (1) Inventario  
- Inventario (1) —— (N) MovimientoInventario  
- MovimientoInventario (N) —— (1) TipoMovimientoInventario  

---

### Relación N:M

Existe una relación muchos a muchos (N:M) entre:

- Pedido y Producto  

La cual se resuelve mediante la tabla intermedia:

- detalle_pedido  

Esto permite:
- que un pedido tenga múltiples productos  
- que un producto pueda estar en múltiples pedidos  

---

## 4. Consideraciones de diseño

- Se implementaron restricciones NOT NULL para campos obligatorios  
- Se utilizaron restricciones UNIQUE en atributos clave para evitar duplicidad  
- Se definieron claves foráneas explícitas para garantizar integridad referencial  
- Se mantuvo consistencia en los nombres de claves primarias  
- El modelo cumple con principios de normalización  
- Se asegura coherencia entre modelo conceptual, lógico y físico