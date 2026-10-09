# Triage Rubric — Filtro Rápido de Candidatos

Screening de 5 preguntas SI/NO por candidato. **Sin búsquedas nuevas** — se decide solo con la evidencia de Fase 1 + el perfil de contexto de Fase 0. Objetivo: pasar de 8-20 problemas crudos a 3-5 candidatos viables en ~15 tool calls totales.

Las preguntas NO cambian en número ni en cut rule (sigue ≥3/5). El contexto (capital, norma de pago, canal, ventana) **calibra** cómo se lee cada una — no abre gates nuevos.

## Las 5 preguntas

1. **¿Hay gente real y reciente quejándose del problema?**
   Menciones de los últimos 2 años con engagement mínimamente visible. Antigüedad >2 años sola = NO (busca señal fresca). **Calibrador:** quejarse en el canal real del cluster. Si el dolor solo aparece en un canal donde el cluster no está (p.ej. Reddit EN para un cluster solo-MX), rebaja a NO salvo que haya fuente local — registra `Q1+canal`.
2. **¿No existe un workaround gratis y "suficiente"?**
   SI existe workaround gratis que la comunidad considera suficiente (lección SSL) → NO. El matiz clave: el workaround debe ser *realmente usado*, no solo posible. Si todos usan "la opción gratis que ya funciona", no hay mercado. **Calibrador:** en cluster con cultura gift (todo se comparte gratis), un workaround "gratis y aceptado" pesa más — pide evidencia dura de que la gente sufre, no que lo tolera.
3. **¿Alguien paga hoy por resolverlo?** (o pagaría pese al workaround)
   Busca en la evidencia: gente mencionando lo que les cobran, suscripciones, "vale la pena", quejas de precio (quejarse del precio = están pagando). Nadie pagando y todos contentos con gratis = NO. **Calibrador capital:** aunque "alguien pague", pregunta por la **banda $/mes** (columna Capital). Si el cluster paga pero muy por debajo del umbral mínimo que un negocio de este tipo necesita cobrar → NO (Q3+capital). Dos menciones de pago sin banda citada = sigue SI pero anota "sin anclas de precio".
4. **¿Hay hueco atacable frente a incumbentes?**
   Si el candidato tiene un incumbente con usuarios felices y gratis → NO. Si los incumbentes tienen quejas, precios desorbitados, o segmento desatendido (idioma, región, tipo de usuario) → SI. **Calibrador:** el segmento desatendido por país/idioma cuenta fuerte: un incumbente global que no habla el idioma del cluster o no acepta su método de pago = hueco real.
5. **¿Encaja con el perfil y recursos del usuario?**
   Factores: skills (dev/marketing/ventas), idioma, región, tiempo disponible, ambición (lifestyle vs venture). Un candidato brillante que nadie del equipo puede ejecutar = NO en este pipeline (pero queda registrado en la traza). **Calibrador contexto:** suma el cluster objetivo: si el usuario no domina el idioma/canales del cluster donde está el dolor, o el canal exige presencia local que no puede dar, rebaja el SI.

## Reglas de corte

- Pasa al top si suma **≥3 de 5**.
- Máximo **5 pasan**. Si hay empate, gana quien tenga mejor evidencia de pregunta 3 (alguien pagando); desempata la **banda de capital** citada y la **ventana temporal** (atemporal o deadline aprovechable > estacional sin fecha).
- **Veto automático:** pregunta 1 = NO → elimina directo. Sin dolor reciente, no hay idea. El contexto (capital bajo, norma gift, canal flojo) NUNCA veto solo: rebaja la pregunta que calibra y, si llega, se documenta como `Qn+contexto` en la traza.
- Los que no pasen se registran en la candidate-table con la columna "Descartado por: Qn" — la traza previene re-proponer.

## Señales de alarma en esta fase (documentar)

- Workaround gratis generalizado (Q2 NO) pero con 2+ menciones de *dolor* intenso → candidato posible a PIVOT (tipo "vende el servicio, no el producto").
- Sector donde todas las queries devuelven marketing de incumbentes y cero quejas → "sector vacío": no forzar, reportar.
- Quejas hispanas silenciosas aunque el sector sea hispano → señalar en la traza; validar en campo (entrevistas) antes de invertir.
- Dolor global fuerte pero cluster objetivo con capital bajo (Q3+capital) → NO KILL automático: marca PIVOT de precio (pre-pago, servicio, planes por uso en moneda local) y déjalo en ranking de "rescatables".
- Quejas que solo viven en un canal donde el cluster no está (Q1+canal) → no descartar el dolor; verificar el canal real en campo antes de invertir.
- Señal solo estacional o pegada a un deadline que ya pasó este ciclo → planear lanzamiento para el próximo ciclo, no descartarlo por silencio fuera de temporada.

## Salida

Ranking corto 3-5 candidatos, cada uno con:
- problema (frase cruda)
- porqué pasa (qué 3+ preguntas le dieron SI, con la evidencia)
- target, geografía y **cluster confirmado** (con su banda de capital y ventana temporal)
- 1 riesgo principal ya visible (incluye riesgos de contexto: capital, norma de pago, canal, timing)