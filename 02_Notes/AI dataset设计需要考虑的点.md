---
created: 2026-09-28
updated: 2026-10-29
tags: [方法, AI购物, 数据集设计]
---

# AI dataset 设计需要考虑的点

设计一个「人用 AI 购物」的数据集前，先回答四个前置问题。下面每个问题后汇总了 vault 里现有笔记能提供的**完整证据**（关键 prompt / 模板 / 原文照录），并标出仍是空白的部分。链接指回出处。

---

## 1. 人们用 AI 购物吗，这是一个 trend 吗

**是，且正从试点走向落地（pilot → deployment）。** 证据来自行业会议与厂商数据（注意：多为厂商自报口径，需审慎）。

### 从试点到真实部署
- Groceryshop 2026 的总趋势判断：AI 购物助手正从 pilot 走向 deployment。[[2026-09-28 Groceryshop 2026]]

### 厂商自报的使用成效
- **Anthropic（Claude Commerce Agents）**：在 Claude 上跑购物智能体的零售商，购物车规模最高 **+35%**、完成购买可能性 **+60%**；报告推测这至少部分反映 AI 用户更有目的性（more intentional）。[[2026-10-19 Anthropic 商务智能体蓝图]]
  - 落地极快：Wix **15 分钟**内跑通一个能接受指令的商务智能体，Fetch **不到一小时**让两个智能体本地跑通；工程团队普遍反映上线周期从**数月压到 1–2 周**。
- **DoorDash（Ask DoorDash，对话式助手，可上传食谱创意生成购物车）**：上线之初购物车规模 **+35%**、结账速度快 **3×**；后来提升到购物车 **+50%**、结账快 **5×**；用 AI 的顾客订购的**独特 SKU +60%**（说明 AI 扩大发现范围，不只加速复购）。[[2026-09-28 Groceryshop 2026]]
- **Kroger**：今年年初先给**员工**推 AI 助手，2026-07-28 再推面向**顾客**的购物助手。两个意外发现：[[2026-09-24 克罗格 AI 购物助手]]
  - **普适性**：原以为主要吸引年轻人，实际吸引力是普适的，迅速打破"哪个年龄段更爱用"的固有观念。
  - **产品发现率上升**：购物者获得更精准推荐后反而更多自行探索——"因为简化了一个摩擦点，给了客户时间和信心去拓展到该特定目的之外。"（*it's given time and confidence to the customer to branch out beyond that specific purpose.*）
- **Albert Heijn（荷兰 Ahold 旗下）**：先推一款主打膳食灵感的助手（建立在 2 万多道菜谱数据库上，解决"晚餐吃什么"），随接受度提高再扩展到客流量更高的购物环节。[[2026-09-28 Groceryshop 2026]]
- **Migros（瑞士）**：用 AI 把营销内容制作从几天压缩到几分钟。[[2026-09-28 Groceryshop 2026]]

### 为什么是结构性趋势而非单点
- **多主体同时入场（"谁拥有客户"三方争夺）**：大型 AI 公司、Instacart/DoorDash 等平台、零售商自身都在推 AI 购物工具。杂货商虽握有食品专业知识，却在探索一项并非其核心业务的技术。[[2026-09-28 Groceryshop 2026]]
- **被推动的痛点**：
  - 杂货品类"高频 + 高复杂"天然适合 AI（Instacart CEO Chris Rogers）：消费者要反复权衡偏好、饮食需求、预算、促销和家庭需求。
  - 最常被提及的用例是「晚饭吃什么？」；从"搜 SKU"转向"解决问题"（DoorDash）。
  - Kroger×Gemini 把切口定在**选择过载（choice overload）**：给的选择/产品/配送选项越多，消费者越难决定，助手正是切入这个痛点。[[2026-09-28 克罗格×谷歌Gemini购物助手]]
