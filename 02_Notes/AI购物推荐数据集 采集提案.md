---
created: 2026-11-09
tags: [方法, AI购物, 数据集设计, 提案, methods]
source: "[[AI dataset设计需要考虑的点]]"
---

# AI 购物推荐数据集 · 采集提案

> 配套背景见主笔记 [[AI dataset设计需要考虑的点]](四个前置问题 + 全部文献);本提案是可执行的采集设计。

## 1. 研究对象与目标
- **对象**:顾客用 AI 助手**搜索产品、获得推荐**这一行为;记录 prompt 与回复。
- **目标**:**模拟并每日采集,跑 6–12 个月看趋势**,覆盖不同市场;可与 sales 数据结合
- **测量层**:**API(模型)层**。测的是模型给出的推荐。

## 2. 已锁定的设计决策
- **界面**:纯 API
- **prompt**:开放式、不给商品清单、**单一固定问法**
- **模型**:仅 API 可得的。
- **市场**:DE / FR / UK / US(两个本地语言国 + 两个英语国)。
- **测量**:记推荐

## 3. 市场与语言
| 市场  | 语言  | 作用                     |
| --- | --- | ---------------------- |
| UK  | en  | 与 US 组成"同语言不同国"→ 纯地理效应 |
| US  | en  | 同上                     |
| DE  | de  | 不同语言不同国                |
| FR  | fr  | 不同语言不同国                |

- **注入方式**(API 不带终端位置,必须注入,见主笔记 §4②):① 查询语言;② `user_location` 参数 = 市场;③ 文本里的地点/可得性短语(DE/FR 母语化)。
- **内生局限**:DE 只跑德语、FR 只跑法语 → 对这两国"语言"与"国家"绑定、分不开

## 4. 品类与产品(候选菜单,供导师挑选;每个 = 产品 + function)
> 涉入度在这组里天然从高到低,可作为分析维度。注意:PC 偏高涉入、HHC 偏低涉入,**品类与涉入度相关**,解读时别混淆。

**PC(个护)**
| 产品 | FUNCTION | 涉入度 |
|---|---|---|
| 去屑洗发水 | dandruff | 高 |
| 防脱洗发水 | hair loss | 高 |
| 护发素 | dry hair / curly hair | 中 |
| 保湿护肤(面霜) | dry skin | 高 |
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

### 为什么固定一句(而不是轮换多种问法)
- **趋势研究要"除时间外都别动"**:每天换措辞会把"措辞影响"和"时间变化"混在一起,固定一句让时间序列干净可读。
- **"which … should I get" 是中性问法**,绕开 "best" 自带的大牌/在位偏置(Chu & Hou 的在位优势),又自然、又能逼出品牌。

### 稳健性(一次性,不进日常)
在**一个子集**上用 2–3 个等价问法(如 "What's a good {P} for {F}?" / "Can you recommend a {P} for {F}?")各跑几次,证明"换个说法、推的牌子大体一样"(LLM 对措辞敏感,Sclar et al., ICLR 2024)。日常 tracker 只用那一句。

### 各产品的英文问法(DE/FR 需母语者校对)
| 产品 | EN prompt(填 {LOCATION}) |
|---|---|
| 去屑洗发水 | I'm in {LOC}, which shampoo should I get for dandruff? |
| 防脱洗发水 | …which shampoo should I get for hair loss? |
| 护发素(干发) | …which conditioner should I get for dry hair? |
| 护发素(卷发) | …which conditioner should I get for curly hair? |
| 保湿面霜 | …which moisturiser should I get for dry skin? |
| 面部防晒 | …which facial sunscreen should I get? |
| 抗敏牙膏 | …which toothpaste should I get for sensitive teeth? |
| 防蛀牙膏 | …which toothpaste should I get to prevent cavities? |
| 护色洗衣液 | …which laundry detergent should I get for coloured clothes? |
| 厨房油污清洁剂 | …which kitchen cleaner should I get for grease? |
| 管道疏通剂 | …which drain cleaner should I get to unclog a drain? |
| 去除水垢 | …which descaler should I get to remove limescale? |

