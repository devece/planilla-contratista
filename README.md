# Planilla Contratista · Mis Proyectos

App independiente para que cada contratista administre sus propios proyectos de
instalación GLP: identificación simple (sin login real), creación de proyectos
propios y seguimiento de 9 hitos recomendados del proceso (fecha manual o botón
"Ahora"), igual interacción que el gestor interno de Abastible.

**No tiene relación con el repo `abastible-gestion-proyectos`** ni con su tabla
`proyectos` — es una herramienta separada, pensada para el contratista.

## Archivos

- `index.html` — la app (HTML/CSS/JS, sin build, conecta directo a Supabase).
- `schema.sql` — documentación del esquema (`contratista_proyectos` y
  `contratista_notif_cola`) en el proyecto Supabase compartido
  `aocbetucqvgxxjopjbjm` ("planilla maestra"). Ya aplicado; no re-ejecutar tal cual.

## Notificaciones automáticas

Cada proyecto puede activar un aviso por correo al completar un hito. Por ahora
solo se guarda la preferencia y el aviso queda en cola en `contratista_notif_cola`
(sumando también el correo del Supervisor Abastible si está cargado) — el envío
real (proveedor de correo / Edge Function) se conecta más adelante.

## Carga desde iAuditor / Detalle Comercial

- **Nuevo proyecto**: si el contratista tiene el PDF del informe iAuditor
  ("Levantamiento Visita Ventas Proyectos Masivos") pero todavía no tiene
  Detalle Comercial, puede subirlo al crear el proyecto. El parser
  (`parseIAuditor` en `index.html`, corre con pdf.js en el navegador) completa
  cliente, dirección, comuna/región, contacto del cliente, **Vendedor
  Abastible** (quien hizo la visita comercial), tipo de proyecto, potencia
  instalada, tanque y qué declaraciones aplican (TC2/TC6/TC7/TC8/Sello
  Verde/Inspección Reducida). Todo queda editable antes de guardar.
- El **Supervisor Abastible** (quien queda a cargo de la ejecución) es un
  dato distinto que el iAuditor no trae — se carga siempre a mano, apenas
  se sepa quién es, normalmente al adjudicarse el proyecto.
- **Proyecto existente**: la misma carga se puede hacer después desde el
  detalle, y solo rellena los campos que estén vacíos (nunca pisa datos ya
  cargados a mano).
- **Detalle Comercial (DC)**: se puede adjuntar en cualquier momento desde el
  detalle del proyecto. No tiene parser propio todavía (formato no
  estandarizado) — se guarda el PDF y su texto extraído como referencia, y
  el contratista completa a mano lo que corresponda.
- Los PDF se guardan en el bucket público `contratista-docs` de Supabase
  Storage (mismo proyecto, mismo criterio de acceso abierto que el resto).