- **下一阶段：从建议转向行动**——个性化膳食计划、预装购物篮（pre-loaded baskets）、对话式偏好更新，以及优惠券激活、改门店等服务型任务。[[2026-09-28 Groceryshop 2026]]

> **空白**：以上是厂商/会议口径，缺独立的**消费者侧渗透率**数据（多少人、多频繁、哪些品类真的在用）。建数据集时这正是要补的一手证据。

---

## 2. 好的 prompt 是什么样的

你的观察成立：**现有材料几乎都在讲「如何 prompt agent 让它工作更好」（系统/实验 prompt），而不是「真人实际在用什么样的 prompt」。** 把两类分开。

### A. Agent / 实验 prompt（研究者设计的，原文照录可直接复用）

**A1. 截图式购物 agent 的系统指令**（arXiv 2508.02630）— 价格敏感、只看属性不看位置、先说理由再下单：[[2026-10-26 GEO偏见与AI购物prompts]]
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

**A2. GEO 偏见实验的三种协议**（arXiv 2606.17443）— 可直接作为实验骨架，均带强制输出格式：[[2026-10-26 GEO偏见与AI购物prompts]]

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

**A3. Persona 示例（地理操纵）**— 同一人设，英文设在 California、中文译为 Shanghai，用地点信号做地理变量：[[2026-10-26 GEO偏见与AI购物prompts]]
```
English: I'm a 25-year-old male programmer with oily, acne-prone skin. My face and scalp get greasy easily. I live in California.

Chinese (translation): I am a 25-year-old male programmer with oily acne-prone skin; my face and scalp get greasy easily. I live in Shanghai.
```

### B. 真人实际意图 / query（只有零散侧写，没有系统语料）
- 行业观察到的自然语言需求：[[2026-09-28 Groceryshop 2026]] · [[2026-09-24 克罗格 AI 购物助手]]
  - "冰箱里这些食材能做什么晚餐"
  - "给我一份孩子爱吃的健康餐，40 美元以内"（*a healthy meal my kids will like, under $40*）
  - 策划儿童生日派对、找齐某道餐的食材、管理饮食限制、在 SNAP（补充营养援助计划）资格限制下购物
- 趋势：从「搜具体 SKU」转向「解决问题」（DoorDash）；对话式界面让用户提开放式问题，可能比 feed/search 更分散曝光。[[2026-09-24 克罗格 AI 购物助手]]

> **修正（见 §5 清单）**：B 类真实用户 prompt 语料**并非不存在**——已经有一批：ConsumerQ 专门从 LMSYS/WildChat 抽取真人的"求购/选品"请求；WildChat-4.8M、Search Arena 24k、ShareChat、InVivoGPT、荷兰 D3I 捐赠、Global South 捐赠语料里都含真人购物对话；Profound/Scrunch 还有真人 panel 语料。
>
> **真正的缺口更精确**：① 绝大多数**不是购物专用**，购物子集要靠过滤且规模未知；② 很少有**为"购物 prompt"本身设计**的语料（多是整段对话，没有 prompt 分类体系：带不带预算/饮食/场合约束、是否暴露身份/地域/偏好信号）；③ 真正"真人 prompt + 真人当时看到的回答"两头都真实的，数量有限（见 §5 A）。这才是自建数据集值得切入的角度。

---

## 3. CS 的人们在研究 shopping AI 的哪些方面，什么结论

目前 vault 覆盖到的 CS 侧工作主要围绕**推荐偏见与 agent 行为**。

### GEO（生成式引擎优化）= 在产品描述里注入营销语言来影响 LLM 推荐
来源 arXiv 2606.17443。[[2026-10-26 GEO偏见与AI购物prompts]]

**三档偏见模板（原文照录，可直接作为注入文本的操纵强度）：**

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

> **同一篇论文**：这篇 arXiv 2606.17443 在 §5 清单里就是 **"Incumbent Advantage: Brand Bias and Cognitive Manipulation Dynamics in LLM Recommendation Systems"（Chu & Hou, 2026）**——GEO 偏见实验 = Incumbent Advantage 的数据集。