（价格默认不写——FMCG 便宜、真实查询也少带预算;若日后想测 premium↔value,把 "a good/affordable {P}" 当一次性因子加回。)

## 6. 独立性协议(技术)
- **1 trial = 1 次无状态调用**:`store=false`、无记忆、不传 `previous_response_id`;绝不在同一线程串多个 trial(多轮上下文改变行为,Laban et al. 2025, arXiv:2505.06120:多轮比单轮掉约 39%)。
- **`temperature` 固定但 ≠ 确定性**:输出当分布的样本,每个 cell 重复 N 次,报稳定性(TARr@N / TARa@N,Atil et al. arXiv:2408.04667)。
- **记录快照**:模型 snapshot、时间戳、`system_fingerprint`、全部参数;同名服务会短期漂移(Chen, Zaharia & Zou, arXiv:2307.09009),版本变(fingerprint 变)当事件做**中断时间序列**。
- **按 prompt/item 聚类**:N 次重复 ≠ N 个独立观测 → cluster-robust SE(Miller 2024, arXiv:2411.00640)。
- 选 N:Żatuchin 2026(arXiv:2609.04047)D-study——5 次信度 0.58、10 次 0.74、15 次 0.81。

## 7. 抓取与编码(技术)
- 存 **raw reply** + 结构化字段:`final_recommendation`(排序/首位)、`brands_mentioned`、`sources_cited`、`sponsored_flag`、`price_mentioned`、`refusal`。
- **关键**:记**最终推荐**而非仅"被提及"(AIVO:品牌出现 95.7% 但最终被选仅 12.7%);既记 mention 又记 recommendation → 可算"出现→被选"存活率。
- 解析:半结构化 + LLM 抽取 + 人工抽检 + 双源交叉验证。

### cell 结构与字段 schema
一个 **cell** = `product×function × market/language × model`,每次采集重复 **N** 次(trial)。
每条 trial 记录:`cell_id, trial_id, date, timestamp, product, function, market, language, user_location, model, model_snapshot, system_fingerprint, temperature, prompt_text, raw_response, final_recommendation, brands_mentioned, sources_cited, sponsored_flag, price_mentioned, refusal, parse_status`。

## 8. 节奏与规模
- **每日核心 panel**:固定 cell 天天跑(趋势只能从固定 cell 的时间序列看出);另设**更宽的 panel** 每周/每月跑一轮。
- **单日 run 公式(已简化,无措辞维度)**:
  `P(产品×功能) × R(市场/语言) × M(模型) × N(重复)`
- **N 参考**:10–15(日常 10,关键 cell 补到 15)。
- **预算参考**(粗估,按当前 API 价;R=4、M=1–2):

| 档 | P | ≈ 次/天 | ≈ 次/年 | 粗估花费/年 |
|---|---|---|---|---|
| 精简/试点 | ~6 | ~0.5–1k | ~20–36 万 | ~$1k–5k |
| 中档 | ~12 | ~1–2k | ~40–70 万 | ~$3k–15k |
| 丰富 | 全部 ~12 产品 × 多 N | ~2–4k | ~70–150 万 | ~$5k–30k |

- 单次购物问答 ≈ 500–2000 token;便宜档(flash/mini/Qwen)≈ $0.002–0.005/次,旗舰/开 web_search ≈ $0.01–0.03/次。
- **两个主导成本旋钮**:① 是否开 web_search/grounding(更贵 + 引入实时检索漂移,但更接近真实,可只在部分 cell 开);② 模型档位(日常用便宜档、关键复核才上旗舰)。

## 9. 分析
- 每个 cell 的时间序列:品牌**推荐份额**、top-k 构成、**mention→recommendation 落差**、稳定性 TAR@N、品牌多样性、拒答率。
- 对比:市场、**语言 vs 地理分解**、模型;模型版本更新前后断点(中断时间序列);**与 sales 数据结合**(推荐份额 ↔ 实际销量)。
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
