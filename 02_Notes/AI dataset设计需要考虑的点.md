---
created: 2026-09-28
updated: 2026-11-03
tags: [方法, AI购物, 数据集设计]
---

# AI dataset 设计需要考虑的点

---

## 1. 人们用 AI 购物吗，这是一个 trend 吗


### 厂商侧信号
- **Anthropic（Claude Commerce Agents）**：在 Claude 上跑购物智能体的零售商，购物车规模最高 **+35%**、完成购买可能性 **+60%**；报告推测这至少部分反映 AI 用户更有目的性（more intentional）。（来源：[Coresight Research《…Three Key Pillars for Agentic Commerce…》](https://coresight.com/research/with-announcements-from-meta-stripe-and-anthropic-the-three-key-pillars-for-agentic-commerce-are-now-in-place-agents-payments-and-tools/)）
  
- **DoorDash（Ask DoorDash，对话式助手，可上传食谱创意生成购物车）**：上线之初购物车规模 **+35%**、结账速度快 **3×**；后来提升到购物车 **+50%**、结账快 **5×**；用 AI 的顾客订购的**独特 SKU +60%**（说明 AI 扩大发现范围，不只加速复购）。（来源：[Grocery Dive《5 takeaways from Groceryshop》, 2026](https://www.grocerydive.com/news/takeaways-groceryshop-conference-2026-las-vegas/831421/) 与 [Coresight Research·Groceryshop 2026 Day Two 回顾](https://coresight.com/research/groceryshop-2026-day-two-ai-moves-into-action-as-retailers-redefine-value-and-commerce/)；DoorDash 数据另见 [Grocery Dive《DoorDash launches conversational shopping assistant》](https://www.grocerydive.com/news/doordash-grocery-tools-conversational-shopping-assistant-agentic-ai/822735/)）
- **Kroger**：今年年初先给**员工**推 AI 助手，2026-07-28 再推面向**顾客**的购物助手。两个意外发现：（来源：[Grocery Dive《Kroger leans on AI to reshape the shopping experience》, 2026-09-23](https://www.grocerydive.com/news/kroger-ai-technology-groceryshop/831102/)）
  - **普适性**：原以为主要吸引年轻人，实际吸引力是普适的，迅速打破"哪个年龄段更爱用"的固有观念。
  - **产品发现率上升**：购物者获得更精准推荐后反而更多自行探索——"因为简化了一个摩擦点，给了客户时间和信心去拓展到该特定目的之外。"（*it's given time and confidence to the customer to branch out beyond that specific purpose.*）
- **Albert Heijn（荷兰 Ahold 旗下）**：先推一款主打膳食灵感的助手（建立在 2 万多道菜谱数据库上，解决"晚餐吃什么"），随接受度提高再扩展到客流量更高的购物环节。（来源：[Coresight Research·Groceryshop 2026 Day Two 回顾](https://coresight.com/research/groceryshop-2026-day-two-ai-moves-into-action-as-retailers-redefine-value-and-commerce/) 与 [Grocery Dive《5 takeaways from Groceryshop》, 2026](https://www.grocerydive.com/news/takeaways-groceryshop-conference-2026-las-vegas/831421/)）
### 咨询机构 / 调研：消费者采用数据


- **McKinsey**（Agentic Commerce Consumer Survey，2026-06，约 21,000 人 / 11 国）：**53%** 的消费者已用 AI 购物；中国 80%、印度 76% 领先，日本 37%、法国 44% 最低。最近一次购买里，**29%** 的 AI 用户说"AI 对话/搜索工具"影响最大——是传统搜索引擎（9%）的三倍，也超过"零售商平台 + 零售商 AI 助手"之和（21%）。品类上美妆（34%）、杂货（32%）已逼近消费电子（38%）、服装（37%）、旅游（35%）。核心判断：零售商正把"购物旅程的起点"丢给 AI 工具。（[McKinsey《Who wins when AI does the shopping?》](https://www.mckinsey.com/capabilities/growth-marketing-and-sales/our-insights/who-wins-when-ai-does-the-shopping-new-evidence-on-agentic-commerce)）
- **McKinsey × EuroCommerce**（欧洲）：用 AI 做发现/评估的约 **61%**（部分口径"约一半"）。但越往漏斗下游越窄——84% 每天用 AI、38% 用于产品调研/购买决策、约 15% 在零售商网站上用过 AI、仅 **1–3%** 真的通过 AI 平台下过单。另有分项（法/德/英）：**63%** 比较品牌/型号/价格/评价、55% 了解一个品类、46% 找灵感；**56%** 接受建议但自己拍板、47% 不愿让 AI 自动打理复购。（[McKinsey《Europe's agentic commerce moment》](https://www.mckinsey.com/capabilities/quantumblack/our-insights/europes-agentic-commerce-moment-decision-influence-is-here-execution-is-coming)）
- **Deloitte**（2026 Holiday Retail Survey，4,000 美国消费者，2026-08 调研）：**39%** 把生成式 AI 当作至少一项假日购物任务的主要工具；但仅 **16%** 愿意让 AI 代为完成购买。（[Deloitte](https://www.deloitte.com/us/en/insights/industry/retail-distribution/holiday-retail-sales-consumer-survey.html)）
- **Adobe**（Digital Insights，2026）：到 2026-07，**42%** 美国消费者用过 AI 助手网购（3 月为 39%）；用 AI 的人 77% 对购买更有信心；流向美国零售商的 AI 导流 Q1 同比 **+393%**。（[TechCrunch 报道 Adobe 数据](https://techcrunch.com/2026/04/16/ai-traffic-to-us-retailers-rose-393-in-q1-and-its-boosting-their-revenue-too/)）
- **Salesforce**（Connected Shoppers Report，第 6 版 / 2025，数据采集于 2024 年末）：**39%** 购物者（Gen Z **54%**）用 AI 做产品发现；75% 零售商认为 AI agent 将成为竞争必需。（[Salesforce](https://www.salesforce.com/news/stories/consumer-shopping-ai-trends-2025/)）
- **Bain**（预测）：美国 agentic commerce 到 2030 年约 **3,000–5,000 亿美元**、占电商 15–25%。（经 [commercetools 汇编](https://commercetools.com/blog/agentic-commerce-stats-enterprise-guide)）
- **McKinsey × ICSC**（美国，2026-04，3,004 名消费者 + 高管访谈）：过去 3 个月 **68%** 用过至少一种 AI 工具；预计 agentic commerce 到 2030 年达约 **1 万亿美元**。
- **BCG**（Consumer Radar，2025/26）：购物是生成式 AI 的**第三大用途**；2025-02 至 11 购物类使用 **+35%**；60%+ 高度信任 GenAI 输出；印度 **64%** 在购买过程中使用。
- **在旅程中的角色**（*Shopping with a Platform AI Assistant*）：AI 对话与传统搜索在同一阶段**互换使用、彼此补充**；约 **42%** 的请求是探索型（attraction / destination 类）。


"人们在用 AI 购物"成立，但目前主要集中在**发现/评估**环节，自主下单仍是早期。

### 供给侧：区域部署全景
平台与零售商正大规模把商品目录接进 AI 入口，与上面的消费者采用数据互补（铺得多 ≠ 用得多）。连接标准正在成形：**UCP（Universal Commerce Protocol）**，Google + Shopify 于 2026 年初推出的开放 AI-商务标准，商家暴露一个标准接口，AI 实时读库存、套会员折扣、代顾客在对话内一键结账（[UCP](https://developers.google.com/merchant/ucp)）。

- **美国**（最领先）：
  - **Target × OpenAI**（2025-11）：Target 商品可在 ChatGPT 内被调用（[OpenAI](https://openai.com/index/powering-product-discovery-in-chatgpt/)）。
  - **Walmart × Google**（2026-01, NRF）：沃尔玛 + 山姆目录接入 Gemini，可在对话内规划、建购物车、结账（[Walmart 新闻室](https://corporate.walmart.com/news/2026/01/11/walmart-and-google-turn-ai-discovery-into-effortless-shopping-experiences)）。
  - **Best Buy × OpenAI**（2026-08，财报电话会披露）：目录接入 ChatGPT，可在对话内发现/推荐/下单（[Digital Commerce 360](https://www.digitalcommerce360.com/2026/09/16/best-buy-opens-up-gift-buying-and-discover-through-chatgpt-ahead-of-holidays/)）。
- **欧洲**（整体晚于美国/中国）：**Frasers Group × Microsoft**（2026-01）推进 AI 驱动的零售搜索（据 EuroCommerce 整理）。
- **东南亚**：**Shopee × OpenAI**（2026-06）：Shopee App 进入 ChatGPT，覆盖 8 个市场（印尼、马、菲、新、泰、台、越 + 巴西），对话内拿推荐、点回 Shopee 结账（[TechNode](https://technode.global/2026/06/22/sea-limited-openai-to-jointly-expand-ai-access-for-e-commerce-shopee-users-sellers/)）。
- **中国**：**淘宝 × Qwen**（2026）：阿里把 Qwen 接入淘宝/天猫全量目录（40 亿+ 商品），助手可比价、下单，30 天比价器达目标价即**自动下单**（[阿里巴巴](https://www.alibabagroup.com/en-US/document-1991231293551017984)）。



---

## 2. 好的 prompt 是什么样的

**现有材料几乎都在讲「如何 prompt agent 让它工作更好」（系统/实验 prompt），而不是「真人实际在用什么样的 prompt」。**

### A. Agent / 实验 prompt

**A1. 截图式购物 agent 的系统指令**（[arXiv:2508.02630](https://arxiv.org/abs/2508.02630)）— 价格敏感、只看属性不看位置、先说理由再下单：
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

**A2. GEO 偏见实验的三种协议**（[arXiv:2606.17443](https://arxiv.org/abs/2606.17443)，Chu & Hou 2026, *Incumbent Advantage*）— 可直接作为实验骨架，均带强制输出格式：

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

**A3. Persona 示例（地理操纵）**同一人设，英文设在 California、中文译为 Shanghai，用地点信号做地理变量（[arXiv:2606.17443](https://arxiv.org/abs/2606.17443)）：
```
English: I'm a 25-year-old male programmer with oily, acne-prone skin. My face and scalp get greasy easily. I live in California.

Chinese (translation): I am a 25-year-old male programmer with oily acne-prone skin; my face and scalp get greasy easily. I live in Shanghai.
```

### B. 真人实际意图 / query（只有零散侧写，没有系统语料）
- 行业观察到的自然语言需求（来源：[Grocery Dive《5 takeaways from Groceryshop》, 2026](https://www.grocerydive.com/news/takeaways-groceryshop-conference-2026-las-vegas/831421/)、[Coresight Research·Groceryshop 2026 Day Two 回顾](https://coresight.com/research/groceryshop-2026-day-two-ai-moves-into-action-as-retailers-redefine-value-and-commerce/)；及 [Grocery Dive《Kroger leans on AI…》, 2026-09-23](https://www.grocerydive.com/news/kroger-ai-technology-groceryshop/831102/)）：
  - "冰箱里这些食材能做什么晚餐"
  - "给我一份孩子爱吃的健康餐，40 美元以内"（*a healthy meal my kids will like, under $40*）
  - 策划儿童生日派对、找齐某道餐的食材、管理饮食限制、在 SNAP（补充营养援助计划）资格限制下购物
- 趋势：从「搜具体 SKU」转向「解决问题」（DoorDash）；对话式界面让用户提开放式问题，可能比 feed/search 更分散曝光。

### D. 真人怎么问（query 模式，非购物专用；2026-10-28 整理）
- **AI Mode 查询 ≈ 传统搜索的 3 倍长**，追问量每月 +40%；开头词偏 what / how / I / is / can（用 "I" = 把它当对话）；"which" 类解决得快约 40%（多是 "which of / which one"）；"where should I" 和 "ideas for" 在上升。
- **Amazon Rufus 的四类问题**（[Amazon](https://www.aboutamazon.com/news/retail/how-to-use-amazon-rufus)）：单品（好不好清洗？是不是 clean beauty？）、比较（燃气 vs 柴火烤箱？）、查自己订单（上次买防晒是什么时候？）、场景驱动（办夏日派对要备什么？）。
- **OpenAI 购物**（[OpenAI](https://openai.com/index/chatgpt-shopping-research/)）：简单问（价格、单一特性）vs 深度问（多项比较、多约束、权衡）；深度问集中在参数多的品类——电子、美妆、家居园艺、厨房、运动户外。

### C. 哪里能找到真人 prompt（来自数据集清单）

**我们要的数据**：**Prompt**（真人问，或由真实问题仿真）×**Reply**（当时给出的回答，或事后重跑）×**Content**（购物相关、回答里带产品推荐）

已有的：

- **ConsumerQ**（公开，[arXiv:2609.18729](https://arxiv.org/abs/2609.18729)）：专门从 LMSYS/WildChat 抽出真人求购请求，2,528 条请求里 117 条实物产品 query，**附录带编码手册**。

**真人捐赠的完整对话历史**
- **InVivoGPT**：300 用户 / 138K 对话（[arXiv:2602.01114](https://arxiv.org/abs/2602.01114)）。
- **荷兰 D3I/Port** 数据捐赠（[uu.nl](https://www.uu.nl/en/organisation/methodology-and-statistics/data-donation)）。
- **Global South 语料**：1,252 用户 / 202,590 对话，印度/巴基斯坦/巴西/尼日利亚（[arXiv:2609.38279](https://arxiv.org/abs/2609.38279)）。
- **SparkToro × Gumshoe**：600 志愿者、12 意图、2,961 回答，公开（[blog](https://sparktoro.com/blog/new-research-ais-are-highly-inconsistent-when-recommending-brands-or-products-marketers-should-take-care-when-tracking-ai-visibility/)）。

**公开语料，但要先过滤出购物子集**
- **WildChat-4.8M**：约 275 万对话，标 `purchasable_products`（[HuggingFace](https://huggingface.co/datasets/how2everything/WildChat-4.8M)）。
- **Search Arena 24k**（[HuggingFace](https://huggingface.co/datasets/lmarena-ai/search-arena-24k)）。
- **ShareChat**：142,808 对话，多平台（[arXiv:2512.17843](https://arxiv.org/abs/2512.17843)）。


**缺口**：① **不是购物专用**，购物子集要靠过滤且日期旧；② 几乎没有**为"购物 prompt"本身设计**的语料；③ "真人 prompt + 真人当时看到的回答"两头都真实的仍少

### 数据源 / 工具（付费；测量级与采集）
- **Grips Intelligence**（[方法论](https://gripsintelligence.com/data-methodology)）：每个产品 × 零售商 × 天一条，含渠道销量（如经 ChatGPT 引流的部分）——可看 AI 引流的真实成交量级（亦是 §1「是不是 trend」的量化证据）。
- **Similarweb · AI chatbot traffic**（[链接](https://aisearch.similarweb.com/ai-chatbot-traffic/)）：任意网站的 AI 聊天机器人引流量。
- **Ahrefs Brand Radar · AI responses API**（[文档](https://docs.ahrefs.com/en/api/reference/brand-radar/get-ai-responses)）：抓 AI 回答里的品牌与引用链接（其 prompt 是改写的搜索词，非真人输入）。


---

## 3. CS 的人们在研究 shopping AI 的哪些方面，什么结论

目前 vault 覆盖到的 CS 侧工作主要围绕**推荐偏见与 agent 行为**。

### GEO（生成式引擎优化）= 在产品描述里注入营销语言来影响 LLM 推荐
来源：[arXiv:2606.17443](https://arxiv.org/abs/2606.17443)（Chu & Hou 2026, *Incumbent Advantage: Brand Bias and Cognitive Manipulation Dynamics in LLM Recommendation Systems*）。

**三档偏见模板：**

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

**主要发现：**
1. **条件垄断（conditional monopoly）**：所有产品规格相同时，知名品牌 100% 获推荐（IAI = 10.0）；但竞品的星级评分优势一旦小于 0.1 分，垄断就消失。
2. **权威式营销语言**（含捏造的临床证据）会在「偏见盈余（bias surplus）」达到 **+0.17 分**时打破垄断，且各模型反应不一。
3. **多品牌 GEO 竞争的社会困境（social dilemma）**：所有品牌采用相同优化策略时，按收益代理指标，单个品牌收益从 **+0.802 跌到 +0.007**；未参与的品牌在测试中拿不到任何推荐。
4. **结论**：GEO 是一种正在重塑市场竞争格局的新兴营销实践。

### Agent 行为偏见
- 截图式购物 agent 研究里显式要求"忽略商品位置（Do not be influenced by the position of the product）"，说明 CS 在关注**位置/呈现偏见**对 agent 决策的影响（[arXiv:2508.02630](https://arxiv.org/abs/2508.02630)）。


### 学界实证论文
**一支：品牌推荐偏见 / 审计**
- **Evaluating Brand Retrieval and Ranking in LLM Recommendations**（Malthouse et al. 2026, [arXiv:2609.16304](https://arxiv.org/abs/2609.16304)）：把 LLM 推荐当作**随机的检索-排序过程**，6 个 LLM × 5 品类重复采样，测品牌出现概率与平均倒数排名（MRR）——发现推荐高度不稳定。
- **"Global is Good, Local is Bad?"**（Kamruzzaman, Nguyen & Kim, EMNLP 2024，[ACL Anthology](https://aclanthology.org/2024.emnlp-main.707/)）：15 国各 3 全球 + 3 本地品牌，构造 SAI/ASA 选择题与送礼任务，测 LLM 的**全球 vs 本地品牌偏见**。结论：GPT-4、Llama-3 等**一致地把正面属性给全球品牌、负面给本地品牌**；在 prompt 里声明用户所在国会触发 country-of-origin effect——更偏好该国本地品牌，方向甚至反转。

**另一支：购物对话 agent 的合成数据集**（NLP/agent 向：为训练 / 评测 agent 造数据）
- **Wizard of Shopping**（全称 *Target-Oriented E-commerce Dialogue Generation with Decision Tree Branching*；Amazon, ACL 2025, [arXiv:2502.00969](https://arxiv.org/abs/2502.00969)）：方法 **TRACER**——把生成锚定在"对话计划"（即产品搜索轨迹）上，两个 LLM 扮顾客/助手、按决策树展开，3,600 段（每域 1,200、均长 19.7 轮）。贡献：兼顾**大规模 + 自然**（既往数据集要么大而不真、要么真而太小），并证明能提升对话式 query 生成与商品排序。
- **ShopDial**（全称 *Bottom-Up Synthesis of Knowledge-Grounded Task-Oriented Dialogues*；[arXiv:2504.14375](https://arxiv.org/abs/2504.14375)）：首个**自底向上**合成的电商对话数据集——先生成产品 QA 对再缝合成对话，6 品类 × 1,000 段（含"信息不足"的 unknown 轮，更贴近真实）。评测：真实性/自然度/整体质量胜过自顶向下的 PLACES 基线，但连贯性/信息量/完整性略逊。

### 实证：AI 推荐是否真的改变消费者行为（2026-10-28 整理）
- **AI 推荐能推动购买（开放网络）**：当 AI 把一个**此前未接触**的品牌推荐给用户，7 天内该品牌搜索 **+4.3pp**、品牌官网访问 +2.4、零售页访问 +1.0；这条路径大多对 last-click 归因**不可见**。方法：opt-in 用户一个身份标签，把其 AI 对话与浏览时间线在个人层面对齐（如 14:00 在 ChatGPT 被推荐 "Garmin"、14:05 就去 Google 搜 "Garmin"）。（Iannelli & Ai 2026）
- **AI 在改变线上行为**：采用 LLM 约 20 周后，用户**传统搜索比采用前降 20%+**；大站扛得住，**小站出现明显流量流失**；展示广告曝光下降，重度网购者尤甚。（Padilla, Lam, Lambrecht & Hollenbeck 2025/26；Comscore 点击流，100 万+ 用户，2022–2023）
- **信任是逐步建立的**：通过一个动态的"信任校准（trust calibration）"过程。


---

## 4. 如果我们自己建数据库，如何保证 ① 独立性（没有历史）② 区域合理

### ① 独立性
一次 query 会不会被"上一条"或"别人那条"污染，来源分四层；真正的**跨查询串扰（carry-over）几乎只存在于前两层**，后两层是时间相关的噪声与漂移，不会把内容"带到下一条"：
1. **Context（上下文）**：同一会话里显式的对话历史。
2. **Account / product（账户与产品）**：记忆、个性化、地理与语言信号。
3. **Service（服务层）**：缓存、批处理、静默的模型更新。
4. **Statistical（统计层）**：同一 prompt 的重复采样能否当作 i.i.d.？

### 独立性的设计原则（建库即照此采集）
- **一次无状态 API 调用 = 一个观测单元**：一个 trial 一个全新请求、带完整 prompt。绝不在同一线程里跑多个 trial——多轮上下文会改变行为（Laban et al. 2025, *LLMs Get Lost In Multi-Turn Conversation*, [arXiv:2505.06120](https://arxiv.org/abs/2505.06120)：多轮比单轮掉约 **39%**）。例：Responses API 用 `store=false`，忽略 ChatGPT Memory 与聊天历史。
- **`temperature=0` + 固定 seed ≠ 确定性**：把输出当成"分布里的一个样本"——每个 prompt 重复采样，报告稳定性指标。
- **记录** model snapshot、日期、`system_fingerprint` 与全部参数：同名服务会在短期内漂移（Chen, Zaharia & Zou, *How is ChatGPT's behavior changing over time?*, [arXiv:2307.09009](https://arxiv.org/abs/2307.09009)）。
- **Consumer UI（ChatGPT 网页 / App）与 API 是两个不同的实验对象**（系统提示、审核、记忆、搜索、地理都不同）。要研究真实消费者看到什么，用 sock-puppet（受控账户）或登出态设计，并控制 IP 与语言。
- **按 prompt / item 聚类**：一个 prompt 重复 N 次 ≠ N 个独立观测。用 cluster-robust SE + 配对差分（Miller 2024, *Adding Error Bars to Evals*, [arXiv:2411.00640](https://arxiv.org/abs/2411.00640)；naive SE 可能低估不确定性 3 倍以上），逻辑同 `reghdfe ..., cluster()`。
- **每个 prompt × 条件重复 N 次**，报告一致率 TARr@N（raw）/ TARa@N（parsed）（Atil et al., *Non-Determinism of "Deterministic" LLM Settings*, [arXiv:2408.04667](https://arxiv.org/abs/2408.04667)）加方差与置信区间。
- **随机化 trial 顺序、在同一时间窗内交错各条件**（别"上午跑 A、下午跑 B"）；长周期采集按时间分块并加时间固定效应。
- **用多个语义等价的措辞 / 格式**，报告一个区间而非单条 prompt 的结果（Sclar et al., ICLR 2024, [arXiv:2310.11324](https://arxiv.org/abs/2310.11324)）。

### ② 区域合理——地理作为受控变量
- **模型层（API / 开源权重）**：几乎都靠 **prompt 注入**地理（国家人设、"assume you are from X"、目标语言提问），因为 API 调用本身不带终端用户位置（例：Kamruzzaman et al. 2024 的国家人设；GEO 实验的 California / Shanghai，[arXiv:2606.17443](https://arxiv.org/abs/2606.17443)）。
- **消费产品审计（ChatGPT 网页、Copilot、Gemini）**：用住宅代理 / VPN / 固定机构 IP + 浏览器语言设置（先例：AI Forensics / AlgorithmWatch 2023，VPN + 瑞士/德国住宅 IP + 语言分组，[报告](https://aiforensics.org/work/bing-chat-elections)；登出 ChatGPT vs API，[arXiv:2608.30052](https://arxiv.org/abs/2608.30052)）。
- **在 prompt 里声明国家**会把输出拉向本地，但带来**刻板印象**；Kamruzzaman et al.（2024, [ACL](https://aclanthology.org/2024.emnlp-main.707/)）的"country-of-origin effect"——声明用户国家会让模型更偏好该国本地品牌，方向甚至可能反转。
- **UI 与 API 分叉极大**（推荐来源可能几乎不重叠），所以只在 API 上得到的结论不能外推到真实用户（Kirgis et al. 2026, [arXiv:2604.06188](https://arxiv.org/abs/2604.06188)；Lipphardt et al. FOCI 2026, [Dual Standards](https://petsymposium.org/foci/2026/foci-2026-0004.php)；登出 vs API，[arXiv:2608.30052](https://arxiv.org/abs/2608.30052)）。
- **可用参数**：OpenAI web-search（[docs](https://developers.openai.com/docs/guides/tools-web-search)）与 Perplexity Sonar API（[docs](https://docs.perplexity.ai/guides/user-location-filter-guide)）都支持 `user_location`（国家、城市、region）。

### 技术隐患清单 H1–H7
> [!note]- 展开：建库时要显式处理 / 记录的 7 个隐藏状态来源
> | # | 隐藏状态来源 | 机制 | 证据 | 缓解 |
> | --- | --- | --- | --- | --- |
> | H1 | 同线程对话历史 | 前几轮进入上下文 | Laban et al. 2025（[arXiv:2505.06120](https://arxiv.org/abs/2505.06120)）; Tjuatja et al. 2024（[arXiv:2311.04076](https://arxiv.org/abs/2311.04076)） | 一 trial 一请求 |
> | H2 | 服务端会话状态（Responses API） | `previous_response_id` / `conversation` 在服务端串历史；`store` 默认保存 | [OpenAI conversation-state 文档](https://developers.openai.com/api/docs/guides/conversation-state) | `store=false`、不传串联参数，或用 Chat Completions |
> | H3 | ChatGPT Memory / 历史引用 | 记忆与蒸馏历史注入后续回答；删对话 ≠ 删记忆 | [OpenAI Memory 公告](https://openai.com/index/memory-and-new-controls-for-chatgpt/)（2024；2025-04/06 更新） | 用 API；若 UI 则登出或新账户关记忆 |
> | H4 | 账户元数据画像 | 系统把地区 / 设备 / 账龄 / 习惯喂给模型 | Simon Willison, *ChatGPT's new memory dossier* (2025)（[链接](https://simonwillison.net/2025/May/21/chatgpt-new-memory/)） | 新账户、固定设备与地区、记录 |
> | H5 | 记忆诱发的迎合（sycophancy） | 用户画像让模型更倾向认同 | Jain et al. 2025（MIT, [arXiv:2509.12517](https://arxiv.org/abs/2509.12517)） | 零上下文基线对照 |
> | H6 | 出口 IP / 查询语言 | 决定推荐哪个市场的商品 | [arXiv:2608.30052](https://arxiv.org/abs/2608.30052)（登出 ChatGPT vs API） | 固定并作为因子操纵 |
> | H7 | 接口层差异（UI vs API） | 系统提示 / 审核 / 搜索 / 格式不同 | Kirgis et al. 2026（*LLM Spirals of Delusion*, [arXiv:2604.06188](https://arxiv.org/abs/2604.06188)）; Encarnación et al.（AIES, [arXiv:2608.06202](https://arxiv.org/abs/2608.06202)）; Lipphardt et al.（FOCI 2026, [Dual Standards](https://petsymposium.org/foci/2026/foci-2026-0004.php)） | 由研究问题决定接口并报告选择 |



---

## 5. 深度文章摘录：AI 不会杀死品牌，只会暴露弱品牌（Joachimsthaler, 2026-10-23）

- **作者**：Erich Joachimsthaler（Vivaldi 创始人兼 CEO；与 David Aaker 合著 1997 HBR《Building Brands Without Mass Media》；著有 *The Interaction Field* 2020）
- **标题**：*AI Will Not Kill Brands, It Will Expose Weak Ones*
- **出处 / 日期**：Medium，2026-10-23。[原文](https://medium.com/@ejoachimsthaler/ai-will-not-kill-brands-it-will-expose-weak-ones-9b64de04e0c1)（正文经 RSS 全文抓取）

### 核心论点
- **"被 agent 看见 ≠ 被 agent 选择"**（Being visible to an agent is not the same as being chosen by one）。
- 流行预测：机器能更理性地比价/比参数/比评价 → 选择变客观、品牌不重要、价格与性能取胜。**部分对**（AI 让"选品牌的弱理由"更容易被戳穿，劣质品无处藏，大铺货保护力下降），**但结论错**：品牌不会消失，只是**门槛升高、工作内容变了**——"A brand now has to be built for a reader that never sees an ad."（品牌要为一个"从不看广告的读者"而建。）

### 开场实验：跑鞋（多轮 → demand space）
- 让 ChatGPT 推荐"第一次跑马拉松的最佳跑鞋"，先得到几个熟悉大牌。接着逐步加约束：预算、扁平足、纽约冬天在柏油路训练……**到第 4 个问题，最初排第一的品牌常常消失**，换成别的答案。
- 启示：每加一个约束，就把"品类问题"变成一个 **demand space**（谁在买、什么场合、什么约束、要达成什么结果）。

### 第一步：agent 得先能"读"你（machine legibility）
- agent 依赖结构化目录、产品 feed、已验证库存、价格、图片、顺畅的结账路径。**读不了/验不了/买不了，就进不了候选名单。**
- Adobe Q1 流量数据：相当一部分美国零售网站**还不能被给它们导流的模型完整读取**。[note 2 → TechCrunch Adobe 393%]
- Skift × McKinsey 旅行研究：把相同 travel prompt 给 5 个 AI 助手/在线工具，**没有一家酒店同时出现在全部 5 个答案里**。[note 3] → "可见性"不是一个数字，而是散落在各读法不同的系统里。
- 术语 **machine availability**：agent 能否看到产品、知道它是什么、查库存与价格、完成购买。这是"管道工程"，必要但不让人爱上品牌。**Being readable gets you into the race. It does not tell the agent why you should win.**

### 第二步：它会去找"证据"（evidence）
- **AI systems don't take a company's word for it.** 它从更广的市场拼出答案：评论、零售商、媒体、专家、社群、分析师、监管文件、客户体验、第三方数据库。**品牌不能再单方面宣称立场，得有别人替它背书。**
- 旧模型：造一句信息、重复到被记住。新模型：你提一个声明，agent 去核。说你最可靠→它调故障率与维修记录；说你高端→它问产品是否配得上价格；说你是全球银行最佳方案→企业 agent 翻实施案例、认证、安全史、集成要求、服务级别、TCO。**比 30 秒广告受到的审视多得多。**
- 品牌于是活在一片**大多不由公司拥有的证据场**里 = 作者说的 **Brand System**（品牌不是 logo/门店/campaign，而是整个系统）。[note 4 → WARC]

### 第三步：名气有用，但只到某个点
- **Chu & Hou（2026-06，arXiv:2606.17443）**[note 5]：测 GPT-4o-mini / Claude Sonnet / Gemini 3 Flash。选护肤（买前无法判断质量、依赖口碑）。
  - 规格完全相同时，**知名品牌每次都被推荐**；但给竞品**不到 0.1 星**的评分优势，这种统治就蒸发。
  - **权威式营销语言（含编造的临床声明）也能把在位者掀下来** → 系统可被操纵（作者赌这种操纵最终会被发现并惩罚）。
  - 当多个品牌都用同样的 GEO 手法，各自收益从 **0.802 崩到 0.007**，而不参与的品牌**一个推荐都拿不到** → 典型**囚徒困境**：人人必须玩，一旦都玩，没人赢。
- **Allouah, Besbes, Figueroa, Kanoria & Kumar（arXiv:2508.02630）**[note 6]：把 AI 购物 agent 放进受控市场，变动价格/评分/评论/位置/赞助标签/平台背书。**agent 对这些全都有反应**：给"赞助"标签打折扣、奖励平台背书、偏好最上面一行、有时比人类更把需求堆到少数几个产品上 → **agent 的选择也不是完全理性，只是另一种带自己怪癖的决策者。**
- 作者结论：**熟悉度在报价相同时值点钱，但挡不住更好的证据。名牌能打破平局；强 Brand System 让 agent 根本看不到平局。**（A famous brand can break a tie. A strong Brand System makes sure the agent never sees a tie in the first place.）

### 第四步：被看见 ≠ 被选择（GEO/AEO/"AI 可见度"太窄）
- 公司现在追踪"模型多常提到我 / 是否被引用 / share of model"——有用但是**中间指标**。历史重演：impressions 不是销售、clicks 不是偏好、engagement 不是经济价值，**AI 答案里的 citation 也不会是。**
- 旧代理指标在侵蚀：**Pew** 实测——有 AI 摘要时，人们点传统搜索结果的比例 **8%**，没有摘要时 **15%**。[note 7] 赢 click 的价值在下降；诱惑是换成"赢 mention"——但那是在"楼上"犯同样的错。
- **AIVO**（Tim de Rosen 创立，测"推荐"而非"提及"）：模拟买家开场问品类、多轮加需求、最后要推荐。[note 8/9]
  - **1,427 次 journey 中，品牌在早期答案出现 95.7%，但最终被推荐只有 12.7%。**
  - 20,000+ probes、200+ 品牌：助手在到达决策前，**把已经引用过的品牌丢弃的比例 87.3%。**
  - 相同 prompt 跑 3 次：**被引用的来源变化 95.8%**，**最终推荐的品牌只变 14.6%** → 大多数 dashboard 追的东西像弹珠乱跳，真正重要的几乎不动。
  - 作者的 caveat：AIVO 未经同行评审、且卖它倡导的测量；当作"强行业证据"而非定论，但方向与上面的学术研究一致。
- **导向推荐的 5 步序列**：
  1. **Machine legibility**：agent 能否读取、验证、交易该报价？
  2. **Evidence**：是否有独立信息支撑其声明？
  3. **Demand relevance**：对这个具体 demand space 是否合适（不只是品类）？
  4. **Trust**：信心是否足以不再继续搜索就行动？
  5. **Recommendation**：agent 是否判定"这就是答案"？

### 一个"只在测第一步"的十亿美元行业
- 测 AI 可见度两年内成行业：2024–2025 成立的 7 家创业公司到今秋募近 **5 亿美元**，大头给 **Profound（9 月估值 18 亿美元）**；Semrush、Ahrefs、Similarweb、HubSpot 都加了 AI 追踪。[note 10] **几乎全在测第一步**（提及、引用、情感、share of voice）。
- 少数在往后走：OH-SO 的 **RAIDAR.GEO**（追哪些来源支撑/削弱品牌=证据步）、**ARA**（Jared Richardson；问模型是否建立了准确且独特的品牌认知）、**AIVO**（测品牌是否存活到最终推荐）。[note 11]
- **工具不重要，顺序才重要**：每步都是下一步的必要非充分条件；"被找到但没被佐证、被佐证但没被理解、被理解仍没被选"。只有最后一步进入收入，其余是诊断。

### 被选"在要紧处"（demand space 加权）
- 被选不是一个数字：agent 总在某个**情境 = demand space** 里选。一个品牌可能在**小的/慢的/不赚钱的** demand space 里常被选，却输掉那些**承载经济价值**的。跨所有 prompt 的平均胜率恰好会掩盖这点。**要紧的是在对的 demand space 里被选、按各自价值加权。**

### 品牌 = 让你停止搜索
- Skift×McKinsey 日记：用 AI 找/比选项的旅客，仍回头查评论、朋友、OTA、酒店官网来复核；**近一半人在已经订了之后又改了酒店。**[note 3] AI 降低信息成本，但不消除不确定性，有时反而增加（更多选项、更多比较、更多理由重开已定的决策）。
- **强品牌让你停止搜索**——这是经济表述：**降低搜索成本与决策风险，人愿为降低风险付费**，这就是为什么即便每个规格都一键可查，品牌溢价仍存活。

### 谁拥有这个 agent？（三方之争）
- 多数讨论默认 agent 为顾客服务，其实有三种，争夺已开始：
  1. **顾客自己的 agent**：ChatGPT、Gemini、Perplexity 的 Comet 浏览器，代她搜与买。
  2. **平台的 agent**：两大美国零售商路径迥异——**Amazon** 封锁来自 OpenAI/Google/Perplexity 的 agent，2 月起诉 Perplexity（Comet），9 月起阻止经 Meta Muse 的购买；同时自建 **Rufus**（一份分析称带来近 **120 亿美元**增量年化销售）与 **Buy for Me**（在其它商家站点完成购买）。**Walmart** 反向：与 OpenAI、Google 都合作（可在 ChatGPT、Gemini 里买沃尔玛商品），自营助手 **Sparky**，10 月 21 日开放**邀请制 Agent Gateway**，按沃尔玛条款、经 Sparky 放外部 agent 进来。[note 12]
     - 分析把分歧归于**经济而非理念**：Amazon 的 **686 亿美元**广告业务靠赞助位，顾客 agent 可直接忽略；Walmart 广告业务小得多，开放代价更低。**谁拥有 agent，谁决定哪些信号算数。**
  3. **供应商自己的 agent**：Brian Chesky——"我设想有一天 Airbnb app 本身变成一个 agent"，把竞争描述为争当"quarterback"（你凡事都经过的主 agent）；坦言 Airbnb 在新消费 agent 上"还不行"（"I've used Airbnb on Muse and Instinct. And it doesn't work very well."）。[note 13]
- **Sangeet Paul Choudary** 的框架[note 14]：今日 agent 是 **agentic participants**——各代表市场一方，买方 agent 仍只能从卖方已固定的报价里挑。"Markets are relationships between economic actors, while most agents today represent only one actor." 真正变化来自 **agentic markets**（买卖双方 agent 共同搭成交易）。
- → 一个品牌现在被**三个有不同议程的 agent** 读：顾客 agent 找最佳答案、平台 agent 护平台经济、公司自己的 agent 为品牌谈判。Brand System 要在三者面前都站得住。

### 从"推荐"到"谈判"
- 目前一切（连最聪明的测量）仍是"顾客 agent 从公司已发布的报价里选"。但方向在变、轨道在快速铺设：
  - **Google UCP（Universal Commerce Protocol）** 1 月随 Walmart、Shopify、Target 等推出，之后加了支付层（agent 可在用户设限内付款）；Amazon、Meta、Microsoft、Salesforce 已加入其技术委员会。[note 15]
  - 9 月最忙：**Stripe** 让每个托管结账页 agent-ready；**Shopify** 默认开启 agent 结账；**Meta Muse** 开始在 100 万+ 商家买东西。
  - 未settled：**OpenAI 3 月撤回了 in-chat Instant Checkout（上线 6 个月后）**；agent 目前只涉及约 **3%** 的商家交易；只有 **28%** 商家愿意按与其它渠道相同条款向 agent 开放全部货品。（28% 来自 PYMNTS 商家调查，3% 来自 Checkout.com）
- 一旦你自己的 agent 坐上谈判桌，**推荐不再是终点，而是谈判的开始**：问题从"是否被选"变成"为被选你放弃了什么"——**目前没人在测这个。**

### 品牌 = 给你自己 agent 的指令
- agent 对agent 市场里，公司的 agent 要决定：提供什么、怎么打包、价格能让多少、保护体验的哪些部分、拒绝什么。Choudary 补一条关键条件：这些 agent 需要**提交产能、条款、取舍的授权**，不只是给建议。[note 16]
- 此时**品牌不再只是顾客 agent 读的信号，而是你自己 agent 据以行动的一套指令**。作者去年在 WARC 提出品牌建设已从静态定义/一次性 campaign 转向 **Brand Operating System**（编排与顾客的持续互动）；企业 agent 让它变得可执行。[note 4]
- agent 要知道：品牌为哪些 demand space 而建、在哪有权赢、哪可延展、哪可让步、哪绝不妥协、能撑什么价、有什么证据背书。**漏掉这些，agent 就会优化最容易的——几乎总是价格**：那就是"用极高效率一次次理性让步地把品牌拆掉"。
- 且**不是一套指令**：让步取决于所处 demand space——品牌对买家目标**核心**处要守价护体验、**边缘**处可让/打包/走开。到处同样谈判的 agent 会"赢错的生意、送走对的生意"。

### 三个品牌案例（能被 agent 读的"系统"）
- **LEGO**[note 17]：品牌不是塑料砖上的 logo，而是一个系统——产品、玩法逻辑、授权与原创故事、儿童与成人社群、零售、媒体、粉丝创作、教育、几代信任，各部分互相增值（interaction field）。agent 判断 LEGO 是否适合某情境，靠的是系统深度（独自搭还是亲子？复刻电影场景还是自创？收藏还是啃 Technic？或成人只想离屏两小时）——相关性取决于 demand space,不是品类"玩具"。
- **Airbnb**：品牌让陌生人彼此信任（睡进陌生人家/让陌生人睡你家）——身份核验、双向评价、支付处理、房东房客保护、服务补救降低不确定性。agent 推荐一次入住，就是在**默默为这整套背书**。
- **Rolls-Royce TotalCare**[note 18]：航司按"每发动机飞行小时"付费，劳斯莱斯承担维护风险——商业模式对齐航司真正在意的"让飞机在天上"。背后是全机队预测性监控、深工程、全球服务、装机知识、数十年问责。**采购 agent 能比推力和油耗,但无法把"数十年的风险转移"压进规格表**；高风险 B2B 里，降低感知风险常比改进规格更值钱,而品牌正是风险降低的所在。→ **B2B 品牌在 agentic 市场里可能更重要，而非更不重要。**

### 给领导层的三问
1. agent 能否准确读取、验证并交易我们的报价？
2. 有什么**独立证据**显示我们的品牌对某个具体 demand space 合适？
3. 我们自己的 agent 能否**按 demand space 逐一**说清：品牌可提供/可让步/可延展/须拒绝什么？

> 结语：AI 不会杀死品牌，但会暴露那些只靠广告投放、铺货或单纯熟悉度、却没建更深"被选理由"的品牌。**信息遍地时，意义更值钱；比较无成本时，信心更值钱。** 过去品牌的难题是"如何被知道"，现在是"如何在要紧的 demand space 里、以你负担得起的条款，成为那个答案。"

### 对本项目（AI 购物数据集）的用处
- **直接证据（§3 推荐 vs 提及、agent 偏见）**：AIVO 的 95.7%→12.7%、来源变 95.8% 而推荐只变 14.6%、87.3% 掉落；Allouah et al. 的 agent 对赞助/背书/位置/需求集中的反应。→ 强化"mention≠chosen"、重复采样必要性（呼应 §4）。
- **多轮改变推荐（§2 query）**：跑鞋实验——加约束到第 4 轮，首位品牌常消失 = demand space 决定推荐；与 §2「真人怎么问」互证。
- **demand space 作为分析单元**：建库时"被选"要按 demand space 分层、按价值加权，不能用跨 prompt 平均胜率。
- **"谁拥有 agent"三方**：顾客/平台/供应商 agent，补强 §1 供给侧与「谁拥有客户」之争。
- 同一批论文已在 dataset 笔记：Chu & Hou(2606.17443)、Allouah et al.(2508.02630)、Pew、Adobe 393%、UCP。

---

### 全部引用与链接（note 1–18，原文照录）
1. David A. Aaker & Erich Joachimsthaler, *Building Brands Without Mass Media*, Harvard Business Review 75(1), Jan–Feb 1997.（无在线链接）
2. Adobe Analytics Q1 2026 零售流量，转引自 *AI traffic to US retailers rose 393% in Q1…*, TechCrunch, 2026-04-16 — https://techcrunch.com/2026/04/16/ai-traffic-to-us-retailers-rose-393-in-q1-and-its-boosting-their-revenue-too/
3. Skift Research & McKinsey, *Winning Hearts in an Age of Infinite Travel Choices*, 2026-09。McKinsey 新闻稿 2026-10-08 — https://www.mckinsey.com/de/news/presse/2026-10-08-reiseplanung ；ANI 报道 2026-09-26 — https://www.newkerala.com/news/a/travel-industry-may-need-prioritise-continuity-trust-as-499.htm
4. Erich Joachimsthaler, *Reinventing Brand Strategy: The Holistic Brand Model*, WARC Exclusive, 2025-09-21 — https://www.warc.com/content/article/warc-exclusive/reinventing-brand-strategy-the-holistic-brand-model/en-gb/161714
5. Xi Chu & Yupeng Hou, *Incumbent Advantage: Brand Bias and Cognitive Manipulation Dynamics in LLM Recommendation Systems*, arXiv:2606.17443, 2026-06 — https://arxiv.org/abs/2606.17443
6. Amine Allouah, Omar Besbes, Josué D. Figueroa, Yash Kanoria & Akshit Kumar, *What Is Your AI Agent Buying? Evaluation, Implications and Emerging Questions for Agentic E-Commerce*, arXiv:2508.02630, 2025 — https://arxiv.org/abs/2508.02630
7. Pew Research Center, *Google Users Are Less Likely to Click on Links When an AI Summary Appears in the Results*, 2025-07-22 — https://www.pewresearch.org/short-reads/2025/07/22/google-users-are-less-likely-to-click-on-links-when-an-ai-summary-appears-in-the-results/
8. AIVO Journal Editorial Board, *Appeared in 96% of Journeys, Chosen in 13%*, 2026-09-28（未经同行评审）— https://www.aivojournal.org/appeared-in-96-of-journeys-chosen-in-13/
9. AIVO Journal Editorial Board, *Profoundly Wrong: Why AEO (and GEO) Are Not the Answer*, 2026-10-15 — https://www.aivojournal.org/profoundly-wrong-why-aeo-and-geo-are-not-the-answer/ ；Paul Sheals & Tim de Rosen, *The AIVO Standard Methodology, Version 4.1: From Visibility to the Decision*, 2026-09-11 — https://www.aivojournal.org/the-aivo-standard-methodology-version-4-1-from-visibility-to-the-decision/
10. Dealroom, *Generative Engine Optimization Startups*（数据截至 2026-09-18）— https://dealroom.co/charts/generative-engine-optimization-startups ；Sacra, Profound 公司档案 — https://sacra.com/c/profound ；Similarweb AI brand visibility — https://aisearch.similarweb.com/de/ai-brand-visibility/ ；Semrush — https://www.semrush.com/blog/which-tools-help-benchmark-my-ai-visibility-against-competitors/ ；Ahrefs 新闻稿 2026-01-20 — https://businesswire.com/news/home/20260120714417/en/Ahrefs-Launches-Custom-AI-Prompt-Tracking-for-Brand-Visibility
11. OH-SO Digital, RAIDAR.GEO — https://oh-so.com/raidar-geo/en ；ARA, *Does AI trust your brand?* — https://araco.ai/ ；AIVO 见 note 8。
12. Ivinco, *Amazon's Walled Garden and AI Shopping*, 2026 — https://www.ivinco.com/blog/amazon-walled-garden-ai-shopping ；Digiday, *Amazon quietly blocks more of OpenAI's ChatGPT web crawlers…*, 2025-11 — https://digiday.com/media-buying/amazon-quietly-blocks-more-of-openais-chatgpt-web-crawlers-from-accessing-its-site/ ；FinTech Weekly, 2026-10-04 — https://www.fintechweekly.com/magazine/articles/agentic-commerce-launch-month-liability-risk-2026 ；ActuIA, *Walmart sets the rules for AI shopping agents*, 2026-10-21 — https://actuia.com/en/news/walmart-sets-the-rules-for-ai-shopping-agents
13. Ivan Mehta, *Brian Chesky interview: AI agents need their own operating system*, TechCrunch, 2026-10-01 — https://techcrunch.com/?p=3172101
14. Sangeet Paul Choudary, *Agents — and Their Better Half*（Part 1: From Agentic Participants to Agentic Markets）, 2026-10-04 — https://platforms.substack.com/p/agents-and-their-better-half
15. *Google I/O 2026: UCP and AP2 Define Agentic Commerce*, Efficiently Connected, 2026 — https://www.efficientlyconnected.com/google-io-2026-agentic-commerce-protocols-ucp-ap2/ ；*Agentic Commerce Had Its Biggest Launch Month. Nobody Wants to Own the Risk*, FinTech Weekly, 2026-10-04 — https://www.fintechweekly.com/magazine/articles/agentic-commerce-launch-month-liability-risk-2026 （28% 来自 PYMNTS 商家调查，3% 来自 Checkout.com）；Nuvei, *OpenAI tried to check out. It couldn't*, 2026 — https://www.nuvei.com/posts/openai-tried-to-checkout-it-couldnt
16. Sangeet Paul Choudary, *How Agents Unlock New Markets*（Part 2 of *Agents, and Their Better Half*）, 2026-10-11 — https://platforms.substack.com/p/how-agents-unlock-new-markets
17. Erich Joachimsthaler, *The Interaction Field: The Revolutionary New Way to Create Shared Value for Businesses, Customers, and Society*, PublicAffairs, 2020.（书）
18. Rolls-Royce, *The Trent 1000 XE with TotalCare: Engineered for More*, 2026 — https://www.rolls-royce.com/media/our-stories/discover/2026/the-trent-1000-xe-with-totalcare-engineered-for-more.aspx ；Rolls-Royce, TotalCare agreement with T'way Air, 2022-06-22 — https://www.rolls-royce.com/media/press-releases/2022/22-06-2022-poweroftrent-rr-signs-totalcare-agreement-with-south-korean-airline-tway.aspx

---

### 链接完整摘录（逐条抓取）

#### [note 8] AIVO Journal — *Appeared in 96% of Journeys, Chosen in 13%*（2026-09-28）
- 语料：**25,000+ 多轮 probes、250+ 品牌**，基于 **20 亿+ 真实用户 prompt**。隔离分析 **1,427 条 journey**。
- **品牌在早期答案出现 95.7%，最终被推荐仅 12.7%。**
- 核心命题："Appearance and recommendation are separate states in an AI-mediated decision."——可见度(96%)与真实推荐(13%)的落差说明行业在测**错的结果变量**。
- 结论：早期排名对购买决策的预测力不足；品牌要测的是**在多轮对话里（买家需求累积、可行选项被重塑）能否存活**。
- 方法：AIVO "AI Win-Rate Methodology v1.0"（Zenodo DOI: 10.5281/zenodo.22280231）。
- 背景数据：Profound Series D **1.8 亿美元 @ 18 亿估值**、1,000+ 企业客户（含 1/3 财富 100）。

#### [note 9] AIVO Journal — *Profoundly Wrong: Why AEO (and GEO) Are Not the Answer*（2026-10-15）
- **95.8%**：相同 prompt 重复 3 次时**被引用来源**变化率（1,800 个品牌级分组、各跑 3 次）。
- **14.6%**：相同条件下**最终推荐品牌**变化率。**85.4%**：三次结果完全一致的分组占比。
- **87.3%**：AI 在到达推荐前**丢弃此前已引用品牌**的比例。（20,000+ probes、200+ 品牌）
- 论点：AEO/GEO 的前提（引用频率可靠预测 AI 推荐）不成立——"citation frequency is not a stable or reliable enough proxy for recommendation behaviour to manage a brand against."
- 判据金句："If a metric changes when nothing has changed, it cannot measure improvement." + "A brand present in the opening response was usually gone by the time the AI system made its choice."
- 替代方案：**AI Win-Rate**（多轮、重复跑、对照既定客户标准测推荐频率）。方法 v2.0：Zenodo records/22663407。

#### [note 6] Allouah, Besbes, Figueroa, Kanoria & Kumar — *What Is Your AI Agent Buying?*（arXiv:2508.02630；2025-08 提交、2025-12 修订）
- 框架 **ACES**（provider-agnostic，审计 agent 决策）。摘要要点：
  - **选择同质化 / 需求集中**：agent 常把需求堆到少数"modal"产品上、完全忽略其它。
  - **偏好不稳定**：模型更新会剧烈重排市场份额。
  - **位置偏见强**：随 provider 与版本变化，连纯文本 "headless" 界面也存在——"top rank"无普适意义。
  - **一致地惩罚"赞助(sponsored)"标签、奖励"平台背书(platform endorsements)"**；对价格/评分/评论的敏感度各模型差异大。
  - **卖方可反制**：seller-side agent 做简单的、随 query 条件变化的描述微调，就能显著拉高市场份额。
  - 结论：agentic 市场**波动大、与以人为中心的商务根本不同**，需持续审计；对平台设计/卖方策略/监管提出新问题。

#### [note 12] Ivinco — *Amazon's Walled Garden and AI Shopping*（2026）
- **Amazon（封闭）**：Rufus 2025 年 **3 亿+** 用户用过、带来近 **120 亿美元**增量年化销售、假日期转化率 **3.5×**、互动同比 **+210%**；GMV **8,300 亿**、广告收入 **686 亿**（Q4 单季 213 亿、+23%）。封锁 ChatGPT-User / OAI-SearchBot（2025-11）与 Google agent；2025-08 曾令 ChatGPT 导流 Amazon **环比 -18%**。Shop Direct（1 亿+ 商品 / 40 万商家）、Buy for Me（外站自动结账）；180+ 商家称被未经授权上架。Alexa+ 2026-02-04 全美上线（Prime 免费 / 单售 $19.99/月、可无确认自动下单）。
- **Walmart（开放）**：Sparky 用户下单比非用户**大 ~35%**、约 **50%** app 用户试过；加入 UCP，与 OpenAI、Google 合作（可在 ChatGPT/Gemini 买沃尔玛商品）。
- **法律先例 Perplexity v. Amazon**：2026-03-09 联邦法官 Maxine Chesney 依 CFAA 禁 Perplexity 的 Comet 访问 Amazon（"强证据"表明未授权访问，裁定需**平台授权**、用户许可不够）；**2026-10 第九巡回法院撤销该禁令**。
- **经济解释**：AI agent **绕过赞助位**，威胁零售媒体搜索广告（~**380 亿**市场）；Amazon 686 亿广告收入形成"排斥外部 agent"的结构性动机，Walmart 广告小故能开放。Jassy（Q4 2025 财报电话）："a lot of customers are ultimately going to choose to use a great shopping agent from that retailer."

#### [note 14] Sangeet Paul Choudary — *Agents and Their Better Half*（Part 1，2026-10-04）
- **agentic participants**（用智能在既有市场机制内代表委托人）vs **agentic markets**（多方都用 agent 表达目标 → 决定"报价本身如何被做出"，而非只从既有报价里选）。
- 金句："Markets are relationships between economic actors, while most agents today represent only one actor in that relationship."
- **不对称问题**：消费侧 agent（如 Muse）对买方偏好理解丰富，却只能通过静态目录/feed/API 接触供给侧 → "lopsided agent economy"，导航变好但市场机制没变。
- 双方都有 agent 时：从"买方在预制报价里选"→"双方共同**构造可执行的报价**"。三例：招聘（两套目标与约束的互动）、旅行（represented 双方谈判产定制方案）、B2B 采购（供应商 agent 分析产能与利润→自适应响应）。
- 框架：Agentic AI Observatory（reshufflebook.com/agentic-ai-observatory/）。

#### [note 16] Sangeet Paul Choudary — *How Agents Unlock New Markets*（Part 2，2026-10-11）
- 核心：agent 的主要价值不是让既有交易更高效，而是**让原本不会发生的交易变得经济可行**——"Commercial arrangements that were previously too expensive to negotiate became economically worthwhile."
- **三个必要条件**：① **操作授权**（agent 要能真的预留产能/承诺交期，不只解释选项；买方 agent 要能授权可接受的取舍）；② **理解底层需求**而非表面规格（"What buyers ask for and what sellers offer are often simplified versions of what they actually need and what they could provide."）；③ **跨组织协调机制**（互相发现、交换提案、验证、达成双方可执行的协议）。
- **真实案例（规模）**：Walmart 用 AI 对 **10 万+ 供应商**逐一谈标准化条款（过去不划算）；Honeywell **2,500+ 自主谈判、覆盖 5 亿美元**支出；Circle Logistics **18%** 货运订舱无人工完成；Anthropic *Project Deal* **69 名员工的 agent 谈成 186 份真实协议、价值 4,000 美元+**。
- **三种市场扩张机制**：解锁潜在需求（为稀缺技能组合重设岗位）、解锁潜在供给（酒店按运营弹性提供非标房/服务组合）、跨供应商再打包。
- 一句话区分："An agentic participant becomes more effective … within an existing market. An agentic market can … expand the opportunities that become available for exchange in the first place."

#### [note 3] Skift × McKinsey 旅行研究（经 newkerala/ANI 转述；McKinsey.de 原稿抓取超时）
- 旅行触点：**2026 年 65 个 vs 2018 年 45 个**；**71%** 旅客愿用 AI 找灵感；**86%** 未来会考虑 AI 预订；60% 把社媒列入前三灵感源；样本 1,000+ 美国旅客 + 旅行日记。
- **相同 query 给 5 个 AI/OTA 工具，没有一家酒店出现在全部 5 个答案里**；**约一半**旅客在订房后又因发现更好选项而改订。
- 金句："Always-on inspiration creates more entry points, but trust determines which ideas gain momentum." → 订房确认不再是客户关系的终点。

#### [note 15a] UCP / AP2（Efficiently Connected，Google I/O 2026）
- **UCP（Universal Commerce Protocol）**：开源标准，支持 agent 跨"发现→验库存→结账→售后追踪"的 agent-to-agent 通信。
- **AP2（Agent Payments Protocol）**：加密、代币化的护栏——"tamper-proof token bound to a specific SKU, merchant, and spending cap"，在用户设定的策略参数内自主执行支付。
- Tech Council（本文列）：Amazon、Meta、Microsoft、Salesforce、Stripe。**Universal Cart** 进入 Google Search 与 Gemini app，接 Google Wallet。
- ⚠️ 与 Joachimsthaler 原文小出入：原文说 UCP"1 月随 Walmart/Shopify/Target 推出"，此文归为"Google I/O 2026 发布"且未把 Walmart/Shopify/Target 列入 Tech Council——时间线/成员表两处口径不一，引用时注明。

#### [note 15b] Nuvei — *OpenAI tried to check out. It couldn't*
- OpenAI Instant Checkout：**2025-09 上线**（Stripe 支撑，2026-01 曝出对成交收 **4%** 费），**2026-03 关停**/弱化原生 in-chat 结账。官方："We are evolving our commerce strategy within ChatGPT to better meet merchants and users where they are."
- 数据：familiar 用户里**仅 8%** 真用它买过；Forrester——**10%** 在线成年人用过 AI agent 购买、**61%** 不愿用 AI agent 买、**33%** 过去三个月用 AI agent 找/比产品；ChatGPT 周活 **9 亿**（2026 初）。Shopify 的 AI 导流自 2025-01 **×7**、AI 归因订单 **×11**。
- 失败归因（四层基建没人同时搞定）：实时产品 feed、授权时可验证的同意、针对 agent 行为的反欺诈、端到端税务/合规/争议处理。
- ⚠️ 注意：Joachimsthaler 原文的"agent 仅涉 3% 商家交易、28% 商家愿开放"来自 FinTech Weekly（PYMNTS/Checkout.com），与本文 Nuvei 的 8%/10% 口径不同，分别标注。

#### [note 12b] ActuIA — *Walmart sets the rules for AI shopping agents*（2026-10-21）
- Walmart 对在 Walmart.com / Sam's Club 购物的 agent 定三件套：**Agent Profiles**（账户内每个授权 agent 独立档案、可见订单与审批）、**Walmart Agent Gateway**（技术入口，走 **MCP**）、**Terms of Use**。
- 规则：花费上限可选"逐单审批"或 **$50 / $100 / $200** 封顶；**数据最小化**（数据留在零售商，只给任务所需）；**定价**——"We set the price of products, not of people."（agent 看到与人相同的价）；**默认需审批**，即便在额度内 Walmart 也保留追加验证的权利；**不合规的 agent 直接封禁**。Gateway 现为邀请制 early beta、可随时暂停。

#### [note 13] Brian Chesky 访谈（TechCrunch，Ivan Mehta，2026-10-01）
- 真实链接：https://techcrunch.com/2026/10/01/brian-chesky-interview-ai-agents-need-their-own-operating-system/
- 观点：行业缺真正为 AI 建的 OS（当前只是在 iOS/macOS/Windows 上做 AI app）——"no one is developing a full operating system software developer kit"；主张 AI 在 kernel 层、组件可互操作。
- "the Airbnb app as one day becoming an agent … interoperable with MCP"；争当 "quarterback"（凡事都经过的主 agent）。
- 坦诚："I've used Airbnb on Muse and Instinct … doesn't work very well … even hotels don't work that well."

#### 其余链接（工具 / 融资 / 营销 / 付费墙页；要点已在正文内联，未逐页深抓）
- note 2 TechCrunch Adobe 393%、note 5 arXiv:2606.17443、note 7 Pew（8% vs 15%）——均已在本项目 dataset 笔记完整收录。
- note 10 融资/工具：Dealroom（GEO 创业公司、~5 亿美元）、Sacra（Profound 档案）、Similarweb / Semrush / Ahrefs（AI 可见度工具）、Ahrefs 新闻稿（Custom AI Prompt Tracking）。
- note 11 工具：OH-SO RAIDAR.GEO、ARA（araco.ai）。
- note 4 WARC（*Reinventing Brand Strategy*，付费墙）、note 17 书（*The Interaction Field*, 2020）、note 18 Rolls-Royce TotalCare（营销页，要点见正文案例）、note 1 HBR 1997（无在线版）。
- 需要我把以上任意一条也逐页深抓的话再说。
