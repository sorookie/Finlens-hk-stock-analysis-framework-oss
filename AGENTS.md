# Finlens OSS Routing Rules

This repository separates market-data acquisition from analysis and supports optional connectors.

## Hard routing rules

1. If the answer includes any current market fields, resolve the best available provider first.
Current market fields include:
* current price
* daily change
* turnover or volume
* 52 week range
* recent performance
* intraday context
* K-line based technical analysis
* support and resistance derived from recent price action
* moving averages, RSI, MACD

2. Provider priority:
* configured broker or market-data connector such as Longbridge, Futu, or IBKR
* reputable public market-data source
* Tier 1 web search: 新浪财经, 同花顺, 雪球, 东方财富, Yahoo Finance, Reuters, Bloomberg
* Tier 2 web search: ProSearch (online-search skill) with strict verification

3. Use `Finlens-hk-stock-analysis-oss` for analytical structure, valuation framing, thesis building, ownership and positioning work, risk analysis, and report generation.

4. Use company filings and exchange disclosures for fundamentals and corporate events.
Prefer:
* HKEX filings
* annual and interim reports
* investor relations materials
* dividend and buyback disclosures

5. Use ownership and positioning sources by function:
* Southbound = Stock Connect shareholding statistics
* Daily short flow = HKEX short-selling turnover
* Weekly short inventory = SFC aggregated reportable short positions
* CCASS participant concentration = optional local connector only when the user enables it for personal use

6. If no configured provider is available, state that clearly and label the market data as live, delayed, end of day, or last available.
Do not present stale quote data as fully current.

**Web search fallback hierarchy:**
- Tier 1: curated financial websites (sina, 10jqka, xueqiu, eastmoney, yahoo finance, reuters, bloomberg)
- Tier 2: ProSearch (online-search skill) with strict verification
- If all fail: explain to user and request data

7. Separate live market data from filings and ownership data in the final answer.
Label which numbers came from:
* configured provider data
* public market-data source
* web-sourced data (Tier 1 or Tier 2)
* filings and corporate disclosures
* ownership and positioning sources

**Data source labeling format:**
```
[Data Type]: [Value]
Source: [Source type] | [URL if web-sourced] | [Date]
Freshness: [Live/Delayed/EOD/Last available] | [Tier 1/Tier 2 if web-sourced]
```

## Execution order for stock analysis

1. Resolve entity to the correct Hong Kong ticker
2. Resolve the best available market-data provider
3. Fetch market data and label freshness (use Tier 1/Tier 2 fallback if needed)
4. Fetch filings and company materials (primary sources, with web search fallback)
5. Fetch ownership and positioning data when relevant (official sources, with web search fallback)
6. Run the Finlens analysis workflow
7. In the output, label freshness and source type clearly
