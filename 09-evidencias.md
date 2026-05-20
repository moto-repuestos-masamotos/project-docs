## Evidencias del Proyecto

Este documento presenta las evidencias de ejecución de los componentes desarrollados en el sistema de gestión de tienda de repuestos, incluyendo triggers, funciones, procedimientos almacenados, consultas JOIN y aportes DML/DDL versionados con Liquibase.

---

## 📌 Integrantes del Proyecto

| # | Integrante | Rol |
|---|---|---|
| 1 | Santiago Manrique Gonzalez | Desarrollo de triggers, functions, procedures, JOIN y DML |
| 2 | Eric Mauricio Castañeda Murcia | Desarrollo de triggers, functions, procedures, JOIN y DML |
| 3 | Juan David Manrique Urbina | Desarrollo de triggers, functions, procedures, JOIN y DML |
| 4 | Francisco Bautista Vanegas | Desarrollo de triggers, functions, procedures, JOIN y DML |

---

## ✅ Evidencias por Integrante

### Integrante 1 - Santiago Manrique Gonzalez

#### DDL/DML Versionado
- **Archivo**: `liquibase/dml/volumetric/008-movimiento_inventario.sql`
- **Descripción**: Aporte DML versionado en Liquibase para insertar datos en la tabla movimiento_inventario
- **Comando**: `docker compose run --rm liquibase --defaultsFile=liquibase.properties update`

#### Trigger - Fecha Automática Pedido
- **Archivo**: `scripts/triggers/trigger_fecha_pedido.sql`
- **Descripción**: Asigna automáticamente la fecha actual a un pedido cuando se inserta un registro sin fecha
- **Comando de prueba**: 
  ```sql
  INSERT INTO pedido (id, cliente_id, estado_pedido_id) 
  VALUES (6000, 1, 1);
  SELECT * FROM pedido WHERE id = 6000;
  ```
- **Resultado esperado**: `fecha_pedido = CURRENT_DATE`

#### Function - Total Inventario
- **Archivo**: `scripts/functions/function_total_inventario.sql`
- **Descripción**: Cuenta cuántos registros hay en la tabla inventario
- **Comando de prueba**: `SELECT total_inventario();`
- **Resultado esperado**: Retorna la cantidad total de registros en inventario (ej: 40)

#### Procedure - Actualizar Precio Producto
- **Archivo**: `scripts/procedures/procedure_actualizar_precio.sql`
- **Descripción**: Permite actualizar el precio de un producto mediante su identificador
- **Comando de prueba**: 
  ```sql
  CALL actualizar_precio_producto(1, 150000);
  SELECT id, precio FROM producto WHERE id = 1;
  ```
- **Resultado esperado**: El precio se actualiza correctamente (ej: 120000 → 150000)

#### Consulta JOIN de más de 5 tablas - Reporte Cliente
- **Archivo**: `scripts/joins/join_reporte_cliente.sql`
- **Descripción**: Visualiza información de compras realizadas por clientes, incluyendo producto, cantidad, factura, método de pago y estado del pedido
- **Tablas unidas**: 8 tablas (cliente, pedido, detalle_pedido, producto, factura, pago, metodo_pago, estado_pedido)

---

### Integrante 2 - Eric Mauricio Castañeda Murcia

#### DDL/DML Versionado
- **Archivo**: `liquibase/dml/volumetric/009-factura_integrante2.sql`
- **Descripción**: Aporte DML versionado en Liquibase para insertar datos en la tabla factura
- **Comando**: `docker compose run --rm liquibase --defaultsFile=liquibase.properties update`

#### Trigger - Fecha Automática Factura
- **Archivo**: `scripts/triggers/trigger_fecha_factura.sql`
- **Descripción**: Asigna automáticamente la fecha actual a una factura cuando se inserta un registro sin fecha
- **Comando de prueba**: 
  ```sql
  INSERT INTO factura (id, pedido_id, estado_factura_id, numero_factura, total) 
  VALUES (10000, 100000, 1, 'FAC-10000', 100000);
  SELECT * FROM factura WHERE id = 10000;
  ```
- **Resultado esperado**: `fecha_factura = CURRENT_DATE`

#### Function - Total de Clientes
- **Archivo**: `scripts/functions/function_total_clientes.sql`
- **Descripción**: Cuenta la cantidad total de clientes registrados en la base de datos
- **Comando de prueba**: `SELECT total_clientes();`
- **Resultado esperado**: Retorna el número total de clientes (ej: 100)

#### Procedure - Actualizar Valor de Pago
- **Archivo**: `scripts/procedures/procedure_actualizar_pago.sql`
- **Descripción**: Permite actualizar el valor de un pago mediante su identificador
- **Comando de prueba**: 
  ```sql
  CALL actualizar_pago(1, 200000);
  SELECT * FROM pago WHERE id = 1;
  ```
- **Resultado esperado**: El valor del pago se actualiza correctamente (ej: 100000 → 200000)

#### Consulta JOIN de más de 5 tablas - Reporte Ventas
- **Archivo**: `scripts/joins/join_ventas.sql`
- **Descripción**: Visualiza información de compras realizadas por clientes, incluyendo producto, cantidad, factura, método de pago y estado de la factura
- **Tablas unidas**: 8 tablas (cliente, pedido, detalle_pedido, producto, factura, pago, metodo_pago, estado_factura)

---

