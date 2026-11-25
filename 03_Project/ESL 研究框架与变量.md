---
created: 2026-11-24
updated: 2026-11-25
tags: [project, ESL, 研究设计, 变量, 计量]
---

# ESL 研究框架与变量（最终版）

承接 [[ESL]]（机制与测量）、[[2026-10-20 Meeting]]（数据库设计、解释变量）、[[2026-11-20 Meeting]]（西欧完成、一页报告）。
依据：Zotero「ESL」分类 13 篇 + 「Example paper Project1」7 篇；补充网络检索（scanner 采用文献、欧盟法规、数据源）；以及对现有数据的实际核查（`global-esl/data/processed/esl_by_country/`、`supermarket_all.csv`）。

---

## 0. 反思：上一版做得好的、漏掉的、错了的

**做得好的**
- 用示例论文的「前因 → 后果 → 匹配度」结构，把研究定位清楚。
- 意识到 ESL 决策常在集团层做出（数据里 102 行状态为 `follows parent`，印证了这一点）。
- 意识到「没搜到 ≠ 没采用」的覆盖偏差。
- 把 ESL 的用途拆成六类，每类对应不同前因（见 §2）。

**漏掉的**
1. **最直接的类比文献：零售技术（收银扫描仪）的采用研究**，不在 Zotero 里，我之前只从 Basker & Simcoe 的引用里瞥到：
   - Levin, Levin & Meisel 1987（REStat）：用比例风险模型研究超市采用扫描仪的先后。早期是平均店面大、不属于连锁、所在市场集中度低、收入和工资高的企业先采用；随着扩散推进，集中度、份额、规模的作用变弱。
   - Levin, Levin & Meisel 1992（REStat）：份额大的企业**更早开始采用**，但在自己门店间**铺开更慢**。这直接对应我们的「试点年 vs 多数铺开年」。
   - Beck, Grajek & Wey 2011（Applied Economics）：欧洲 10 国 1981–1996 年扫描仪扩散。各国主要差在长期饱和水平，时机和速度差别较小；大卖场竞争降低长期采用水平；就业保护法规没有显著影响。
   - Das, Falaris & Mulligan 2009：扫描仪采用的门店「年份效应」。新店和翻新店更易采用；Basker & Simcoe 附录也指出装扫描仪通常要整改收银区。
   - → **建议把这几篇加进 Zotero。**
2. **Stamatopoulos, Bassamboo & Moreno 2021（Management Science）** 之前只是转引，现已核实摘要：2015 年某国际零售商采用 ESL 后，毛利率大幅上升，幅度远超省下的人工；价格变动更频繁、幅度更小、多为降价、时间上更分散，效应集中在短保质期品类。
3. **欧盟价格标示规则**：Omnibus Directive（2019/2161）在 Price Indication Directive（98/6）中加入 Article 6a。宣布降价时，必须同时标示过去至少 30 天内的最低价。各国转化期限为 2021-11-28，实际适用日期各国不同（例如比利时 2022-05-28）。2024-09 欧盟法院 Aldi Süd 案（C-330/23）确认降价幅度必须按这个「先前价格」计算。促销越多的零售商，合规负担越重，ESL 的价值也越大。
4. **国家层面的劳动成本冲击**，比如大幅上调最低工资。这类冲击的时点外生，可以帮助识别。

**错了或需要更正的**
1. **没先核查数据就推荐变量和方法。** `supermarket_all.csv` 里的单店面积、平均收银台数、食品占比，每个 banner 历年都是同一个值（模型估算）。所以：
   - 这三个变量只能用作横截面特征，不能当随时间变化的变量；
   - 之前提议的随机前沿生产率（投入含收银台数）不可行。
2. **「2021–22 芯片短缺推迟 ESL 交付」未经核实。** 检索没有找到证据，Digitimes 2022-12 反而报道 ESL 供应链库存偏高。先从识别策略中拿掉，除非能在 Vusion、Pricer 年报里找到交付延迟的记录。
3. **方法写得过于生僻**（copula、frailty、三层模型）。本版改为「一个主模型 + 少量稳健性检验」。
4. **Nutri-Score 各国年份**只核实了法国（2017-10）和卢森堡（2021-05），其余国家需要查官方来源再用。

---

## 1. 现有数据的实际情况（决定样本怎么划）

- status 表共 750 行（banner × 国家）。`Collection status`：
  - `collected` 131 行、`no evidence` 52 行：搜过，可用；
  - `follows parent` 102 行：状态跟随母集团；
  - `not-started` 323 行、`not assessed` 61 行：没搜过；
  - `excluded` 76 行：已排除。
