---
name: market-research
description: Run deep market research and validation on an app, product, SaaS, or startup idea, producing a structured markdown report with a GO/PIVOT/KILL verdict. Use this skill whenever the user wants to validate an idea, research a market or niche, check if an idea is "worth building", analyze competitors, size a market (TAM/SAM/SOM), find pain points for a product concept, or asks things like "is there demand for X", "research this idea", "should I build X", or "who are the competitors for X" — even if they don't explicitly say "market research."
---

# Market Research & Idea Validation

Validate an idea by researching two things: **macro trends** (is the market growing?) and **micro pain points** (are real people complaining about a specific problem?). Produce a single markdown report file with evidence, scores, and a verdict.

## Step 0: Detect tools & scope the idea

**Tools (adapt to what's available):**

- If Firecrawl / Tavily MCP tools are available, prefer them: `tavily_search` or `firecrawl_search` for broad research, `firecrawl_scrape` / `tavily_extract` for reading specific pages (competitor pricing pages, review pages). Load them via tool search if deferred.
- Otherwise use built-in `web_search` and `web_fetch`.
- No live tools at all → tell the user research will be from training knowledge only and dated; offer to proceed anyway.

**Scope with the user (only if unclear — don't interrogate):**

- One-line description of the idea and the core problem it solves
- Target user (consumer / prosumer / B2B) — this changes which sources matter
- Geography focus (global, US, India, etc.) if relevant to pricing/demand

If the user gives a clear idea, just start. State assumptions in the report rather than blocking on questions.

## Research phases

Run phases 1–6 below. Budget roughly 2–4 searches per phase; go deeper where signals are strong or contradictory. Track every claim's source URL as you go — the report requires evidence links.

Read `references/query-recipes.md` before starting phase 1 — it has the exact search patterns per phase.

### Phase 1: Pain point discovery (social listening)

Find real humans complaining about the problem. Search Reddit, Quora, X/Twitter, Hacker News, niche forums for complaint language ("I hate it when", "is there an app for", "alternative to"). Record: verbatim quotes (short), thread engagement (upvotes/replies), recency, which communities. **If you cannot find anyone talking about the problem, that is itself a major red flag — say so plainly.**

### Phase 2: Demand quantification (search trends & keywords)

Estimate whether people actively search for a solution: Google Trends direction (rising/flat/dying), keyword search volume estimates from SEO sources, question patterns (AnswerThePublic-style "how do I…" queries). You can't access Google Trends interactively — search for published trend data, "keyword volume" articles, or infer from content volume and recency.

### Phase 3: Competitor & gap analysis

Identify 3–7 existing solutions (app stores, Product Hunt, G2/Capterra for B2B, GitHub for dev tools). For each: what it does, pricing, and — most important — **what users hate about it**. Mine 1–2 star reviews, Product Hunt comment complaints, G2 "Cons" sections. The gaps found here become the differentiation opportunities in the report. A crowded market with unhappy users is an opportunity; a crowded market with happy users is a warning.

### Phase 4: Market data & monetization

- **Market size & trajectory:** industry reports, Statista-style figures, funding activity (Crunchbase mentions, recent raises in the space). VC money flowing in = financially viable market.
- **Monetization signals:** competitor pricing models (subscription/one-time/freemium tiers), evidence of willingness to pay ("I'd pay for", "worth every penny", complaints about price = they ARE paying), typical price points in the niche. Adjust for geography if user has a regional focus (e.g., India price sensitivity).

### Phase 5: TAM/SAM/SOM sizing

Lightweight bottoms-up estimate, clearly labeled as an estimate:

- **TAM:** total people/businesses with the problem × plausible annual revenue per user
- **SAM:** the segment reachable with this product form (platform, language, geography)
- **SOM:** realistic 1–3 year capture (usually 0.1–2% of SAM for an indie/startup)
  Show the arithmetic and the assumptions. Never present sizing as fact.

### Phase 6: Distribution check

Where would users actually come from? Assess: SEO difficulty (are top results dominated by giants?), community channels (subreddits/Discords that allow promotion), App Store keyword competition, content/social viability, paid-ads feasibility at the niche's price point. An idea with demand but no reachable channel scores poorly.

## Scoring & verdict

After the phases, score the idea using `references/scoring-rubric.md` (read it at this point). Six dimensions, 0–10 each, with defined anchors: Pain Intensity, Demand Trend, Competition Gap, Monetization, Market Size, Distribution. Compute the weighted total and map it to **GO / PIVOT / KILL** per the rubric, including the standard override rules (e.g., Pain Intensity ≤ 2 forces KILL regardless of total).

## Report output

Write the report as a markdown file following `references/report-template.md` (read it before writing). Save to the working/output directory as `market-research-<idea-slug>.md` and present it to the user with the file-presentation tool if available.

After delivering the file, give a 3–5 sentence verdict summary in chat: the score, the verdict, the single biggest opportunity, and the single biggest risk. Do not restate the whole report.

## Validation plan (human next steps)

Research can't replace real-world testing. The report's final section must give the user an actionable validation plan they execute themselves:

- Landing page smoke test: suggested headline + CTA, and what conversion rate would count as a positive signal (~10%+ of visitors leaving an email is strong; wide traffic-source caveats apply)
- 3–5 survey/interview questions that measure behavior, not politeness (ask "how much do you currently pay / what do you currently do", never "would you use this?")
- Which specific communities (from Phase 1) to post in and what to ask

## Principles

- **Evidence over vibes.** Every material claim links to a source. If evidence is thin, say "weak signal" — don't pad.
- **Be willing to kill the idea.** The user is better served by an honest KILL than a flattering GO. Never inflate scores to be nice.
- **Contradictions are findings.** If trend data says growing but communities are silent, report the tension instead of resolving it silently.
- **Timebox.** This is a research sprint (~15–30 tool calls total), not an academic review. Depth beats breadth in the phases where signals are strongest.
