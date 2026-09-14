# Candidate Table — Registro de Problemas Crudos

Se completa en Fase 1 (Cazar). **Una fila por problema** (aún sin solución). La columna "Descartado por" se llena en Fase 2 (Filtrar).

| # | Problema crudo (≤1 línea) | Quota textual (≤15 palabras) | Fuente (URL) | Comunidad | Fecha | Engagement (approx) | Fortaleza 🔥/ok/✗ | Workaround actual | ¿Alguien paga? | Descartado por |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | | | |
| 2 | | | | | | | | | | |

## Reglas de llenado

- **Problema crudo:** lenguaje del usuario, no jerga de producto. Ej. "los devs pierden fines de semana migrando DB sin herramienta" (no "saaS de migración").
- **Quota:** frase textual corta de la fuente (la Fase 3 la usará como evidencia).
- **Engagement:** upvotes/replies/vistas si el medio lo muestra; si no, "n/a".
- **Fortaleza:** el criterio de `hunting-queries.md` (🔥 fuerte / ok / ✗ débil).
- **Workaround actual:** 1 línea honesta de lo que hace la gente hoy sin el producto.
- **¿Alguien paga?:** sí / no / evidencia de pago (queja de precio cuenta).

## Reglas de descarte (Fase 2)

- Solo se les escribe algo en "Descartado por": `Q1` (sin queja reciente), `Q2` (workaround gratis suficiente), `Q3` (nadie paga), `Q4` (incumbentes felices), `Q5` (no encaja perfil).
- Los no descartados pasan al ranking del `triage-rubric.md`.
- **No borres filas.** El archivo completo (con descartados) es la traza y evita re-proponer.

## Archivo de salida

Volcado a `reports/candidate-hunts-<fecha>.md` al cerrar la Fase 2, con 3 secciones: pasan, descartados (con motivo), y notas de señal débil.