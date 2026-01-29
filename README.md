# Modelado de Bases de Datos: Envíos, Retail y Banca

Este repositorio contiene ejemplos de **modelado Entidad–Relación (ER)**, **normalización hasta 3FN** y su implementación en **SQL** para tres sistemas distintos:

1. Sistema de Envíos
2. Sistema Retail
3. Sistema de Administración de Cuentas Bancarias

Se incluyen diagramas ER (para dbdiagram.io) y scripts SQL con tablas, relaciones, restricciones y datos de ejemplo.

---

## 1. Sistema de Envíos

**Entidades principales:**
- `cliente`: datos del cliente.
- `sucursal`: sucursales de origen/destino.
- `encomienda`: encomiendas enviadas, con referencia a cliente, sucursales y tarifa.
- `historial_estado`: seguimiento de cambios de estado de cada encomienda.
- `tarifa`: costos según rango de peso.

**Relaciones:**
- Un cliente puede tener varias encomiendas.
- Cada encomienda tiene origen y destino en sucursales.
- Cada encomienda tiene asociada una tarifa según su peso.
- Una encomienda puede tener varios estados en `historial_estado`.

**Ejemplo de consulta:**
Sql
SELECT e.id_encomienda, c.nombre AS cliente, 
       s_origen.nombre AS origen, s_destino.nombre AS destino,
       e.peso, t.costo, e.estado
FROM encomienda e
JOIN cliente c ON e.id_cliente = c.id_cliente
JOIN sucursal s_origen ON e.id_sucursal_origen = s_origen.id_sucursal
JOIN sucursal s_destino ON e.id_sucursal_destino = s_destino.id_sucursal
JOIN tarifa t ON e.id_tarifa = t.id_tarifa;
2. Sistema Retail
Entidades principales:

cliente: datos de clientes.

categoria: categorías de productos.

producto: productos con referencia a categoría.

pedido: pedidos realizados por clientes.

detalle_pedido: relación N–M entre pedidos y productos, incluye cantidad y precio.

pago: pagos realizados por pedido.

Relaciones:

Un cliente puede tener varios pedidos.

Un pedido puede incluir varios productos.

Cada pedido puede tener uno o varios pagos.

Ejemplo de consulta:

SELECT p.id_pedido, c.nombre AS cliente, p.total, p.estado
FROM pedido p
JOIN cliente c ON p.id_cliente = c.id_cliente;
3. Sistema Bancario
Entidades principales:

cliente: datos del cliente.

cuenta: cuentas bancarias de cada cliente.

tipo_transaccion: tipo de movimiento (depósito, retiro, transferencia, pago).

transaccion: movimientos realizados en cada cuenta.

Relaciones:

Un cliente puede tener varias cuentas.

Cada cuenta puede tener varias transacciones.

Cada transacción tiene un tipo definido en tipo_transaccion.

Ejemplo de consulta:

SELECT t.id_transaccion, t.fecha, tt.nombre AS tipo, t.monto, t.descripcion
FROM transaccion t
JOIN tipo_transaccion tt ON t.id_tipo = tt.id_tipo
WHERE t.id_cuenta = 1
ORDER BY t.fecha;
Uso
Abrir dbdiagram.io para ver los diagramas ER.

Ejecutar el script SQL script.sql en PostgreSQL para crear las tablas y cargar los datos de ejemplo.

Ejecutar consultas para explorar los datos y probar joins, filtros y agregaciones.

Buenas prácticas incluidas
Nombres en singular y snake_case.

Claves primarias (PK) y foráneas (FK) definidas.

Relaciones 1–N y N–M correctamente modeladas.

Datos de ejemplo para pruebas y screenshots.

Tipos adecuados y restricciones básicas (UNIQUE, NOT NULL, CHECK).
