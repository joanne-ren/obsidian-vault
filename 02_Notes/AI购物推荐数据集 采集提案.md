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
- **我们要抓的三种variation:
  1. **缓慢漂移**:品牌份额稳定还是慢慢移。
  2. **品牌进出**:有没有新品牌突然冒出 / 老品牌掉出。
  3. 事件冲击:如果某品牌/零售商宣布 AI 合作、上广告 pilot 后,其份额是否阶跃
- **模型更新必须 log**:只记 `system_fingerprint`/snapshot,用来**区分"真实漂移/新品牌"与模型被悄悄换了。

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
## 4. 品类与产品每个 = 产品 + function


**PC(个护)**
| 产品 | FUNCTION | 涉入度 |
|---|---|---|
| 去屑洗发水 | dandruff | 高 |
| 防脱洗发水 | hair loss | 高 |
| 护发素 | dry hair | 中 |
| 保湿护肤 | dry skin | 高 |
| 面部防晒 | facial sun protection（⚠ 季节性,夏搜冬掉) | 高 |
| 抗敏牙膏 | sensitive teeth | 中高 |
| 防蛀牙膏 | cavity  | 中 |

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



##  独立性协议
- **1 trial = 1 次无状态调用**:`store=false`、无记忆、不传 `previous_response_id`;绝不在同一线程串多个 trial(多轮上下文改变行为,Laban et al. 2025, arXiv:2505.06120:多轮比单轮掉约 39%)。
- **`temperature` 固定但 ≠ 确定性**:输出当分布的样本,每个 cell 重复 N 次,报稳定性(TARr@N / TARa@N,Atil et al. arXiv:2408.04667)。
- **记录快照**:模型 snapshot、时间戳、`system_fingerprint`、全部参数;同名服务会短期漂移(Chen, Zaharia & Zou, arXiv:2307.09009),版本变(fingerprint 变)**只用来区分"真实漂移"与"模型被换"**,本身不作研究对象(见「我们希望观察到什么」)。
- **按 prompt/item 聚类**:N 次重复 ≠ N 个独立观测 → cluster-robust SE(Miller 2024, arXiv:2411.00640)。
- 选 N:Żatuchin 2026(arXiv:2609.04047)D-study——5 次信度 0.58、10 次 0.74、15 次 0.81。
- 存 **raw reply** + 结构化字段
### cell 结构与字段 schema
一个 **cell** = `product×function × market/language × model`,每天分时间（比如早中晚）采集重复 **N** 次(trial)

这样下来一次需要多少token？比如说我问`I'm in the UK, which shampoo should I get for dandruff?`，with web search

## 9. 分析
- 每个 cell 的时间序列:品牌**推荐份额**、top-k 构成、**mention→recommendation 落差**、稳定性 TAR@N、品牌多样性、拒答率。
- 对比:市场、**语言 vs 地理分解**、模型(ChatGPT vs Gemini 是否各偏平台盟友品牌)。
- **事件研究**:品牌/零售商 AI 合作公告前后的份额阶跃(event study,机会型);模型版本更新**仅作干扰排除**,不作研究对象。
- **与 sales 数据结合**:推荐份额 ↔ 实际销量的落差与方向(尤其高涉入 vs 低涉入)。
- **涉入度维度**:高涉入(PC)vs 低涉入(HHC)的推荐行为、与 sales 的吻合度是否不同。

## 10. 设计依据(文献 + 语料,技术小结)
- **涉入度当变量**:人只对高涉入品类搜 AI;我们从 ShareChat / Search Arena 真实购物子集提取发现 **PC 查询个位数、HHC ≈ 0**(真实公开用户几乎不问家清)→ 低涉入/HHC 外部效度弱,须写明;也说明这两个语料**无法直接供给 PC/HHC 真实问法**,prompt 需按观察到的 pattern 构造。
- **真实问法 pattern**:best/which + 功能/价格/渠道/地点约束 → 模板据此(中性 which + 地点)。
- **在位优势**(Chu & Hou, arXiv:2606.17443):"best" 偏在位大牌 → 改用中性 "which should I get"。
- **mention ≠ chosen**(AIVO):测最终推荐 + 重复采样。
- **UI ≠ API**(Kirgis et al. arXiv:2604.06188;Lipphardt FOCI 2026):只测 API 是边界,结论不外推到真人。
- **平台合作是 representation 混淆**:欧莱雅系把 CeraVe / La Roche-Posay / Garnier / Maybelline 的产品 feed 喂进 ChatGPT,并有 ChatGPT 广告 pilot → 美妆/护肤的推荐**并非完全有机**;且 PC(美妆)偏 **OpenAI**、HHC 大厂(P&G、Unilever)偏 **Google/Gemini** → **ChatGPT vs Gemini 会各自偏向盟友品牌**,选品/解读要留意。
- **跨市场换名 = 白送的地理实验**:P&G 在四国换名(Flash/Mr Clean/Meister Proper/M. Propre;Fairy/Dawn;Ariel/Tide)→ 同一产品在不同国被推成不同本地名,HHC 这块尤其明显。

## 11. 可选扩展(讨论过,暂不进主干)
- **Track B 受控实验**:给 10 个产品清单(含**虚构品牌 + 固定属性**),用 GEO 三协议(Top-K / 单选 / 成对)测**干净的品牌偏见**,操纵名气/评分/价格/位置/赞助标签/营销语言(权威·社会证明·锚定)。
- **多轮 demand-space**:逐轮加约束,看推荐随轮次变化。
- **UI sock-puppet 季度抽查**:只为量 API 与真实 UI 的差距,不进主干。
- **价格因子**:加 "affordable" 变体测 premium↔value。

## 12. 边界与已知限制
- **API ≠ 真人所见**(换可复现 + 可日跑的取舍,须写进每处结论)。
- 本批市场不含**中国**;地区是**注入信号**(人设/语言/`user_location`),非真实出口 IP。
- 我们是在**模拟**而非观测真实用户(外部效度)。
- **健康敏感品类**(护肤靠近此线)可能触发免责/拒答,污染"推哪个牌子";非健康 FMCG 数据更干净。

## 待定项
- [ ] 导师从 §4 菜单选定最终产品
- [ ] N(参考 10–15)与每日预算 / panel 宽度
- [ ] DE/FR 是否加英文臂做语言×地理解耦
- [ ] web_search 开 / 关
- [ ] DE/FR prompt 母语者校对
