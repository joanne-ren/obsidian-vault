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
- **McKinsey × ICSC**（美国，2026-04，3,004 名消费者 + 高管访谈）：过去 3 个月 **68%** 用过至少一种 AI 工具；预计 agentic commerce 到 2030 年达约 **1 万亿美元**。（[ICSC × McKinsey《Shopping in the Age of AI》](https://www.icsc.com/news-and-views/icsc-exchange/icsc-mckinsey-company-release-shopping-in-the-age-of-ai-redefining-stores-for-a-new-era-report)）
- **BCG**（Consumer Radar，2025/26）：购物是生成式 AI 的**第三大用途**；2025-02 至 11 购物类使用 **+35%**；60%+ 高度信任 GenAI 输出；印度 **64%** 在购买过程中使用。（[BCG《Consumers Trust AI to Buy Better》](https://www.bcg.com/publications/2026/consumers-trust-ai-to-buy-better-brands-must-adapt)）
- **在旅程中的角色**（*Shopping with a Platform AI Assistant*，Ctrip「Wendao」3100 万用户，[arXiv:2603.24947](https://arxiv.org/abs/2603.24947)）：AI 对话与传统搜索在同一阶段**互换使用、彼此补充**；约 **42%** 的请求是探索型（attraction / destination 类）。


"人们在用 AI 购物"成立，但目前主要集中在**发现/评估**环节，自主下单仍是早期。

### 供给侧：区域部署全景
平台与零售商正大规模把商品目录接进 AI 入口，与上面的消费者采用数据互补（铺得多 ≠ 用得多）。连接标准正在成形：**UCP（Universal Commerce Protocol）**，Google + Shopify 于 2026 年初推出的开放 AI-商务标准，商家暴露一个标准接口，AI 实时读库存、套会员折扣、代顾客在对话内一键结账（[UCP](https://developers.google.com/merchant/ucp)）。

- **美国**（最领先）：
  - **Target × OpenAI**（2025-11）：Target 商品可在 ChatGPT 内被调用（[OpenAI](https://openai.com/index/powering-product-discovery-in-chatgpt/)）。
  - **Walmart × Google**（2026-01, NRF）：沃尔玛 + 山姆目录接入 Gemini，可在对话内规划、建购物车、结账（[Walmart 新闻室](https://corporate.walmart.com/news/2026/01/11/walmart-and-google-turn-ai-discovery-into-effortless-shopping-experiences)）。
  - **Best Buy × OpenAI**（2026-08，财报电话会披露）：目录接入 ChatGPT，可在对话内发现/推荐/下单（[Digital Commerce 360](https://www.digitalcommerce360.com/2026/09/16/best-buy-opens-up-gift-buying-and-discover-through-chatgpt-ahead-of-holidays/)）。
- **欧洲**（整体晚于美国/中国）：**Frasers Group**（2026-01, NRF）接入 Algolia × Microsoft 的 AI 购物搜索、上线 Ask Frasers 助手（[Algolia 新闻](https://www.algolia.com/about/news/algolia-collaborates-with-microsoft-to-drive-real-time-product-data-to-shopping-experiences)）。
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
- **多轮会改变推荐**：问"第一次马拉松最佳跑鞋"先给几个大牌；逐步加预算、扁平足、冬天柏油路，到第 4 轮首位品牌常被换掉——每加一个约束就把"品类问题"变成一个 **demand space**（谁买、什么场合、什么约束、要什么结果）。说明**建库要保留多轮、按 demand space 记录约束**。（Joachimsthaler 2026 的跑鞋实验，[Medium](https://medium.com/@ejoachimsthaler/ai-will-not-kill-brands-it-will-expose-weak-ones-9b64de04e0c1)）

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

### Agent 行为偏见（Allouah et al., *What Is Your AI Agent Buying?*, [arXiv:2508.02630](https://arxiv.org/abs/2508.02630)）
用 ACES 框架在受控市场里审计 agent 决策，变动价格/评分/评论/位置/赞助标签/平台背书：
- **位置偏见强**：随 provider / 版本变化，连纯文本 headless 界面也存在——"top rank"无普适意义（故那条截图 agent 系统指令才显式要求"忽略商品位置"，见 §2 A1）。
- **一致地惩罚"赞助(sponsored)"标签、奖励"平台背书"**；对价格/评分/评论的敏感度各模型差异大。
- **选择同质化 / 需求集中**：常把需求堆到少数"modal"产品、忽略其余。
- **偏好不稳定**：模型更新会剧烈重排市场份额。
- **卖方可反制**：seller-side agent 随 query 条件微调描述，就能显著拉高份额。


### 学界实证论文
**一支：品牌推荐偏见 / 审计**
- **Evaluating Brand Retrieval and Ranking in LLM Recommendations**（Malthouse et al. 2026, [arXiv:2609.16304](https://arxiv.org/abs/2609.16304)）：把 LLM 推荐当作**随机的检索-排序过程**，6 个 LLM × 5 品类重复采样，测品牌出现概率与平均倒数排名（MRR）——发现推荐高度不稳定。
- **"Global is Good, Local is Bad?"**（Kamruzzaman, Nguyen & Kim, EMNLP 2024，[ACL Anthology](https://aclanthology.org/2024.emnlp-main.707/)）：15 国各 3 全球 + 3 本地品牌，构造 SAI/ASA 选择题与送礼任务，测 LLM 的**全球 vs 本地品牌偏见**。结论：GPT-4、Llama-3 等**一致地把正面属性给全球品牌、负面给本地品牌**；在 prompt 里声明用户所在国会触发 country-of-origin effect——更偏好该国本地品牌，方向甚至反转。

**另一支：购物对话 agent 的合成数据集**（NLP/agent 向：为训练 / 评测 agent 造数据）
- **Wizard of Shopping**（全称 *Target-Oriented E-commerce Dialogue Generation with Decision Tree Branching*；Amazon, ACL 2025, [arXiv:2502.00969](https://arxiv.org/abs/2502.00969)）：方法 **TRACER**——把生成锚定在"对话计划"（即产品搜索轨迹）上，两个 LLM 扮顾客/助手、按决策树展开，3,600 段（每域 1,200、均长 19.7 轮）。贡献：兼顾**大规模 + 自然**（既往数据集要么大而不真、要么真而太小），并证明能提升对话式 query 生成与商品排序。
- **ShopDial**（全称 *Bottom-Up Synthesis of Knowledge-Grounded Task-Oriented Dialogues*；[arXiv:2504.14375](https://arxiv.org/abs/2504.14375)）：首个**自底向上**合成的电商对话数据集——先生成产品 QA 对再缝合成对话，6 品类 × 1,000 段（含"信息不足"的 unknown 轮，更贴近真实）。评测：真实性/自然度/整体质量胜过自顶向下的 PLACES 基线，但连贯性/信息量/完整性略逊。

### 实证：AI 推荐是否真的改变消费者行为（2026-10-28 整理）
- **AI 推荐能推动购买（开放网络）**：当 AI 把一个**此前未接触**的品牌推荐给用户，7 天内该品牌搜索 **+4.3pp**、品牌官网访问 +2.4、零售页访问 +1.0；这条路径大多对 last-click 归因**不可见**。方法：opt-in 用户一个身份标签，把其 AI 对话与浏览时间线在个人层面对齐（如 14:00 在 ChatGPT 被推荐 "Garmin"、14:05 就去 Google 搜 "Garmin"）。（Iannelli & Ai 2026, *From Prompt to Purchase*, [arXiv:2606.10907](https://arxiv.org/abs/2606.10907)）
- **AI 在改变线上行为**：采用 LLM 约 20 周后，用户**传统搜索比采用前降 20%+**；大站扛得住，**小站出现明显流量流失**；展示广告曝光下降，重度网购者尤甚。（Padilla, Lam, Lambrecht & Hollenbeck 2025/26, *The Impact of LLM Adoption on Online User Behavior*, [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5393256)；Comscore 点击流，100 万+ 用户，2022–2023）
- **AI 摘要挤走点击**：有 AI 摘要时用户点传统搜索结果 **8%**，无摘要时 **15%**。（[Pew Research, 2025-07](https://www.pewresearch.org/short-reads/2025/07/22/google-users-are-less-likely-to-click-on-links-when-an-ai-summary-appears-in-the-results/)）
- **信任是逐步建立的**：通过一个动态的"信任校准（trust calibration）"过程。
- **被看见 ≠ 被选择**（AIVO，行业证据、未经同行评审）：模拟买家多轮问答里，品牌在早期答案**出现 95.7%、最终被推荐仅 12.7%**；到达决策前 **87.3%** 的已引用品牌被丢弃。相同 prompt 跑 3 次，**被引来源变 95.8%、最终推荐只变 14.6%**——dashboard 常追的"提及/引用"像噪声，真正的推荐却相对稳定。启示：**建库要测"最终推荐"而非"是否被提及"，且必须重复采样**（呼应 §4）。（[AIVO Journal, 2026](https://www.aivojournal.org/appeared-in-96-of-journeys-chosen-in-13/)）


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