- 有任一带日期里程碑的 banner：115 个；达到多数铺开的：51 个。
- 首次事件年份分布：2003、2004 各 1 个（Eroski、Carrefour 西班牙，早于 2006）；2010–2019 共 36 个；2020 年 22 个（峰值）；2021–2025 共 47 个；2026 年 8 个，超出 Flywheel 的实际数据期（≤ 2025）。
- 各国搜索覆盖不均。比如意大利 157 行只搜了 26 行，德国和法国全部搜过。

**样本规则（建议）**
1. 只保留搜过的 banner（`collected` 和 `no evidence`）。`not-started`、`not assessed` 不进样本，避免把「没搜」当成「没采用」。
2. `follows parent`：主分析中把集团的采用年份赋给该 banner；稳健性检验中剔除这些 banner。
3. 观察期 2006–2025。2006 年前已采用的 2 个 banner 不进风险集；2026 年的事件在 2025 年视为右删失（尚未采用）。
4. 敏感性检验：按各国前 10、前 15（同 Bombaij & Dekimpe 2020）、全部 banner 分别估计。

---

## 2. ESL 给零售商带来什么：六种用途

前因变量都从这张表推导出来。现有文献多把 ESL 当成「降低改价成本」的单一技术，这里把它拆开。

| 用途 | 证据 | 受什么因素驱动 |
|---|---|---|
| ① 省换签人工（menu cost） | Levy et al. 1997：换签成本约占营收 0.7%、净利 35%（Stamatopoulos et al. 2026 引）；Spann et al. 2024：合作零售商上 ESL 前规定每年只改价两次 | 人工成本、门店数、SKU 数 |
| ② 生鲜和临期降价 | Stamatopoulos et al. 2021：效应集中在短保质期品类；Chehrazi et al. 2025；Ray et al. 2019：EDLP 店用于减损 | 生鲜占比、业态 |
| ③ 试价、学习价格 | Ray et al. 2019：Hi-Lo 店价格对过去价格的依赖从 3.21 周缩短到 2.13 周 | Hi-Lo、促销强度 |
| ④ 分店定价 | Ray et al. 2019 引 DellaVigna & Gentzkow 2019：统一定价平均牺牲约 7% 利润 | 门店数、地域分散度 |
| ⑤ 信息展示与合规 | Ray et al. 2019：意大利生鲜产地标示法；Vandevijvere & Berger 2021：Delhaize 用 ESL 展示 Nutri-Score；欧盟 30 天最低价规则 | 国家标签法规、Nutri-Score、Omnibus |
| ⑥ 门店运营（拣货、补货） | Coresight 2021：闪灯辅助线上订单拣货 | 线上全渠道占比 |

---

## 3. 研究设计总览

- **第一阶段，前因**：什么决定一个 banner 何时开始试点 ESL？（主模型 M1）
- **第一阶段补充，铺开速度**：开始试点后多久铺到多数门店？（M2，对应 Levin et al. 1992）
- **第二阶段，后果**：铺开后 banner 的销售表现是否变化？效应因定价策略、业态、国家而异吗？（M3、M4）
- **可选，匹配度**：按自身条件「该早上」的 banner 如果迟迟不上，表现是否更差？（M5，参照 Keller, Dekimpe & Geyskens 2016；Gielens & Dekimpe 2007）

---

## 4. 变量清单

图例：✅ `supermarket_all.csv` 已有（随时间变化）· 🟡 已有但历年不变，只能横截面用 · 🔧 可由已有数据计算 · 🔍 需另外收集

### A. 因变量 / 处理变量

| 变量 | 定义 | 用途 | 来源 |
|---|---|---|---|
| `pilot_year` | 第一家门店上线 ESL 的年份 | M1 的事件 | 🔧 事件表 Pilot；缺失时用 Announced 作替代并标注 |
| `majority_year` | 过半门店完成的年份 | M2 的终点、M3 的处理开始 | 🔧 事件表 Majority |
| `rollout_years` | majority_year − pilot_year | M2 因变量 | 🔧 |
| `ESL_scope` | 全店 / 仅生鲜 / 其他部分 / 未说明 | 调节变量；稳健性检验 | 🔍 已完成双人编码，待确认（见 §7） |
| `vendor` | 主要供应商 | 计算 C5；描述统计 | 🔧 事件表 Vendor |

### B. 零售商（banner）层面的前因

