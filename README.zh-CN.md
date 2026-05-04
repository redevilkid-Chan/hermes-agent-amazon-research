# Hermes Agent — 亚马逊智能选品与市场战略分析系统

[English](./README.md) · [中文文档](./README.zh-CN.md)

> AI 驱动的亚马逊全链路选品研究系统。  
> 基于 **Hermes Agent** + **DeepSeek V4 Pro** + **MiniMax**。  
> 14 个自建 Skill | 多 Agent 协作 | BCG 矩阵 | DeckOS 专业演示

---

## 🎯 这是什么

一套全自动、多 Agent 协作的亚马逊市场调研流水线。系统自动接入品类原始数据（Jungle Scout / Helium 10），执行竞品分析、生成 BCG 矩阵，并产出数据驱动的市场战略建议——全程由 Hermes Agent 编排调度。

### 解决的核心问题

亚马逊卖家面对海量品类数据，但缺乏系统化的多维度分析框架，决策依赖直觉而非数据。本系统将"数据→分析→策略→演示"全链路自动化，把单品类调研从 3 天压缩到 2 小时。

---

## 🧠 多 Agent 协作架构

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│ 数据摄入 │ → │ BCG矩阵  │ → │ 战略生成 │ → │ DeckOS   │
│  Agent   │    │  Agent   │    │  Agent   │    │ 报告Agent│
└──────────┘    └──────────┘    └──────────┘    └──────────┘
 Jungle Scout    明星/金牛       五维度决策       Dark/Noir/SaaS
 Helium 10       问题/瘦狗       Devil's Advocate 42页专业投影片
 3年历史数据     P25/P50/P75    批判性验证        自动质量评分
```

### 四个 Agent 分工

| # | Agent | 功能 |
|---|-------|------|
| ① | **数据摄入 Agent** | 拉取 3 年销量/价格/评价数据，竞品标签交叉验证 |
| ② | **BCG 矩阵分析 Agent** | 13+ 竞品四象限分类，输出分位值而非均值 |
| ③ | **战略生成 Agent** | 五维度决策矩阵 → 市场进入策略（如「肌酸人格矩阵」） |
| ④ | **DeckOS 报告 Agent** | 自动生成多风格 HTML 演示（深色/极暗/SaaS 三种风格） |

所有 Agent 由 **Hermes** 统一编排，支持并行子任务分发。

---

## 📊 实际产出

| 指标 | 数值 |
|------|------|
| 已分析品类 | 3 个（皮质醇、肌酸、镁） |
| 每品类竞品数 | 13+ |
| 专业演示文档 | 10+ 份（每种 3 风格） |
| 自建 Skill | 14 个 |
| 日均输出 Token | 30-60 万 |
| 日均 API 请求 | 500-900 次 |
| 效率提升 | 3 天 → 2 小时（36 倍） |

---

## 🛠 自建 Skill 体系

14 个专项 Skill 覆盖完整工作流：

| Skill | 领域 |
|-------|------|
| `amazon-product-research` | 亚马逊选品全链路分析 |
| `douyin-video-analysis` | 抖音视频内容提取与分析 |
| `deckos` / `deckos-deck-generation` | HTML 幻灯片生成 |
| `hermes-guardian` / `hermes-autopilot` | 自主健康监控与服务管理 |
| `web-design-engineer` | 高质量 Web 界面构建 |
| `noir-style` | 极暗风格 HTML 视觉 |
| `session-recovery` | 跨会话上下文重建 |
| `hermes-git-backup` | Agent 配置版本控制 |
| `openwrt-luci-automation` | 软路由自动化配置 |
| `apple-notes` / `apple-reminders` / `imessage` / `findmy` | macOS 原生集成 |

详见 [/skills/](./skills/)

---

## 💰 API 消费证明

DeepSeek API 8 天账单数据（2026.4.27 – 5.4）：

- **总消费：** ¥104.64 CNY
- **日均：** ¥13.08
- **输出 Token：** 278 万（日均 35 万）
- **缓存命中：** 4.58 亿（高效复用上下文）
- **总请求：** 4,820 次（日均 602 次）
- **峰值日：** 5 月 2 日（¥17.91、62.6 万输出、884 请求）

👉 [查看交互式账单面板](https://redevilkid-chan.github.io/hermes-agent-amazon-research/billing-summary.html)

---

## 📁 仓库结构

```
hermes-agent-amazon-research/
├── README.md              ← 英文版（当前）
├── README_CN.md           ← 中文版（你在这里）
├── index.html             ← GitHub Pages 双语着陆页
├── billing-summary.html   ← DeepSeek 消费可视化
├── workflow.md            ← 详细多 Agent 工作流
├── reports/               ← 精选 BCG/战略报告
├── decks/                 ← DeckOS HTML 演示
├── skills/                ← Skill 目录
└── docs/                  ← 补充文档
```

---

## 🚀 在线演示

通过 GitHub Pages 部署：
- **双语首页：** [index.html](https://redevilkid-chan.github.io/hermes-agent-amazon-research/)
- **消费面板：** [billing-summary.html](https://redevilkid-chan.github.io/hermes-agent-amazon-research/billing-summary.html)
- **DeckOS 报告：** [/decks/](https://redevilkid-chan.github.io/hermes-agent-amazon-research/decks/)

---

*由 Hermes Agent 与 DeepSeek V4 Pro 驱动构建。小米 MiMo Orbit 百万亿 Token 创造者激励计划申请材料。*
