# Planteamiento del problema

## Contexto del dominio
Una tienda física de venta de repuestos para motos es un negocio dedicado a la comercialización de piezas, accesorios y componentes necesarios para el mantenimiento y reparación de motocicletas, atendiendo directamente al cliente final en el punto de venta. La operación diaria incluye la atención presencial a los clientes, el registro de pedidos, la emisión obligatoria de facturas, el manejo de pagos y el control del inventario de repuestos disponibles.
En este entorno participan actores como vendedores y responsables administrativos, quienes realizan actividades relacionadas con la venta, la facturación, la consulta de productos y la actualización de existencias. Debido a la diversidad de repuestos, marcas y tipos de productos, la correcta gestión de la información resulta fundamental para el funcionamiento eficiente del negocio.

## Problema a resolver
En muchos casos, la gestión de ventas, facturación e inventario en este tipo de tiendas se realiza mediante procesos manuales o herramientas no integradas, lo que genera inconsistencias en la información, errores en el control de existencias y dificultades para mantener un registro confiable de las ventas realizadas. Al ser la facturación un proceso obligatorio, la ausencia de un control adecuado incrementa el riesgo de errores administrativos y contables.
Asimismo, la falta de un sistema centralizado dificulta la consulta de información histórica, como el volumen de ventas por producto, los repuestos con mayor rotación, los niveles de inventario disponibles o la relación entre pedidos, facturas y pagos. Estas limitaciones afectan la toma de decisiones, reducen la eficiencia operativa y generan incertidumbre en la gestión del negocio.

## Justificación del uso de base de datos
La implementación de una base de datos relacional permite centralizar y organizar la información de la tienda de manera estructurada y consistente. A través de un modelo de datos adecuado, es posible representar las relaciones entre productos, pedidos, facturas, pagos y el inventario controlado por cantidad, garantizando la integridad y confiabilidad de los datos.
El uso de una base de datos facilita además la validación de reglas de negocio, como la obligatoriedad de la facturación por venta y el control de existencias, así como la ejecución de consultas que permiten analizar información histórica relevante para el control y la planificación del negocio.

## Alcance del sistema
El sistema contempla la gestión de ventas mediante pedidos asociados a facturación obligatoria, el registro de pagos, y el control del inventario basado en cantidades disponibles de los distintos repuestos. También incluye el registro de información relacionada con productos y clientes finales. El enfoque del proyecto se limita exclusivamente al diseño, documentación e implementación de la base de datos relacional que soporta estas operaciones.
No se incluyen funcionalidades relacionadas con comercio electrónico, gestión de envíos, pasarelas de pago en línea ni el desarrollo de interfaces gráficas, ya que el alcance del proyecto está centrado únicamente en el modelado y gestión de la base de datos.