### Integrante 3 - Juan David Manrique Urbina

#### DDL/DML Versionado
- **Archivo**: `liquibase/dml/volumetric/010-pedido_integrante3.sql`
- **Descripción**: Aporte DML versionado en Liquibase para insertar datos en la tabla pedido
- **Comando**: `docker compose run --rm liquibase --defaultsFile=liquibase.properties update`

#### Trigger - Validación Cantidad Inventario
- **Archivo**: `scripts/triggers/trigger_inventario.sql`
- **Descripción**: Valida que la cantidad ingresada en inventario no sea negativa. Si se intenta insertar o actualizar con un valor menor a 0, el sistema la reemplaza automáticamente por 0
- **Comando de prueba**: 
  ```sql
  UPDATE inventario SET cantidad = -5 WHERE id = 1;
  SELECT * FROM inventario WHERE id = 1;
  ```
- **Resultado esperado**: La cantidad negativa se corrige automáticamente a 0

#### Function - Total Pedidos
- **Archivo**: `scripts/functions/function_total_pedidos.sql`
- **Descripción**: Cuenta cuántos registros existen en la tabla pedido
- **Comando de prueba**: `SELECT total_pedidos();`
- **Resultado esperado**: Retorna el número total de pedidos (ej: 50)

#### Procedure - Actualizar Stock Inventario
- **Archivo**: `scripts/procedures/procedure_actualizar_stock.sql`
- **Descripción**: Permite actualizar la cantidad en inventario de un producto, identificándolo por su ID
- **Comando de prueba**: 
  ```sql
  CALL actualizar_stock(1, 25);
  SELECT * FROM inventario WHERE id = 1;
  ```
- **Resultado esperado**: La cantidad del registro se actualiza correctamente a 25

#### Consulta JOIN de más de 5 tablas - Pagos por Cliente
- **Archivo**: `scripts/joins/join_pagos.sql`
- **Descripción**: Visualiza los pagos realizados por clientes, incluyendo pedido, factura, valor pagado, método de pago y estado de la factura
- **Tablas unidas**: 6 tablas (cliente, pedido, factura, pago, metodo_pago, estado_factura)

---

### Integrante 4 - Francisco Bautista Vanegas

#### DDL/DML Versionado
- **Archivo**: `liquibase/dml/volumetric/011-producto_integrante4.sql`
- **Descripción**: Aporte DML versionado para insertar productos en la tabla producto
- **Comando**: `docker compose run --rm liquibase --defaultsFile=liquibase.properties update`

#### Trigger - Validar Valor de Pago
- **Archivo**: `scripts/triggers/trigger_pago.sql`
- **Descripción**: Valida el valor de un pago antes de insertarlo o actualizarlo. Si el valor es negativo, automáticamente lo convierte en 0
- **Comando de prueba**: 
  ```sql
  UPDATE pago SET valor = -100 WHERE id = 1;
  SELECT * FROM pago WHERE id = 1;
  ```
- **Resultado esperado**: El valor negativo se corrige automáticamente a 0

#### Function - Total de Facturas
- **Archivo**: `scripts/functions/function_total_facturas.sql`
- **Descripción**: Cuenta la cantidad total de facturas registradas en la base de datos
- **Comando de prueba**: `SELECT total_facturas();`
- **Resultado esperado**: Retorna el número total de facturas (ej: 40)

#### Procedure - Actualizar Estado Pedido
- **Archivo**: `scripts/procedures/procedure_estado_pedido.sql`
- **Descripción**: Permite actualizar el estado de un pedido mediante su identificador
- **Comando de prueba**: 
  ```sql
  CALL actualizar_estado_pedido(1, 2);
  SELECT * FROM pedido WHERE id = 1;
  ```
- **Resultado esperado**: El estado del pedido se actualiza correctamente (ej: estado_pedido_id = 2)

#### Consulta JOIN de más de 5 tablas - Consulta Inventario
- **Archivo**: `scripts/joins/join_inventario.sql`
- **Descripción**: Visualiza información de productos en inventario, categoría, marca, movimientos y tipo de movimiento
- **Tablas unidas**: 6 tablas (producto, categoria, marca, inventario, movimiento_inventario, tipo_movimiento_inventario)

---

## 📊 Resumen de Aportes

| Integrante | Trigger | Function | Procedure | JOIN | DML/DDL | Total |
|---|---|---|---|---|---|---|
| Santiago Manrique | ✅ | ✅ | ✅ | ✅ (8 tablas) | ✅ | 5 |
| Eric Castañeda | ✅ | ✅ | ✅ | ✅ (8 tablas) | ✅ | 5 |
| Juan David Manrique | ✅ | ✅ | ✅ | ✅ (6 tablas) | ✅ | 5 |
| Francisco Bautista | ✅ | ✅ | ✅ | ✅ (6 tablas) | ✅ | 5 |
| **TOTAL** | **4** | **4** | **4** | **4** | **4** | **20** |

---

## 🔍 Verificación de Requisitos

- ✅ Cada integrante tiene 1 aporte DDL/DML versionado en Liquibase
- ✅ Cada integrante tiene 1 trigger funcional
- ✅ Cada integrante tiene 1 procedure
- ✅ Cada integrante tiene 1 function
- ✅ Cada integrante tiene 1 consulta JOIN con 6+ tablas
- ✅ Total: 20 evidencias técnicas (5 por integrante × 4 integrantes)