<!-- prettier-ignore -->
<div align="center">

# find-ideas

**AI-powered idea discovery and validation pipeline.**

Research real pain points, validate market demand, and get GO/PIVOT/KILL verdicts — all driven by agent skills.

[![Built with opencode](https://img.shields.io/badge/Built%20with-opencode-6B46C1?style=flat-square)](https://opencode.ai)
![Node.js](https://img.shields.io/badge/Node.js->=20-3c873a?style=flat-square)

[How it works](#how-it-works) • [Skills](#skills) • [Reports](#reports) • [Quick start](#quick-start)

</div>

## How it works

`find-ideas` is a pipeline that takes a **sector or domain** as input and produces structured, evidence-backed research reports with investment-grade verdicts.

```
Sector input → Idea Hunt → Triage → Market Research → Verdict (GO/PIVOT/KILL)
```

Each stage is powered by an [opencode](https://opencode.ai) agent skill that runs autonomously end-to-end — no human prompts between phases.

> [!TIP]
> Ask the agent: *"Busca ideas de proyectos en el sector minero"* or *"Hunt ideas in fintech LATAM"* — the pipeline handles the rest.

## Skills

The pipeline is built on three composable agent skills:

| Skill | Purpose | Output |
|-------|---------|--------|
| **idea-hunter** | Caza problemas reales de comunidades (Reddit, Quora, LinkedIn), los filtra con triage y delega validación | `reports/candidate-hunts-<date>.md` |
| **market-research** | Investiga una idea: pain points, demanda, competencia, tamaño de mercado, monetización | `reports/market-research-<slug>.md` |
| **find-skills** | Descubre e instala skills adicionales del ecosistema | Instalación en `.agents/skills/` |

### idea-hunter pipeline

1. **Hunt** — Búsqueda bilingüe (EN/ES) de quejas reales en comunidades. Mínimo 8 problemas crudos con URL y engagement.
2. **Filter** — Triage con 5 preguntas SI/NO. Pasan los que sumen ≥3/5 (máximo 5).
3. **Validate** — Delega a `market-research` por cada candidato, uno a la vez.
4. **Analyze** — Matriz comparativa de todas las ideas validadas con veredicto final.

### market-research phases

| Phase | Focus |
|-------|-------|
| 1. Pain discovery | Reddit, Quora, forums — real complaints, verbatim quotes |
| 2. Demand signals | Search trends, keyword volume, content activity |
| 3. Competitor gaps | 3-7 competitors, pricing, user complaints (1-2 star reviews) |
| 4. Market data | Market size, VC funding, monetization signals |
| 5. TAM/SAM/SOM | Bottom-up sizing with shown arithmetic |
| 6. Distribution | SEO, communities, channels, virality check |

Each report includes a **6-dimension scorecard** (Pain Intensity, Demand Trend, Competition Gap, Monetization, Market Size, Distribution) with weighted scoring and a final verdict:

- **GO** — Total ≥ 7.0, no dimension below 4
- **PIVOT** — Total 4.5-6.9, or total ≥ 7.0 with a weak dimension
- **KILL** — Total < 4.5

## Reports

All generated research reports live in the `reports/` directory:

```
reports/
├── candidate-hunts-2026-09-14.md                              # Raw idea hunt trace
├── market-research-revision-contratos-ia-firmas-pequenas.md   # Legal AI contract review (ES)
├── market-research-mining-predictive-maintenance.md           # Mining predictive maintenance
├── market-research-mine-safety-iot.md                         # Mine safety IoT platform
├── market-research-miningops-data-hub.md                      # Mining data integration hub
└── pipeline-ideas-2026-09-14.md                               # Comparative analysis
```

Each market research report contains:

- Executive summary with verdict and confidence level
- 6-dimension scorecard with weighted total
- Pain point evidence with source URLs
- Competitor landscape table with gaps
- TAM/SAM/SOM sizing with assumptions
- Distribution plan
- Risks and open questions
- Validation plan (landing page test, user interview questions, community targets)

## Quick start

> [!NOTE]
> This project runs on [opencode](https://opencode.ai) with agent skills. Make sure opencode is installed and configured.

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd find-ideas
```

### 2. Ask the agent to hunt ideas

```
Busca ideas de proyectos en [sector]
```

The agent will autonomously run the full pipeline and save reports to `reports/`.

### 3. Or validate a specific idea

```
Investiga si vale la pena construir [idea description]
```

The agent will run `market-research` directly and produce a single report.

### 4. Compare multiple ideas

```
Compara las ideas del pipeline y dime cuál atacar primero
```

The agent will generate a comparative matrix with prioritized execution order.

## Project structure

```
find-ideas/
├── .agents/
│   └── skills/
│       ├── find-skills/       # Skill discovery
│       ├── idea-hunter/       # Idea hunting pipeline
│       └── market-research/   # Deep market validation
├── reports/                   # Generated research reports
└── skills-lock.json           # Installed skill registry
```

## Example sectors

The pipeline has been tested on:

- **IA para abogados** — Legal AI for small firms (ES/LatAm)
- **Minería** — Predictive maintenance, safety IoT, data integration
- More sectors can be explored by triggering the agent with new domain keywords
