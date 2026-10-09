# Pipeline Report Template — Análisis Comparativo de Ideas

Salida de Fase 4 de `idea-hunter`. Resume N ideas validadas (cada una con su `reports/market-research-<slug>.md`) y las compara. Idioma español (salvo citas). Extensión: 600-1200 palabras + tablas. Densidad, no relleno.

---

```markdown
# Pipeline de Ideas: <sector/dominio>

**Fecha:** <fecha> · **Skill:** idea-hunter → market-research · **Incógnitas sin validar:** <n> · **Cluster asumido:** <país/región o inferido, con 1-liner de porqué>

## 1. Resumen

<3-4 frases: cuántas ideas se cazaron, cuántas pasaron el filtro, cuántas salieron viables tras validar, y cuál se recomienda construir primero. Mencionar el contexto capital/ventana que más pesó.>

## 2. Matriz comparativa

| Idea (slug) | Pain | Trend | Gap | Money | Size | Dist. | **Total** | Capital/Ventana | Veredicto |
|---|---|---|---|---|---|---|---|---|---|
| <slug> | X/10 | X/10 | X/10 | X/10 | X/10 | X/10 | **X.X** | <banda $/mes + ventana temporal> | GO/PIVOT/KILL |
| ... | | | | | | | | | |

<Nota: los puntajes salen de cada informe market-research; no recalculados aquí. La columna Capital/Ventana sale de la ficha de contexto (Fase 0) + evidencia de cada informe.>

## 3. Ranking y recomendación

| Posición | Idea | Por qué | Riesgo principal |
|---|---|---|---|
| 1 | | 1-liner (oportunidad × encaje × capital del cluster) | 1-liner (incl. capital, norma de pago o timing) |
| 2 | | | |
| 3 | | | |

**Orden de ejecución sugerido:** build first → <slug>. Véase su informe §10 para validación en campo.

## 4. Cross-cutting findings

<2-4 hallazgos que cruzan ideas (patrones de dolor comunes, incumbentes que se repiten, geografías con señales). Incluir hallazgos de contexto: clusters que pagan y clusters que no (con banda $), estacionalidades/deadlines compartidos, canales donde la queja vive de verdad. No repetir la tabla.>

## 5. Honestidad

<Si ninguna salió GO, dilo sin dulcificar. Si todas salieron débiles pero una es "la menos mala", nómbrala PIVOT y explica qué cambio exacto (audiencia / features / precio / canal) la rescataría. Si el cluster objetivo tiene capital bajo o ventana corta, dilo y nombra el ajuste de precio/pre-pago necesario.>

## 6. Próximos pasos

1. Validación en campo de la #1 (landing + entrevistas; ver su informe §10). Validar PAGO REAL: probar cobro en el cluster con la banda de precio asumida — no solo interés declarado.
2. Re-cazar solo si la #1 muere en campo — usar la traza `candidate-hunts-<fecha>.md` para esa decisión.

## Fuentes

<todas las URLs de los informes individuales, o referencia cruzada a cada market-research-<slug>.md §§Sources si ya están listadas.>
```

---

## Style rules

- Verdicto primero, tablas después, prosa solo donde aporta.
- Puntajes = copia literal de los informes individuales; si dos informes chocan con el dato, anotar la contradicción aquí.
- No inventar números. Si un informe fue "low-confidence", marcarlo con 🔻 al lado del veredicto.
- Citar cada informe por su nombre de archivo (link relativo) y su §Sources.