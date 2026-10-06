---
created: 2026-10-06
tags: [project]
---

# ESL

电子价签（ESL）作为「超市可以更随意地调价」的信号，如何侵蚀信任（trust）。走实证路线，数据为 scanner data。核心约束：trust 是潜变量，scanner data 不直接记录它。
  - ESL as a signal that "the store can adjust prices more freely" and how it erodes trust. Empirical route, scanner data. Key constraint: trust is latent and scanner data does not record it directly.

- **测量思路**：不是用 scanner data「测 trust」，而是测 trust 所支配的可观测行为，即价格警惕/防备（vigilance）。trust 在模型里是潜在中介，不是因变量。
  - Don't measure trust with scanner data; measure the observable behavior trust governs, i.e. price vigilance. Trust is a latent mediator, not the dependent variable.
- 承接 [[防备成本 low-effort shopping & cost]] 的「行为测量」小节：下表把那组指纹正式化为 ESL→trust 设计的操作化矩阵。
  - Extends the behavioral-fingerprint section of [[防备成本 low-effort shopping & cost]] into an operationalization matrix for the ESL→trust design.

---

## 三类结果变量

- **顾客行为至少可拆成三类结果变量**，这是 scanner-data 设计的因变量总结构，下面的行为签名表是它逐项的展开。
  - Customer behavior decomposes into at least three families of outcome variables, the DV backbone of the scanner-data design; the signature table below is its item-level expansion.
- **① 价格响应（price response）**：价格弹性、对促销的反应、囤货与跨期替代。
  - Price response: price elasticity, promotion response, stockpiling and intertemporal substitution.
- **② 篮子构成（basket composition）**：品类选择、品牌与自有品牌切换、篮子规模、信息密集型商品的偏好。
  - Basket composition: category choice, brand vs private-label switching, basket size, preference for information-intensive products.
- **③ 关系层面（relationship）**：光顾频率、忠诚度、流失、价格信任。
  - Relationship level: trip frequency, loyalty, churn, price trust.

---

## 信任侵蚀的行为签名 → scanner data 代理

| 信任侵蚀后的行为签名 | scanner data 代理变量 | 对应的 effort dimension | 预测方向 |
| --- | --- | --- | --- |
| 整体价格警惕 | 需求价格弹性（à la Ray 2019） | 比价成本 | 弹性 ↑ |
| 囤货/提前购买 | 促销时购买量、跨期囤积、购买间隔随促销周期 | 「下周会不会更便宜？」 | 促销囤货 ↑ |
| 挑便宜货 | cherry-picking 指数（只买促销品的篮子占比） | 比价+等折扣 | ↑ |
| 退守「安全默认」 | 自有品牌(PL) vs 全国品牌份额、包装/单价最优化 | 算单价 | 方向需论证* |
| 对折扣的信任 | 促销提升量（promo lift） | 「折扣是真的吗？」 | 双向，见下 |
| 门店信任/流失 | 钱包份额、到店频率、篮子大小、转向硬折扣店 | 整体信任 | 份额 ↓（需家户面板） |

- **\*PL 方向是理论岔口**：PL 恰是 low-effort / trust-the-default 那一极。信任掉了可能退守 PL（守住可信默认），也可能逃离这家店转去 Lidl/Aldi（硬折扣=EDLP 可信极）。两个方向都是可检验的竞争假设。
  - The PL prediction forks. PL is the low-effort / trust-the-default pole. Lost trust may drive retreat into PL (holding a trusted default) or exit to Lidl/Aldi (the EDLP discounter pole). Both are testable competing hypotheses.
- **promo lift 双向**：若顾客变警惕去抢折扣，promo lift ↑；若开始怀疑折扣真假（参考价不可信），promo lift ↓。到底哪个占上风，本身就是一个发现。
  - Promo lift cuts both ways: more vigilant deal-hunting pushes lift up, while distrust of discount authenticity pushes it down. Which dominates is itself a finding.

---

## 两条相反的机制（competing mechanisms）

- **(+) 准确性/能力信任（competence）**：ESL 让货架价与收银价一致，减少「结账被多扣」的摩擦，顾客信任上升。
  - Competence: ESL aligns shelf price with checkout price, reducing the "overcharged at checkout" friction, so trust rises.
  - → 预测：光顾频率、忠诚度上升，长期流失下降。
    - Prediction: trip frequency and loyalty rise, long-run churn falls.
- **(−) 可变性/正直信任（integrity）**：顾客意识到 ESL 会带来价格变化，因此显得对价格更敏感（警惕被重新激活）。
  - Integrity: shoppers realize ESL enables price changes, so they appear more price-sensitive (vigilance reactivated).
  - → 预测：见上面的信任侵蚀行为签名（弹性 ↑、cherry-picking ↑ 等）。
    - Prediction: the trust-erosion signatures above (elasticity up, cherry-picking up, etc.).
- **净效应取决于哪个方向占上风**，并被门店定位调节（EDLP/高信任店 vs Hi-Lo 店）。这正是实证要估的东西。
  - Net effect depends on which direction dominates, moderated by store positioning (EDLP/high-trust vs Hi-Lo). This is exactly what the empirical work estimates.

---

## 识别（identification）

- **关键假设**：某门店何时安装 ESL，不由该店顾客行为的潜在趋势决定（平行趋势 / 外生采用时点）。
  - Key assumption: when a store installs ESL is not driven by that store's latent consumer-behavior trend (parallel trends / exogenous adoption timing).
- **头号威胁：安装决策内生**。零售商可能先给高流量/高竞争的门店装，而这些店的信任与行为轨迹本就与其他店不同。
  - #1 threat: endogenous rollout. Retailers may install first in high-traffic or high-competition stores, whose trust and behavior trajectories already differ from the rest.
  - → 应对：利用交错铺开（staggered rollout），事件研究检查处理前 pre-trends，控制门店特征，或寻找安装顺序由外生因素（供应商产能、物流排期）决定的情形。
    - Mitigation: exploit the staggered rollout, check pre-trends in an event study, control store characteristics, or find settings where install order is set by exogenous factors (supplier capacity, logistics scheduling).

---

相关：[[防备成本 low-effort shopping & cost]] · [[2026-09-30 Meeting]] · [[零售摩擦]]
