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
* web search with freshness labeling

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

## Execution order for stock analysis

1. Resolve entity to the correct Hong Kong ticker
2. Resolve the best available market-data provider
3. Fetch market data and label freshness
4. Fetch filings and company materials
5. Fetch ownership and positioning data when relevant
6. Run the Finlens analysis workflow
7. In the output, label freshness and source type clearly
