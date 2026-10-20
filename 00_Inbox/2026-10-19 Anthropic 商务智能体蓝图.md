---
created: 2026-10-19
tags: [inbox, 案例]
---
# Anthropic Claude Commerce Agents：智能层而非关系所有者

来源：Coresight Research，*With Announcements from Meta, Stripe and Anthropic, the Three Key Pillars for Agentic Commerce Are Now in Place: Agents, Payments and Tools*。含 Shoptalk Fall 2026 上一位 Anthropic 高管的发言。[原文链接](https://coresight.com/research/with-announcements-from-meta-stripe-and-anthropic-the-three-key-pillars-for-agentic-commerce-are-now-in-place-agents-payments-and-tools/)

- **事件**：Anthropic 于 9 月 2 日发布 Claude Commerce Agents，一套开源蓝图（open-source blueprint），内含购物智能体（shopping agent）与商家智能体（merchant agent）两个参考实现，零售商可 fork 后按自家商品目录与政策定制。
  - On September 2, Anthropic launched Claude Commerce Agents, an open-source blueprint with reference implementations of a shopping agent and a merchant agent that retailers can fork and customize to their own catalogs and policies.

- **成效数据**：Anthropic 称在 Claude 上运行购物智能体的零售商，购物车规模最高增大 35%，顾客完成购买的可能性高出 60%。报告推测这至少部分反映了使用 AI 工具的消费者更有目的性（more intentional）。
  - Retailers running shopping agents on Claude report carts up to 35% larger and customers 60% more likely to complete a purchase, likely reflecting in part that AI-tool users are more intentional.

- **落地极快**：Wix 开始后十五分钟内就有一个能接受指令的商务智能体；Fetch 在不到一小时内让两个智能体本地跑通；工程团队普遍反映上线周期从数月压缩到一到两周。
  - Adoption is fast: Wix had a working agent within fifteen minutes, Fetch had both running locally in under an hour, and timelines broadly compressed from months to one to two weeks.

- **刻意保持中立于技术栈（agnostic）**：蓝图可跨 Claude API、Amazon Bedrock、Microsoft Foundry、Google Cloud Vertex AI 部署，兼容任意支付类型或协议；Anthropic 已在 Shopify、Priceline 和亚马逊 Alexa+ 支持智能体部署。
  - The blueprint is deliberately agnostic: deployable across Claude API, Amazon Bedrock, Microsoft Foundry and Google Cloud Vertex AI, working with any payment type or protocol; already supporting Shopify, Priceline and Amazon's Alexa+.

- **定位：智能层，不争夺商家关系**。高管称 Claude 是「智能层（intelligence layer）」，不谋求拥有与商家的关系：零售商保留顾客关系，Claude 只提供背后的上下文（context）。
  - Positioning: Claude as an intelligence layer that does not seek to own the merchant relationship. The retailer keeps the customer relationship; Claude provides the context behind it.

- **三部分信任框架（trust framework）**：
  - 隐私（privacy）：购物者与智能体之间的对话保持私密。
    - Conversations between shopper and agent stay private.
  - 准确（accuracy）：与零售商共担责任，避免给出不准确的声明。
    - Shared responsibility with the retailer for avoiding inaccurate claims.
  - 无偏（unbiased）：高管称这是三者中最重要的一条，因为 Anthropic 不收广告费，零售商无法花钱买到在 Claude 推荐里更高的排名。
    - Called the most important: Anthropic takes no advertising money, and a retailer cannot pay for higher ranking in Claude's recommendations.

- **时间窗口**：高管强调，即便到 9 月下旬，仍有可能赶在假期（holidays）前把智能体商务跑起来。
  - The executive stressed that even as of late September, it was still possible to get agentic commerce running before the holidays.

- **为何值得记**：这给「AI 作为购物中介」的图景补上了关键一方，即模型供应商（而非零售商、也非 ChatGPT/Perplexity 式代买）如何自我定位。Anthropic「不拥有关系、无偏、不卖排名」的立场，与 Schnucks「零售商要掌控关系」互为镜像，也直接对话 [[Geyskens Gielens Steenkamp - GenAI Brand Trust]] 的「AI 货架（AI shelf）」与 [[平台渠道权力]] 里「算法奖励转化而非来源」的担忧：如果供应商真的不卖排名，selection/representation 机制的权力分配会不同。学术钩子：「不收广告费」能否成为一种可信承诺，还是仍存在非价格形式的隐性偏置？
  - Worth noting: it adds the model-provider's self-positioning to the AI-as-shopping-intermediary picture. Anthropic's "no ownership, unbiased, no paid ranking" mirrors Schnucks' "retailer owns the relationship" and speaks directly to the AI-shelf (selection/representation) and channel-power concerns about algorithms rewarding conversion over provenance.

---
相关：[[2026-09-24 Schnucks AI 购物助手]]（零售商侧「掌控关系」立场的镜像）· [[2026-09-28 克罗格×谷歌Gemini购物助手]] · [[2026-09-24 克罗格 AI 购物助手]] · [[Geyskens Gielens Steenkamp - GenAI Brand Trust]]（AI 货架：selection/representation）· [[平台渠道权力]]（算法作为准渠道、奖励转化）· [[Gielens 2026 - Shopper]]（AI agent 作为中介层）
