# Scoring Rubric & Verdict Rules

Six dimensions, each scored 0–10 using the anchors below. Score from evidence gathered in the phases — cite which findings justify each score in the report's scorecard table.

## Dimensions & anchors

### 1. Pain Intensity (weight 25%)

How badly do people want this solved?

- **0–2:** Nobody is talking about the problem anywhere. Or it's a mild inconvenience people shrug at.
- **3–4:** Occasional mentions; low engagement; workarounds are "fine".
- **5–6:** Regular complaints in multiple communities; people actively ask for solutions.
- **7–8:** Frequent, emotional complaints; high-engagement threads; people describe hacky workarounds they've built.
- **9–10:** People are begging for a solution, already paying for bad ones, or building their own.

### 2. Demand Trend (weight 15%)

Is interest growing?

- **0–2:** Clearly declining niche; dying platform/technology.
- **3–4:** Flat or slowly eroding.
- **5–6:** Stable with steady content/search activity.
- **7–8:** Visibly growing; rising trend data or surging content volume.
- **9–10:** Explosive growth; new niche breaking into mainstream.

### 3. Competition Gap (weight 20%)

Is there room to be meaningfully better/different?

- **0–2:** Dominant incumbents with happy users and free tiers; no complaints to exploit.
- **3–4:** Crowded; complaints exist but are minor polish issues.
- **5–6:** Several players, each with real weaknesses (pricing, missing features, bad UX) you could attack.
- **7–8:** Existing solutions widely disliked, abandoned, or missing an obvious segment.
- **9–10:** Clear unmet need; users cobbling together spreadsheets/scripts; or no direct competitor despite proven pain. (Careful: no competitors + no pain = no market, which is Pain Intensity's job to catch.)

### 4. Monetization (weight 15%)

Will anyone pay, and how much?

- **0–2:** Audience expects free; ad-only economics; race-to-zero pricing.
- **3–4:** Weak willingness to pay; heavy free alternatives.
- **5–6:** Established paid products exist at modest price points.
- **7–8:** Users demonstrably pay recurring prices; complaints about competitor pricing (proof they pay).
- **9–10:** B2B budgets or prosumers paying premium prices; pricing power evident.

### 5. Market Size (weight 10%)

From the TAM/SAM/SOM estimate.

- **0–2:** SOM too small to matter even if fully captured.
- **3–4:** Lifestyle-business ceiling at best, with difficulty reaching even that.
- **5–6:** Comfortable indie/small-team business potential (SOM supports meaningful revenue).
- **7–8:** Large SAM; venture-scale possible.
- **9–10:** Massive, well-documented market with published sizing.

Note: for an indie hacker, 5–6 here is _good_. Score the market honestly; interpret in the verdict relative to the user's ambitions if known.

### 6. Distribution (weight 15%)

Can you actually reach users?

- **0–2:** No discoverable channel; SEO owned by giants; communities ban promotion; paid ads uneconomical.
- **3–4:** Channels exist but expensive or saturated.
- **5–6:** At least one plausible organic channel (SEO niche keywords, active communities, app store discovery).
- **7–8:** Multiple viable channels; communities hungry for solutions; low keyword competition.
- **9–10:** Built-in virality or an underserved channel you can own.

## Computing the total

Weighted total = PainIntensity×0.25 + DemandTrend×0.15 + CompetitionGap×0.20 + Monetization×0.15 + MarketSize×0.10 + Distribution×0.15

Result is 0–10. Round to one decimal.

## Verdict mapping

- **GO** — total ≥ 7.0 and no dimension below 4
- **PIVOT** — total 4.5–6.9, or total ≥ 7.0 with a dimension below 4. The report must name what to pivot: audience, feature focus, pricing, or channel.
- **KILL** — total < 4.5

## Override rules (apply regardless of total)

1. **Pain Intensity ≤ 2 → KILL.** No pain, no product. Full stop.
2. **Distribution ≤ 2 → cap at PIVOT.** A product nobody can find can't win; the pivot must address reach.
3. **Monetization ≤ 2 AND the user intends a paid product → cap at PIVOT** toward a different business model.
4. **Evidence quality caveat:** if fewer than ~8 solid sources were found overall, add an explicit "low-confidence" flag to the verdict and recommend the human validation steps before any build effort.

## Honesty requirements

- Never nudge scores upward to be encouraging. A wrong GO costs the user months of wasted build time; a wrong KILL costs a re-check.
- If two anchors both seem plausible, take the lower one and note the uncertainty.
- The verdict paragraph must include the strongest argument AGAINST the verdict (steelman the other side in 1–2 sentences).