| 变量 | 定义 / 测量 | 预期方向 | 依据 | 来源 |
|---|---|---|---|---|
| B1 规模 | log 门店销售额（滞后 1 年） | + | 固定投资可摊薄、议价能力强；Levin et al. 1987：大企业先采用；Bombaij & Dekimpe 2020 控制规模 | ✅ |
| B2 门店数 | log 门店数 | 试点 +；铺开速度 − | 用途①④随门店数增加；Levin et al. 1992：大企业开始早、铺开慢 | ✅ |
| B3 单店面积 | 每店平方英尺 | + | 店越大 SKU 越多，换签越多；Levin et al. 1987：平均店面大者先采用 | 🟡 |
| B4 业态 | hypermarket、discounter dummy（超市为基准） | hyper +；discounter 待检验 | 大卖场 SKU 最多；折扣店 SKU 少但极度追求人效；业态分类同 Bombaij & Dekimpe 2020 | ✅ Channel |
| B5 价格策略 | Hi-Lo = 1，EDLP = 0 | Hi-Lo + | Hi-Lo 改价和促销多，用途①③⑤价值更大（Ray et al. 2019；Stamatopoulos et al. 2021）。竞争性假设：EDLP 也可能采用，用来稳住价格一致性（Ray 2019：EDLP 店价格变动幅度 45% → 12%）。编码方式同 Gielens et al. 2008、Ailawadi et al. 2010；参考比例：Bombaij 2020 为 65% Hi-Lo，Keller 2016 为 73% | 🔍 手工编码 |
| B6 食品/生鲜占比 | grocery sales ÷ total sales | + | 用途②（Stamatopoulos 2021；Chehrazi 2025） | 🟡 |
| B7 线上全渠道占比 | omnichannel e-commerce ÷ total sales | + | 用途⑥ | ✅（需先确认是否随时间变化） |
| B8 集团跨国程度 | 集团进入的国家数 | + | 集团层签约（Aldi Nord 9 国、Carrefour–Pricer 6 国）；可在多国摊薄学习成本 | ✅ Market Count |
| B9 同集团他国已采用 | 同集团在其他国家的 banner 中，上一年已采用的比例 | + | Keller et al. 2016 把「其他市场的先前决策」作为前因；数据中 102 行跟随母集团 | 🔧 |
| B10 所有权结构 | 合作社 / 加盟 = 1，直营 = 0 | 试点 ±，铺开 − | 决策分散，统一铺开慢（Rewe、Edeka、Spar、Consum、Coop）；但 Levin 1987 发现非连锁企业先采用，个别店主可能更早试点。所以对两个里程碑的预测不同 | 🔍 手工编码 |
| B11 会员计划 | 有会员计划 = 1 | + | 有数字化能力；也是个性化定价的前提（James 2026 报道的 Walmart 专利） | 🔍 可参照 Bombaij & Dekimpe 2020 的编码 |
| B12 新店型 / 翻新 | 当年是否推出新店型或大规模翻新 | + | Das et al. 2009 的年份效应；ESL 常随新店型一起上（AH 新店型、Netto 3.0） | 🔍 部分可从事件表 Update 获取 |

### C. 竞争与传染

| 变量 | 定义 / 测量 | 预期方向 | 依据 | 来源 |
|---|---|---|---|---|
| C1 国内竞争者已采用比例 | 同国其他 banner 上一年已采用的份额加权比例；分同业态 / 不同业态两组，加二次项 | 先 +，可能趋平 | Gielens & Dekimpe 2007：先正当化、后阻吓，呈倒 U 形（技术采用没有抢占店址，阻吓可能较弱）；Basker & Simcoe：竞争者采用的网络效应；Vomberg et al. 2025：普及后消费者反弹变小 | 🔧 |
| C2 邻国竞争者已采用比例 | 相邻国家 banner 的采用比例 | + | Bombaij & Dekimpe 2020：邻国竞争者的选择也有影响；在 M3 里也可当工具变量 | 🔧 |
| C3 市场集中度 | 国家前 5 大份额之和（CR5） | − | Levin et al. 1987：集中度低的市场先采用 | 🔧 |
| C4 大卖场竞争强度 | 国内大卖场业态的销售份额 | − | Beck, Grajek & Wey 2011：大卖场竞争降低长期采用水平 | 🔧 |
| C5 供应商在该国的装机基础 | 主要供应商在该国已服务的 banner 数 | + | 本地有服务网络和集成商，采用成本更低；类比 Basker & Simcoe 的渠道网络效应 | 🔧 |

