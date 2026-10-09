# Triage Rubric — Filtro Rápido de Candidatos

5 preguntas SI/NO por candidato. **Sin búsquedas nuevas** — solo evidencia de F1 + perfil F0. Objetivo: 8-20 → 3-5 en ~15 calls. Las preguntas y el cut rule (≥3/5) NO cambian. El contexto (capital, norma de pago, canal, ventana) **calibra** cómo se lee cada una — no abre gates nuevos.

## Las 5 preguntas

1. **¿Hay gente real y reciente quejándose?**
   Menciones <2 años con engagement visible. Antigüedad >2 años sola = NO. **Calibrador:** quejarse en el canal real del cluster; dolor solo en canal donde el cluster no está (Reddit EN para MX puro) = NO salvo fuente local → `Q1+canal`.
2. **¿No existe workaround gratis y "suficiente"?**
   Sí existe gratis que la comunidad considera suficiente (lección SSL) → NO. Debe ser *realmente usado*, no solo posible. **Calibrador:** cluster gift → workaround gratis pesa más; exige evidencia de sufrimiento, no de tolerancia.
3. **¿Alguien paga hoy?** (o pagaría pese al workaround)
   Busca: cobros citados, suscripciones, "vale la pena", queja de precio (= pagando). Nadie pagando y todos contentos con gratis = NO. **Calibrador capital:** paga pero por debajo del umbral mínimo del negocio → `Q3+capital`. 2 menciones sin banda citada = SI + "sin anclas de precio".
4. **¿Hay hueco atacable vs incumbentes?**
   Incumbente con usuarios felices y gratis → NO. Quejas, precios desorbitados, o segmento desatendido (idioma/región/tipo) → SI. **Calibrador:** incumbente global sin el idioma del cluster o sin su método de pago = hueco real.
5. **¿Encaja con el perfil y recursos del usuario?**
   Skills, idioma, región, tiempo, ambición (lifestyle vs venture). Brillante que nadie puede ejecutar = NO en este pipeline (queda en traza). **Calibrador:** usuario no domina el idioma/canales del cluster, o presencia local imposible → rebaja el SI.

## Reglas de corte

- Pasa **≥3/5**. Máximo **5**. Empate → mejor evidencia de Q3 (alguien pagando); desempata banda de capital citada y ventana (atemporal o deadline aprovechable > estacional sin fecha).
- **Veto automático:** Q1 = NO → elimina directo. El contexto (capital bajo, norma gift, canal flojo) **NUNCA** veto solo: rebaja la pregunta que calibra y se documenta `Qn+ctx` en la traza.
- Los que no pasen → candidate-table "Descartado por: Qn" (traza contra re-proponer).

## Señales de alarma (documentar)

- Workaround gratis generalizado (Q2 NO) + 2+ menciones de dolor intenso → posible PIVOT ("vende el servicio, no el producto").
- Todas las queries devuelven marketing de incumbentes y cero quejas → "sector vacío": no forzar, reporta.
- Quejas hispanas silenciosas pese a sector hispano → traza; validar en campo antes de invertir.
- Dolor global fuerte pero cluster con capital bajo (Q3+capital) → NO KILL: PIVOT de precio (pre-pago, servicio, moneda local), déjalo en "rescatables".
- Queja solo en canal sin cluster (Q1+canal) → no descartar el dolor; verificar canal real en campo.
- Señal estacional o deadline ya pasado → planear el próximo ciclo, no descartar.

## Salida

Ranking 3-5, cada uno: problema (frase cruda) · porqué pasa (qué 3+ preguntas dieron SI, con evidencia) · target + geografía + cluster confirmado (banda capital + ventana) · 1 riesgo visible (capital/norma/canal/timing). Texto caveman-terse.