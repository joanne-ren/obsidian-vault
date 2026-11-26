---
created: 2026-11-26
type: protocol
tags: [AI购物, 数据集设计, methods, protocol]
lang: en
status: draft
---

# Main collection protocol (draft)

Related: [[2026-11-20 Meeting]], [[2026-11-19 AI购物pilot小结]], [[AI购物数据集 - 采集方法 methods]]

## Aim
Track, over time, which brands an AI assistant recommends when a consumer asks it for a product, across four markets and four everyday categories.

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
| HHC | Dishwashing liquid | Gentle on hands |

## Prompt texts
Wording rule: within a wording, the same frame for every product; within a product, the same need phrase in both wordings.

| Market | Product | W1 (main) | W3 (robustness) |
|---|---|---|---|
| UK, US | Shampoo | Which shampoo should I get for dandruff? | Can you recommend some shampoos for dandruff? |
| UK, US | Detergent | Which laundry detergent should I get for tough stains? | Can you recommend some laundry detergents for tough stains? |
| UK, US | Conditioner | Which conditioner should I get for dry hair? | Can you recommend some conditioners for dry hair? |
| UK | Dishwashing liquid | Which washing-up liquid should I get that's gentle on hands? | Can you recommend some washing-up liquids that are gentle on hands? |
| US | Dishwashing liquid | Which dish soap should I get that's gentle on hands? | Can you recommend some dish soaps that are gentle on hands? |
| DE | Shampoo | Welches Shampoo sollte ich gegen Schuppen kaufen? | Kannst du mir ein paar Shampoos gegen Schuppen empfehlen? |
| DE | Detergent | Welches Waschmittel sollte ich gegen hartnäckige Flecken kaufen? | Kannst du mir ein paar Waschmittel gegen hartnäckige Flecken empfehlen? |
| DE | Conditioner | Welche Spülung sollte ich für trockenes Haar kaufen? | Kannst du mir ein paar Spülungen für trockenes Haar empfehlen? |
| DE | Dishwashing liquid | Welches Spülmittel sollte ich kaufen, das schonend zu den Händen ist? | Kannst du mir ein paar Spülmittel empfehlen, die schonend zu den Händen sind? |
| FR | Shampoo | Quel shampooing contre les pellicules devrais-je acheter ? | Peux-tu me recommander quelques shampooings contre les pellicules ? |
| FR | Detergent | Quelle lessive contre les taches tenaces devrais-je acheter ? | Peux-tu me recommander quelques lessives contre les taches tenaces ? |
| FR | Conditioner | Quel après-shampooing pour cheveux secs devrais-je acheter ? | Peux-tu me recommander quelques après-shampooings pour cheveux secs ? |
| FR | Dishwashing liquid | Quel liquide vaisselle doux pour les mains devrais-je acheter ? | Peux-tu me recommander quelques liquides vaisselle doux pour les mains ? |

Note for analysis: "gentle on hands" echoes a common advertising claim in the category (e.g. Fairy's "kind to hands" in the UK). Brands whose own marketing uses this language may be favoured (cf. Malthouse, Lee & Yang 2026).

## Setup
- **Model.** `chat-latest`, OpenAI's alias for the Instant model currently serving ChatGPT. The returned model name and token use are logged on every reply.
- **Location.** The country is never stated in the question text. Country and time zone are passed only through the API's `user_location`.
- **Search.** Web search is forced on every call. All retrieved and cited sources are logged.
- **Stateless calls.** Each call is independent (`store=False`), with no memory or context.
- **What we log.** Every raw response, its sources, token usage, local collection time and whether the slot was collected on time.

## Cost
At about $0.06 per reply (pilot estimate): about $3.9 a day, $117 a month, about $1,430 over one year (about 23,400 replies). To be re-checked after the first week, since the two new products may produce answers of different length.

## Operations
- **Credit.** Auto-recharge and a monthly budget alert in the OpenAI account. The collector stops at the first billing error and switches its schedule off.
- **Health check.** A daily automatic check of the previous day's replies against the 64 expected, with a notification when replies are missing or failed.
- **Trigger.** cron-job.org triggers each market's two slots; GitHub's own schedule runs as a backup.
- **Time zones.** Slots follow each market's local time, including the daylight-saving changes in March 2027 (US 14 March, EU 28 March).

### Pre-launch checklist (from the code review, 2026-11-26)
- [ ] Rewrite the collector for the new design (products, wordings, slots, no country in text); remove the pilot end date, which would otherwise switch the schedule off at the first run.
- [ ] cron-job.org: one job per market and slot in that market's own time zone, always sending `mode=auto`; failure notifications on; access token limited to this repo and valid beyond the end of collection.
- [ ] Time limits: per call (about 90 s, 2 retries) and per run (20 min).
- [ ] A missed slot may be made up only within one hour after its window, not hours later.
- [ ] Separate daily health-check workflow: replies per market × product × slot (expected 64), error rows, returned model names, collector still enabled; opens an issue and sends an email on any shortfall.
- [ ] Billing errors make the run fail visibly (email), not end silently.
- [ ] Build the readable reply files locally rather than on every run, to keep the repository small (raw data about 180 MB over six months).
- [ ] OpenAI account: auto-recharge and a monthly budget alert.
- [ ] One manual test run per market before launch.

## 待讨论
- Prompt texts in English (UK and US), German and French for all four products.
- w3 with "some" (plural) was not part of the pilot, which used "Can you recommend a …?". Do we run a short test first?
- A small control arm with a fixed, dated model version, to separate model updates from changes on the web?
- Start date, duration and monthly budget cap.
- The rationale for the four categories.
- Brand coding: how often, and how it is checked.
