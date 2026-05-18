# Modelo Físico – Tienda de Repuestos para Motos

## 1. Introducción

El modelo físico representa la implementación final de la base de datos en PostgreSQL, 
definiendo estructuras, tipos de datos, restricciones, llaves primarias y foráneas.

Este modelo garantiza integridad referencial, consistencia de los datos y cumplimiento
de reglas de negocio, y es ejecutado mediante Liquibase en un entorno Docker.

---

## 2. Definición de tablas

```sql
CREATE TABLE cliente (
    id_cliente INT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    correo VARCHAR(100) UNIQUE NOT NULL,
    telefono VARCHAR(20)
);

CREATE TABLE categoria (
    id_categoria INT PRIMARY KEY,
    nombre VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE marca (
    id_marca INT PRIMARY KEY,
    nombre VARCHAR(100) UNIQUE NOT NULL
);

CREATE TABLE producto (
    id_producto INT PRIMARY KEY,
    categoria_id INT NOT NULL,
    marca_id INT NOT NULL,
    nombre VARCHAR(100) NOT NULL,
    descripcion TEXT,
    precio DECIMAL(10,2) NOT NULL CHECK (precio > 0),
    FOREIGN KEY (categoria_id) REFERENCES categoria(id_categoria),
    FOREIGN KEY (marca_id) REFERENCES marca(id_marca)
);

CREATE TABLE inventario (
    id_inventario INT PRIMARY KEY,
    producto_id INT UNIQUE NOT NULL,
    cantidad INT NOT NULL CHECK (cantidad >= 0),
    FOREIGN KEY (producto_id) REFERENCES producto(id_producto)
);

CREATE TABLE tipo_movimiento_inventario (
    id_tipo_movimiento INT PRIMARY KEY,
    nombre VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE movimiento_inventario (
    id_movimiento INT PRIMARY KEY,
    inventario_id INT NOT NULL,
    tipo_movimiento_inventario_id INT NOT NULL,
    cantidad INT NOT NULL,
    fecha_movimiento DATE NOT NULL,
    FOREIGN KEY (inventario_id) REFERENCES inventario(id_inventario),
    FOREIGN KEY (tipo_movimiento_inventario_id) 
        REFERENCES tipo_movimiento_inventario(id_tipo_movimiento)
);

CREATE TABLE estado_pedido (
    id_estado_pedido INT PRIMARY KEY,
    nombre VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE pedido (
    id_pedido INT PRIMARY KEY,
    cliente_id INT NOT NULL,
    estado_pedido_id INT NOT NULL,
    fecha_pedido DATE NOT NULL,
    FOREIGN KEY (cliente_id) REFERENCES cliente(id_cliente),
    FOREIGN KEY (estado_pedido_id) REFERENCES estado_pedido(id_estado_pedido)
);

CREATE TABLE detalle_pedido (
    id_detalle_pedido INT PRIMARY KEY,
    pedido_id INT NOT NULL,
    producto_id INT NOT NULL,
    cantidad INT NOT NULL CHECK (cantidad > 0),
    precio_unitario DECIMAL(10,2) NOT NULL CHECK (precio_unitario > 0),
    FOREIGN KEY (pedido_id) REFERENCES pedido(id_pedido),
    FOREIGN KEY (producto_id) REFERENCES producto(id_producto)
);

CREATE TABLE estado_factura (
    id_estado_factura INT PRIMARY KEY,
    nombre VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE factura (
    id_factura INT PRIMARY KEY,
    pedido_id INT UNIQUE NOT NULL,
    estado_factura_id INT NOT NULL,
    numero_factura VARCHAR(20) UNIQUE NOT NULL,
    total DECIMAL(10,2) NOT NULL CHECK (total > 0),
    fecha_factura DATE NOT NULL,
    FOREIGN KEY (pedido_id) REFERENCES pedido(id_pedido),
    FOREIGN KEY (estado_factura_id) REFERENCES estado_factura(id_estado_factura)
);

CREATE TABLE metodo_pago (
    id_metodo_pago INT PRIMARY KEY,
    nombre VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE pago (
    id_pago INT PRIMARY KEY,
    factura_id INT NOT NULL,
    metodo_pago_id INT NOT NULL,
    valor DECIMAL(10,2) NOT NULL CHECK (valor > 0),
    fecha_pago DATE NOT NULL,
    FOREIGN KEY (factura_id) REFERENCES factura(id_factura),
    FOREIGN KEY (metodo_pago_id) REFERENCES metodo_pago(id_metodo_pago)
);
```

## Restricciones y reglas de negocio

- Se aplican restricciones NOT NULL en todos los campos obligatorios
- Se utilizan restricciones UNIQUE para evitar duplicidad
- Se implementan CHECK para validar reglas de negocio
- Se definen claves foráneas en todas las relaciones

## Consideraciones técnicas

- Se mantiene consistencia en claves primarias
- Se garantiza integridad referencial
- El modelo está normalizado
- Se implementa con Liquibase
- Se ejecuta en Docker