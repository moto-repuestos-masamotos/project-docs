## Reglas de Negocio y Datos Canónicos

### 0. Contexto de aplicación

Las siguientes reglas de negocio se aplican directamente a los procesos definidos en el documento de requerimientos del sistema, particularmente en los procesos de venta, pedido, facturación, pagos e inventario.

Estas reglas serán implementadas posteriormente en la base de datos mediante restricciones, triggers, procedures y validaciones SQL.

---

### 1. Reglas de negocio

Las reglas de negocio definen cómo debe comportarse el sistema en cada proceso.

#### Clientes

RN-01 Cada cliente debe tener un documento de identidad único en el sistema.  
RN-02 No se puede eliminar un cliente que tenga pedidos o facturas registradas.  
RN-03 La fecha de registro del cliente se guarda automáticamente al crearlo.  

#### Productos

RN-04 Todo producto debe pertenecer a una categoría y a una marca registrada.  
RN-05 El precio de un producto debe ser mayor a cero.  
RN-06 El stock de un producto no puede ser negativo.  
RN-07 La referencia o código de cada producto debe ser único en el sistema.  
RN-08 No se puede eliminar un producto que haya sido incluido en algún pedido.  

#### Pedidos

RN-09 Todo pedido debe estar asociado a un cliente existente.  
RN-10 Un pedido debe tener al menos un producto.  
RN-11 La cantidad de cada producto en el pedido debe ser mayor a cero.  
RN-12 No se puede agregar al pedido un producto sin stock disponible.  
RN-13 La fecha del pedido se registra automáticamente al momento de crearlo.  
RN-14 El estado de un pedido solo puede ser: pendiente, completado o anulado.  
RN-15 Un pedido anulado no puede generar factura.  

#### Facturación

RN-16 Todo pedido completado debe generar obligatoriamente una factura.  
RN-17 Cada factura corresponde a un único pedido.  
RN-18 El total de la factura se calcula sumando el precio por cantidad de cada producto del pedido.  
RN-19 Una factura no puede eliminarse del sistema, solo puede marcarse como anulada.  
RN-20 La fecha de emisión de la factura se registra automáticamente.  
RN-21 El número de factura debe ser único y consecutivo.  

#### Pagos

RN-22 Todo pago debe estar asociado a una factura existente.  
RN-23 El monto de un pago debe ser mayor a cero.  
RN-24 El método de pago debe ser uno de los registrados en el catálogo del sistema.  
RN-25 La suma de los pagos de una factura no puede superar el total de dicha factura.  
RN-26 Cuando los pagos cubren el total de la factura, esta se marca automáticamente como pagada.  

#### Inventario

RN-27 Al completarse un pedido, el stock de cada producto vendido se reduce automáticamente.  
RN-28 No se puede vender un producto con stock en cero.  
RN-29 Si un pedido es anulado, el stock de los productos involucrados se restaura.  
RN-30 Todo cambio en el inventario queda registrado con fecha, tipo de movimiento y cantidad.  

---

### 2. Datos canónicos

#### Categorías de productos

| ID | Nombre |
|----|------|
| 1 | Motor |
| 2 | Frenos |
| 3 | Transmisión |
| 4 | Eléctrico |
| 5 | Carrocería |
| 6 | Suspensión |
| 7 | Filtros |
| 8 | Iluminación |
| 9 | Accesorios generales |

#### Marcas

| ID | Nombre |
|----|------|
| 1 | Honda |
| 2 | Yamaha |
| 3 | Suzuki |
| 4 | Kawasaki |
| 5 | AKT |
| 6 | Hero |
| 7 | Bajaj |
| 8 | Auteco |
| 9 | KTM |
| 10 | Genérico |

#### Métodos de pago

| ID | Nombre |
|----|------|
| 1 | Efectivo |
| 2 | Transferencia bancaria |
| 3 | Tarjeta débito |
| 4 | Tarjeta crédito |

#### Estados de pedido

| Estado | Descripción |
|-------|-----------|
| pendiente | El pedido fue registrado pero aún no se ha procesado |
| completado | El pedido fue entregado y genera factura |
| anulado | El pedido fue cancelado y no genera factura |

#### Estados de factura

| Estado | Descripción |
|-------|-----------|
| activa | Factura válida y vigente |
| anulada | Factura cancelada, permanece en el sistema |

#### Tipos de movimiento de inventario

| ID | Nombre |
|----|------|
| 1 | Entrada |
| 2 | Salida por venta |
| 3 | Ajuste manual |
| 4 | Devolución por anulación |