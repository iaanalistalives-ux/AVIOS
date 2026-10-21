# CLAUDE.md — Artes de Avíos (AVIOS)

Las reglas generales de trabajo están en el repo privado `lives-instrucciones` (CLAUDE.md). Este archivo solo describe esta herramienta.

## Qué hace
Archivo de los **artes** que envían los proveedores antes de fabricar los **avíos** (etiquetas ID, de marca/talla, de composición y cuidado, stickers de talla/código y de precio, hangtags). Cada **carga** (código `ART-000123`) es uno o más archivos de un mismo arte con sus datos.
- `index.html` — **visor**: tarjetas con miniatura, estado, item, cliente · proveedor, tipo, OC/pedido y fecha. Búsqueda por varias palabras (incluye el texto leído de los PDF), filtros de cliente, proveedor, tipo y estado (Vigentes / POR APROBAR / APROBADO / RECHAZADO / ANULADO), orden y "Mostrar más" con regla 500. Ficha con vista previa (pdf.js o imagen), descargar, datos e historial de cargas del item. Quien tiene permiso puede **editar datos** (incluido anular; no hay borrado). Excel LIVES.
- `subir_arte.html` — **carga** para Logística y Calidad, en 3 pasos:
  1. Archivos: PDF, JPG o PNG, hasta 10 por carga y 15 MB cada uno; avisa duplicados.
  2. Datos: la pantalla lee el PDF y propone OC, pedido, estilo, item, cliente, proveedor, tipo y estado (APROBADO solo si encuentra el sello APPROVED). Obligatorios: item, cliente, proveedor, tipo y estado.
  3. Quién sube: área LOGÍSTICA o CALIDAD; el nombre sale del usuario del portal.
  - Lo nuevo se guarda como carga nueva; lo anterior no se borra.

## Base de datos (Supabase lives-datos)
- `avios_listar` (cargas, catálogos y si la persona puede editar), `avios_minis` (miniaturas), `avios_editar` (cambios, con historial en `avios_historial`), `avios_registrar` (nueva carga en `avios_artes`; revisa que cada archivo exista en el almacén; un código de envío evita duplicar).
- Catálogos de cliente, proveedor y tipo en `avios_catalogos` (la pantalla tiene una lista de respaldo).
- Archivos: bucket privado `avios`, ruta `AAAA/MM/<envío>/<archivo>`.
- El SQL de creación (AV01) va incrustado en `subir_arte.html` como texto, sin ejecutarse.

## Quién la usa
Según las entradas por el portal de los últimos 30 días al 21/10/2026: 2 personas (Comercial y Calidad Manufactura), más Logística y Calidad que suben artes.

## Quién puede subir o editar
- Lo decide la base: `avios_puede_subir()` con la tabla `permisos` (permiso a "Subir arte"). Vale para subir, editar y anular. Sin permiso, el visor se ve igual y el botón Guardar queda desactivado.
- A Sistemas: `avios_puede_subir` es la pieza que reemplazan con su seguridad.

## Pendientes vistos al escribir esto (21/10/2026)
- El visor dice "súbelos desde + Subir arte", pero no hay ese botón (se entra a la carga desde el portal).
- Comentario obsoleto en `index.html` que menciona un Apps Script y `artes_carga.html` (no existe).
