# Multi-Agent Collaboration Workflow

## Architecture Overview

The Amazon product research system follows a **4-stage linear pipeline with parallel sub-task distribution**. Each stage is an independent Agent that can spawn child agents for heavy computation.

```
                   ┌──────────────────────────┐
                   │     Hermes Orchestrator   │
                   │  (Hermes Agent + DeepSeek)│
                   └──────┬──────────┬────────┘
                          │          │
              ┌───────────┤          ├──────────┐
              ▼           ▼          ▼          ▼
        ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐
        │ Stage 1 │ │ Stage 2 │ │ Stage 3 │ │ Stage 4 │
        │  Data   │ │   BCG   │ │Strategy │ │ DeckOS  │
        │ Agent   │ │  Agent  │ │  Agent  │ │  Agent  │
        └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘
             │            │            │            │
        ┌────┴────┐  ┌────┴────┐  ┌────┴────┐  ┌────┴────┐
        │ 子Agent │  │ 子Agent │  │ 子Agent │  │ 子Agent │
        │ 并发拉取 │  │ 并发计算 │  │ 并发评分 │  │ 并发渲染 │
        └─────────┘  └─────────┘  └─────────┘  └─────────┘
```

---

## Stage 1: Data Ingestion Agent

**Model:** DeepSeek V4 Pro  
**Skills Activated:** `amazon-product-research`, `amazon-supplement-facts-extraction`, `amazon-product-scraping`

### Input
- Jungle Scout / Helium 10 CSV exports
- Amazon category ASIN lists
- Competitor tag data

### Process
1. Parse raw CSV data into structured competitor objects
2. Cross-validate competitor tags via Amazon scraping
3. Extract Supplement Facts for dietary supplement categories
4. Fetch 3-year historical review data per ASIN
5. Normalize all metrics (revenue, price, rating, review count) to common scale

### Output
- `competitors.json` — 13+ competitors with normalized metrics
- `reviews/*.xlsx` — Review detail files per ASIN
- `supplement_facts.md` — Precise nutritional data

### Parallel Strategy
Each ASIN's review data and Supplement Facts are fetched in parallel via `delegate_task()` sub-agents.

---

## Stage 2: BCG Matrix Analysis Agent

**Model:** DeepSeek V4 Pro  
**Skills Activated:** `amazon-blue-ocean-analysis`

### Input
- `competitors.json` from Stage 1
- Category metadata (market size, growth rate)

### Process
1. Calculate **market share** per competitor (revenue-based)
2. Calculate **market growth** (YoY review/revenue change)
3. Compute P25, P50, P75 percentiles for each dimension
4. Classify into 4 quadrants:
   - ⭐ **Stars:** High share + High growth
   - 🐄 **Cash Cows:** High share + Low growth
   - ❓ **Question Marks:** Low share + High growth
   - 🐕 **Dogs:** Low share + Low growth
5. Flag statistically significant outliers

### Output
- `BCG_matrix.xlsx` — Quadrant classification with metrics
- `analysis_summary.md` — Narrative analysis with P25/P50/P75 benchmarks

### Quality Gates
- Must identify ≥ 2 Stars and ≥ 2 Question Marks
- All quadrant boundaries validated against percentile distributions
- Devil's Advocate review: "What would make a Star become a Dog in 6 months?"

---

## Stage 3: Strategy Generation Agent

**Model:** DeepSeek V4 Pro  
**Skills Activated:** `amazon-product-research` (strategy mode)

### Input
- BCG matrix from Stage 2
- Category benchmark data
- Supplement Facts (if applicable)

### Process
1. **5-Dimension Decision Matrix:**

| Dimension | Weight | Sub-factors |
|-----------|--------|-------------|
| Market Attractiveness | 25% | Market size, growth rate, seasonality |
| Competitive Intensity | 25% | # of competitors, Star count, review barriers |
| Entry Feasibility | 20% | Supplier availability, regulatory, differentiation |
| Margin Potential | 20% | Price premium potential, COGS estimation |
| Synergy | 10% | Fit with existing portfolio, cross-sell potential |

2. Score each candidate product strategy (1-10 per dimension)
3. Generate **Personality Matrix** for consumer-facing categories:
   - Segment users by purchase motivation (e.g., "Athlete", "Biohacker", "Beginner", "Clinician")
   - Map each personality to SKU architecture (Base product + Enhancement packs)
4. Draft PPC cold-start budget and targeting strategy

### Output
- `strategy_recommendation.md` — Full strategy document
- `personality_matrix.html` — Visual consumer segmentation
- PPC budget allocation table

### Devil's Advocate Protocol
Every strategy must survive 3 rounds of adversarial review:
1. "This market is too competitive — why enter at all?"
2. "Your differentiation is replicable in 30 days — what's the moat?"
3. "If you had half the budget, what would you cut first?"

---

## Stage 4: DeckOS Report Agent

**Model:** DeepSeek V4 Pro  
**Skills Activated:** `deckos`, `deckos-deck-generation`, `noir-style`

### Input
- All outputs from Stages 1-3
- Style preference (Dark/Noir/SaaS)

### Process
1. Structure content into 42-page deck layout:
   - Pages 1-3: Executive summary + key findings
   - Pages 4-12: Data ingestion & methodology
   - Pages 13-22: BCG matrix visualization & analysis
   - Pages 23-30: Strategy recommendations
   - Pages 31-38: Financial projections & PPC plan
   - Pages 39-42: Appendix & data sources
2. Generate 3 style variants (Dark DeckOS, Noir, Linear SaaS)
3. Run automated QA:
   - Token color compliance check (0 non-token colors allowed)
   - Keyboard navigation (F1-F12)
   - Visual consistency score
   - Narrative progression audit
4. Save as standalone HTML files (no external dependencies)

### Output
- 3 × HTML deck files (one per style)
- `quality-report.json` — Automated QA scores

### Deployment
All decks are self-contained HTML. Deploy to GitHub Pages for instant online preview.

---

## Infrastructure

### Model Stack

| Role | Model | Purpose |
|------|-------|---------|
| Primary | DeepSeek V4 Pro | All Agent reasoning |
| Fallback | MiniMax | Automatic failover |
| Lightweight | DeepSeek V4 Flash | Simple classification tasks |

### Health Monitoring

- **Light Check:** Every 15 minutes (Gateway, Web UI, Telegram)
- **Deep Check:** Every 12 hours (full diagnostics, error log scan, port conflict detection)
- **Auto-recovery:** 4-level escalation (retry → kickstart → reboot → alert)
- **API Balance:** DeepSeek balance checked every check cycle

### Version Control

All Hermes Agent configurations, Skills, and scripts are Git-tracked at `~/.hermes/` with automatic pre/post-change commits.

---

## Performance Metrics

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Single category analysis | ~3 days | ~2 hours | 36x faster |
| Competitive reports per week | 1 | 5+ | 5x throughput |
| Data accuracy (Supplement Facts) | ~70% | ~98% | 40% fewer errors |
| Decision confidence | Intuition-based | Data-driven (P25/P50/P75) | Quantifiable |
