# Hermes Agent — Amazon Market Research System

> AI-powered Amazon product research & market strategy analysis system.  
> Built on **Hermes Agent** + **DeepSeek V4 Pro** + **MiniMax**.  
> 14 custom Skills | Multi-Agent collaboration | BCG Matrix | DeckOS HTML reports

---

## 🎯 What This Is

A fully autonomous, multi-Agent market research pipeline for Amazon sellers. It ingests raw category data (Jungle Scout / Helium 10), runs competitive analysis, generates BCG matrices, and produces data-driven strategy recommendations — all orchestrated by Hermes Agent.

### Core Problem Solved

Amazon sellers drown in category data but lack systematic analysis frameworks. Decisions rely on intuition, not data. This system automates the entire research chain from data to strategy.

---

## 🧠 Multi-Agent Architecture

```
┌─────────────┐    ┌──────────────┐    ┌─────────────┐    ┌──────────────┐
│ Data Ingestion│ → │ BCG Matrix   │ → │ Strategy Gen │ → │ DeckOS Report│
│    Agent     │    │    Agent     │    │    Agent     │    │    Agent     │
└─────────────┘    └──────────────┘    └─────────────┘    └──────────────┘
  Jungle Scout      Stars / Cash Cows   5-Dimension        Dark / Noir / SaaS
  Helium 10         Question Marks      Decision Matrix    42-page slides
  3-year history    P25/P50/P75         Devil's Advocate   Auto QA scoring
```

### Agent Breakdown

| # | Agent | Function |
|---|-------|----------|
| ① | **Data Ingestion** | Pulls 3-year sales/price/review data, cross-validates competitor tags |
| ② | **BCG Matrix Analysis** | Classifies 13+ competitors into 4 quadrants, outputs percentile distributions |
| ③ | **Strategy Generation** | 5-dimension decision matrix → market entry strategy (e.g., "Creatine Personality Matrix") |
| ④ | **DeckOS Report** | Auto-generates multi-style HTML presentations (Dark/Noir/SaaS, 42 pages) |

All Agents orchestrated by **Hermes** with parallel sub-task distribution.

---

## 📊 Real-World Results

| Metric | Value |
|--------|-------|
| Product categories analyzed | 3 (Cortisol, Creatine, Magnesium) |
| Competitors analyzed | 13+ per category |
| Professional decks produced | 10+ (3 styles each) |
| Custom Skills built | 14 |
| Daily token consumption | 300K-600K output tokens |
| Daily API requests | 500-900 |
| Time saved per analysis | 3 days → 2 hours |

---

## 🛠 Skills Ecosystem

14 purpose-built Skills extending Hermes Agent capabilities:

| Skill | Domain |
|-------|--------|
| `amazon-product-research` | Full Amazon research pipeline |
| `douyin-video-analysis` | Douyin content extraction & analysis |
| `deckos` | HTML slide deck generation |
| `hermes-guardian` | Autonomous health monitoring + recovery |
| `hermes-autopilot` | Unified service management |
| `web-design-engineer` | High-quality web artifacts |
| `noir-style` | Dark aesthetic HTML style |
| `openwrt-luci-automation` | Router configuration automation |
| `session-recovery` | Cross-session context reconstruction |
| `hermes-git-backup` | Version control for agent config |
| `apple-notes` / `apple-reminders` / `imessage` / `findmy` | macOS integration suite |

See [/skills](./skills/) for full directory structure.

---

## 💰 API Consumption Proof

8-day DeepSeek API billing data (2026.4.27 – 5.4):

- **Total cost:** ¥104.64 CNY
- **Avg daily:** ¥13.08
- **Output tokens:** 2.78M (avg 348K/day)
- **Cache hits:** 458M (efficient context reuse)
- **Total requests:** 4,820 (avg 602/day)
- **Peak day:** May 2 (¥17.91, 626K output, 884 requests)

See [billing-summary.html](https://redevilkid-Chan.github.io/hermes-agent-amazon-research/billing-summary.html) for interactive visualization.

---

## 📁 Repository Structure

```
hermes-agent-amazon-research/
├── README.md                  ← You are here
├── billing-summary.html       ← DeepSeek usage visualization
├── workflow.md                ← Detailed multi-Agent workflow docs
├── reports/                   ← Curated BCG/strategy reports (MD)
├── decks/                     ← DeckOS HTML presentations
├── skills/                    ← Skill directory tree
└── docs/                      ← Additional documentation
```

---

## 🚀 GitHub Pages

This repo is deployed via GitHub Pages. View live:
- **Billing Dashboard:** [billing-summary.html](https://redevilkid-Chan.github.io/hermes-agent-amazon-research/billing-summary.html)
- **DeckOS Reports:** [/decks/](https://redevilkid-Chan.github.io/hermes-agent-amazon-research/decks/)

---

*Built with Hermes Agent and DeepSeek V4 Pro. Part of Xiaomi MiMo Orbit 100T Creator Incentive application.*
