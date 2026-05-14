# Diagramas Iniciales — Tienda de Repuestos para Motos

Estos diagramas representan una aproximación inicial al dominio de la tienda física de venta de repuestos para motos.  
Su propósito es facilitar el análisis del sistema antes de construir el modelo conceptual definitivo.

No representan el modelo final obligatorio.

---

## 1. Diagrama de contexto

```mermaid
flowchart LR
 Cliente[Cliente] --> Consulta[Consulta de productos]
 Cliente --> Pedido[Generación de pedido]
 Cliente --> Pago[Registro de pago]

 Vendedor[Vendedor] --> Pedido
 Vendedor --> Facturacion[Gestión de facturación]

 Administrador[Administrador] --> Inventario[Control de inventario]
 Administrador --> Reportes[Consultas y reportes]

 Consulta --> BD[(Base de datos)]
 Pedido --> BD
 Facturacion --> BD
 Pago --> BD
 Inventario --> BD
 Reportes --> BD
```

---

## 2. Flujo principal del sistema

```mermaid
flowchart TD
 A[Cliente llega a la tienda] --> B[Consulta productos disponibles]
 B --> C[Selecciona productos]
 C --> D[Se genera pedido]
 D --> E[Se genera factura obligatoria]
 E --> F[Registro de pago]
 F --> G[Actualización de inventario]
 G --> H[Fin de la operación]
```

---

## 3. Modelo conceptual inicial

```mermaid
erDiagram

 CLIENTE ||--o{ PEDIDO : realiza
 PEDIDO ||--|| FACTURA : genera
 FACTURA ||--|| PAGO : registra
 PEDIDO ||--o{ DETALLE_PEDIDO : contiene
 PRODUCTO ||--o{ DETALLE_PEDIDO : pertenece
 PRODUCTO ||--|| INVENTARIO : controla
```
