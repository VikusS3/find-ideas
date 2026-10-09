# Hunting Queries — Caza de Dolor en Modo Amplio

Adaptado de `../market-research/references/query-recipes.md`, en modo *idea sourcing* (busca quejas, no soluciones). Todas las queries se corren por el **cluster objetivo** de Fase 0 (país/región + canales reales). Mantener queries cortas (2-6 palabras).

## Por medio de queja

### Reddit (prioridad #1 cuando el cluster lee EN — engagement visible)
- `[sector] reddit "is there an app"`
- `[sector] reddit "I hate"`
- `[sector] reddit alternative`
- `[sector] "how do I" reddit`
- `[sector] "am I the only one" reddit`
- ES: `[sector] reddit "no hay" OR "falta" OR "molesta"`
- ES: `[sector] app alternativa reddit`
- Solo si el cluster es de país EN/US. Para cluster hispano, Reddit es canal secundario → priorizar canales locales abajo.

### Quora / Q&A
- `[sector] quora problem`
- `"I wish there was" [sector]`
- ES: `[sector] quora "cómo" problema`
- ES: `"ojalá existiera" [sector]`

### Hacker News (dev/prosumer)
- `[sector] hacker news`
- `show hn [sector]` (lee los comentarios: piden features que no existen = huecos)
- `[sector] hn thread`

### LinkedIn / B2B
- `[sector] "struggling with" linkedin`
- `[sector] workflow frustrating`
- ES: `[sector] linkedin "se nos hace difícil" OR "nos cuesta"`

### Foros de nicho (B2B, regulatorio)
- `[sector] forum complaint`
- `[sector] community "does anyone else"`
- Si el sector tiene vocación hispana: busca `[sector] comunidad foro problema` (ej. ForoSAP, WordPress en español, foros de abogados, etc.)

### X/Twitter
- `[sector] twitter "why can't I"`
- `[sector] twitter rant`

## Canales locales por cluster (Fase 0)

El canal real de cada cluster hispano NO es Reddit. Según el perfil de Fase 0:

### Cluster MX / Andina (latam general)
- `[sector] facebook grupo problema` y `[sector] grupo de facebook "alguien más"`
- `[sector] what(s)app OR telegram canal queja`
- `[sector] tiktok problema OR frustración` (lee los comments, no el video)
- `[sector] foro méxico OR perú OR colombia problema`
- ES: `[sector] "a alguien más le pasa"`

### Cluster Cono Sur (AR/CL/UY)
- `[sector] foro chile OR argentina problema`
- `[sector] twitter mala experiencia OR "se me hace difícil"`
- `[sector] grupo de facebook argentina OR chile`

### Cluster España
- `[sector] forocoches problema`
- `[sector] foro españa "os pasa a vosotros"`
- `[sector] telegram canal españa queja`

### Regla de canal
- Si Fase 0 dice que el público vive en canal X, busca ahí primero. Quejas en canal equívoco (p.ej. Reddit EN para un cluster solo-MX) = señal flaca, registra con `✗ débil` y busca el canal real antes de descartar el dolor.

## País / filtros de dominio (si el cluster es un país concreto)

- Añade `site:` del dominio-país cuando el medio lo soporte: `site:.com.mx`, `site:.com.pe`, `site:.com.ar`, `site:.es`.
- Prefijos de moneda en queries hispanas: `$`, `usd`, `mx`, `pesos` — marcan cuánto se paga y en qué moneda se piensa.
- Ej: `[sector] "cuánto cobran" mx`, `[sector] "$" precios argentina`.

## Capital dispuesto (qué pueden pagar)

Corre 2-3 de estas si Fase 0 dejó dudas de poder de compra:
- `[sector] "dispuesto a pagar"` / ES `[sector] "dispuesto a pagar"`
- `[sector] "cuánto pagas" OR "cuánto pagáis"` (`cuánto cobran` si es B2B)
- `[sector] "estoy pagando" $ OR [moneda]`
- `[sector] "vale la pena" [herramienta/alternativa]` (dudar antes de pagar = precios en mente)
- `[sector] queja precio` (quejarse del precio = están pagando)

Anota el rango $/mes que aparece en la columna `Capital (banda $/mes)` de la candidate-table.

## Timing / ventanas temporales

- Estacionalidad: `[sector] "in [temporada]"`, `[sector] [mes] problema`, ES: `[sector] "temporada de"`, `[sector] [mes] colapsado`.
- Deadlines fiscales/regulatorios (ej. impuestos, eInvoice, registro): `[sector] "antes de [deadline]"`, `[sector] [deadline] plazo OR obligación`, ES: `[sector] "último día para"`.
- Regreso a clases / vacaciones / cosechas según país: `[sector] "regreso a clases"`, `[sector] temporada [actividad]`.
- Registra la ventana en la columna `Ventana temporal` (estacional / deadline / atemporal). Atemporal también es válido — solo anótalo.

## Por tipo de audiencia (añadir prefijo)

| Audiencia | Prefijo |
|---|---|
| Dev/prosumer | `hacker news/github/stackoverflow [sector]` |
| B2B small | `msp hosting agencies [sector]` |
| Consumer | `reddit [sector] "worth it"` (gente dudando si pagar = señal de valor) |
| Cluster de país (MX/PE/CO) | versión ES + canal local del país (sección canales por cluster) + `site:` dominio-país |
| Cono Sur (AR/CL/UY) | versión ES + foros locales + twitter local |
| España | versión ES + forocoches + `site:.es` |

## Señales que convierten un "problema" en candidato

Al registrar, marca con **[🔥 fuerte]** / **[ok]** / **[✗ débil]**:
- 🔥: queja reciente (<2 años), varias menciones, engagement alto (↑100 upvotes / >15 replies / hilo largo), gente describiendo workaround casero o "yo lo pago hoy". En un cluster de país: la queja debe salir del **canal real del cluster**, no de un Reddit EN con cero audiencia local.
- ok: mención reciente aislada pero precisa, o dolor mencionado en artículo/review. Si viene con banda de precio citada o en temporada activa, sube a ok fuerte.
- ✗: hilo de >3 años sin actividad, queja vaga ("sería bueno"), dolor resuelto por un workaround que todo el mundo llama "fácil y gratis", o dolor en canal equivocado (cluster no presente allí).

## Contraseña contra el falso candidato

El caso SSL lo enseñó: si el workaround estándar de la comunidad es **gratis y "suficiente"**, no hay mercado pagado aunque exista la queja. Pregunta al registrar: *¿qué hace la gente AHOra mismo?, ¿pagando, sufriendo, o con una solución gratis que ya conocen?* Solo el primer y segundo caso producen candidatos.

## Cómo registrar

Usa `references/candidate-table.md`. Una fila por candidato. Máx. 5-10 filas fuertes > 30 débiles. Rellena además las columnas de contexto: `País/Cluster`, `Capital (banda $/mes)`, `Ventana temporal` (estacional/deadline/atemporal) y `Norma de pago` (digital/efectivo/gift) con lo que la evidencia muestre — la Fase 3 las usa para fijar geografía y pricing.