**主要发现：**
1. **条件垄断（conditional monopoly）**：所有产品规格相同时，知名品牌 100% 获推荐（IAI = 10.0）；但竞品的星级评分优势一旦小于 0.1 分，垄断就消失。
2. **权威式营销语言**（含捏造的临床证据）会在「偏见盈余（bias surplus）」达到 **+0.17 分**时打破垄断，且各模型反应不一。
3. **多品牌 GEO 竞争的社会困境（social dilemma）**：所有品牌采用相同优化策略时，按收益代理指标，单个品牌收益从 **+0.802 跌到 +0.007**；未参与的品牌在测试中拿不到任何推荐。
4. **结论**：GEO 不只是安全风险，更是一种正在重塑市场竞争格局的新兴营销实践。

### Agent 行为偏见
- 截图式购物 agent 研究里显式要求"忽略商品位置（Do not be influenced by the position of the product）"，说明 CS 在关注**位置/呈现偏见**对 agent 决策的影响。arXiv 2508.02630。[[2026-10-26 GEO偏见与AI购物prompts]]

### 对照：营销侧框架（非 CS 但同题）
- GenAI 作为**信息中介**，削弱品牌对信任信号的控制。分两型：平台 GenAI（公开信息）vs 零售商 GenAI（零售商控制的信息）。[[Geyskens Gielens Steenkamp - GenAI Brand Trust]]
- 两个基础机制：**selection（哪些品牌被浮现）+ representation（如何被刻画/比较）**，共同形成随 query 变化的「**AI 货架（AI shelf）**」。
- 购后：AI 还塑造"预期"与"归因"，形成品牌信任的**递归更新**；同一品牌属性在不同中介下可能是优势也可能是劣势。[[Gielens 2026 - Shopper]]
- 另一侧补充：AI 暴露弱品牌——AI 系统不轻信企业一面之词，而是从评论、零售商、媒体、专家、社群、分析师、监管文件、第三方数据库等更广泛市场搜集信息；品牌不能再单方面宣称立场，必须有外部佐证。[[2026-10-26 GEO偏见与AI购物prompts]]

### 学界实证论文一览（来自 §5 清单，可直接当 CS 侧综述骨架）
- **Incumbent Advantage / GEO**（Chu & Hou 2026, arXiv 2606.17443）：真实 + 虚构品牌混合、属性固定/变动，测品牌偏见与操纵——结论见上（条件垄断、权威语言、社会困境）。
- **Evaluating Brand Retrieval and Ranking in LLM Recommendations**（Malthouse et al. 2026, arXiv 2609.16304）：把 LLM 推荐当作**随机的检索-排序过程**，6 个 LLM × 5 品类重复采样，测品牌出现概率与平均倒数排名（MRR）。
- **ChoiceEval**（Oxford × Stupid Human 2026）：按 VALS 式心理画像聚类生成问题，每问新开 session 取 top-5，追问来源——测**心理画像**对推荐的影响。
- **"Global is Good, Local is Bad?"**（Kamruzzaman, Nguyen & Kim, EMNLP 2024）：15 国各 3 全球 + 3 本地品牌，构造 SAI/ASA 选择题与送礼任务——测 LLM 的**全球 vs 本地品牌偏见**（直接对应 §4 区域问题）。
- **ConsumerQ**（Maastricht, Uberti-Bona Marin et al. 2026, arXiv 2609.18729）：从真人语料抽取求购请求再重跑，测消费者 UI vs API 的推荐差异。

> **空白**：以上多为 2024–2026 的 arXiv/会议预印本，少数已过同行评审（EMNLP 2024、ACL 2025）。做正式综述前仍应系统补检 "LLM/agent + recommendation bias / brand bias / shopping agent / GEO"。

---

## 4. 如果我们自己建数据库，如何保证 ① 独立性（没有历史）② 区域合理

