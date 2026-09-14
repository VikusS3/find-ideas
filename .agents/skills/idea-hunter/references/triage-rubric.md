# Triage Rubric — Filtro Rápido de Candidatos

Screening de 5 preguntas SI/NO por candidato. **Sin búsquedas nuevas** — se decide solo con la evidencia de Fase 1. Objetivo: pasar de 8-20 problemas crudos a 3-5 candidatos viables en ~15 tool calls totales.

## Las 5 preguntas

1. **¿Hay gente real y reciente quejándose del problema?**
   Menciones de los últimos 2 años con engagement mínimamente visible. Antigüedad >2 años sola = NO (busca señal fresca).
2. **¿No existe un workaround gratis y "suficiente"?**
   SI existe workaround gratis que la comunidad considera suficiente (lección SSL) → NO. El matiz clave: el workaround debe ser *realmente usado*, no solo posible. Si todos usan "la opción gratis que ya funciona", no hay mercado.
3. **¿Alguien paga hoy por resolverlo?** (o pagaría pese al workaround)
   Busca en la evidencia: gente mencionando lo que les cobran, suscripciones, "vale la pena", quejas de precio (quejarse del precio = están pagando). Nadie pagando y todos contentos con gratis = NO.
4. **¿Hay hueco atacable frente a incumbentes?**
   Si el candidato tiene un incumbente con usuarios felices y gratis → NO. Si los incumbentes tienen quejas, precios desorbitados, o segmento desatendido (idioma, región, tipo de usuario) → SI.
5. **¿Encaja con el perfil y recursos del usuario?**
   Factores: skills (dev/marketing/ventas), idioma, región, tiempo disponible, ambición (lifestyle vs venture). Un candidato brillante que nadie del equipo puede ejecutar = NO en este pipeline (pero queda registrado en la traza).

## Reglas de corte

- Pasa al top si suma **≥3 de 5**.
- Máximo **5 pasan**. Si hay empate, gana quien tenga mejor evidencia de pregunta 3 (alguien pagando).
- **Veto automático:** pregunta 1 = NO → elimina directo. Sin dolor reciente, no hay idea.
- Los que no pasen se registran en la candidate-table con la columna "Descartado por: Qn" — la traza previene re-proponer.

## Señales de alarma en esta fase (documentar)

- Workaround gratis generalizado (Q2 NO) pero con 2+ menciones de *dolor* intenso → candidato posible a PIVOT (tipo "vende el servicio, no el producto").
- Sector donde todas las queries devuelven marketing de incumbentes y cero quejas → "sector vacío": no forzar, reportar.
- Quejas hispanas silenciosas aunque el sector sea hispano → señalar en la traza; validar en campo (entrevistas) antes de invertir.

## Salida

Ranking corto 3-5 candidatos, cada uno con:
- problema (frase cruda)
- porqué pasa (qué 3+ preguntas le dieron SI, con la evidencia)
- target y geografía asumidos
- 1 riesgo principal ya visible