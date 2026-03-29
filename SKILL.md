---
name: Finlens-hk-stock-analysis-oss
description: Analyze Hong Kong listed stocks and ETFs with a structured research workflow for fundamentals, valuation, technicals, ownership, and positioning. Use this skill when the task is to interpret a Hong Kong stock, compare names, or generate a full research note. In this open-source version, use a configured market-data provider first when available. If no private connector is configured, fall back to official disclosures, reputable public market-data sources, and web search with explicit freshness labeling. Do not assume Longbridge, Futu, or IBKR is available.
---

# Finlens HK Stock Analysis OSS

## Scope

This open-source skill is for general Hong Kong stock research with provider aware routing.
It covers:

* basic stock snapshots
* fundamental analysis
* valuation analysis
* ownership and positioning analysis
* technical analysis
* side by side stock comparison
* full investment report generation

Keep the scope on the Hong Kong listed stock itself unless the user explicitly asks for cross market mapping.

## Language Handling

* The skill body is written in English for portability.
* The user's input language should control the response language.
* If the user asks in Chinese, answer in Chinese by default.
* If the user asks in English, answer in English by default.
* Mixed requests such as Chinese plus stock code, company name, valuation, dividend, buyback, southbound, technical, short interest, or CCASS are normal and should still trigger this skill.

## Core Working Style

Use a research first approach:

1. **Classify the request first**
   * Basic snapshot
   * Fundamental analysis
   * Ownership and positioning analysis
   * Technical analysis
   * Comparison analysis
   * Full report

2. **Resolve the best available provider first**
   * configured market-data provider if available
   * official disclosures and exchange data
   * reputable public market-data and finance sources
   * web search for recent context when needed

3. **Separate facts from interpretation**
   * Facts = reported numbers, filing language, current or delayed market data, dated events
   * Interpretation = business quality judgment, valuation framing, positioning read, technical read, thesis strength

4. **Be explicit about time context**
   * State the data period being used
   * State whether metrics are TTM, quarterly, interim, annual, forward, or historical average
   * State whether market data is live, delayed, end of day, or last available
   * Avoid mixing mismatched periods in the same conclusion

5. **Keep the answer balanced**
   * Present both the bull case and bear case
   * Identify what must go right for the thesis to work
   * Identify what could break the thesis

## Source Policy by Data Type

Use the right source for the right data type.
Do not use one source hierarchy for everything.

### 1. Market data and technical raw data
Preferred order:

* configured broker or market-data connector such as Longbridge, Futu, or IBKR when the user has set one up
* reputable public market-data API or finance portal
* web search with freshness labeling as a fallback

Use this layer for:

* current or last available price
* daily change
* turnover and volume
* recent 5 day and 20 day performance
* 52 week range when available
* intraday context when the provider supports it
* K-line based technical analysis
* moving averages, RSI, MACD input data
* support and resistance derived from recent price action

### 2. Company filings and corporate actions
Prefer primary sources:

* HKEX filings and announcements
* annual reports, interim reports, earnings releases, circulars, and shareholder announcements
* official investor relations pages
* company presentations, management commentary, and webcast materials

### 3. Ownership and positioning data
Prefer official and disclosed sources:

* southbound and Stock Connect statistics
* HKEX daily short-selling turnover
* SFC aggregated reportable short positions
* buyback disclosures and dividend schedules
* optional local CCASS connector only when the user enables it for personal use

### 4. Financial context and consensus framing
Use high quality financial media and research summaries only for recent developments, market framing, and context.
Do not use them as the sole basis for core financial numbers when primary sources are available.

If multiple sources disagree, state that clearly and prefer the most primary and most recent source for that data type.

## Freshness Contract

For any Hong Kong stock request involving current market context, resolve the best available market-data provider before analysis.

If a configured provider is available, use it first for:

* current price
* daily change
* turnover and volume
* 52 week range
* recent 5 day or 20 day performance
* daily or weekly K-line data
* moving averages, RSI, MACD, support and resistance
* intraday context

If no configured provider is available:

1. use a reputable public source or web search
2. label the freshness clearly
3. state whether the data is live, delayed, end of day, or last available
4. do not present stale quote data as fully current

## Data to Gather

### Always gather what is needed for the specific request

**Basic market data**
* current or last available price
* daily change
* market cap
* turnover and average turnover when available
* 52 week range
* recent performance when relevant
* trading currency
* board lot size when relevant to trading context
* freshness label

**Financial data**
* revenue
* gross profit
* operating profit
* net profit
* EPS
* operating cash flow
* free cash flow
* cash and debt
* margins
* return metrics when available

**Valuation data**
* trailing P/E
* forward P/E when available
* PEG when relevant
* P/B when relevant
* P/S when relevant
* EV/EBITDA when relevant
* EV/Sales when relevant
* dividend yield
* FCF yield when relevant
* valuation versus history and peers

