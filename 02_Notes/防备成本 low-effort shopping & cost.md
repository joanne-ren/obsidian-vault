---
created: 2026-09-28
tags: [概念]
---

购物者真正讨厌的是**搜索与防备成本**，不是价格本身。大量可替代、同质的商品要自己筛选，还怕错过，这份负担才是疲惫的来源。

---

## Idea

- 相信「默认情况就是公平的」，所以不需要比价、不需要算单价、不需要等打折、不需要怀疑「原价」是不是虚标。
  - **Low-effort shopping**:  trust the default is fair, so no need to compare prices, compute unit prices, wait for sales, or suspect the "original price" is inflated.

---

## The two poles

- **低防备极：不可替代、连贯、可信**。零售商本身就是品牌（宜家、超市自有品牌），货架收得紧，你信任里面每一件。
  - Low-effort pole: non-substitutable, coherent, trusted. The retailer is itself the brand (IKEA, grocery private label), assortment tightly curated, each item trusted.

- **高防备极：无限、可替代、疲惫**。开放同质货架（多品牌 sale、线上翻衣服、Temu、平替、频繁上新）。
  - High-effort pole: infinite, substitutable, exhausting. The open homogeneous shelf (multi-brand sales, browsing clothes online, Temu, dupes, frequent newness).

- 前两篇笔记正是高防备极的两种机制：[[2026-09-28 寻宝式轮换与新鲜感频率]]（新鲜感速率）与 [[2026-09-28 平替与自有品牌模仿]]（模仿与象征价值侵蚀）。本构念是把它们收到一个屋顶下的母概念。
  - The treasure-hunt note (velocity) and the dupe note (imitation) are two mechanisms of the high-guardedness pole; this construct is their shared roof.

---

## 

| 需要防备的 What you guard against | 降低防备的做法 Retailer practice       | 对应缺口 Gap                |
| ---------------------------- | ------------------------------- | ----------------------- |
| 价格是否划算、下周会不会更便宜              | 稳定定价（EDLP）、价格保证                 | §4 price-realization    |
| 折扣是不是真的                      | 可信的参考价、少做高低价促销                  | §4                      |
| 缩水通胀（包装变小、价格不变）              | 单位价格透明（unit-price transparency） | §4                      |
| 选错、买后悔                       | 精简货架、宽松退货                       | §5 assortment-usability |
| 质量参差                         | 自营/自有品牌的统一标准                    | §5 / trust              |

- **理论动作**：论文描述的是零售商实践制造的「缺口（供给侧）」；防备成本是这些缺口强加给购物者的「代价（消费者侧）」。两者是同一现象的两面。
  - The paper describes supply-side gaps created by retailer practices; vigilance cost is the consumer-side price those gaps impose. Two sides of one phenomenon.

---

## 文献

**1. 「不用防备」的核心：价格可信、可预测**
- [[Breugelmans & Gielens 2025 - 零售波动 volatility]] §3.2「Trust in pricing: is fairness the new value proposition?」最直接对应；§1 提到 Trader Joe's、ALDI 把价格稳定当品牌理念。
- [[Gielens 2022 - Navigate Chaos]]：price confusion（店内价签太多 → 更难找到真好价 → 削弱信任），恢复对 list price 的信任可能是促销有效的前提；紧接的 shrinkflation 段，被背叛感持续很久。
- **In the paper §4 price-realization**：§4.1 display-checkout mismatch 把 price-verification costs 转嫁给消费者（几乎就是「防备」的学术表述）；电子价签把问题从「价签过时（under-synchronization）」变成「价格过于流动（over-fluidity）」，消费者从防备错价变成防备变价；§4.2 promotion complexity（EDLP「一个低价、人人都有、无需卡券 App」 vs 条件式低价）；§9.2 政策句：当消费者需要持续监控价格/促销/质量/其他零售商时，仅提供更多信息不够。

**2. 寻宝疲惫**
- **In the paper §6.2 treasure-hunt**：Aldi 轮换特价、Middle of Lidl、TK Maxx、Action、Temu/Shein 倒计时与无尽信息流。
- [[Gielens 2026 - Shopper]]：「Friction relocated as choice fragmentation」，个性化承诺解脱、碎片化带来疲惫；摩擦对零售商下降、对购物者只是被转移，而领域还缺概念与测量工具去看这种不对称。→ 这是给本构念 + 行为测量的直接邀请。

