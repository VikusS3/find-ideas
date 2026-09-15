# Candidate Table — Registro de Problemas Crudos

Se completa en Fase 1 (Cazar). **Una fila por problema** (aún sin solución). La columna "Descartado por" se llena en Fase 2 (Filtrar). Las columnas de contexto (País/Cluster, Capital, Ventana, Norma de pago) vienen del perfil de Fase 0 y se afinan con la evidencia de cada fila; se usan en Fase 2 para calibrar y en Fase 3 para fijar geografía/pricing.

| # | Problema crudo (≤1 línea) | Quota textual (≤15 palabras) | Fuente (URL) | Comunidad | Fecha | Engagement (approx) | Fortaleza 🔥/ok/✗ | País/Cluster | Capital (banda $/mes) | Ventana temporal | Norma de pago | Workaround actual | ¿Alguien paga? | Descartado por |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | | | | | | | |
| 2 | | | | | | | | | | | | | | |

## Reglas de llenado

- **Problema crudo:** lenguaje del usuario, no jerga de producto. Ej. "los devs pierden fines de semana migrando DB sin herramienta" (no "saaS de migración").
- **Quota:** frase textual corta de la fuente (la Fase 3 la usará como evidencia).
- **Engagement:** upvotes/replies/vistas si el medio lo muestra; si no, "n/a".
- **Fortaleza:** el criterio de `hunting-queries.md` (🔥 fuerte / ok / ✗ débil).
- **País/Cluster:** país concreto o cluster (MX/Andina/Cono Sur/ES/global) donde se vio el dolor. Si no coincide con el cluster objetivo, anótalo — es señal a calibrar.
- **Capital (banda $/mes):** rango de precio que la evidencia cita (`"dispuesto a pagar $X"`, quejas de precio) o referencia del poder de compra del cluster. Si no aparece nada: "sin anclas".
- **Ventana temporal:** estacional / deadline fiscal-regulatorio / atemporal. Importa para planear lanzamiento, no para descartar.
- **Norma de pago:** digital (tarjeta/wallet), efectivo, "gift" (cultura de todo-gratis), mixto. Calibra "¿alguien paga?".
- **Workaround actual:** 1 línea honesta de lo que hace la gente hoy sin el producto.
- **¿Alguien paga?:** sí / no / evidencia de pago (queja de precio cuenta).

## Reglas de descarte (Fase 2)

- Solo se les escribe algo en "Descartado por": `Q1` (sin queja reciente), `Q2` (workaround gratis suficiente), `Q3` (nadie paga), `Q4` (incumbentes felices), `Q5` (no encaja perfil). Pueden añadirse sufijos de contexto al motivo: `Q3+capital` (cluster sin poder de compra), `Q3+norma` (cultura gift/no-pago en el canal), `Q1+canal` (dolor en canal equivocado, cluster no presente).
- Los no descartados pasan al ranking del `triage-rubric.md`.
- **No borres filas.** El archivo completo (con descartados) es la traza y evita re-proponer.

## Archivo de salida

Volcado a `reports/candidate-hunts-<fecha>.md` al cerrar la Fase 2, con 3 secciones: pasan, descartados (con motivo), y notas de señal débil.