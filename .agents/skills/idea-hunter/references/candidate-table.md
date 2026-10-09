# Candidate Table — Registro de Problemas Crudos

F1 llena; **1 fila por problema** (aún sin solución). "Descartado por" se llena en F2. Contexto base viene del perfil de F0 y se afina con la evidencia de cada fila; se usa en F2 (calibrar) y F3 (geografía/pricing). Fila vacía de contexto = hereda perfil F0.

| # | Problema (≤1 línea) | Quota (≤15 palabras) | Fuente (URL) | Comunidad | Fecha | Engagement | F | Ctx | W/P | Descartado por |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | | | | | | | | | | |
| 2 | | | | | | | | | | |

## Columnas

- **Problema:** lenguaje del usuario, no jerga de producto. Ej. "los devs pierden fines de semana migrando DB" (no "saaS de migración").
- **Quota:** frase textual corta de la fuente (la F3 la usa como evidencia).
- **Engagement:** upvotes/replies/vistas si el medio lo muestra; si no "n/a".
- **F:** 🔥 / ok / ✗ según `hunting-queries.md`.
- **Ctx:** `=` si coincide con el perfil de F0. Si diverge, shorthands separados por `|`: `país/cluster|banda $/mes|estac/deadline/atemp|digital/efectivo/gift/mixto`. Ej. `MX|120$/m|estac|digital`. Si no aparece banda: `sin anclas`.
- **W/P:** workaround actual + señal de pago en una celda. Ej. `rake gratis|alguien paga $15` / `todo gratis|nadie` / `sufre|queja precio` / `paga hoy|$X`.

## Reglas de descarte (F2)

- Motivos en "Descartado por": `Q1` (sin queja reciente), `Q2` (workaround gratis suficiente), `Q3` (nadie paga), `Q4` (incumbentes felices), `Q5` (no encaja perfil). Sufijos de contexto: `Q3+capital` (cluster sin poder de compra), `Q3+norma` (cultura gift), `Q1+canal` (dolor en canal equivocado).
- Los no descartados pasan al ranking del `triage-rubric.md`.
- **No borres filas.** Archivo completo (con descartados) = traza contra re-proponer.

## Archivo de salida

Volcado a `reports/candidate-hunts-<fecha>.md` al cerrar F2, con 3 secciones: pasan, descartados (motivo), y notas de señal débil.