**3. 判断上的「不用防备」：品类精简与可信选择**
- **In the paper §5 assortment-usability**：线下折扣店是「限制式」失败（选项太少），线上平台是「泛滥且无法验证」式失败；§5.2 Aldi/Lidl 以质量控制建立声誉。宜家与 Skims 恰处中间：品类收紧，但每件可信。
- [[Breugelmans & Gielens 2025 - 零售波动 volatility]] §3.3「Assortment: can it be fluid without undermining choice?」，一致性受重视的长期假设正被挑战。
- [[Gielens 2022 - Navigate Chaos]] curation vs 无尽货架。

**4. 不可替代性（Skims）与 dupes**
- [[Gielens 2025 -  copyconomy]] §1：最易被模仿的是设计线索与无形价值主导的品类，含时尚与家居（Skims/宜家领域）；§6 建议投资难以模仿的属性（community, service, ecosystems, trust）；§5：Aldi/Lidl 自有品牌在 dupe 文化下信任可能被侵蚀。

**5. 自营带来的信任（宜家的「有保障」）**
- **JR AI ms（Sept 14）Corollary 5.3**：带零售商店名的自有品牌，购后体验会同时更新对零售商的信任。与本构念的「自己人」感同一逻辑，也是与 GenAI 线的交叉点（见下）。

---

## 行为测量（measures，家庭面板/行为数据）

- **只在促销时买的比例（deal share）**：越高越防备。
  - Deal share: the higher, the more guarded.
- **跨店比价/挑拣（cherry-picking）**：一个家庭在几家店之间分散购买的程度。
  - Cross-store cherry-picking: how much a household disperses purchases across stores.
- **囤货与择时购买**：促销时大量买、平时不买。
  - Stockpiling and purchase-timing around promotions.
- **线上**：浏览时长、加购后等降价、退货率。
  - Online: dwell time, add-to-cart-then-wait-for-price-drop, return rate.

---

## 研究问题

- 零售商的哪些做法降低了消费者的防备成本？这又如何改变**购买行为与忠诚度**？（用上面的行为指标测消费者这一侧的防备成本）
  - Which retailer practices lower 'effort' cost, and how does that change purchase behavior and loyalty? (measuring the consumer-side cost with the behavioral fingerprints above)

---

## open contributions

- **spend-vs-fatigue 缺口**：论文 §6.2 关注的结果是「多花钱（预算失控）」，你的体验是「疲惫」。同一机制（寻宝陈列）、两种消费者侧产出（花费 vs 耗竭）→ 这本身可立一个小贡献：防备成本至少有 spending 与 depletion 两个不同产出。
  - Same treasure-hunt mechanism, two distinct consumer-side outcomes: overspending vs fatigue. The construct plausibly has both a spending and a depletion output.

- **脆性不对称（向下难、向上易）**：低防备值钱，恰因为它脆。它靠声誉与 EDLP 一致性慢慢挣来，却被一次缩水、一次虚标原价迅速摧毁（Gielens 2022 shrinkflation「被背叛感持久」+ Breugelmans & Gielens §3.2 fairness）。研究里防备是黏性、非对称的变量。
  - Low-guardedness is valuable because it is fragile: built slowly through reputation and EDLP consistency, destroyed fast by one shrinkflation or fake "original price." Vigilance is a sticky, asymmetric variable.

---

## 与 GenAI 线的交叉点（bridge，不合并）

- 自营/自有品牌 → 信任回流（Corollary 5.3），以及「零售商亲自书写语料 → 自有品牌在 retailer GenAI 里的结构优势」（见 [[2026-09-22 Direction]]）。低防备 ↔ 愿意相信零售商自己的推荐/AI 货架。这是防备构念与 GenAI 线的桥，暂作交叉引用而非并线。
  - Private label → trust spillover (Corollary 5.3) and the retailer-authored corpus advantage in retailer GenAI. Low-guardedness ↔ trusting the retailer's own AI shelf. A bridge to the GenAI line, kept as a cross-reference.

---
相关：[[零售摩擦]] · [[购物者体验]] · [[反身性零售 reflexive retail]] · [[Perils of Low-Price Retailing]] · [[Breugelmans & Gielens 2025 - 零售波动 volatility]] · [[Gielens 2022 - Navigate Chaos]] · [[Gielens 2026 - Shopper]] · [[Gielens 2025 -  copyconomy]] · [[2026-09-28 寻宝式轮换与新鲜感频率]] · [[2026-09-28 平替与自有品牌模仿]] · [[2026-09-22 Direction]]
