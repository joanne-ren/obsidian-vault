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
- **Weekends.** Both slots also run on weekends; how weekend days are treated is an analysis decision.
- **Time zones.** Slots follow each market's local time, including the daylight-saving changes in March 2027 (US 14 March, EU 28 March).

## Infrastructure and storage
Everything runs in the cloud; no local computer is needed for collection or coding. A new computer only needs `git clone` of the repository for local analysis.

### Components
| Component | Where | What it does |
|---|---|---|
| Trigger | cron-job.org, 3 jobs | 09:05 and 19:05 local time in Europe/London, Europe/Paris (Germany and France) and America/New_York; each calls the GitHub workflow `collect` with `mode=auto` |
| Backup trigger | GitHub Actions schedule | Runs `collect` at :45 in the UTC hours that cover both slots in winter and summer time; finds nothing to do when a slot is already collected |
| Collector | GitHub Actions, workflow `collect` (`collect.py`) | Asks the 32 questions that are due for the open slot, saves the replies and commits them to the repository |
| Daily health check | GitHub Actions, workflow `health` (`health.py`), triggered by a 4th cron-job.org job at 07:30 Europe/Amsterdam (GitHub's own 06:30 UTC schedule as backup; GitHub schedules proved unreliable on 2026-11-26/27) | Checks the previous local day (64 replies expected), errors, model name changes and whether `collect` is still enabled; on a problem opens the GitHub issue "Collection health check" and sends an email |
| Page archive | GitHub Actions, workflow `archive` (`archive/archive_pages.py`), after every `collect` run | Fetches the web pages the new replies cite and saves their text (see Cited-page archive) |
| Brand coding | Claude Code scheduled cloud task "ai-shopping weekly brand coding", Mondays 05:00 UTC | Builds the monthly tables, codes the new replies with Sonnet subagents, checks them and commits the results |
| Code and data | GitHub repository `joanne-ren/ai-shopping-pilot` (private), branch `main` | Single place for code, raw data, tables and coding output |

### Accounts and credentials
| Item | Stored in | Expires |
|---|---|---|
| OpenAI API key | GitHub repository secret `OPENAI_API_KEY` | About 2027-11-26 (365 days); renew before |
| OpenAI credit | OpenAI account (Launch tier) | $100 prepaid on 2026-11-26, enough for about three weeks |
| GitHub token `cron-job-trigger` | cron-job.org request header | No expiry date |
| Claude subscription | Claude account, connected to GitHub as `joanne-ren` | Used by the weekly coding task; no API cost |

### Repository layout
```
ai-shopping-pilot/
├── collect.py                  collector (design, prompt texts, slots, start/end date)
├── health.py                   daily health check
├── .github/workflows/          collect.yml, health.yml
├── main_runs/<YYYY-MM>/        raw data, one pair of files per collecting run
│     <stamp>__index.jsonl      one row per call (metadata, answer text, or the error)
│     <stamp>__raw.jsonl        full request and full API response (sources, search queries)
├── tables_main/<YYYY-Www>/     tidy tables, one folder per ISO week (Mon–Sun), written once
│     responses.csv             one row per reply
│     answers.jsonl             reply texts without citation links (input for coding)
│     sources.csv               one row per web page retrieved or cited
│     mentions.csv              one row per brand named in a reply
├── coding/                     brand coding: INSTRUCTIONS.md, WEEKLY_TASK.md, scripts,
│     coded/*.json              the subagents' output (never edited by hand)
│     brands.csv                brand name -> canonical name; status "new" = to review
├── archive/                    cited web pages
│     pages/<YYYY-MM>/*.jsonl.gz  one line per fetched page (text, title, structured data)
│     index.csv                 one row per cited URL: first/last cited, last fetch
├── test_runs/                  test replies (not part of the data)
├── pilot_runs/, tables/, analysis/   pilot data, tables and analysis
└── pilot/                      pilot collector, archived (also tag pilot-final)
```
Raw data are stored in monthly folders; tables in weekly folders, written once when the week is complete, so the repository history holds each table only once.

### GitHub limits (checked 2026-11-27)
- **Actions minutes.** GitHub Free account: 2,000 free minutes a month, shared by all private repositories of the account (also global-esl), reset on the 1st. Use in November 2026 up to the 27th: 422 minutes (pilot 383), cost $0. When they are used up, all workflows stop until the next month, including collection. Estimated use: about 1,000 to 1,300 minutes a month (collection about 12 a day, backup schedule 2 to 14, page archive about 15 to 20 after caching, health check 1). Check monthly under GitHub → Settings → Billing and licensing → Usage (filter: Actions). Weekly brand coding runs in Claude's cloud and uses no Actions minutes.
- **Repository size.** About 0.6 to 0.8 GB after one year (raw data about 300 MB, page archive 100 to 200 MB, weekly tables about 180 MB). GitHub recommends staying below 1 GB (strongly below 5 GB); no single file comes near the 100 MB file limit.
- **Runner resources.** 2 CPUs, 7 GB memory, 14 GB disk per run; our scripts use a few hundred MB at most. Job time limits are set to 20 to 25 minutes (GitHub's maximum is 6 hours).

### Main fields
- **Index row (raw data):** `utc`, `local` (market-local time), `local_date`, `slot` (09 / 19), `on_time`, `market`, `country`, `language`, `category` (PC / HHC), `product_key`, `product`, `need`, `wording` (w1_which / w3_rec), `prompt`, `request_model`, `resp_model`, `id`, `usage`, `answer`; failed calls carry `error` instead of an answer.
- **responses.csv:** reply id, time, local date and weekday, market, language, slot, on time, category, product, wording, prompt, model requested and returned, input / cached / output tokens, number of searches, search queries, sources retrieved and cited, answer length.
- **sources.csv:** reply id, url, domain, title, retrieved by search, cited in answer, number of citations.
- **mentions.csv:** reply id, market, product, order, brand (canonical), brand as coded, product name, role (recommended / negative / neutral), own label of, explicit top pick, quote, asks questions, coded by.

### Weekly rhythm
| When (UTC) | What |
|---|---|
| Daily, 2 slots per market | Collection (64 replies a day) |
| Daily 06:30 (07:30 Amsterdam) | Health check; email and issue only when something is wrong |
| Monday 05:00 | Brand coding of the past week; tables updated |
| Monday, after coding | Human review of brands with status "new" in `coding/brands.csv` |

### Where to look
- Collection runs and errors: GitHub → repository → Actions.
- Problems: email from GitHub, and the issue "Collection health check".
- Coding runs: claude.ai/code/routines.
- Trigger history: cron-job.org dashboard.
- One-screen status: `python3 status.py` in the repository folder.
- What to do when something goes wrong: `docs/RUNBOOK.md` in the repository (in Chinese).
- Context for any new Claude session: `CLAUDE.md` in the repository.

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

## Cited-page archive
**Why.** The web pages that ChatGPT cites change over time; a page opened months later may no longer be the version the model read. To study what the cited pages have in common (cf. Aggarwal et al. 2024, GEO: statistics, quotations, sources), we keep a copy of each cited page from the time it was cited.

**What.**
- After every collection run, the workflow `archive` fetches the pages cited in the new replies (`url_citation` in the answer text). Pages only retrieved by search, not cited, are not archived (about 27 per reply against 1 to 3 cited).
- A page is fetched when first cited, and again when it is cited again more than 7 days after its last fetch, so that changes over time are captured.
- Saved per fetch: the main text as Markdown (headings, lists, tables), title, meta description, structured data (JSON-LD, e.g. product ratings and prices), HTTP status, final URL, fetch time and a hash of the HTML (to detect changes).
- Pages built by JavaScript (e.g. dm.de product pages) are opened in a headless browser; PDFs are read as text.
- robots.txt is respected. Tracking parameters (utm_, mi_ ...) are removed from URLs for de-duplication; the raw data keep the original URLs.

**Coverage (first run on GitHub, 97 cited pages, 2026-11-27).** 80 archived with text (61 plain HTML, 12 via browser, 7 PDFs); 1 disallowed by robots.txt; 16 not available: 13 blocked by the site (HTTP 403; e.g. carrefour.fr, intermarche.com, sainsburys.co.uk, mayoclinic.org; some of these block cloud servers only, as a test from a home connection reached 85 of 97), 2 no longer online (404), 1 without text. Blocked pages remain identifiable by URL and title in `sources.csv`.

**Storage.** `archive/pages/<YYYY-MM>/*.jsonl.gz` and `archive/index.csv` in the repository; about 4 KB per page, roughly 150 to 200 MB a year. No API cost; GitHub Actions time only.

## Brand coding
- Every Monday at 05:00 UTC a scheduled Claude Code cloud task (Claude Sonnet) codes the previous week's replies: Sonnet subagents read each reply and list the brands it names, in order, with a verbatim quote. Rules: `coding/INSTRUCTIONS.md`, the pilot's rules extended to conditioner and dishwasher tablets (pilot agreement with a keyword codebook: Cohen's κ = 0.996).
- A script checks every quote against the reply text and recodes failures; results go to `tables_main/<YYYY-Www>/mentions.csv`.
- New brand names are listed in `coding/brands.csv` with status "new" for a weekly human review.
- All names are kept: `mentions.csv` stores the verbatim quote, the product name and the brand as coded, next to a unified `brand` column (umbrella level, e.g. Elvive/Elseve -> L'Oréal) used for counting. The brand level for analysis (umbrella brand or product line) will follow the level of our sales data; it can be changed later without recoding.
- Runs on the subscription account; no API cost.

## Deviations log
- 2026-11-26: Dishwashing liquid ("gentle on hands") replaced by dishwasher tablets ("tough stuck-on food") before any data were collected.
- 2026-11-26: The stored API key had expired; replaced before launch.
- 2026-11-26 (first day): collection started after the morning slot in the UK, Germany and France, so these three morning slots are missing (24 replies). The US morning slot is also missing (8 replies): the cron-job.org jobs had not yet been enabled. The Germany and France evening slot was triggered by hand at 18:42 UTC (19:42 local, within the slot). From the UK evening slot on 2026-11-26, collection ran on the cron-job.org triggers.

## 待讨论
- Monthly budget (around $120), to be agreed.
- Outcome measures for the analysis (supported by literature), given that W3 lists more brands than W1. On hold.
- How to treat weekend days in the analysis.