### D. 国家 × 年层面

| 变量 | 定义 / 测量 | 预期方向 | 依据 | 来源 |
|---|---|---|---|---|
| D1 零售业人工成本 | 小时人工成本指数，NACE G（批发零售） | + | 用途①；Levin et al. 1987：工资高的地区先采用 | 🔍 Eurostat `lc_lci_r2_q`（细到 G 门类，G47 需确认是否可得） |
| D2 最低工资大幅上调 | 当年最低工资涨幅 ≥ 10% 的 dummy（如德国 2022-10 涨至 €12、荷兰 2023-01 上调约 10%） | + | 外生的人工成本冲击，时点不由零售商决定，有助于识别 | 🔍 各国官方（日期需逐一核实） |
| D3 食品通胀 | HICP 食品分项的年变化 | + | 通胀高时改价次数激增，用途①的价值上升 | 🔍 Eurostat HICP |
| D4 30 天最低价规则 | 该国开始适用 Omnibus Article 6a 之后 = 1 | +（Hi-Lo 更强） | 用途⑤：每次促销都要标示 30 天最低价 | 🔍 各国转化法（比利时 2022-05-28 已核实） |
| D5 Nutri-Score 推行 | 该国正式推行之后 = 1 | + | 用途⑤；Vandevijvere & Berger 2021 | 🔍 已核实法国 2017-10、卢森堡 2021-05，其余待查 |
| D6 文化：不确定性规避 | Hofstede 分数（不随时间变） | − | 消费者对「价格随时变」更反感（参照 Keller 2016 的国家变量选择） | 🔍 Hofstede et al. 2010 |
| D7 就业保护 | OECD 就业保护指数 | 控制变量 | Beck et al. 2011 发现无显著影响；放进模型以排除其影响 | 🔍 OECD |
| D8 人均 GDP | log GDP per capita | 控制变量 | Levin 1987（收入高者先采用）；Bombaij 2020 也控制了 | 🔍 Eurostat / 世界银行 |

### E. 时间
- **年份固定效应**：吸收硬件价格下降和全欧共同趋势。Coresight 估计全球 ESL 市场 2021 年约 8.5 亿美元、2024 年 16 亿美元；Walmart 的大单进一步压低价签单价（每个 6–8 美元）。

### F. 后果变量（第二阶段）

| 变量 | 定义 | 依据 | 来源与注意 |
|---|---|---|---|
| F1 单位面积销售额 | 销售额 ÷ 营业面积 | Bombaij & Dekimpe 2020（沿用 Reinartz & Kumar 1999）；Gielens & Dekimpe 2001 | ✅ 但单店面积是估算值：面积要么不变、要么只随门店数变，所以这个指标实际上主要反映销售额变化 |
| F2 log 销售额 | 门店销售额 | Ray et al. 2019：营收 +7.3% | ✅ 主后果变量（最干净） |
| F3 销售增长率 | Sales YoY % | — | ✅ |
| F4 单店销售额 | 销售额 ÷ 门店数 | 剔除扩张的影响 | ✅ |
| F5 国内市场份额 | banner 销售额 ÷ 国家合计 | 竞争效应 | 🔧 |
| （机制）毛利率、人工成本 | — | Stamatopoulos 2021 的主要效应在毛利上 | 只有集团年报有，作补充分析 |

**效应大小的预期**：

| 来源 | 估计 |
|---|---|
| 供应商说法（SES-imagotag，Coresight 2021 引，偏乐观） | 营收 +2–5% |
| Ray et al. 2019（2 店） | 营收 +7.3% |
| Stamatopoulos et al. 2026（100+ 店） | 定价行为几乎不变 |

在 banner × 年数据上，预期效应顶多几个百分点，样本约 45–50 个铺开的 banner。必须先做功效分析，并准备好解读零效应：报告最小可检测效应，参照 Stamatopoulos 2026 的写法。

### G. 后果模型的调节变量
- **G1 Hi-Lo**（B5）：Ray et al. 2019 显示两种策略从 ESL 获益的方式不同。
- **G2 业态**（B4）：Bombaij 2020 发现会员计划在折扣店效果更弱，ESL 可能有类似的业态差异。
- **G3 采用范围（仅生鲜 vs 全店）**：仅生鲜主要是降价减损，全店更容易被顾客察觉（对应 [[ESL]] 的信号渠道）。
- **G4 国内采用普及度**（C1 在铺开当年的值）：Vomberg et al. 2025 的习惯化效应，普及度高时负面反应更小。
- **G5 会员计划**（B11）：有个性化定价能力的零售商，更可能引发 Priester et al. 2020 所说的公平性顾虑。