你在 [[2026-09-22  Direction]] 里已经点出核心隐患，这里落成设计清单。

### ① 独立性 / "没有历史"——隔离模型的参数记忆
- **问题**（原文）：The framework implicitly assumes the training/retrieval corpus covers time windows and languages/regions evenly, which it may not. What happens to a brand that goes viral right after the training cutoff? —— 要区分 **parametric memory（模型背下来的）vs live retrieval / RAG（实时检索）**，以及模型对 recency 的处理。[[2026-09-22  Direction]]
- **设计含义**：
  - 用**虚构/新造的产品与品牌**（像 GEO 实验里 A–J 的匿名产品列表），让模型没有先验记忆可依赖，分离出"纯机制"效应。[[2026-10-26 GEO偏见与AI购物prompts]]
  - 若要测真实品牌，须显式控制**训练截止日期 × 品牌走红时间**，并记录模型版本/日期。
  - 检查驱动变量是否**真的相互独立**：高 informational authority 的品牌是否必然 representational coherence 也高？（可能很高曝光却被描述得不一致——*A brand can be very present yet described inconsistently.*）[[2026-09-22  Direction]]

### ② 区域合理——地理/语言作为受控变量
- **现成手法**：GEO 实验用同一人设、仅切换 California / Shanghai 地点信号来操纵地理变量（见 §2 A3）——可直接借用为区域自变量的操纵方式。[[2026-10-26 GEO偏见与AI购物prompts]]
- **要控制的偏置**：语料的**语言/区域覆盖不均**（英文语料 ≫ 其他），会让"区域"效应与"语料丰度"混淆。设计时要让区域信号与语言、货币、商品可得性解耦。[[2026-09-22  Direction]]
- **延伸问题（值得作为变量）**：[[2026-09-22  Direction]]
  - **Private label advantage**：retailer GenAI 依赖零售商自控语料，自有品牌是否因此有结构性优势（零售商等于语料的作者）？
  - **Trust in the output**：人们到底多相信 AI 货架的推荐？platform GenAI 与 retailer GenAI 之间这种信任是否不同？
  - **Retailer GenAI vs classic recommender**：retailer GenAI 里的品牌选择与传统推荐算法有何不同，是否像排名算法一样绑定库存（in stock）？

### 可借鉴的现成设计（来自 §5 清单）
- **隔离历史 / 独立性**：Incumbent Advantage 用**筛选过的虚构品牌 + 固定 rating/价格/评论数/成分**来剥离参数记忆；ChoiceEval 也用 screened fictional 选项。→ 虚构品牌 + 属性固定是业内标准做法。
- **区域合理**：Global South 捐赠语料本身就按 India/Pakistan/Brazil/Nigeria 分区；"Global is Good, Local is Bad?" 覆盖 15 国的全球/本地品牌；ChoiceEval 用 Swedish IP + English 混合——都说明**区域要作为显式变量并记录 IP/语言**。
- **重跑一致性问题**：多数数据集是"事后重跑（re-run）"而非"真人当时看到的回答"，而 SparkToro/Malthouse 都发现 LLM 推荐**高度不一致（stochastic）**→ 自建数据集必须**重复采样**并记录模型版本/日期，否则无法区分效应与噪声。

---

## 相关
[[2026-09-22  Direction]] · [[2026-10-26 GEO偏见与AI购物prompts]] · [[2026-10-19 Anthropic 商务智能体蓝图]] · [[2026-09-28 Groceryshop 2026]] · [[2026-09-24 克罗格 AI 购物助手]] · [[2026-09-28 克罗格×谷歌Gemini购物助手]] · [[2026-09-24 Schnucks AI 购物助手]] · [[2026-09-28 Coresight 营销个性化技术图谱]] · [[Geyskens Gielens Steenkamp - GenAI Brand Trust]] · [[Gielens 2026 - Shopper]] · [[平台渠道权力]]
