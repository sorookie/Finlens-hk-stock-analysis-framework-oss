# Ownership and Positioning Analysis Reference

## Objective

Evaluate who is holding the stock, whether positioning is becoming more supportive or more crowded, whether short pressure is building or fading, and whether buybacks or southbound demand are absorbing supply.

This module should support trading-structure interpretation, not replace fundamentals.

## Source Semantics

Do not treat every data source as measuring the same thing.

**Southbound holding trend**
* Measures Stock Connect related ownership trend
* Good for checking whether mainland ownership is rising, flat, or falling

**HKEX daily short-selling turnover**
* Measures daily short-selling flow
* Useful for checking whether short activity is elevated on a given day or over a recent window

**SFC aggregated reportable short positions**
* Measures weekly reported net short inventory at the close of the relevant reporting date
* Useful for checking whether short positioning is building, stable, or easing

**Buybacks**
* Measure corporate demand absorbing float
* Useful for checking whether management is actively supporting capital return and share count reduction

**Optional local CCASS connector**
* Can be used only when the user explicitly enables a local personal-use connector
* Useful for participant concentration and change analysis
* Do not assume it is available in the default open-source setup
* Phrase carefully as participant or custody shareholding, not final end-investor ownership

## When to Use This Module

Use this module when the user asks about:

* southbound support
* whether the stock is crowded
* whether big participants are adding or reducing
* short pressure or short squeeze risk
* whether buybacks are offsetting supply
* whether the current move looks supported by ownership and positioning

## Core Workflow

1. Check whether ownership and positioning is relevant to the stock and the question
2. Gather southbound trend when relevant
3. Gather HKEX daily short-selling turnover and ratio when relevant
4. Gather SFC weekly aggregated short positions trend when relevant
5. Gather buyback activity and pace when relevant
6. Use optional CCASS participant concentration only when the connector is enabled
7. Synthesize the signals
8. State whether positioning looks supportive, neutral, crowded, or deteriorating
9. State the main caveats clearly

## What to Gather

### Southbound

Capture:
* latest southbound holding level
* 5 day change
* 20 day change
* whether the trend is accelerating, stable, or fading

### Short-selling flow

Capture:
* daily short-selling turnover
* short-selling ratio versus total market turnover in the stock when available
* change versus recent average

Interpretation notes:
* one elevated short-selling day alone does not prove a bearish thesis
* repeated elevated short-selling activity matters more than one noisy print

### Weekly net short inventory

Capture:
* latest SFC aggregated reportable short position
* 4 week trend
* whether the position is rising, flat, or falling

Interpretation notes:
* rising weekly short inventory with weak price action is more concerning
* falling weekly short inventory with stable or strong price action can support a squeeze or de-crowding read

### Buybacks

Capture:
* latest announced buyback activity
* recent pace and consistency
* whether buyback size is meaningful versus average turnover or market cap

Interpretation notes:
* symbolic buybacks should not be treated as strong support
* repeated buybacks can matter if they are large enough to absorb meaningful supply

### Optional local CCASS connector

Capture when enabled:
* top participants by shareholding
* concentration ratio of top 5 or top 10 participants when useful
* 5 day and 20 day change for key participants
* whether concentration is rising or dispersing

## Synthesis Rules

Positioning looks **supportive** when several of these hold:
* southbound is rising
* daily short-selling pressure is not expanding materially
* weekly net short inventory is flat or falling
* buybacks are active and meaningful
* optional participant data is constructive when available

Positioning looks **neutral** when the signals are mixed or weak.

Positioning looks **crowded** when:
* one holder group dominates too much
* the trade is heavily one sided
* valuation is already stretched and the stock is heavily consensus owned

Positioning looks **deteriorating** when several of these hold:
* southbound is falling
* daily short-selling flow is elevated repeatedly
* weekly net short inventory is rising
* buybacks are absent or too small to matter
* optional participant data is weakening when available

## Output Template

When writing an ownership and positioning section, cover:

* southbound trend
* short-selling flow
* weekly reported short inventory trend
* buyback support
* optional participant concentration and notable recent change when available
* one paragraph conclusion on whether positioning is supportive, neutral, crowded, or deteriorating
* caveats on data semantics

## Caveats

1. Daily short-selling turnover is a flow measure, not a stock measure.
2. Weekly aggregated short positions are lower frequency and should not be overfit.
3. Optional CCASS participant holdings are not the same as final beneficial ownership.
4. Ownership and positioning should refine the thesis, not replace business and valuation work.
