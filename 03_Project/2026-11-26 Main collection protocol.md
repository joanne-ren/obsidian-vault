---
created: 2026-11-26
type: protocol
tags: [AI购物, 数据集设计, methods, protocol]
lang: en
status: first run live
---

# Main collection protocol

Related: [[2026-11-20 Meeting]], [[2026-11-19 AI购物pilot小结]], [[AI购物数据集 - 采集方法 methods]]

## Status
- **Duration:** one year, 2026-11-26 to 2027-11-25 (local dates), as one continuous collection. Collection stops automatically after the last day.
- **First two weeks** (to 2026-12-09) are reviewed while collection continues; the decision to carry on is taken then, without restarting or changing the structure.

## Aim
Track, over time, which brands an AI assistant recommends when a consumer asks it for a product, across four markets and four everyday categories.

**Why these four categories.** They are mass-market products that most consumers buy, and we have sales data for them.

**Model.** We track `chat-latest` only, with no fixed-version control arm: the aim is to follow what the current ChatGPT model recommends, including its updates.

## Design

| Dimension | Values | n |
|---|---|---|
| Market | UK, US, Germany, France (each asked in its local language) | 4 |
| Product | see table below | 4 |
| Wording | w1 "Which … should I get?" (main); w3 "Can you recommend some …?" (robustness) | 2 |
| Time slot (local) | 9–11h (working hours); 19–21h (outside working hours) | 2 |

This yields **64 replies per day**: 4 per market × product per day, about 120 per market × product per month.

| Category | Product | Consumer need |
|---|---|---|
| PC | Anti-dandruff shampoo | Dandruff |
| HHC | Laundry detergent | Stain removal |
| PC | Conditioner | Dry hair |
| HHC | Dishwasher tablets | Tough stuck-on food |

## Prompt texts
Wording rule: within a wording, the same frame for every product; within a product, the same need phrase in both wordings.

| Market | Product | W1 (main) | W3 (robustness) |
|---|---|---|---|
| UK, US | Shampoo | Which shampoo should I get for dandruff? | Can you recommend some shampoos for dandruff? |
| UK, US | Detergent | Which laundry detergent should I get for tough stains? | Can you recommend some laundry detergents for tough stains? |
| UK, US | Conditioner | Which conditioner should I get for dry hair? | Can you recommend some conditioners for dry hair? |
| UK | Dishwasher tablets | Which dishwasher tablets should I get for tough stuck-on food? | Can you recommend some dishwasher tablets for tough stuck-on food? |
| US | Dishwasher tablets | Which dishwasher pods should I get for tough stuck-on food? | Can you recommend some dishwasher pods for tough stuck-on food? |
| DE | Shampoo | Welches Shampoo sollte ich gegen Schuppen kaufen? | Kannst du mir ein paar Shampoos gegen Schuppen empfehlen? |
| DE | Detergent | Welches Waschmittel sollte ich gegen hartnäckige Flecken kaufen? | Kannst du mir ein paar Waschmittel gegen hartnäckige Flecken empfehlen? |
| DE | Conditioner | Welche Spülung sollte ich für trockenes Haar kaufen? | Kannst du mir ein paar Spülungen für trockenes Haar empfehlen? |
| DE | Dishwasher tablets | Welche Spülmaschinentabs sollte ich gegen hartnäckige Essensreste kaufen? | Kannst du mir ein paar Spülmaschinentabs gegen hartnäckige Essensreste empfehlen? |
| FR | Shampoo | Quel shampooing contre les pellicules devrais-je acheter ? | Peux-tu me recommander quelques shampooings contre les pellicules ? |
| FR | Detergent | Quelle lessive contre les taches tenaces devrais-je acheter ? | Peux-tu me recommander quelques lessives contre les taches tenaces ? |
| FR | Conditioner | Quel après-shampooing pour cheveux secs devrais-je acheter ? | Peux-tu me recommander quelques après-shampooings pour cheveux secs ? |
| FR | Dishwasher tablets | Quelles tablettes pour lave-vaisselle contre les résidus alimentaires tenaces devrais-je acheter ? | Peux-tu me recommander quelques tablettes pour lave-vaisselle contre les résidus alimentaires tenaces ? |

