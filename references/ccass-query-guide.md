# CCASS Participant Shareholding Query Guide

## Overview

CCASS (Central Clearing and Settlement System) participant shareholding data shows which brokers/custodians hold shares for a Hong Kong listed stock. This is useful for:

- Identifying broker concentration
- Detecting positioning changes
- Understanding who controls the float

## Data Availability

| Source | Status | Notes |
|:---|:---:|:---|
| Longbridge CLI | ❌ Not supported | No CCASS command available |
| HKEX CCASS Website | ✅ Available | Requires manual query |
| MX API | ❌ Not available | No CCASS endpoint |
| Tier 1 Financial Sites | ❌ Limited | Most don't provide CCASS data |

## Manual Query Steps (HKEX Official)

### Step 1: Access HKEX CCASS Search

**URL**: https://www3.hkexnews.hk/sdw/search/searchsdw.aspx

### Step 2: Enter Query Parameters

1. **Shareholding Date**: Select the date you want to query (default: most recent trading day)
2. **Stock Code**: Enter the 5-digit stock code (e.g., `02228` for 晶泰控股)
3. **Sort By**: Select `Shareholding` to sort by holding size (descending)
4. Click **Search**

### Step 3: Interpret Results

The results table shows:

| Column | Meaning |
|:---|:---|
| Participant ID | CCASS participant identifier |
| Participant Name | Broker/Custodian name |
| Shareholding | Number of shares held |
| % of total | Percentage of total shares |
| 1-day change | Net change from previous day |
| 30-day change | Net change from 30 days ago |

### Step 4: Key Metrics to Extract

For analysis, gather:

1. **Top 10 participants** — Who controls the most shares?
2. **Concentration ratio** — Top 3 / Top 5 / Top 10 holding percentage
3. **30-day trend** — Are major participants accumulating or distributing?
4. **Unusual changes** — Any participant with >1% daily change?

## Example: How to Report CCASS Data

When providing CCASS data to the agent for analysis, use this format:

```
Date: 2026-03-30
Stock: 晶泰控股 (02228.HK)

Top 10 CCASS Participants:
| Rank | Participant | Holding | % | 30d Chg |
|:---:|:---|---:|---:|---:|
| 1 | HSBC | 500M | 12.5% | +0.5% |
| 2 | CCASS - Stock Connect | 450M | 11.2% | +1.2% |
| ... | ... | ... | ... | ... |

Top 3 concentration: 35.2%
Top 5 concentration: 48.6%
Top 10 concentration: 62.1%
```

## Tips for Analysis

### Concentration Thresholds

| Top 10 Concentration | Interpretation |
|:---:|:---|
| < 40% | Dispersed, many small holders |
| 40% - 60% | Moderate concentration |
| 60% - 80% | High concentration, potential volatility |
| > 80% | Very concentrated, high positioning risk |

### Red Flags

- Single participant holds >20%
- Rapid accumulation (>2% in 30 days) by single participant
- Sudden exit by major participant
- Stock Connect (CCASS - Stock Connect) rapidly increasing = Southbound accumulating

### Bullish Signals

- Major participants gradually accumulating
- Stock Connect share increasing steadily
- Low concentration = less manipulation risk

### Bearish Signals

- Major participants distributing
- Sudden large transfers between participants
- Stock Connect share declining = Southbound exiting

## Limitations

1. **Data lag**: CCASS data is T+1 (next day after trade)
2. **No short positions**: CCASS only shows long holdings
3. **Beneficial owners hidden**: Shares held in street name, actual owners unknown
4. **Manual query required**: No automated API available

## Alternative Sources

If you have access to:

- **Bloomberg Terminal**: `HDS <GO>` function
- **Reuters**: CCASS data available
- **Wind (万得)**: CCASS data for mainland users
- **Choice (东方财富Choice)**: CCASS data for institutional clients

These platforms provide automated CCASS data access.
