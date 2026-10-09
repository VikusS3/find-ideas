# Pipeline Report Template — Análisis Comparativo de Ideas

Salida de F4 de `idea-hunter`. Resume N ideas (cada una con su `reports/market-research-<slug>.md` o mini-report) y las compara. Español (salvo citas). 600-1200 palabras + tablas. Densidad, no relleno.

```markdown
# Pipeline de Ideas: <sector/dominio>

**Fecha:** <fecha> · **Skill:** idea-hunter → market-research · **Incógnitas sin validar:** <n> · **Cluster asumido:** <país/región o inferido, 1-liner de porqué>

## 1. Resumen

<3-4 frases: cazadas, pasaron filtro, viables tras validar, cuál construir primero. Contexto capital/ventana que más pesó.>

## 2. Matriz comparativa

| Idea (slug) | Pain | Trend | Gap | Money | Size | Dist. | **Total** | Capital/Ventana | Veredicto |
|---|---|---|---|---|---|---|---|---|---|
| <slug> | X/10 | X/10 | X/10 | X/10 | X/10 | X/10 | **X.X** | <banda $/mes + ventana> | GO/PIVOT/KILL |

<Scores literal de cada informe (no recalculados aquí). Capital/Ventana = ficha F0 + evidencia del informe.>

## 3. Ranking y recomendación

| Posición | Idea | Por qué | Riesgo principal |
|---|---|---|---|
| 1 | | 1-liner (oportunidad × encaje × capital) | 1-liner (capital, norma de pago o timing) |

**Orden de ejecución sugerido:** build first → <slug>. Véase su informe §10.

## 4. Cross-cutting findings

<2-4 hallazgos entre ideas: patrones de dolor, incumbentes que se repiten, geografías con señales; clusters que pagan y no (banda $), estacionalidades/deadlines compartidos, canales donde la queja vive de verdad. No repetir la tabla.>

## 5. Honestidad

<Nada GO → dilo sin dulcificar. Todas débiles → la "menos mala" = PIVOT con cambio exacto (audiencia/features/precio/canal). Cluster capital bajo o ventana corta → dilo + ajuste de precio/pre-pago.>

## 6. Próximos pasos

1. Validación en campo de la #1 (landing + entrevistas; PAGO REAL en el cluster con la banda asumida, no interés declarado).
2. Re-cazar solo si la #1 muere en campo — usar traza `candidate-hunts-<fecha>.md`.

## Fuentes

<Todas las URLs de informes, o ref cruzado a cada mercado-research-<slug>.md §Sources.>
```

## Style rules

- Verdicto primero, tablas después, prosa solo donde aporta.
- Puntajes = copia literal de los informes; contradicción entre informes → anotarla aquí.
- No inventar números. Informe low-confidence → 🔻 al lado del veredicto.
- Citar cada informe por nombre de archivo (link relativo) y §Sources.