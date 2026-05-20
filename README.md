# Proyecto Final — Base de Datos
## Tienda de Repuestos para Motos

---

## Información general

- **Asignatura:** Modelado y Gestión de Base de Datos  
- **Tipo de proyecto:** Proyecto final  
- **Dominio:** Tienda física de venta de repuestos para motos  

---

## Equipo de trabajo

- **Organización GitHub:** https://github.com/moto-repuestos-masamotos  

### Integrantes:

- Santiago Manrique Gonzalez  
- Eric Mauricio Castañeda Murcia  
- Juan David Manrique Urbina  
- Francisco Bautista Vanegas  

### Profesor / Revisor:

- `ariel5253` - Jesus Ariel González Bonilla  

---

## Repositorios del proyecto

- 📂 Documentación: `project-docs`  
- 🗄 Base de datos: `project-bd`  

---

## Descripción del proyecto

Este proyecto tiene como objetivo el diseño, documentación e implementación de una base de datos relacional para una tienda física de venta de repuestos para motos.  

El sistema permite gestionar productos, clientes, pedidos, facturación obligatoria, pagos e inventario, garantizando la integridad y consistencia de los datos.

---

## Contexto del dominio

La tienda opera atendiendo clientes de manera presencial, registrando ventas mediante pedidos, generando facturas obligatorias, procesando pagos y controlando el inventario disponible.

---

## Alcance del sistema

### Incluye:

- Gestión de pedidos  
- Facturación obligatoria  
- Registro de pagos  
- Control de inventario  
- Gestión de productos  
- Registro de clientes  

### No incluye:

- Comercio electrónico  
- Envíos  
- Pagos en línea  
- Interfaces de usuario  

---

## Estructura del proyecto

```plaintext
project-docs/
├── README.md
├── 01-planteamiento-problema.md
├── 02-requerimientos.md
├── 03-reglas-negocio.md
├── 04-diagramas-iniciales.md
├── 05-modelo-conceptual.md
├── 06-modelo-logico.md
├── 07-modelo-fisico.md
├── 08-diccionario-datos.md
├── 09-evidencias.md
└── 10-conclusiones.md

---

## Implementación de la base de datos

La base de datos fue desarrollada utilizando:

- DDL: definición de tablas, llaves primarias y foráneas
- DML: inserción de datos canónicos y volumétricos
- Migraciones: controladas mediante Liquibase
- Ejecución: mediante Docker

---

## Datos del sistema

### Datos canónicos
Datos base necesarios para el funcionamiento del sistema, tales como:

- Categorías
- Marcas
- Métodos de pago
- Estados del sistema

--- 

## Datos volumétricos
Datos utilizados para pruebas del sistema, permitiendo validar relaciones y consultas complejas.

---