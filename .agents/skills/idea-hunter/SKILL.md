# Skill: idea-hunter

Caza ideas de negocio/proyectos desde el dolor real de la gente, las filtra, las valida con el skill `market-research` y analiza el conjunto frente a frente. Pipeline completo con un solo trigger.

## Cuándo usar

- El usuario dice "dame ideas", "busca ideas de proyectos", "caza ideas de [sector]", "qué puedo construir".
- El usuario pregunta qué proyecto tiene sentido construir en un sector dado.
- El usuario tiene varias ideas y quiere saber cuál atacar primero (checkpoint de Fase 4).

NO usar para validar una única idea ya concreta — eso es trabajo del skill `market-research` directo.

## Configuración

- **Entrada:** el usuario da 1-2 palabras de sector/dominio (ej. "fintech LATAM", "IA para abogados"). Si no da sector, propone 5-8 dominios y pregunta (una sola pregunta, sin interrogatorio).
- **Autonomía:** corre Fases 1→4 de punta a punta sin pausas. No pregunta hasta entregar el informe.
- **Idioma:** búsquedas bilingües (fuentes EN + hispanas); informes, matrices y resúmenes siempre en español.
- **Salidas:** `reports/candidate-hunts-<fecha>.md` (traza cruda), `reports/market-research-<slug>.md` (por idea validada, vía skill market-research), `reports/pipeline-ideas-<fecha>.md` (análisis comparativo final).

## Pipeline (4 fases)

### Fase 1 — Cazar (idea sourcing)

Basado en los recipes de búsqueda de `market-research`, pero en modo amplio. Lee `references/hunting-queries.md` para los patrones por medio y por tipo de audiencia.

Rutina por lote:
- Busca queja cruda del sector: `reddit "is there an app for" [sector]`, `"I wish I could" [sector]`, `"am I the only one" [sector]`, `quora [sector] problem`, `[sector] reddit "how do I"`. Prefijo bilingüe: mismas queries en español (`"ojalá hubiera" [sector]`, `[sector] reddit frustración`).
- Si el sector es B2B: añade `"struggling with" [sector] linkedin`. Si es de dev: `[sector] hacker news`, `github manage [pain]`.
- Presupuesto: 6-10 búsquedas (3-5 si el primer lote ya da señales fuertes). No repetir queries fallidas más de una vez.
- Registra CADA candidato en la candidate-table (`references/candidate-table.md`): problema crudo, quota ≤15 palabras, URL, comunidad, fecha, engagement estimado.

**Regla de oro:** solo es candidato si hay gente hablando del problema en los últimos 2 años. Sin dolor reciente → no entra a la tabla.

**Salida de fase:** lista de 8-20 problemas crudos (aún sin solución). Son "problemas", no productos.

**Sesgo anunciado:** recoge el problema con las citas textuales; NO inventar la solución todavía.

### Fase 2 — Filtrar (triage rápido)

Aplica `references/triage-rubric.md` a cada candidato: 5 preguntas SI/NO. Sin búsquedas nuevas — solo decisión documentada sobre la evidencia de Fase 1.

Pasan los que sumen ≥3/5. Máximo 5 pasan. Los descartados quedan registrados con su porqué (traza contra re-proponer).

**Salida de fase:** ranking corto de 3-5 candidatos con 1-liner de porqué pasa cada uno.

### Fase 3 — Validar (delegada)

Para cada candidato del top, **en orden, uno a la vez**, invoca el skill `market-research` completo (Phase 0 opcional ya resuelta; dar idea, target y geografía explícitos en el prompt del skill). El skill genera `reports/market-research-<slug>.md` (reutiliza sus `query-recipes.md`, `scoring-rubric.md` y `report-template.md` — NO duplicar esa lógica aquí).

No intercales candidatos: una validación terminada antes de empezar la siguiente (para ajustar presupuesto si una va floja).

**Salida de fase:** N informes market-research completos + anotación breve por cada uno (score y veredicto).

### Fase 4 — Analizar (comparativo)

Con los informes listos, redacta `reports/pipeline-ideas-<fecha>.md` con la plantilla `references/pipeline-report.md`:
- Matriz 6 dimensiones × ideas (con el score de cada informe).
- Veredicto relativo: mejor oportunidad, mejor riesgo/barrera, esfuerzo estimado.
- Orden de ejecución recomendado (build first / run next), con justificación 1-liner.
- Nota de honestidad: si ninguna idea salió GO o todas salieron débiles, dilo sin suavizar.

## Timebox (sprint completo)

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