---

## 5. 推荐模型（主模型尽量简单，复杂方法只作稳健性检验）

### M1 前因主模型：离散时间风险模型（discrete-time hazard，logit）
- **数据怎么排**：每个 banner 从 2006 年（或进入市场的年份）开始，每年一行，直到试点那年（该年 `adopt = 1`）为止，之后的年份删掉。从未采用的 banner 一直排到 2025 年，`adopt` 全为 0。
- **模型**：`adopt_it = 1` 的概率 = logit(年份效应 + 国家效应 + β·X_i,t−1)。
- **含义**：「在还没采用的 banner 中，某一年开始采用的概率」受哪些因素影响。系数取指数即为优势比（odds ratio）：大于 1 表示更早采用。
- **为什么选它**：和普通 logit 一样好估计、好解释，又正确处理了时间和删失。Gielens & Dekimpe 2007、Levin et al. 1987、Basker & Simcoe 都用风险模型思路。
- **标准误**：按母集团聚类（同集团 banner 不独立）。
- **软件**：Stata `logit adopt x1 x2 i.year i.country, vce(cluster group) or`；R `glm(adopt ~ x + factor(year) + factor(country), family = binomial)`，再加聚类稳健标准误。
- **稳健性检验**：
  - 换成 complementary log-log，与比例风险模型等价；
  - 按国家分层的 Cox 模型（Gielens & Dekimpe 2007）；
  - 剔除 `follows parent` 的 banner；
  - 前 10 / 前 15 / 全部 banner。

### M2 铺开速度
- **样本**：已试点的 banner。
- **因变量**：`rollout_years`。仍未达到多数铺开的视为右删失。
- **模型**：同样用离散时间风险模型（事件 = 达到多数铺开），或在完整数据上用 OLS 估计 log(rollout_years)。
- **核心预测**：B2 门店数和 B10 合作社 / 加盟会减慢铺开（Levin et al. 1992）。

### M3 后果主模型：事件研究（event study）+ 交错 DiD
- **模型**：y_it = banner 固定效应 + 年份固定效应 + Σ_k δ_k · 1[t − 铺开年 = k]，k = −4 … +4，以 k = −1 为基准。
- **怎么读**：δ_k 画成图。采用前（k < 0）应接近 0，说明没有事先趋势；采用后的 δ_k 就是效应。
- **处理时间交错的问题**：各 banner 铺开年不同，直接用普通双向固定效应会把「早采用者」当成「晚采用者」的对照，效应随时间变化时结果会偏。用 Callaway & Sant'Anna 2021 的估计量，只拿「尚未采用」的 banner 当对照。
  - Stata `csdid`，R `did` 包，输入数据格式和 M1 差不多。
- **对照组**：尚未铺开的 banner，加上从未采用的 banner。
- **标准误**：按母集团聚类。

### M4 调节效应
- 按调节变量分组，分别跑 M3，比较各组的 δ。比如 Hi-Lo 组 vs EDLP 组、仅生鲜 vs 全店、高普及国家 vs 低普及国家。
- 这比在模型里放交互项直观，也能避开交错 DiD 中交互项的偏误。

### M5（可选）匹配度
- 用 M1 预测每个 banner 每年的采用概率，定义「该上没上」= 预测概率高但实际未采用。
- 检验这类 banner 之后的销售表现是否更差。
- 依据：Keller, Dekimpe & Geyskens 2016 的 congruence 检验；Gielens & Dekimpe 2007 发现偏离行业惯例会损害效率。

### 自选择的稳健性检验（只作补充）
- **问题**：表现好的 banner 可能本来就更早采用。
- **检验 1**：事件研究图中的采用前趋势（M3 已含）。
- **检验 2**：匹配。为每个采用者按规模和采用前增长率找一个未采用者（Basker & Simcoe），再跑 M3。
- **检验 3**：Heckman 式两步法。第一步用 M1，工具变量是 C2 邻国竞争者采用比例（影响自己是否采用，但不太可能直接影响自己的销售）；第二步加入逆米尔斯比。做法同 Bombaij & Dekimpe 2020、2022 和 Geyskens et al. 2015。如果校正项不显著，就回到主模型，Bombaij 的处理方式也是这样。

---

