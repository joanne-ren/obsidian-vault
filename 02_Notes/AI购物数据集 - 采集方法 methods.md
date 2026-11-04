---
created: 2026-11-04
tags: [方法, AI购物, 数据集设计, methods]
source: "[[AI dataset设计需要考虑的点]]"
---

# AI 购物数据集 · 采集方法（methods）

## 研究对象与边界
- 对象：**顾客用 AI 助手搜索零售产品、获得推荐**这一行为；记录 prompt 与回复。
- 目标：**模拟并每日采集，跑 6–12 个月看趋势**，覆盖不同地区。
- 测量层：**API 层（模型层）**。测的是模型给出的推荐。


- **界面**：纯 API（可复现、可日跑、可记录 `system_fingerprint`）。
- **prompt设计：
	- 品类（电子 / 美妆 / 食杂 / 服饰 / 家居 ）
	- demand-space 约束（预算 / 饮食 / 场合 / 用途）

- **模型**：仅 API 可得的。
- **地区**：**待议**
	- API 调用不带终端用户位置，地区只能靠注入：
	- 国家人设写进 prompt；
	- 查询语言；
	- `user_location` 参数（OpenAI web-search、Perplexity Sonar 支持 country/city）；
	- 货币
- 每次采集重复 **N** 次
	- **N、每日预算**： 单日run数量 = P(意图，包括品类和需求) × W(措辞，语言) × R(地区) × M(模型) × N(重复)。

