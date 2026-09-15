---
name: idea-hunter
description:
  Caza ideas de negocio/proyectos desde el dolor real de la gente, las filtra,
  las valida con market-research y analiza el conjunto frente a frente, teniendo
  en cuenta el contexto sociocultural del nicho (país/cluster, capital dispuesto,
  fechas y canales). Pipeline completo con un solo trigger. Use for "dame ideas",
  "busca ideas de proyectos", "caza ideas de [sector]", "caza ideas para [país]",
  "qué puedo construir".
---

# Skill: idea-hunter

Caza ideas de negocio/proyectos desde el dolor real de la gente, las filtra, las valida con el skill `market-research` y analiza el conjunto frente a frente. Pipeline completo con un solo trigger.

## Cuándo usar

- El usuario dice "dame ideas", "busca ideas de proyectos", "caza ideas de [sector]", "qué puedo construir".
- El usuario pregunta qué proyecto tiene sentido construir en un sector dado.
- El usuario tiene varias ideas y quiere saber cuál atacar primero (checkpoint de Fase 4).

NO usar para validar una única idea ya concreta — eso es trabajo del skill `market-research` directo.

## Configuración

- **Entrada:** el usuario da 1-2 palabras de sector/dominio (ej. "fintech LATAM", "IA para abogados") y, opcionalmente, un país/geografía. Si no da sector, propone 5-8 dominios y pregunta (una sola pregunta, sin interrogatorio).
- **Contexto (país/cluster):** si el usuario da país, se usa para todo el pipeline. Si no lo da, se infiere el cluster sociocultural del nicho de las señales de Fase 1 (MX/Andina/Cono Sur/España/global o uno combinado del sector) y **se declara el default asumido** al inicio del informe.
- **Autonomía:** corre Fases 0→4 de punta a punta sin pausas. No pregunta hasta entregar el informe.
- **Idioma:** búsquedas bilingües (fuentes EN + hispanas/localizadas por cluster); informes, matrices y resúmenes siempre en español.
- **Salidas:** `reports/candidate-hunts-<fecha>.md` (traza cruda), `reports/market-research-<slug>.md` (por idea validada, vía skill market-research), `reports/pipeline-ideas-<fecha>.md` (análisis comparativo final).

## Pipeline (5 fases)

### Fase 0 — Contextualizar (perfil sociocultural-económico)

Construye el perfil del nicho ANTES de cazar. Máx 3 tool calls; la mayor parte sale de conocimiento base + 1-2 búsquedas finas solo si la duda es estructural.

- **Cluster cultural:** país/región (o el inferido), idioma, y los **canales reales** donde vive esa gente: Reddit/hilos EN vs Facebook grupos, WhatsApp/Telegram, TikTok/IG comments, foros locales por país (ForoCoches ES, foros .com.mx, comunidades peruanas, etc.). El canal manda: si la audiencia del cluster no está en donde tú buscarías, las quejas no aparecen aunque existan.
- **Normas de pago:** cómo paga ese cluster: tarjeta/vs wallet/vs giros en efectivo; cultura "gift/community commons" (todo gratis y compartido) vs disposición a pagar por software/servicios. Esto calibra (no reemplaza) la lectura de "¿alguien paga?".
- **Capital dispuesto:** banda de precio citada en hilos del sector (`"dispuesto a pagar"`, `"cuánto cobran"`) + referencia de poder de compra (salario mínimo del país, costo de vida, PPP). Pregunta rectora: *¿el bolsillo del cluster puede cubrir el umbral mínimo de lo que un negocio de este tipo necesita cobrar?*
- **Timing del nicho:** estacionalidad del dolor (regreso a clases, temporada de impuestos, cosechas, fin de año), deadlines fiscales/regulatorios (IVA en abril, eInvoice mandates) y ventanas de trend. Un dolor que solo aparece en una ventana = timing a gestionar, no freno.

**Salida de fase:** ficha de contexto de 5-10 líneas. Se vuelca al informe final y se usa en Fases 1-3.

### Fase 1 — Cazar (idea sourcing)

Basado en los recipes de búsqueda de `market-research`, pero en modo amplio. Lee `references/hunting-queries.md` para los patrones por medio y por tipo de audiencia.

Rutina por lote:

- Busca queja cruda del sector en los **canales del cluster** definidos en Fase 0 (no solo Reddit): `reddit "is there an app for" [sector]`, `"I wish I could" [sector]`, `"am I the only one" [sector]`, `quora [sector] problem`, `[sector] reddit "how do I"`. Prefijo bilingüe: mismas queries en español (`"ojalá hubiera" [sector]`, `[sector] reddit frustración`) + queries en canal local (`[sector] facebook grupo problema`, `[sector] telegram/wpp queja`, `[sector] foro [país]`). Añade filtro `site:` del dominio del país si el cluster es un país concreto.
- Busca capital y timing: `"[sector] dispuesto a pagar"`, `"[sector] cuánto cobran"/"cuánto pagas"`, `"[sector] estoy pagando $"`; temporales `"[sector] in [temporada/mes]"`, `"[sector] [deadline fiscal/regulatorio]"`.
- Si el sector es B2B: añade `"struggling with" [sector] linkedin`. Si es de dev: `[sector] hacker news`, `github manage [pain]`.
- Presupuesto: 6-10 búsquedas (3-5 si el primer lote ya da señales fuertes). No repetir queries fallidas más de una vez.
- Registra CADA candidato en la candidate-table (`references/candidate-table.md`): problema crudo, quota ≤15 palabras, URL, comunidad, fecha, engagement estimado.

**Regla de oro:** solo es candidato si hay gente hablando del problema en los últimos 2 años **en el cluster objetivo** (del perfil de Fase 0). Sin dolor reciente → no entra a la tabla. Queja fresca global no cuenta si el cluster no paga, y dolor local silencioso en foros externos no invalida a un cluster que sí habla en sus canales reales.

**Salida de fase:** lista de 8-20 problemas crudos (aún sin solución). Son "problemas", no productos.

**Sesgo anunciado:** recoge el problema con las citas textuales; NO inventar la solución todavía.

### Fase 2 — Filtrar (triage rápido)

Aplica `references/triage-rubric.md` a cada candidato: 5 preguntas SI/NO calibradas por la ficha de contexto (capital del cluster, norma de pago, ventana temporal). Sin búsquedas nuevas — solo decisión documentada sobre la evidencia de Fase 1.

Pasan los que sumen ≥3/5. Máximo 5 pasan. Los descartados quedan registrados con su porqué (traza contra re-proponer).

**Salida de fase:** ranking corto de 3-5 candidatos con 1-liner de porqué pasa cada uno.

### Fase 3 — Validar (delegada)

Para cada candidato del top, **en orden, uno a la vez**, invoca el skill `market-research` completo (Phase 0 opcional ya resuelta; dar idea, target y geografía explícitos en el prompt del skill). **Pasa al prompt la ficha de contexto de Fase 0**: país/cluster, banda de capital, ventana temporal y norma de pago — para que fije geografía, pricing y segmento correctos desde el arranque. El skill genera `reports/market-research-<slug>.md` (reutiliza sus `query-recipes.md`, `scoring-rubric.md` y `report-template.md` — NO duplicar esa lógica aquí).

No intercales candidatos: una validación terminada antes de empezar la siguiente (para ajustar presupuesto si una va floja).

**Salida de fase:** N informes market-research completos + anotación breve por cada uno (score y veredicto).

### Fase 4 — Analizar (comparativo)

Con los informes listos, redacta `reports/pipeline-ideas-<fecha>.md` con la plantilla `references/pipeline-report.md`:

- Matriz 6 dimensiones × ideas (con el score de cada informe), con columna extra de `Capital/Ventana` por idea.
- Veredicto relativo: mejor oportunidad, mejor riesgo/barrera, esfuerzo estimado. Nota de contexto: si el cluster es low-capital o hay ventana temporal, decirlo sin esconderlo.
- Orden de ejecución recomendado (build first / run next), con justificación 1-liner.
- Nota de honestidad: si ninguna idea salió GO o todas salieron débiles, dilo sin suavizar.

## Timebox (sprint completo)

- Fase 0: ≤3 tool calls (idealmente 0-1; el perfil se arma con conocimiento base + los canales/capital del cluster).
- Fases 1-2: ≤15 tool calls.
- Fase 3: presupuesto del propio market-research por idea (~15-30 tool calls cada una).
- Fase 4: redacción directa, sin búsquedas nuevas.
- Si un sector no da candidatos viables en Fase 2: KILL temprano del sector — date cuenta y reporta "sector vacío" en vez de inventar señales.

## Reglas de honestidad (heredadas de market-research)

- Evidencia > vibra. Toda claim material con URL. Señal débil → di "weak signal", no rellenes.
- Sé willing to KILL. La traza de descartados protege de proponer lo mismo dos veces.
- Contradicciones = hallazgos. Si los datos dicen crecer pero las comunidades callan, repórtalo.
- No inflar scores para ser amable.

## Entregables al cierre

1. Informe crudo de candidatos (`candidate-hunts-<fecha>.md`) — opcional si es ruido; al menos se conserva como traza.
2. Un `market-research-<slug>.md` por idea validada.
3. `pipeline-ideas-<fecha>.md` final.
4. Resumen en chat (3-5 frases): mejor candidato, peor candidato, cuál construir primero y qué valida en campo antes de construir.