**Ownership and positioning data**
* southbound holding trend
* daily short-selling turnover
* short-selling ratio versus total turnover when available
* weekly aggregated reportable short positions
* buyback pace and absorption
* positioning crowding or easing signals
* optional CCASS participant concentration and recent change only when a local connector is enabled

**Business and thesis data**
* business segments
* core growth drivers
* competitive positioning
* management commentary
* recent catalysts and risks
* listing structure when relevant, such as red chip, H share, dual primary listing, or spin-off context

**Technical data**
* trend direction
* price versus key moving averages
* RSI
* MACD
* volume pattern
* support and resistance
* notable chart patterns when visible
* freshness label for the market-data input

## Analysis Modes

### 1. Basic Snapshot

Use when the user wants a quick read.

Deliver:

* what the company does
* current or last available price context
* 5 to 8 key metrics
* one paragraph on what is currently driving the name
* one sentence on dividend, buyback, southbound, or short context when relevant

### 2. Fundamental Analysis

Use when the user wants business quality, financial health, dividend support, or valuation work.

Workflow:

1. Read `references/fundamental-analysis.md`
2. Read `references/financial-metrics.md`
3. Read `references/ownership-positioning.md` when flow or positioning matters
4. Gather 3 to 5 years of financial trend data when available
5. Assess business quality
6. Assess financial health
7. Assess growth quality and cash flow quality
8. Assess shareholder return quality, including dividends and buybacks when relevant
9. Compare valuation versus peers and history
10. Identify red flags and key risks
11. Generate a balanced conclusion

### 3. Ownership and Positioning Analysis

Use when the user asks about:

* southbound
* CCASS
* participant concentration
* short interest or short positioning
* whether the stock is crowded
* whether buybacks are absorbing supply

Workflow:

1. Read `references/ownership-positioning.md`
2. Gather the relevant ownership and positioning data
3. Distinguish between custody data, flow data, and net short inventory
4. Summarize whether positioning looks supportive, neutral, crowded, or deteriorating
5. State the main caveats clearly

### 4. Technical Analysis

Use when the user asks for technical setup, chart structure, trading view, or support resistance.

Workflow:

1. Read `references/technical-analysis.md`
2. Establish the primary trend first
3. Identify key support and resistance levels
4. Check moving averages, RSI, MACD, and volume
5. Note liquidity conditions and whether board lot or low turnover may distort the chart
6. Identify whether a pattern is actually present or only tentative
7. State the levels that would confirm or invalidate the setup
8. Provide short term and medium term technical outlook

### 5. Full Investment Report

Use when the user wants a complete stock writeup or recommendation.

Workflow:

1. Run the fundamental workflow
2. Run the ownership and positioning workflow when relevant
3. Run the technical workflow if useful or explicitly requested
4. Read `references/report-template.md`
5. Synthesize the findings into a single report
6. Provide a rating view such as Buy, Hold, Sell only when the evidence supports it
7. State the valuation basis for any target price or fair value range

### 6. Comparison Analysis

Use when the user asks to compare two or more Hong Kong stocks.

Workflow:

1. Gather the same categories of data for each name using comparable periods
2. Read `references/fundamental-analysis.md`
3. Read `references/financial-metrics.md`
4. Read `references/ownership-positioning.md` when flow or positioning matters
5. Read `references/report-template.md` comparison section when a full comparison report is needed
6. Compare business model, growth, margins, cash flow, balance sheet, valuation, ownership, positioning, dividend and buyback support, and technical posture
7. Conclude on relative attractiveness and why

## Output Rules

### General

* be concise first, then detailed
* start with the direct answer when the user asks a narrow question
* use tables for metric heavy sections
* keep units consistent
* label all time periods clearly
* quantify claims where possible
* cite or name the source basis for important numbers
* acknowledge uncertainty and missing data
* state whether figures are in HKD, RMB, USD, or another currency when relevant
* label live, delayed, end of day, or last available market data clearly

### Reasoning Discipline

When making a judgment, explain which of these buckets it comes from:

* reported financial evidence
* market pricing evidence
* management guidance or filings
* peer comparison
* ownership and positioning evidence
* technical structure
* shareholder return evidence
* market consensus context

### Recommendation Discipline

If providing a recommendation or target price:

* explain the basis clearly
* state the timeframe
* state major assumptions
* mention what would change the view
* avoid sounding certain when the evidence is mixed

## Reference Files

Load these files when relevant:

**references/fundamental-analysis.md**
Use for business quality, financial health, valuation framing, shareholder return review, risk review, and red flag checks.

**references/financial-metrics.md**
Use for ratio definitions, interpretation, and metric selection.

**references/technical-analysis.md**
Use for indicator interpretation, chart structure, support resistance, and technical workflow.

**references/ownership-positioning.md**
Use for southbound holding trend, daily short-selling turnover, weekly aggregated reportable short positions, buyback absorption, and positioning conclusions. Use optional CCASS participant data only when a local connector is enabled.

**references/report-template.md**
Use for full reports and comparison reports.
