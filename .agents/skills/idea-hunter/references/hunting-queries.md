# Hunting Queries — Caza de Dolor (modo amplio)

Adaptado de market-research `query-recipes.md`, modo *idea sourcing* (busca quejas, no soluciones). Corre por el **cluster objetivo** de F0 (país/región + canales reales). Queries cortas (2-6 palabras).

## Por medio

### Reddit (prio #1 si el cluster lee EN — engagement visible)
- `[sector] reddit "is there an app"` · `"I hate"` · `alternative` · `"how do I"` · `"am I the only one"`
- ES: `[sector] reddit "no hay" OR "falta" OR "molesta"` · `app alternativa reddit`
- Cluster hispano: Reddit = canal secundario → prioriza canales locales abajo.

### Quora / Q&A
- `[sector] quora problem` · `"I wish there was" [sector]` · ES `"ojalá existiera" [sector]`

### Hacker News (dev/prosumer)
- `[sector] hacker news` · `show hn [sector]` (lee comments: piden features que no existen = huecos) · `[sector] hn thread`

### LinkedIn / B2B
- `[sector] "struggling with" linkedin` · `[sector] workflow frustrating` · ES `[sector] "se nos hace difícil" OR "nos cuesta"`

### Foros de nicho / X
- Foro: `[sector] forum complaint` · `[sector] community "does anyone else"` · ES `[sector] comunidad foro problema`
- X: `[sector] twitter "why can't I"` · `[sector] twitter rant`

## Canales locales por cluster (F0)

### Cluster MX / Andina
- `[sector] facebook grupo problema` · `[sector] "a alguien más le pasa"` · wpp/telegram canal queja · tiktok problema (lee comments, no video) · foro méxico/perú/colombia

### Cluster Cono Sur (AR/CL/UY)
- `[sector] foro chile OR argentina problema` · twitter mala experiencia · grupo facebook argentina OR chile

### Cluster España
- `[sector] forocoches problema` · `[sector] foro españa "os pasa a vosotros"` · telegram canal españa queja

### Regla de canal
- Cluster vive en canal X → busca ahí primero. Queja en canal equívoco (p.ej. Reddit EN para cluster solo-MX) = ✗ débil hasta confirmar el canal real.

## Filtros de país (cluster = país concreto)
- `site:` dominio-país (`site:.com.mx/.com.pe/.com.ar/.es`) si el medio lo soporta — web_search built-in NO tolera operadores, omitir ahí.
- Prefijos de moneda: `$`, `usd`, `mx`, `pesos` — marcan cuánto se paga y en qué moneda se piensa.

## Capital dispuesto (2-3 si F0 dejó dudas)
- `[sector] "dispuesto a pagar"` · `"cuánto pagas"/"cuánto pagáis"` (`cuánto cobran` si B2B) · `"estoy pagando" $` · `"vale la pena" [herramienta]` (dudar antes de pagar = precios en mente) · queja de precio (= están pagando)
- Anota la banda $/mes en columna `Ctx` de candidate-table.

## Timing / ventanas temporales
- Estacional: `[sector] "in [temporada]"` · `[mes] problema` · ES `temporada de` · `[mes] colapsado`
- Deadlines: `"antes de [deadline]"` · `[deadline] plazo OR obligación` · ES `"último día para"`
- Registra en `Ctx`: estacional / deadline / atemporal (atemporal también vale).

## Por tipo de audiencia (prefijo)
| Audiencia | Prefijo |
|---|---|
| Dev/prosumer | `hacker news/github/stackoverflow [sector]` |
| B2B small | `msp hosting agencies [sector]` |
| Consumer | `reddit [sector] "worth it"` (dudando si pagar = señal de valor) |
| MX/PE/CO | ES + canal local + `site:` dominio-país |
| Cono Sur | ES + foros locales + twitter local |
| España | ES + forocoches + `site:.es` |

## Fuerza de señal (marcar 🔥/ok/✗ al registrar)
- 🔥: queja <2 años, varias menciones, engagement alto (↑100 upvotes / >15 replies / hilo largo), workaround casero o "yo lo pago". Cluster de país: la queja debe salir del **canal real del cluster**, no Reddit EN sin audiencia local.
- ok: mención reciente aislada pero precisa, o dolor en review/artículo. Con banda de precio citada o temporada activa sube a ok fuerte.
- ✗: hilo >3 años sin actividad, queja vaga ("sería bueno"), workaround gratis que todos llaman "fácil y suficiente", o canal equivocado.

## Contraseña contra el falso candidato (lección SSL)
Si el workaround estándar de la comunidad es **gratis y "suficiente"**, no hay mercado pagado aunque exista la queja. Al registrar pregunta: *¿qué hace la gente AHORA? ¿pagando, sufriendo, o con solución gratis que ya conocen?* Solo las dos primeras producen candidatos.

## Cómo registrar
`references/candidate-table.md`, 1 fila por candidato. Prefiere 5-10 filas fuertes a 30 débiles. Rellena `Ctx` con la evidencia — la F3 la usa para fijar geografía y pricing.