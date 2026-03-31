# Finlens HK Stock Analysis OSS

Open-source framework for structured Hong Kong stock and ETF analysis.

Finlens HK Stock Analysis OSS is a provider-aware research skill for analyzing Hong Kong listed equities and ETFs. It supports fundamentals, valuation, technicals, ownership and positioning, stock comparison, and full report generation.

This open-source version does not assume any private broker or local connector is available. If the user has configured a market-data provider such as Longbridge, Futu, or IBKR, the workflow can use it first. Otherwise, it falls back to official disclosures, reputable public market-data sources, and web search with explicit freshness labeling.

## Table of contents

- [Why this exists](#why-this-exists)
- [What this skill does](#what-this-skill-does)
- [Typical use cases](#typical-use-cases)
- [How Finlens thinks about data](#how-finlens-thinks-about-data)
- [Data routing logic](#data-routing-logic)
- [Analysis modes](#analysis-modes)
- [Quick start](#quick-start)
- [Configuration](#configuration)
- [Example requests](#example-requests)
- [Output style](#output-style)
- [Repository structure](#repository-structure)
- [Limitations](#limitations)

## Why this exists

Most stock-analysis prompts collapse everything into one bucket and mix stale price data, company filings, chart commentary, market rumors, and positioning interpretation into a single answer.

Finlens is built to avoid that.

It separates:

- market data from filings
- ownership flow from net short inventory
- facts from interpretation
- quick answers from full research notes
- provider-backed data from public fallback data

The goal is not to generate generic stock opinions. The goal is to produce structured, source-aware, time-aware Hong Kong stock analysis.

## What this skill does

This skill is designed for Hong Kong stock research with a structured, repeatable workflow.

It can be used for:

- basic stock snapshots
- fundamental analysis
- valuation analysis
- ownership and positioning analysis
- technical analysis
- stock versus stock comparison
- full investment report generation

By default, the scope stays on the Hong Kong listed security itself unless the user explicitly asks for cross-market mapping.

## Typical use cases

Use this framework when you want to answer questions such as:

- What does this Hong Kong stock do, and what is driving it now?
- Is the business high quality?
- Is the valuation cheap, fair, or stretched?
- Is the dividend actually sustainable?
- Are buybacks meaningful or symbolic?
- Is southbound flow supportive?
- Is short pressure building or fading?
- Does the chart setup still look constructive?
- Which stock looks more attractive between two Hong Kong names?
- Can I generate a full structured investment note instead of a quick opinion?

## How Finlens thinks about data

Finlens separates facts from interpretation.

Facts include:

- reported financials
- filing language
- dated corporate events
- current or delayed market data
- official ownership and short-position disclosures

Interpretation includes:

- business quality judgment
- valuation framing
- ownership and positioning read
- technical setup read
- investment thesis strength

The framework also enforces time-context discipline:

- label whether data is live, delayed, end of day, or last available
- label whether metrics are annual, interim, quarterly, TTM, forward, or historical
- avoid mixing mismatched periods in the same conclusion

## Data routing logic

Finlens uses different source priorities for different kinds of data.

### 1. Market data and technical inputs

Preferred order:

- configured market-data provider, if available
- reputable public market-data source
- web search with freshness labeling

Use this for:

- current or last available price
- daily change
- turnover and volume
- 52-week range
- recent performance
- K-line based technical analysis
- moving averages, RSI, MACD
- support and resistance

### 2. Company fundamentals and corporate events

Preferred sources:

- HKEX filings and announcements
- annual reports
- interim reports
- earnings releases
- circulars
- investor relations materials
- official company presentations and commentary

### 3. Ownership and positioning

Preferred sources:

- Stock Connect and southbound statistics
- HKEX daily short-selling turnover
- SFC aggregated reportable short positions
- buyback disclosures
- dividend schedules
- optional local CCASS connector only when the user explicitly enables it

### 4. Market framing and recent context

High-quality public finance media and research summaries can be used for recent context, but they should not be the sole basis for core numbers when primary sources are available.

## Analysis modes

### 1. Basic Snapshot

Best for a quick read.

Typical output:

- what the company does
- current or last available price context
- 5 to 8 key metrics
- one paragraph on what is driving the stock
- one sentence on dividend, buyback, southbound, or short context when relevant

### 2. Fundamental Analysis

Best for:

- business quality
- financial health
- dividend support
- buyback quality
- valuation framing

Typical workflow:

- understand the business
- assess moat and competitive position
- review 3 to 5 years of financial trend data when available
- assess profitability, growth, balance sheet, and cash flow quality
- assess shareholder return quality
- compare against peers and history
- build a balanced bull case and bear case

### 3. Ownership and Positioning Analysis

Best for:

- southbound support
- short interest and short pressure
- crowding
- buyback absorption
- optional CCASS participant concentration

Typical output:

- southbound trend
- daily short-selling flow
- weekly reported short inventory trend
- buyback support
- optional participant concentration when enabled
- conclusion on whether positioning looks supportive, neutral, crowded, or deteriorating
- caveats on data semantics

### 4. Technical Analysis

Best for:

- chart structure
- support and resistance
- trading setup
- short-term or medium-term technical context

Typical output:

- trend direction
- price versus moving averages
- RSI and MACD summary
- volume behavior
- support and resistance zones
- chart pattern if clearly present
- short-term view
- medium-term view
- invalidation level
- liquidity warning when chart reliability is weak

### 5. Full Investment Report

Best for users who want a complete research note.

Typical sections include:

- executive summary
- company overview
- investment thesis
- fundamental analysis
- valuation analysis
- ownership and positioning
- technical analysis when useful
- risks
- catalysts and monitoring timeline
- recommendation
- conclusion

### 6. Comparison Analysis

Best for comparing two or more Hong Kong stocks on a like-for-like basis.

Typical output compares:

- business model
- growth
- margins
- cash flow
- balance sheet
- valuation
- dividend and buyback support
- ownership and positioning
- technical posture
- overall relative attractiveness

## Quick start

### 1. Create the skill folder

```bash
mkdir -p .agents/skills/finlens-oss/references
```

### 2. Copy the main files

```bash
cp SKILL.md .agents/skills/finlens-oss/SKILL.md
cp AGENTS.md .
cp -R references .agents/skills/finlens-oss/
```

### 3. Verify the structure

Your project should look like this:

```text
.
├── AGENTS.md
└── .agents
    └── skills
        └── finlens-oss
            ├── SKILL.md
            └── references
                ├── ccass-query-guide.md
                ├── financial-metrics.md
                ├── fundamental-analysis.md
                ├── ownership-positioning.md
                ├── report-template.md
                └── technical-analysis.md
```

## Configuration

This OSS package is designed to work even when no private provider is configured.

### If a provider is available

If the user has configured a broker or market-data provider such as:

- Longbridge
- Futu
- IBKR

the workflow should use that provider first for current market fields and technical raw data.

### If no provider is available

The workflow should fall back to:

- official disclosures
- exchange data
- reputable public market-data sources
- web search with explicit freshness labeling

### Freshness rule

Do not present stale quote data as if it were fully current.

Always label market data as one of:

- live
- delayed
- end of day
- last available

## Optional CCASS support

Local CCASS-style participant concentration analysis is optional.

This OSS package does not assume a local CCASS connector is available by default.

If a personal-use connector is enabled, it can be used for participant concentration and change analysis. If not, the framework should still work normally without it.

Also note that participant or custody shareholding is not the same as final beneficial ownership.

## Example requests

These are the kinds of prompts this skill is built to handle.

### Basic snapshot

- Analyze 0700 quickly
- Give me a quick snapshot of Tencent
- 0005 现在大概是什么情况，先简版

### Fundamental analysis

- Analyze 0941 from a fundamental and valuation perspective
- Is 0005’s dividend actually sustainable?
- 看一下 0388 的业务质量、现金流和估值

### Ownership and positioning

- Analyze southbound support and short pressure in 0700
- Is 9988 getting crowded?
- 看一下 3690 的南向、卖空、回购和筹码结构

### Technical analysis

- Give me the technical setup for 1211
- What are the key support and resistance levels for 2800?
- 从技术面看 0941 现在这个位置怎么样

### Comparison analysis

- Compare 0700 and 9988
- Which looks more attractive now, 0005 or 3988?
- 比较一下 0388 和 2628，谁更值得看

### Full report

- Write a full investment report on 0005
- Generate a full research note for 2800
- 给我一份完整的 0700 投资分析报告

### Short answer control

- Give me a quick snapshot first
- Keep it concise
- 先不要展开太多
- Start with the conclusion, then go into detail

## Output style

Finlens is built to respond in a research-first format.

General output rules:

- start with the direct answer when the user asks a narrow question
- be concise first, then detailed
- use tables for metric-heavy sections
- keep units and currencies consistent
- state the period for important numbers
- separate market data from filings and ownership data
- acknowledge uncertainty and missing data
- explain whether the conclusion comes from fundamentals, valuation, positioning, technicals, or recent context

## Repository structure

```text
.
├── README.md
├── AGENTS.md
├── SKILL.md
└── references
    ├── financial-metrics.md
    ├── fundamental-analysis.md
    ├── ownership-positioning.md
    ├── report-template.md
    └── technical-analysis.md
```

### File guide

- `README.md`
  Project overview, installation, usage, and examples.

- `SKILL.md`
  The main open-source stock analysis skill. Defines scope, routing expectations, analysis modes, and output rules.

- `AGENTS.md`
  Repository-level routing rules. Defines provider priority, execution order, and source discipline.

- `references/fundamental-analysis.md`
  Framework for business quality, financial health, valuation framing, shareholder return quality, risks, and red flags.

- `references/financial-metrics.md`
  Metric definitions and interpretation rules.

- `references/ownership-positioning.md`
  Framework for southbound, short-selling flow, weekly short inventory, buybacks, and optional CCASS-style analysis.

- `references/technical-analysis.md`
  Framework for trend, momentum, support and resistance, volume confirmation, and invalidation logic.

- `references/report-template.md`
  Template for full stock reports and comparison reports.

## Limitations

This framework is strong on structure and workflow discipline, but it still depends on source availability and data freshness.

Please keep these limits in mind:

- it does not guarantee live data unless a configured provider supports it
- it should not treat all ownership datasets as measuring the same thing
- it should not overfit short-term flow data
- it should not replace primary filings with secondary summaries
- it should not assume private connectors exist in the OSS version
- it should not give false precision on fair value or target price

## Philosophy

Finlens is not built to generate generic stock opinions.

It is built to produce structured, source-aware, time-aware Hong Kong stock analysis that separates facts from interpretation and keeps ownership, positioning, valuation, and technical context in the right place.

## Notes

- Private connectors are optional.
- Ownership and positioning should refine the thesis, not replace fundamentals.
- Always label freshness clearly for non-live market data.
