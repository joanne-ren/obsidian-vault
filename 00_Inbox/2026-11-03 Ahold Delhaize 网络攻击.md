---
created: 2026-11-03
tags: [inbox, 案例]
---
# Ahold Delhaize 网络攻击事件（2026-10-11 起）

来源：自建事件日志 `ah_incident_log_2026-11-03.md`/`.csv`（95 条事件，E001–E095，2026-10-11 至 2026-11-02）。日志按来源分级（Official / Priority media / Other），并逐条标注冲突与存疑，附官方口径链接 [nieuws.ah.nl](https://nieuws.ah.nl/mediastatement-inzake-it-incident/) 及 [Ahold Delhaize newsroom](https://newsroom.aholddelhaize.com/ahold-delhaize-update-on-status-of-cybersecurity-incident/)。

## 事件梗概

- **起点**：2026-10-11（周日）下午，Ahold Delhaize 出于预防主动关停系统，初称「IT 事件」，次日改口「网络安全事件（cybersecurity incident）」。波及 Albert Heijn（荷兰）、Etos、Gall & Gall、AH 比利时与 Delhaize 比利时。
  - On Sunday afternoon 11 Oct, Ahold Delhaize shut systems down as a precaution, first calling it an "IT incident," then a "cybersecurity incident" the next day. It hit Albert Heijn (NL), Etos, Gall & Gall, AH Belgium and Delhaize Belgium.

- **实体店照常、线上全停**：门店保持营业，收银与支付正常；但网站与 App、在线下单与到家配送、客服全部瘫痪，已下订单被全部取消。
  - Physical stores stayed open with checkout and payments working, but websites and apps, online ordering and home delivery, and customer service were all down, and placed orders were cancelled.

- **供应链波及**：多个配送中心（Tilburg、Zwolle、Zaandam 等）一度停摆，货架出现空缺风险，耐储/非食品比生鲜更易补齐。约 10-15 日供应恢复，官方 10-15 称全国货架补满。
  - Several distribution centres (Tilburg, Zwolle, Zaandam) stopped for a time, risking empty shelves, with long-life and non-food recovering faster than fresh. Supply was restored around 13 to 15 Oct, with AH declaring shelves full nationwide on 15 Oct.

## 与 ESL / 定价研究直接相关的切面

- **电子价签错价（核心看点）**：停摆期间货架 ESL 卡在「上周促销价」，出现货架价低于收银价的情形；10-13 恢复常规价，10-18 Bonus/促销价在货架上才恢复正确。参见 [[ESL]] 里 competence（货架价=收银价一致性）这条机制，这次是它在现实中被打断的一次自然实验。
  - Shelf labels stuck on last week's promo prices during the outage, so shelf price could sit below checkout price; regular prices were fixed 13 Oct and Bonus/promo shelf prices only 18 Oct. This is a real-world break in the competence mechanism (shelf = checkout alignment) in [[ESL]].

- **个性化与忠诚体系单点失效**：个性化折扣（Mijn Bonus Box）、Koopzegels、Air Miles、AH Premium 10% 全部下线约一到两周；全国性 Bonus 促销在收银端始终有效。说明「个性化/会员」这层比基础零售功能更脆弱。
  - Personalized discounts (Mijn Bonus Box), Koopzegels, Air Miles and the AH Premium 10% were all offline for one to two weeks, while national Bonus offers kept working at checkout, showing the personalization/loyalty layer is more fragile than base retail functions.

- **补偿机制**：承诺并实施补偿，取消订单每单 10 欧元购物金加退款、Bezorgbundel 额外 10 欧元、错过的 Air Miles 自动补记、koopzegels 可凭小票补购、Premium 补发券；比利时另有对应方案。
  - Compensation was promised and implemented: EUR 10 credit plus refund per cancelled order, extra EUR 10 for Bezorgbundel, missed Air Miles auto-credited, koopzegels buyable with receipt, a Premium coupon, with a parallel scheme in Belgium.

## 恢复时间线与定性

- **恢复节奏**：网站与 Mijn AH App 于 10-18 恢复；自营配送 10-23 以约三分之一运力重启；10-28 起配送回到正常水平。整体停摆约两周半。NL Times（11-02）称集团「上周才恢复正常运营」。
  - Websites and the Mijn AH app came back 18 Oct, own-courier delivery restarted 23 Oct at about one-third capacity, and delivery was back to normal from 28 Oct. The disruption ran about two and a half weeks.

- **性质与数据**：CEO Frans Muller 称系「第三方恶意行为」；10-19 报警，警方开刑事侦查；多次表态未见敏感的顾客/员工/合作方数据被窃。非官方损失估计 1.2 至 1.5 亿欧元。
  - CEO Frans Muller called it "malicious actions by third parties"; a police report was filed 19 Oct and a criminal investigation opened; AH repeatedly said no evidence of sensitive customer, employee or partner data theft. An unofficial damage estimate put losses at EUR 120 to 150m.

- **可能是另一起事件（11-02）**：约 40 家 Delhaize 比利时门店制冷系统被「IT 事件」扰乱，冰柜温度一度升至约 15°C，大量食品报废（单店损失数万欧元）；同期 Carrefour、Intermarché、Spar 也中招。日志明确标注：无来源证实它与 10-11 事件相关，当日即恢复。
  - A possibly separate incident on 2 Nov disrupted refrigeration at about 40 Delhaize Belgium stores, with freezer temperatures rising to around 15°C and large amounts of food discarded; Carrefour, Intermarché and Spar were also hit. The log flags that no source links it to the 11 Oct incident, and it was resolved the same day.

## 为何值得记

- 这是一次「价格与会员基础设施整体宕机」的罕见自然实验，可同时检验 ESL 的 competence 与 integrity 两条机制，也暴露个性化/忠诚层作为单点故障的脆弱性。
  - A rare natural experiment where pricing and loyalty infrastructure went down wholesale, letting one test both the competence and integrity mechanisms for ESL and exposing the personalization/loyalty layer as a single point of failure.
- 日志本身是一份可追溯数据产物（来源分级、冲突标注、官方口径与媒体口径并置），方法上与 [[ESL]] 的 esl-tracker 采集规范同构，可作样例。
  - The log itself is a traceable data artifact (source tiers, flagged conflicts, official vs media wording side by side), methodologically of a piece with the esl-tracker collection standard and usable as a template.

---
相关：[[ESL]] · [[防备成本 low-effort shopping & cost]] · [[2026-11-03 FTC问询九家监控定价]]