## 6. 一页描述性报告与监管背景（保留）
- **定位**：现有 ESL 实证都来自单一零售商、少数门店：
  - Ray et al. 2019：2 店；
  - Stamatopoulos et al. 2021：1 家英国零售商；
  - Chehrazi et al. 2025：1 店 26 个商品；
  - Stamatopoulos et al. 2026：1 家美国连锁、100 多家店；
  - Vandevijvere & Berger 2021：比利时 Delhaize 43 家试点店。

  本数据是第一张跨国、banner 级的 ESL 采用图景。
- **可呈现**：各国首次采用年份分布（2020 年是峰值）、扩散曲线、业态对比、供应商份额、仅生鲜 vs 全店。
- **监管对比**：
  - 美国：联邦和 14 个州提出禁用或限制 ESL 的法案（Stamatopoulos et al. 2026 表 1）。
  - 欧盟：GDPR 针对个性化定价（Zuiderveen Borgesius & Poort 2017）；30 天最低价规则规范的是降价标示；ESL 本身不受限。数字市场法和数字服务法对算法定价只有零星涉及（Spann et al. 2024）。

---

## 7. 待决定
- [ ] 采用范围编码：4 条分歧与 7 条存疑的处理规则（临时结果在 scratchpad，尚未写入 CSV）。
- [ ] `follows parent` 的处理方式（主分析赋集团年份 vs 剔除）。
- [ ] B5 Hi-Lo、B10 所有权、B11 会员计划的手工编码。
- [ ] 核实 D2（最低工资）、D4（各国 Omnibus 适用日期）、D5（Nutri-Score）的具体日期。
- [ ] 确认 B7 线上占比是否随时间变化；确认 Flywheel 哪些字段是实测值。
- [ ] 补进 Zotero：Levin et al. 1987、1992；Beck et al. 2011；Das et al. 2009；Stamatopoulos et al. 2021；Callaway & Sant'Anna 2021。

---

## 来源（网络检索部分）
- Levin, Levin & Meisel 1987：[IDEAS](https://ideas.repec.org/a/tpr/restat/v69y1987i1p12-17.html)
- Levin, Levin & Meisel 1992：[IDEAS](https://ideas.repec.org/a/tpr/restat/v74y1992i2p345-50.html)
- Beck, Grajek & Wey 2011：[EconPapers](https://econpapers.repec.org/RePEc:taf:applec:v:43:y:2011:i:14:p:1737-1748)、[DIW 工作论文](https://econpapers.repec.org/RePEc:diw:diwwpp:dp523)
- Basker 关于扫描仪扩散的综述：[NBER w17825](https://www.nber.org/papers/w17825.pdf)
- Stamatopoulos, Bassamboo & Moreno 2021：[Kellogg](https://www.kellogg.northwestern.edu/academics-research/research/detail/2021/the-effects-of-menu-costs-on-retail-performance-evidence/)、[INFORMS](https://pubsonline.informs.org/doi/fpi/10.1287/mnsc.2019.3551)
- Stamatopoulos, Sanders & Bray（SSRN）：[SSRN 5271491](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5271491)
- Omnibus / Article 6a：[EUR-Lex 98/6 合并版](https://eur-lex.europa.eu/eli/dir/1998/6/2022-05-28/eng)、[比利时实施（DLA Piper）](https://www.dlapiper.com/en-be/insights/publications/2022/05/belgium-adopts-law-implementing-the-omnibus-directive)、[欧盟法院 Aldi Süd 案（Baker McKenzie）](https://insightplus.bakermckenzie.com/bm/international-commercial-trade/european-union-the-cjeu-confirms-that-a-price-reduction-must-be-calculated-based-on-the-lowest-price-in-the-last-30-days)
- Nutri-Score：[OECD](https://www.oecd.org/en/publications/healthy-eating-and-active-lifestyles_40f65568-en/full-report/component-7.html)、[卢森堡 2021 报告](https://mpc.gouvernement.lu/dam-assets/le-minist%C3%A8re/consodur/Report-2021-Steering-committee-VF2.pdf)
- ESL 供应链库存（芯片短缺假设的反证）：[Digitimes 2022-12](https://apps.digitimes.com/news/a20221214PD206/electronic-shelf-label.html?mod=0)
- Eurostat 人工成本：[Labour cost index – recent trends](https://ec.europa.eu/eurostat/statistics-explained/index.php/Labour_cost_index_-_recent_trends)

相关：[[ESL]] · [[2026-10-20 Meeting]] · [[2026-11-20 Meeting]] · [[防备成本 low-effort shopping & cost]]
