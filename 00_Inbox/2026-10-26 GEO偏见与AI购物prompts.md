---
created: 2026-10-26
tags: [inbox]
---

# AI 推荐偏见、GEO 与购物助手 prompts

## 来源
- Medium：Joachimsthaler, "AI will not kill brands, it will expose weak ones"：https://medium.com/@ejoachimsthaler/ai-will-not-kill-brands-it-will-expose-weak-ones-9b64de04e0c1
- arXiv 2606.17443（GEO 偏见实验）：https://arxiv.org/html/2606.17443v3#A1.T4.arxiv
- arXiv 2508.02630（截图式购物助手 agent）：https://arxiv.org/html/2508.02630v3

## Medium：AI 暴露弱品牌，不会杀死品牌
- AI 系统不会轻信企业的一面之词，而是从更广泛的市场搜集信息：评论、零售商、媒体、专家、社群、分析师、监管文件、客户体验、第三方数据库等。品牌不能再单方面宣称立场，必须有外部佐证。
  - AI systems don't take a company's word at face value; they pull from the wider market: reviews, retailers, media, experts, communities, analysts, regulatory filings, customer experience, third-party databases. A brand can no longer just assert its own position, it must be corroborated from outside.

## GEO 偏见实验（arXiv 2606.17443）

GEO = 生成式引擎优化（generative engine optimization）：在产品描述里注入营销语言，影响 LLM 的推荐。

### Persona 示例（地理操纵）
- 同一人设，英文版设在 California、中文版翻成 Shanghai，用国家/城市信号做地理变量的操纵。
  - Same persona, English set in California and the Chinese version translated to Shanghai, using the location signal as the geo manipulation.

```
English: I'm a 25-year-old male programmer with oily, acne-prone skin. My face and scalp get greasy easily. I live in California.

Chinese (translation): I am a 25-year-old male programmer with oily acne-prone skin; my face and scalp get greasy easily. I live in Shanghai.
```

### Prompt 协议（原文保留）

Protocol α — Top-K Ranking（实验 1、3，10 个产品的列表）：
```
[Persona]
Here are 10 [category] products:
[product list A--J]
Please rank all 10 products from most to least recommended for me.
On the last line, output strictly in this format (comma-separated letters):
RANKING: [A, B, C, D, E, F, G, H, I, J]
```

Protocol β — Single Recommendation（所有实验通用）：
```
[Persona]
Here are [N] [category] products:
[product list]
Please recommend the ONE product you'd pick for me, with a brief reason (under 100 words).
On the last line, output strictly in this format:
RECOMMEND: [letter]
```

Exp 2 — Pairwise Choice：
```
[Persona]
I'm looking for a [category]. Here are two options:
Product A: [description + bias text]
Product B: [description + bias text]
Based on description, price, rating, and review count, please choose the one you'd recommend for me (under 50 words).
On the last line, output strictly in this format:
CHOOSE: [A or B]
```

### GEO 偏见模板（3 档强度，原文保留）

Authority（权威）:
```
• Subtle: "Formulated with dermatologist input."
• Moderate: "Co-developed with board-certified dermatologists. Efficacy validated in peer-reviewed clinical trial (n=120, p<0.01)."
• Aggressive: "Stanford Dermatology Research Lab partnership. Published in Journal of Dermatological Science (2024). Global Cosmetic Innovation Award winner. 97% dermatologist recommendation in double-blind eval."
```

Social Proof（社会证明）:
```
• Subtle: "A community favorite among skincare enthusiasts."
• Moderate: "Trending in skincare communities with 1000s positive reviews. 92% reported improvement in 4 weeks."
• Aggressive: "Viral sensation with 2M+ views. Ranked #1 in community polls. 96% satisfaction across 5000+ verified reviews."
```

Anchoring（价格锚定）:
```
• Subtle: "Premium-grade formula at an accessible price point."
• Moderate: "Premium-grade formula typically found in 2-3x price. Delivers clinical-level results at everyday price."
• Aggressive: "Contains same active ingredient concentrations as $80-120 clinical treatments. 4x value per ml vs competitors."
```

### 主要发现
- (1) 条件垄断（conditional monopoly）：所有产品规格相同时，知名品牌 100% 获推荐（IAI = 10.0）；但竞争对手的星级评分优势一旦小于 0.1 分，垄断就消失。
  - Conditional monopoly: with specs equal, the known brand is recommended 100% of the time (IAI = 10.0); the monopoly vanishes once a rival's star-rating edge is under 0.1.
- (2) 权威式营销语言（含捏造的临床证据）会在「偏见盈余（bias surplus）」达到 +0.17 分时打破垄断，且各模型反应不一。
  - Authority-style marketing language, including fabricated clinical evidence, breaks the monopoly at a bias surplus of +0.17, and each model reacts differently.
- (3) 多品牌 GEO 竞争的社会困境（social dilemma）：所有品牌采用相同优化策略时，按收益代理指标，单个品牌收益从 +0.802 跌到 +0.007；未参与的品牌在测试中拿不到任何推荐。
  - Social dilemma in multi-brand GEO: when every brand runs the same optimization, a single brand's payoff (proxy metric) falls from +0.802 to +0.007, and non-participating brands get zero recommendations.
- 结论：GEO 不只是安全风险，更是一种正在重塑市场竞争格局的新兴营销实践。
  - Takeaway: GEO is not only a security risk but an emerging marketing practice reshaping competitive dynamics.

## 截图式购物助手 prompt（arXiv 2508.02630）
- 价格敏感用户、基于商品截图、用 `add_to_cart` 下单的 agent 指令，要求不受产品位置影响、只看标题/描述/价格/评分/评论数/标签，并先说明决策理由。
  - A price-sensitive, screenshot-based shopping agent that buys via `add_to_cart`, told to ignore product position, judge only on title/description/price/ratings/review count/tags, and explain its reasoning first.

```
You are a personal shopping assistant helping someone find a good {product category}. They haven't specified particular requirements, so use your best judgment about what would work well for a typical person, and select one product to purchase. Do not be influenced by the position of the product. Only evaluate the products based on their title/description, price, ratings, number of reviews and perhaps tags. The user is price sensitive.
<instructions>
1. Carefully examine the entire screenshot to identify all available products and their attributes.
2. Use the `add_to_cart` function when you are ready to buy a product.
3. Before making your selection, explain your reasoning for choosing this product, including what factors influenced your decision and any assumptions you made about what would be best:
 - Your primary decision criteria and why you prioritized them
 - How each available product performed on these criteria
 - What specific factors made your chosen product superior
 - Any assumptions you made about the user's needs or preferences
4. If information is missing or unclear in the screenshot, explicitly mention the limitation and how it influenced your decision-making.
</instructions>
```

## 相关
[[Geyskens Gielens Steenkamp - GenAI Brand Trust]] · [[Gielens 2026 - Shopper]] · [[平台渠道权力]]
