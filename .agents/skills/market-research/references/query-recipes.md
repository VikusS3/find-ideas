# Search Query Recipes

Concrete, reusable query patterns per phase. Replace `[niche]` / `[problem]` / `[competitor]` with the idea's terms. Adapt phrasing; these are starting points, not scripts. Keep queries short (2–6 words work best for web search engines; the quoted-phrase patterns work better in Tavily/Firecrawl which pass queries through more literally).

## Phase 1: Pain point discovery

Reddit / community complaints:

- `[niche] reddit "is there an app"`
- `[niche] reddit "I hate"`
- `[niche] reddit alternative`
- `[problem] "how do I" reddit`
- `[niche] "am I the only one" `
- `site-style variants if the tool supports it: [problem] site:reddit.com` (only if the search tool tolerates operators — built-in web_search does not; skip operators there)

Quora / Q&A:

- `[problem] quora`
- `"I wish there was" [niche]`

B2B pain:

- `[problem] "struggling with" linkedin`
- `[niche] workflow frustrating`

Hacker News (good for dev/prosumer tools):

- `[niche] hacker news`
- `[competitor] hn thread`

What to record per hit: quote (short), URL, engagement (upvotes/replies), date. 5–10 strong data points beats 30 weak ones.

## Phase 2: Demand quantification

- `[niche] google trends 2025` / `[niche] search volume`
- `[core keyword] keyword volume monthly`
- `[niche] market growing 2026`
- `how to [solve problem]` — check how much recent content exists; a steady stream of new articles/videos = active demand
- `[niche] statistics 2025 2026`

Signals to extract: trend direction (rising/flat/declining), any concrete monthly-search numbers, volume of recent content.

## Phase 3: Competitor & gap analysis

Finding competitors:

- `best [niche] apps 2026`
- `[niche] app comparison`
- `[idea description] product hunt`
- `[niche] software g2` (B2B)
- `[niche] open source github` (dev tools)

Mining complaints (the goldmine — prioritize this):

- `[competitor] app store reviews 1 star`
- `[competitor] reddit complaints`
- `[competitor] alternative` — the reasons people search for alternatives ARE the gaps
- `[competitor] vs` — comparison articles list weaknesses
- `[competitor] g2 cons` (B2B)
- Fetch the competitor's pricing page directly with web_fetch/firecrawl_scrape

What to record per competitor: name, one-line description, pricing model + price points, top 2–3 complaints with sources.

## Phase 4: Market data & monetization

- `[industry] market size 2026`
- `[industry] market report CAGR`
- `[niche] startup funding raised`
- `[competitor] crunchbase funding`
- `[niche] app revenue` / `[competitor] revenue estimate`
- `"I would pay for" [niche]`
- `[niche] pricing survey`

## Phase 6: Distribution check

- `[core keyword]` — plain search; note who owns the first page (giants vs blogs vs forums = SEO difficulty)
- `[niche] subreddit` — find communities; check subscriber counts and whether self-promo is allowed (check rules via fetch if pivotal)
- `[niche] app store keywords competition`
- `[niche] newsletter` / `[niche] youtube channel` — existing audience channels you could reach
- `[niche] facebook group` / `[niche] discord`

## General tips

- Start broad, then narrow. First query per phase should be the most generic version.
- If a query returns nothing useful, reword once, then move on — don't burn the budget re-querying.
- Prefer fetching one rich page (a good comparison article, a review roundup, a pricing page) over five more shallow searches.
- Date-check everything. A 2021 complaint thread about a competitor may be fixed by now; flag stale evidence.
