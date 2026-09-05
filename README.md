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
— el envío real (proveedor de correo / Edge Function) se conecta más adelante.
