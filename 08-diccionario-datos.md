# Diccionario de Datos — Tienda de Repuestos para Motos

## Descripción

El diccionario de datos describe la estructura de la base de datos, incluyendo tablas principales y tablas de parametrización (datos canónicos), así como el propósito de cada campo dentro del sistema.

Este documento sirve como referencia para entender la estructura de la base de datos y facilitar su uso, mantenimiento y validación.

---

## Tabla: cliente

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador único del cliente |
| nombre | VARCHAR | Nombre del cliente |

---

## Tabla: categoria

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador de la categoría |
| nombre | VARCHAR | Nombre de la categoría |

---

## Tabla: marca

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador de la marca |
| nombre | VARCHAR | Nombre de la marca |

---

## Tabla: producto

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador único del producto |
| categoria_id | INT | Referencia a la categoría del producto |
| marca_id | INT | Referencia a la marca del producto |
| codigo | VARCHAR | Código único del producto |
| nombre | VARCHAR | Nombre del producto |
| descripcion | VARCHAR | Descripción del producto |
| precio | NUMERIC | Precio del producto |

---

## Tabla: pedido

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del pedido |
| cliente_id | INT | Referencia al cliente que realiza el pedido |
| estado_pedido_id | INT | Estado actual del pedido |

---

## Tabla: detalle_pedido

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del detalle del pedido |
| pedido_id | INT | Referencia al pedido |
| producto_id | INT | Referencia al producto |
| cantidad | INT | Cantidad de productos solicitados |

---

## Tabla: factura

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador de la factura |
| pedido_id | INT | Referencia al pedido asociado |
| estado_factura_id | INT | Estado de la factura |
| total | NUMERIC | Valor total de la factura |
| fecha_factura | DATE | Fecha en que se generó la factura |

---

## Tabla: pago

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del pago |
| factura_id | INT | Referencia a la factura |
| valor | NUMERIC | Valor del pago realizado |
| metodo_pago_id | INT | Referencia al método de pago utilizado |

---

## Tabla: inventario

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del inventario |
| producto_id | INT | Referencia al producto |
| cantidad | INT | Cantidad disponible en inventario |

---

## Tabla: movimiento_inventario

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del movimiento |
| inventario_id | INT | Referencia al inventario |
| tipo_movimiento_inventario_id | INT | Referencia al tipo de movimiento (entrada o salida) |
| cantidad | INT | Cantidad que entra o sale del inventario |

---

## Tabla: metodo_pago

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del método de pago |
| nombre | VARCHAR | Nombre del método de pago (efectivo, transferencia, tarjeta, etc.) |

---

## Tabla: estado_pedido

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del estado del pedido |
| nombre | VARCHAR | Estado del pedido (pendiente, en proceso, enviado, entregado, etc.) |

---

## Tabla: estado_factura

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del estado de la factura |
| nombre | VARCHAR | Estado de la factura (pagada, pendiente, anulada, etc.) |

---

## Tabla: tipo_movimiento_inventario

| Campo | Tipo de dato | Descripción |
|------|-------------|-------------|
| id | INT | Identificador del tipo de movimiento |
| nombre | VARCHAR | Tipo de movimiento del inventario (entrada o salida de productos) |
``