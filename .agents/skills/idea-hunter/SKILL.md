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

Caza ideas desde dolor real, filtra, valida con `market-research`, compara. Pipeline 0→4, un trigger, sin paradas.

## Cuándo usar

- "dame ideas", "caza ideas de [sector/país]", "qué puedo construir".
- Varias ideas validadas → decidir cuál atacar primero.
- NO: validar una idea única ya concreta → `market-research` directo.

## Configuración

- **Entrada:** 1-2 palabras de sector + opcional país. Sin sector → propone 5-8 dominios y pregunta una vez (sin interrogatorio).
- **Cluster:** país dado lo fija; si no, se infiere (MX/Andina/Cono Sur/ES/global) de señales de F1 y **se declara el default asumido** al inicio del informe.
- **Autonomía:** F0→F4 sin pausas. NO pregunta hasta entregar.
- **Idioma:** búsquedas bilingües (EN + local por cluster); informes/matrices/resúmenes siempre en español.
- **Salidas:** `reports/candidate-hunts-<fecha>.md` (traza), `reports/market-research-<slug>.md` por idea, `reports/pipeline-ideas-<fecha>.md` (final).

## Pipeline

### Fase 0 — Contexto (perfil sociocultural-económico)

Perfil ANTES de cazar. ≤3 tool calls (ideal 0-1; base de conocimiento + 1-2 búsquedas finas solo si duda estructural).

- **Cluster:** país/región, idioma, **canales reales** (Reddit EN / FB grupos / WhatsApp-Telegram / TikTok-IG comments / foros locales). El canal manda: si el cluster no está donde buscarías, las quejas no aparecen.
- **Norma de pago:** tarjeta/wallet/giros; cultura "gift" vs disposición a pagar. Calibra (no reemplaza) "¿alguien paga?".
- **Capital:** banda de precio citada en hilos + poder de compra del país. Pregunta: *¿el bolsillo del cluster cubre el umbral mínimo que este negocio debe cobrar?*
- **Timing:** estacionalidad del dolor, deadlines fiscales/regulatorios, ventanas de trend. Una ventana = timing a gestionar, no freno.

**Salida:** ficha 5-10 líneas → informe final + Fases 1-3.

### Fase 1 — Cazar (idea sourcing)

Patrones de `market-research` en modo amplio. Lee `references/hunting-queries.md`.

- Queries por **canales del cluster** (F0), bilingüe: `reddit "is there an app"`, `"I wish I could"`, `"am I the only one"`, quora, linkedin/hn según audiencia; ES `"ojalá hubiera"`, canal local (FB/telegram/foro país) + `site:` dominio-país.
- Capital/timing: `"dispuesto a pagar"`, `"cuánto cobran"`, `"estoy pagando $"`, temporada/deadline.
- **Presupuesto:** 4-8 búsquedas (3-5 si el primer lote ya da señales fuertes y **parar**). Preferir 1 página rica sobre 4 superficiales. No repetir query fallida más de una vez.
- Registrar cada candidato en `references/candidate-table.md` (compacta: problema ≤1 línea, quota ≤15 palabras, fuente, comunidad, fecha, engagement).
- **Regla de oro:** candidato solo si dolor reciente (<2 años) **en el cluster objetivo**. Queja global no cuenta si el cluster no paga; dolor local en foro externo no invalida un cluster que habla en sus canales reales.
- **Sesgo anunciado:** registrar la queja textual; NO inventar la solución.
- **Salida:** 8-20 problemas crudos (problemas, no productos).

### Fase 2 — Filtrar (triage rápido)

`references/triage-rubric.md`: 5 preguntas SI/NO calibradas por ficha F0. Sin búsquedas nuevas. Pasan ≥3/5, máx 5. Descartados → traza con motivo `Qn[+ctx]`.

**Salida:** ranking 3-5 candidatos, 1-liner de porqué pasa cada uno (terso).

### Fase 3 — Validar (delegada)

En orden, uno a la vez. Invoca `market-research` pasándole la ficha F0 (cluster, capital, ventana, norma) para fijar geografía/pricing desde arranque.

**Presupuesto ajustado:** triage ≥4/5 + señales fuertes → MR completo (report ~800-2000 palabras). Borderline → **validación ligera** (3-5 búsquedas, mini-report ~400 palabras, marcado de baja confianza). No inventar señales para subir de nivel.

No intercales candidatos (ajusta presupuesto si una va floja).

**Salida:** N informes + anotación breve por cada (score + veredicto).

### Fase 4 — Analizar (comparativo)

`references/pipeline-report.md` → `reports/pipeline-ideas-<fecha>.md`:

- Matriz 6 dimensiones × ideas (scores **literal** de informes, no recalculados) + columna Capital/Ventana.
- Veredicto relativo: mejor oportunidad, mejor riesgo, esfuerzo estimado. Contexto low-capital o ventana sin esconder.
- Orden de ejecución (build first / run next) con justificación 1-liner.
- Nota de honestidad si nada GO o todo débil.

Sin búsquedas nuevas.

## Timebox

- F0: ≤3 calls (ideal 0-1). F1-2: ≤15 calls (objetivo ≤10). F3: por idea (MR completo 15-30 calls; ligera 3-5). F4: redacción directa.
- Sector sin candidatos viables en F2 → KILL temprano: reporta "sector vacío", no inventes señales.

## Economía de tokens (obligatorio)

- **Capa-chat e intermedio: caveman-full.** Sin narración entre tool calls, sin progress notes, sin re-citar lo ya registrado, sin tablas decorativas en chat.
- **`reports/*.md`: SIEMPRE español normal** (boundary caveman: lo persistido vista por humanos = prosa normal). Nunca caveman en entregables.
- Resumen final en chat: **3 bullets** (mejor, peor, build-first) ≤ ~120 tokens.
- Ranking F2 y anotaciones F3: 1-3 líneas terse.
- `websearch`: `numResults` 4-6, `contextMaxCharacters` ~4000, `type` fast.
- Objetivo: presupuesto total (in+out) ~30-60% bajo baseline — refs comprimidas + búsquedas cortas + chat terse.

## Reglas de honestidad (heredadas de market-research)

- Evidencia > vibra. Toda claim material con URL. Señal débil → "weak signal", no rellenes.
- KILL sin pena. La traza de descartados protege de re-proponer.
- Contradicciones = hallazgos. Si los datos crecen pero las comunidades callan, repórtalo.
- No inflar scores para ser amable.

## Entregables al cierre

1. `candidate-hunts-<fecha>.md` (traza; opcional si ruido — al menos se conserva).
2. `market-research-<slug>.md` por idea (o mini-report si validación ligera).
3. `pipeline-ideas-<fecha>.md` final.
4. Resumen chat 3 bullets (mejor, peor, build-first + qué validar en campo antes de construir).