Notes for analysis:
- "Tough stuck-on food" is also common advertising language in the category (e.g. on Cascade and Finish packs). Brands whose own marketing uses this language may be favoured (cf. Malthouse, Lee & Yang 2026).
- W3 asks for "some" products and its replies list more brands (often 4 to 6, against 1 to 3 for W1; test run 2026-11-26). Mention rates are therefore not directly comparable across the two wordings; rank-based measures are.
- Dishwashing liquid ("gentle on hands") was replaced by dishwasher tablets on 2026-11-26, before any data were collected.

## Setup
- **Model.** `chat-latest`, OpenAI's alias for the Instant model currently serving ChatGPT. The returned model name and token use are logged on every reply.
- **Location.** The country is never stated in the question text. Country and time zone are passed only through the API's `user_location`.
- **Search.** Web search is forced on every call. All retrieved and cited sources are logged.
- **Stateless calls.** Each call is independent (`store=False`), with no memory or context.
- **What we log.** Every raw response, its sources, token usage, local collection time and whether the slot was collected on time.

## Cost
At about $0.06 per reply: about $3.9 a day, $117 a month, about $1,430 over one year (about 23,400 replies). In the test run (2026-11-26) the two new products used about as many tokens per reply as the pilot products (9,000 to 11,600). First two weeks (about 870 replies): about $53; $100 credit added. Monthly budget (around $120) to be agreed and set later.

## Operations
- **Credit.** Prepaid credit for the first run, without auto-recharge. The collector stops at the first billing error or invalid API key, switches its schedule off and sends an email.
- **API key.** New key created on 2026-11-26, valid for 365 days; renew before November 2027.
- **Health check.** A daily automatic check of the previous day's replies against the 64 expected, with a notification when replies are missing or failed.
- **Trigger.** cron-job.org runs three jobs at 09:05 and 19:05 local time (Europe/London; Europe/Paris for Germany and France; America/New_York). GitHub's own schedule runs as a backup.
- **Code and data.** GitHub repository `joanne-ren/ai-shopping-pilot` (private). Replies in `main_runs/<YYYY-MM>/` (one folder per month), test replies in `test_runs/`, pilot replies in `pilot_runs/`. The pilot code is archived in `pilot/` and under the tag `pilot-final`.
- **Weekends.** Both slots also run on weekends; how weekend days are treated is an analysis decision.
- **Time zones.** Slots follow each market's local time, including the daylight-saving changes in March 2027 (US 14 March, EU 28 March).

### Pre-launch checklist (from the code review, 2026-11-26)
- [x] Rewrite the collector for the new design; remove the pilot end date.
- [x] cron-job.org: three jobs in local time zones, sending `mode=auto`, failure notifications on; access token limited to this repo (no expiry date).
- [x] Time limits: per call (90 s, 2 retries) and per run (20 min).
- [x] A missed slot may be made up only within one hour after its window.
- [x] Separate daily health-check workflow (06:30 UTC): opens an issue and sends an email on any shortfall.
- [x] Billing and API-key errors make the run fail visibly (email).
- [x] Readable reply files built locally, not on every run (raw data about 360 MB over one year).
- [x] Test run of all products in all markets (2026-11-26).
- [ ] OpenAI account: monthly budget (around $120) and auto-recharge, before the $100 credit runs out (about three weeks after launch).

## Deviations log
- 2026-11-26: Dishwashing liquid ("gentle on hands") replaced by dishwasher tablets ("tough stuck-on food") before any data were collected.
- 2026-11-26: The stored API key had expired; replaced before launch.
- 2026-11-26 (first day): collection started after the morning slot in the UK, Germany and France, so these three morning slots are missing (24 replies).

## 待讨论
- Monthly budget (around $120), to be agreed.
- Outcome measures for the analysis (supported by literature), given that W3 lists more brands than W1. On hold.
- How to treat weekend days in the analysis.
- Brand coding: how to code the replies with an LLM, how often, and how to check it.
