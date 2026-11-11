---
created: 2026-11-11
tags: [方法, AI购物, 数据集设计, 提案, methods, translation]
lang: en
source: "[[AI购物推荐数据集 采集提案]]"
---

# Collecting AI Product Recommendations — A Data-Collection Proposal

## Object and aim
We study a single behavior: a shopper asks an AI assistant to find a product and return a recommendation, and we record the prompt together with the reply. The aim is to simulate and collect this exchange daily, over six to twelve months and across several markets, so that the resulting series can later be set against sales data. Measurement sits at the API (model) layer: what we record is the recommendation the model returns.

## What we hope to observe
Our dependent variable is the recommendation share — for a fixed question (product × function × market × model), which brand the model ultimately recommends, sampled N times a day and logged. Three kinds of variation are of interest: (i) slow drift, whether a brand's share holds or migrates; (ii) entry and exit, whether a name surfaces or drops out; and (iii) event shocks, whether a brand's share steps up after it, or a retailer, announces an AI partnership or an advertising pilot. Model updates are not themselves an object of study, but they must be logged: we keep the `system_fingerprint` and snapshot so that a sudden move can be attributed to the market rather than to a model quietly swapped beneath us. Five questions follow: who is recommended and how concentrated the set is (whether a conditional monopoly forms); whether the recommendation holds, drifts, or turns over; whether it differs across markets; whether a model tilts toward its own platform's partner brands; and how far, and in which direction, recommendation share departs from actual sales.

## Fixed decisions
We query through the API only — reproducible, runnable daily, and amenable to fingerprint logging. The prompt is open-ended, supplies no product list, and is held to a single fixed wording. Four markets are in scope — Germany, France, the United Kingdom, and the United States — and the recorded outcome is the recommendation.

## Markets and language
| Market | Language |
|---|---|
| UK | en |
| US | en |
| DE | de |
| FR | fr |

Because an API call carries no end-user location, geography must be injected, through (i) the query language, (ii) the `user_location` parameter set to the market, and (iii) an in-text availability phrase, rendered natively for German and French (see the main note, §4②).

## Products and functions
Each entry pairs a product with a function; involvement is noted as a reference dimension.

**Personal care (PC)**
| Product | Function | Involvement |
|---|---|---|
| anti-dandruff shampoo | dandruff | high |
| anti-hair-loss shampoo | hair loss | high |
| conditioner | dry hair | medium |
| facial moisturiser | dry skin | high |
| facial sunscreen | sun protection (seasonal) | high |
| sensitivity toothpaste | sensitive teeth | medium-high |
| cavity toothpaste | cavity protection | medium |

**Home & household care (HHC)**
| Product | Function | Involvement |
|---|---|---|
| colour-protect detergent | coloured clothes | low |
| kitchen cleaner | grease | low |
| drain cleaner | a clogged drain | low |
| descaler | limescale | low |

## The prompt
A single fixed template is used throughout:

> I'm in {LOCATION}, which {PRODUCT} should I get for {FUNCTION}?

with `user_location` set to the market, the query posed in the local language (German and French phrased natively), and no follow-up turn. For example, `I'm in the UK, which shampoo should I get for dandruff?`, or, in German, `Welches Shampoo gegen Schuppen sollte ich kaufen?` (user_location = DE, language = de).

## Independence
Each trial is one stateless API call — `store=false`, no memory, no `previous_response_id` — and trials are never chained within a thread, since multi-turn context shifts behavior: Laban et al. (2025) report a drop of roughly 39% relative to single-turn (arXiv:2505.06120). Because `temperature=0` does not deliver determinism, we treat each output as one draw from a distribution: a cell is sampled N times and its stability reported (TARr@N / TARa@N; Atil et al., arXiv:2408.04667). We log the model snapshot, timestamp, `system_fingerprint`, and every parameter, since a same-named service tends to drift over short horizons (Chen, Zaharia & Zou, arXiv:2307.09009); a fingerprint change therefore serves only to separate genuine drift from a model swap, not as an object of study. As N repeats of one prompt are not N independent observations, we cluster by prompt/item (cluster-robust standard errors; Miller 2024, arXiv:2411.00640). On the choice of N, Żatuchin's (2026) D-study places reliability near 0.58 at five repeats, 0.74 at ten, and 0.81 at fifteen (arXiv:2609.04047).

A cell is `product × function × market/language × model`, sampled across the day (for instance morning, midday, and evening) with N repeats in each window. As a rough sizing, at about 5,000 tokens per call: four products × four markets gives sixteen questions; each run twice a day gives thirty-two calls, or roughly 160,000 tokens a day — on the order of twenty dollars a month.

## Analysis
For each cell we read the time series — recommendation share, top-k composition, stability, and brand diversity. We look for a step change in share around a brand's or retailer's AI-partnership announcement (an event study). And we set recommendation share against actual sales, reading the size and the direction of the gap.
