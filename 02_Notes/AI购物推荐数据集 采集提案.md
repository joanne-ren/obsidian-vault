---
created: 2026-11-09
tags: [方法, AI购物, 数据集设计, 提案, methods]
source: "[[AI dataset设计需要考虑的点]]"
---

# AI 购物推荐数据集 · 采集提案


## 1. 研究对象与目标
- **对象**:顾客用 AI 助手**搜索产品、获得推荐**这一行为;记录 prompt 与回复。
- **目标**:**模拟并每日采集,跑 6–12 个月看趋势**,覆盖不同市场;可与 sales 数据结合


### 我们希望观察到什么(观测量)
- **因变量 = 品牌推荐份额**:在一个固定问题下(产品×功能×市场×模型),模型**最终推荐**哪个品牌;每日跑 N 次并记录
- **我们要抓的三种 variation**:
  1. **缓慢漂移**:品牌份额稳定还是慢慢移。
  2. **品牌进出**:有没有新品牌突然冒出 / 老品牌掉出。
  3. **事件冲击**:如果某品牌/零售商宣布 AI 合作、上广告 pilot 后,其份额是否阶跃。
- **模型更新必须 log**:只记 `system_fingerprint`/snapshot,用来区分"真实漂移 / 新品牌"和"模型被悄悄换了"。

- **五个研究问题(= 观察什么的落点)**:① 谁被推、多集中(有无"条件垄断");② 随时间稳定 / 漂移 / 品牌进出;③ 跨市场区别;④ 模型是否偏平台盟友品牌;⑤ 推荐份额 vs 真实销量的落差与方向。

## 2. 已锁定的设计决策
- **界面**:纯 API
- **prompt**:开放式、不给商品清单、**单一固定问法**
- **市场**:DE / FR / UK / US(两个本地语言国 + 两个英语国)。
- **测量**:记推荐

## 3. 市场与语言
| 市场  | 语言  |
| --- | --- |
| UK  | en  |
| US  | en  |
| DE  | de  |
| FR  | fr  |

- **注入方式**(API 不带终端位置,必须注入,见主笔记 §4②):① 查询语言;② `user_location` 参数 = 市场;③ 文本里的地点/可得性短语(DE/FR 母语化)。
## 4. 品类与产品(每个 = 产品 + function)


**PC(个护)**
| 产品 | FUNCTION | 涉入度 |
|---|---|---|
| 去屑洗发水 | dandruff | 高 |
| 防脱洗发水 | hair loss | 高 |
| 护发素 | dry hair | 中 |
| 保湿护肤 | dry skin | 高 |
| 面部防晒 | facial sun protection（⚠ 季节性,夏搜冬掉) | 高 |
| 抗敏牙膏 | sensitive teeth | 中高 |
| 防蛀牙膏 | cavity protection | 中 |

**HHC(家清)**
| 产品 | FUNCTION | 涉入度 |
|---|---|---|
| 护色洗衣液 | coloured clothes | 低 |
| 厨房油污清洁剂 | grease | 低 |
| 管道疏通剂 | a clogged drain | 低 |
| 去除水垢 | limescale | 低 |

## 5. Prompt 设计
### 固定模板
```
I'm in {LOCATION}, which {PRODUCT} should I get for {FUNCTION}?
+ user_location 参数 = {LOCATION}
+ 查询语言 = 当地语言（DE/FR 母语化）
+ 不追问
```
- EN 例:`I'm in the UK, which shampoo should I get for dandruff?`
- DE 例(母语化):`Welches Shampoo gegen Schuppen sollte ich kaufen?`（+ user_location=DE、语言=de）



## 6. 独立性协议
- **1 trial = 1 次无状态调用**:`store=false`、无记忆、不传 `previous_response_id`;绝不在同一线程串多个 trial(多轮上下文改变行为,Laban et al. 2025, arXiv:2505.06120:多轮比单轮掉约 39%)。
- **`temperature` 固定但 ≠ 确定性**:输出当分布的样本,每个 cell 重复 N 次,报稳定性(TARr@N / TARa@N,Atil et al. arXiv:2408.04667)。
- **记录快照**:模型 snapshot、时间戳、`system_fingerprint`、全部参数;同名服务会短期漂移(Chen, Zaharia & Zou, arXiv:2307.09009),版本变(fingerprint 变)**只用来区分"真实漂移"与"模型被换"**,本身不作研究对象(见「我们希望观察到什么」)。
- **按 prompt/item 聚类**:N 次重复 ≠ N 个独立观测 → cluster-robust SE(Miller 2024, arXiv:2411.00640)。
- 选 N:Żatuchin 2026(arXiv:2609.04047)D-study——5 次信度 0.58、10 次 0.74、15 次 0.81。
- 存 **raw reply** + 结构化字段
### cell 结构与字段 schema
一个 **cell** = `product×function × market/language × model`,每天分时段(如早中晚)采集、每次重复 **N** 次(trial)。

一次暂时按 ~5,000 token 估(实际会有波动):
- 4 产品 × 4 国 = 16 个问题(cell)
- 每个每天重复 2 次 = 32 次/天
- 32 次 × ~5,000 token ≈ 160,000 token/天
- 这样算下来还是便宜,大概一个月 20 美元以内。
## 7. 分析
- 每个 cell 的时间序列:品牌**推荐份额**、top-k 构成、稳定性、品牌多样性。
- **事件研究**:品牌/零售商 AI 合作公告前后的份额阶跃
- **与 sales 数据结合**:推荐份额 ↔ 实际销量的落差与方向


