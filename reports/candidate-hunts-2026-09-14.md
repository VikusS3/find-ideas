# Candidate Hunt: "IA para abogados" — Traza cruda

**Fecha:** 14 sep 2026 · **Skill:** idea-hunter Fase 1-2 · **Idioma:** bilingüe

## Problemas cazados (8)

| # | Problema crudo | Quota | Fuente | Comunidad | Fecha | Engagement | Fortaleza | Workaround actual | ¿Pagan hoy? |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Revisión de contratos con IA: alta oferta, los abogados no se fían de que detecten bien los red flags | "I have worked with a couple of AI contract review software solutions, and I barely trusted them to get the red flags right" | https://www.reddit.com/r/legaltech/comments/1o0kcfy/ | r/legaltech | reciente | medio | 🔥 | Revisión manual (2-4h/contrato) o ChatGPT genérico | Sí: Luminance 700+ clientes, Harvey (val. $5B) |
| 2 | Herramientas de contract review fallan con documentos reales (demos impecables, producción rota) | "Demos... always used clean, standardized contracts where the AI looks flawless. The problem shows up when firms run real documents" | https://www.reddit.com/r/legaltech/comments/1rxwwx6/ | r/legaltech | mar 2026 | alto | 🔥 | Plantillas + revisión manual | Sí: LinkSquares, Ironclad suscripciones |
| 3 | Billing con IA: revisión de tiempos contra guidelines de clientes/aseguradoras (write-offs) | billing es "the bane of lawyers' existence"; los carriers descuentan entradas vagas | https://abovethelaw.com/2026/04/ai-and-billing-flipping-the-switch-on-the-bane-of-lawyers-existence | Above the Law | abr 2026 | medio | 🔥 | Validación manual entrada a entrada | Sí: Elite Validate, TimeSolv, Clio |
| 4 | Alucinaciones de IA (citas judiciales inventadas) → sanciones y multas a abogados | "los abogados no comprobaron las autoridades legales citadas... violación de la Regla 11" | https://www.infobae.com/tecno/2026/06/12/... | Infobae + Law360 + ABA | jun 2026 | alto (multimedio) | 🔥 | Verificación manual de cada cita | Indirecto: compradores de research (Lexis, Bloomberg) |
| 5 | Workflows de contratos caóticos en firmas (sin trazabilidad, versiones por nombre de archivo) | "Email threads as workflow... version control through file names (v4_FINAL_FINAL2)" | https://www.reddit.com/r/legaltech/comments/1p66s50/ | r/legaltech | nov 2025 | alto | 🔥 | Email + nombres de archivo + approvals manuales | Sí, pero "midsize firms priced out" |
| 6 | CLM caros y rígidos dejan fuera a firmas pequeñas/medianas | "Are midsize firms being priced out of contract management tech?" | https://www.reddit.com/r/legaltech/comments/1rxwwx6/ | r/legaltech | mar 2026 | medio | ok | Excel + PDFs + email | Parcial: quieren CLM pero no llegan |
| 7 | Adopción real baja de IA legal en solos/small firms (intención alta, uso bajo) | ABA 2024: 30% usa IA; en solos <20%; drama adopción Harvey | https://www.businessinsider.com/harvey-reddit-drama-ceo-winston-weinberg-2025-9 | Business Insider | sep 2025 | alto | ok | ChatGPT gratis + cursos | Flojito |
| 8 | Falta de trazabilidad/explicabilidad en IA legal (cajas negras) que las barras exigen | "This really resonates. The core issue isn't AI—it's chaotic workflows" | https://www.reddit.com/r/legaltech/comments/1p66s50/ | r/legaltech | nov 2025 | medio | ok | Productos propietarios de grandes firmas (Shoosmiths Apollo) | Grandes firmas, no indies |

## Triage (Fase 2)

| Candidato | Q1 dolor reciente | Q2 sin workaround gratis | Q3 alguien paga | Q4 hueco atacable | Q5 encaje | Total | Pasa |
|---|---|---|---|---|---|---|---|
| A. Revisión de contratos IA para small firms | SI | SI (parcial: ChatGPT pero sin fiabilidad) | SI (Luminance, Harvey) | SI (quejas: rigidez, docs reales) | SI (dev+dominio) | 5 | ✔ #1 |
| B. Billing/guideline AI | SI | SI | SI (Elite, TimeSolv) | SI (incipiente) | SI (dev, dominio ligero) | 5 | ✔ #2 |
| C. Check de citas/hallucination | SI | SI | SI (indirecto) | medio (gigantes lo absorben) | SI | 4 | ✔ #3 |
| D. CLM accesible small firms | SI | SI | parcial | SI (hueco fuerte) | medio (esfuerzo alto) | 4 | ✔ #4 |
| E. Onboarding IA para solos | SI | NO (cursos baratos) | flojito | medio | medio | 3 | borderline |

**Descartados:** E (workaround cursos + monetización flojita) → registrado para no re-proponer.

## Notas de señal débil

- Quejas hispanas directas casi inexistentes: el dolor se documenta en EN (r/legaltech, ABA, Law360) y las fuentes ES repiten sanciones/entrevistas. Para el ángulo LATAM hay que validar en campo (colegios de abogados, encuestas ES).
- El sector IA legal tiene dinero VC ($800M en Harvey, CAs invirtiendo) → mercado real, pero los incumbentes son fuertes. El hueco indie está claramente en: small firms / solos, precisión con documentos reales, y CLM/billing accesible.

## Candidato elegido para validar

**#1 (A):** Herramienta de revisión/análisis de contratos con IA para firmas pequeñas y solos (segmento desatendido), ángulo hispano-hablante. Delegar validación completa a skill `market-research`.