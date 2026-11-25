---
created: 2026-11-24
updated: 2026-11-25
tags: [project, ESL, 研究设计, 变量, 计量]
---

# ESL 研究框架与变量

承接 [[ESL顾客层面]]（机制与测量）、[[2026-10-20 Meeting]]（数据库设计、解释变量）、[[2026-11-20 Meeting]]（西欧完成、一页报告）。
依据：Zotero「ESL」与「Example paper Project1」两个分类的文献；网络检索补充的零售技术采用文献、欧盟法规与数据源；对现有数据（`global-esl/data/processed/esl_by_country/`、`supermarket_all.csv`）的核查。

---

## 1. 文献脉络

本研究涉及四支文献，各自提供的内容不同。

**(1) ESL 的实证研究：均基于单一零售商**
- Ray et al. 2019：两家门店（一家 EDLP、一家 Hi-Lo）的伪田野实验，DiD。ESL 后营收 +7.3%，作用方式因定价策略而异。
- Stamatopoulos, Bassamboo & Moreno 2021（Management Science）：一家国际零售商 2015 年采用 ESL。毛利率上升幅度超过人工节省可解释的部分；价格变动更频繁、幅度更小，以降价为主；效应集中在短保质期品类。
- Chehrazi et al. 2025（Marketing Science，经 Stamatopoulos et al. 2026 转引）：单店、26 个商品，主要用于临期降价。
- Stamatopoulos, Sanders & Bray 2026（SSRN 工作论文）：一家美国连锁 100 余家门店分 37 波安装。未发现涨价式 surge pricing，定价行为与 NielsenIQ 中同州 32 家连锁无差异。
- Vandevijvere & Berger 2021：比利时 Delhaize 用 ESL 展示 Nutri-Score，43 家门店配对 DiD，对购买的影响有正有负。
- → 就目前检索所及，尚无跨零售商、跨国家的 ESL 采用研究。

**(2) 消费者对动态定价的反应**
- Vomberg, Homburg & Sarantopoulos 2025（IJRM）：算法动态定价降低信任、延长比价；顾客形成经验或该做法成为市场惯例后，信任下降减弱。
- Priester, Robbert & Roth 2020：个人价格比群体价格更被视为不公平；基于位置的定价比基于购买历史的定价更被视为不公平。
- Winer 2005（MSI 专著）：多数超市顾客记不准所付价格（Dickson & Sawyer 1990）；参考价格效应不对称，涨价的负面影响大于降价的正面影响。
- Coresight 2024 美国调查（n = 400）：25% 近期去过有 ESL 的门店；22% 表示会少去或不去，净值 −2%。

**(3) 零售技术的采用与扩散（与本研究最接近的方法先例）**
- Levin, Levin & Meisel 1987（REStat）：超市采用收银扫描仪的比例风险模型。扩散早期，平均店面较大、不属于连锁、所在市场集中度较低、收入与工资较高的企业较早采用；随扩散推进，集中度、份额与规模的作用减弱。
- Levin, Levin & Meisel 1992（REStat）：市场份额大的企业较早开始采用，但在自身门店间扩散较慢。
- Beck, Grajek & Wey 2011（Applied Economics）：欧洲 10 国 1981–1996 年扫描仪扩散。国家间差异主要在长期饱和水平；大卖场竞争降低长期采用水平；就业保护法规无显著影响。
- Das, Falaris & Mulligan 2009：扫描仪采用存在门店年份效应，新店与翻新店较易采用。
- Basker & Simcoe（NBER）：UPC 条形码采用中的竞争者效应与渠道网络效应；采用后影响用匹配样本事件研究估计。

**(4) 多国 banner 面板研究（研究设计模板）**
- Bombaij & Dekimpe 2020：27 国 358 个 banner，会员计划对销售效率的影响，按设计、零售商、国家特征调节；用控制函数检验自选择。
- Bombaij, Gelper & Dekimpe 2022：45 国约 900 个限时会员计划；用 Heckman 两步法和竞争者过去的决策作工具变量。
- Gielens & Dekimpe 2007：欧洲前 75 大零售商进入东欧的时机，按国家分层的 Cox 模型；竞争者先行呈倒 U 形影响（先正当化、后阻吓）。
- Keller, Dekimpe & Geyskens 2016：先估计自有品牌命名策略的前因，再检验与预测一致的选择是否绩效更好。
- Geyskens, Gielens & Wuyts 2015：采购联盟规模对零售商生产率的影响。
- Gielens & Dekimpe 2001：进入时的决策对长期销售与每平方米销售额的影响。

---

## 2. 现有数据与样本规则

**数据现状**
- status 表共 750 行（banner × 国家）。`Collection status`：
  - `collected` 131 行、`no evidence` 52 行：已检索；
  - `follows parent` 102 行：状态随母集团；
  - `not-started` 323 行、`not assessed` 61 行：未检索；
  - `excluded` 76 行：已排除。
- 有带日期里程碑的 banner：115 个；其中达到多数门店铺开的：51 个。
- 首次事件年份：
  - 2003、2004 各 1 个（Eroski、Carrefour 西班牙）；
  - 2010–2019 共 36 个；
  - 2020 年 22 个；
  - 2021–2025 共 47 个；
  - 2026 年 8 个。
- 各国检索覆盖不均。例如意大利 157 行中检索了 26 行，德国、法国全部检索。
- `supermarket_all.csv` 的数据期为 2006–2025 年，2026 年起为预测值。以下字段为估算值，多数 banner 序列历年不变，只能作横截面特征：平均收银台数（全部序列不变）、食品销售占比（94% 的序列不变）、单店面积（74% 的序列不变）。

**样本规则**
1. 只纳入已检索的 banner（`collected`、`no evidence`），以免把「未检索」误作「未采用」。
2. `follows parent`：主分析把母集团的采用年份赋给该 banner；稳健性检验中剔除。
3. 观察期 2006–2025 年。2006 年前已采用的 2 个 banner 不进入风险集；2026 年的事件在本期内按右删失处理。
4. 按各国前 10、前 15（Bombaij & Dekimpe 2020 的做法）与全部 banner 分别估计，检验覆盖偏差的影响。

---

## 3. ESL 的六种用途

前因变量由下表推导。现有实证多把 ESL 视为降低改价成本的技术；零售商公开说明的用途更多样，各用途的重要性随零售商与国家而异。

| 用途 | 证据 | 相关因素 |
|---|---|---|
| ① 节省换签人工 | Levy et al. 1997：换签成本约占营收 0.7%、净利 35%（Stamatopoulos et al. 2026 转引）；Spann et al. 2024：合作零售商在 ESL 前规定每年只改价两次 | 人工成本、门店数、SKU 数 |
| ② 生鲜与临期降价 | Stamatopoulos et al. 2021：效应集中于短保质期品类；Chehrazi et al. 2025；Ray et al. 2019：EDLP 店用于减损 | 生鲜占比、业态 |
| ③ 试价与价格学习 | Ray et al. 2019：Hi-Lo 店价格对过去价格的依赖由 3.21 周降至 2.13 周 | Hi-Lo、促销强度 |
| ④ 分店差异定价 | Ray et al. 2019 引 DellaVigna & Gentzkow 2019：统一定价平均损失约 7% 利润 | 门店数、地域分散度 |
| ⑤ 信息展示与合规 | Ray et al. 2019：意大利生鲜产地标示法；Vandevijvere & Berger 2021：Nutri-Score；欧盟 30 天最低价规则（见 D4） | 标签法规、Nutri-Score、Omnibus |
| ⑥ 门店运营 | Coresight 2021：价签闪灯辅助线上订单拣货与补货 | 线上全渠道占比 |

---

## 4. 研究设计

- **前因**：哪些因素影响 banner 开始试点 ESL 的时间（M1）。
- **铺开速度**：开始试点后，铺开到多数门店所需的时间（M2）。对应 Levin et al. 1992 对「开始采用」与「企业内扩散」的区分。
- **后果**：铺开后 banner 销售表现的变化，及其随定价策略、业态、国家特征的差异（M3、M4）。
- **匹配度（可选）**：采用决策与按自身条件预测的决策是否一致，是否影响后续表现（M5）。参照 Keller et al. 2016、Gielens & Dekimpe 2007。

---

## 5. 变量

图例：✅ `supermarket_all.csv` 已有且随时间变化 · 🟡 已有但多数序列历年不变 · 🔧 可由已有数据计算 · 🔍 需另行收集

### A. 采用变量

| 变量 | 定义 | 用途 | 来源 |
|---|---|---|---|
| `pilot_year` | 首家门店上线 ESL 的年份 | M1 的事件 | 🔧 事件表 Pilot；缺失时以 Announced 替代并标注 |
| `majority_year` | 过半门店完成的年份 | M2 的终点；M3 的处理开始时间 | 🔧 事件表 Majority |
| `rollout_years` | `majority_year` − `pilot_year` | M2 因变量 | 🔧 |
| `ESL_scope` | 全店 / 仅生鲜 / 其他部分品类 / 未说明 | 调节变量；稳健性检验 | 🔍 已完成双人编码，待确认（见 §8） |
| `vendor` | 主要供应商 | 构造 C5；描述统计 | 🔧 事件表 Vendor |

### B. banner 层面

| 变量 | 测量 | 预期方向 | 依据 | 来源 |
|---|---|---|---|---|
| B1 规模 | log 门店销售额，滞后一年 | + | 固定投资可在更大销售额上摊薄；Levin et al. 1987 | ✅ |
| B2 门店数 | log 门店数 | 试点 +；铺开 − | 用途①④随门店数增加；Levin et al. 1992：大企业开始早、内部扩散慢 | ✅ |
| B3 单店面积 | 每店平方英尺 | + | 店面越大、SKU 越多，换签量越大；Levin et al. 1987 | 🟡 |
| B4 业态 | hypermarket、discounter dummy，超市为基准 | hypermarket +；discounter 不设方向 | 大卖场 SKU 最多；折扣店 SKU 少但人效要求高；分类同 Bombaij & Dekimpe 2020 | ✅ Channel |
| B5 定价策略 | Hi-Lo = 1，EDLP = 0 | Hi-Lo + | Hi-Lo 改价与促销更频繁，用途①③⑤价值更高（Ray et al. 2019；Stamatopoulos et al. 2021）。另一种可能：EDLP 也会采用，用于维持价格一致（Ray et al. 2019 中 EDLP 店平均价格变动幅度由 45.3% 降至 11.7%）。编码参照 Gielens et al. 2008、Ailawadi et al. 2010；Bombaij & Dekimpe 2020 样本中 65% 为 Hi-Lo，Keller et al. 2016 为 73% | 🔍 手工编码 |
| B6 食品销售占比 | grocery sales ÷ total sales | + | 用途②；Stamatopoulos et al. 2021 | 🟡 |
| B7 线上全渠道占比 | omnichannel e-commerce ÷ total sales | + | 用途⑥ | ✅ 需确认是否随时间变化 |
| B8 集团跨国程度 | 集团经营的国家数 | + | 合同常在集团层签订（Aldi Nord 宣布 9 国铺开；Carrefour 与 Pricer 签了 6 国合同） | ✅ Market Count |
| B9 同集团他国已采用 | 同集团其他国家 banner 中，上一年已采用的比例 | + | Keller et al. 2016 以「其他市场的先前决策」为前因；数据中 102 行状态随母集团 | 🔧 |
| B10 所有权结构 | 合作社或加盟体系 = 1 | 试点不设方向；铺开 − | 决策分散于独立店主，统一铺开较慢（如 Rewe、Edeka、Spar、Consum、Coop）；Levin et al. 1987 发现非连锁企业较早采用，个别店主可能先行试点 | 🔍 手工编码 |
| B11 会员计划 | 有会员计划 = 1 | + | 反映数字化能力，也是个性化定价的前提（James 2026 报道的 Walmart 专利） | 🔍 编码参照 Bombaij & Dekimpe 2020 |
| B12 新店型或翻新 | 当年推出新店型或大规模翻新 = 1 | + | Das et al. 2009 的门店年份效应；ESL 常随新店型引入（如 Albert Heijn 新店型、Netto 3.0） | 🔍 部分见事件表 Update |

### C. 竞争环境

| 变量 | 测量 | 预期方向 | 依据 | 来源 |
|---|---|---|---|---|
| C1 国内竞争者采用比例 | 同国其他 banner 上一年已采用的份额加权比例；分同业态 / 不同业态，含二次项 | 正向，可能递减 | Gielens & Dekimpe 2007 的倒 U 形（技术采用不涉及店址抢占，阻吓作用可能较弱）；Basker & Simcoe 的竞争者效应；Vomberg et al. 2025：做法成为市场惯例后，消费者负面反应减弱 | 🔧 |
| C2 邻国竞争者采用比例 | 相邻国家 banner 的已采用比例 | + | Bombaij & Dekimpe 2020：邻国竞争者的选择对采用有影响；亦可作 M3 的候选工具变量 | 🔧 |
| C3 市场集中度 | 国家前五大 banner 份额之和（CR5） | − | Levin et al. 1987 | 🔧 |
| C4 大卖场竞争强度 | 国内大卖场业态的销售份额 | − | Beck, Grajek & Wey 2011 | 🔧 |
| C5 供应商本地基础 | 主要供应商在该国已服务的 banner 数 | + | 本地有服务网络时采用成本较低；类比 Basker & Simcoe 的渠道网络效应 | 🔧 |

### D. 国家 × 年

| 变量 | 测量 | 预期方向 | 依据 | 来源 |
|---|---|---|---|---|
| D1 零售业人工成本 | 小时人工成本指数，NACE G（批发零售） | + | 用途①；Levin et al. 1987 | 🔍 Eurostat `lc_lci_r2_q`；G47 层级是否可得待确认 |
| D2 最低工资大幅上调 | 当年法定最低工资涨幅 ≥ 10% = 1 | + | 时点由政府决定，可视为相对外生的人工成本冲击。候选事件：德国 2022-10（升至 €12）、荷兰 2023-01 | 🔍 各国官方来源，日期待逐一核实 |
| D3 食品通胀 | HICP 食品分项年变化率 | + | 通胀期改价次数增加，用途①的价值上升 | 🔍 Eurostat HICP |
| D4 30 天最低价规则 | 该国开始适用 Omnibus Directive（2019/2161）所增 Article 6a 后 = 1 | +，Hi-Lo 更强 | 宣布降价时必须标示此前至少 30 天内的最低价。转化期限 2021-11-28，各国适用日期不同；欧盟法院 2024-09 Aldi Süd 案（C-330/23）确认降价幅度须以该价格为基准计算。促销越频繁，合规负担越重（用途⑤） | 🔍 各国转化法；比利时 2022-05-28 已核实 |
| D5 Nutri-Score 推行 | 该国正式推行后 = 1 | + | 用途⑤；Vandevijvere & Berger 2021 | 🔍 已核实法国 2017-10、卢森堡 2021-05，其余待查官方来源 |
| D6 不确定性规避 | Hofstede 分数，不随时间变化 | − | 消费者对价格频繁变动的接受度可能较低；国家文化变量的选择参照 Keller et al. 2016 | 🔍 Hofstede et al. 2010 |
| D7 就业保护 | OECD 就业保护指数 | 控制变量 | Beck et al. 2011 未发现显著影响 | 🔍 OECD |
| D8 人均 GDP | log GDP per capita | 控制变量 | Levin et al. 1987；Bombaij & Dekimpe 2020 | 🔍 Eurostat / 世界银行 |

### E. 时间
- **年份固定效应**：吸收硬件价格下降等全欧共同趋势。Coresight 估计全球 ESL 支出 2021 年约 8.5 亿美元、2024 年约 16 亿美元；Walmart 的大规模订单可能进一步压低单价（每个价签 6–8 美元，Solum 数据）。

### F. 后果变量

| 变量 | 定义 | 依据 | 说明 |
|---|---|---|---|
| F1 log 门店销售额 | — | Ray et al. 2019 | ✅ 主后果变量 |
| F2 单店销售额 | 销售额 ÷ 门店数 | 排除门店扩张的影响 | ✅ |
| F3 销售增长率 | Sales YoY % | — | ✅ |
| F4 单位面积销售额 | 销售额 ÷ 营业面积 | Bombaij & Dekimpe 2020；Gielens & Dekimpe 2001 | ✅ 单店面积多为估算值，变化主要来自销售额，与 F1、F2 高度相关 |
| F5 国内市场份额 | banner 销售额 ÷ 国家合计 | 竞争效应 | 🔧 |
| 机制变量：毛利率、人工成本 | — | Stamatopoulos et al. 2021 的主要效应在毛利率 | 仅集团年报可得，作补充分析 |

**效应量参照**

| 来源 | 估计 |
|---|---|
| SES-imagotag（Coresight 2021 引，供应商自报） | 营收 +2–5% |
| Ray et al. 2019（两家门店） | 营收 +7.3% |
| Stamatopoulos et al. 2026（100 余家门店） | 定价行为无显著变化 |

在 banner × 年的年度数据上，可预期的效应在几个百分点以内。可用的处理组为约 51 个达到多数铺开的 banner（晚于 2025 年者需剔除）。估计前应做功效分析；若结果不显著，应报告最小可检测效应（参照 Stamatopoulos et al. 2026）。

### G. 后果模型的调节变量
- **G1 定价策略**（B5）：Ray et al. 2019 显示 EDLP 与 Hi-Lo 从 ESL 获益的方式不同。
- **G2 业态**（B4）：Bombaij & Dekimpe 2020 发现会员计划对折扣店的效果较弱，ESL 可能存在类似差异。
- **G3 采用范围**（`ESL_scope`）：仅生鲜对应用途②；全店采用更易被顾客察觉，对应 [[ESL顾客层面]] 中的信号渠道。
- **G4 国内普及度**（C1 在铺开当年的取值）：Vomberg et al. 2025 的习惯化效应意味着，普及度高时顾客的负面反应较小。
- **G5 会员计划**（B11）：具备个性化定价能力的零售商，更可能引起 Priester et al. 2020 所述的公平性顾虑。

---

## 6. 模型

主模型尽量简单，其余方法作为稳健性检验。

### M1 前因：离散时间风险模型（logit）
- **数据结构**：每个 banner 自 2006 年（或首次出现在数据中的年份）起每年一行，直至试点当年（该年 `adopt = 1`），此后的年份不再纳入。未采用的 banner 排至 2025 年，`adopt` 全为 0。
- **设定**：Pr(`adopt_it` = 1 | 此前未采用) = logit(年份效应 + 国家效应 + β·X_i,t−1)。
- **解释**：在尚未采用的 banner 中，某一年开始采用的条件概率如何随各变量变化。exp(β) 为优势比，大于 1 表示采用较早。
- **选择理由**：估计与解释同普通 logit，同时处理了时间与右删失。Levin et al. 1987、Gielens & Dekimpe 2007、Basker & Simcoe 均采用风险模型。
- **标准误**：按母集团聚类。
- **实现**：Stata `logit adopt x1 x2 i.year i.country, vce(cluster group) or`；R `glm(adopt ~ x + factor(year) + factor(country), family = binomial)`，配合聚类稳健标准误。
- **稳健性检验**：
  - complementary log-log 链接，对应分组时间的比例风险模型；
  - 按国家分层的 Cox 模型（Gielens & Dekimpe 2007）；
  - 剔除 `follows parent`；
  - 前 10、前 15、全部 banner。

### M2 铺开速度
- **样本**：已试点的 banner。
- **设定**：离散时间风险模型，事件为达到多数铺开；尚未达到者右删失。另作对照：以已完成者的 log(`rollout_years`) 为因变量的 OLS。
- **主要检验**：B2 门店数、B10 所有权结构对铺开速度的影响（Levin et al. 1992）。

### M3 后果：事件研究
- **设定**：y_it = banner 固定效应 + 年份固定效应 + Σ_k δ_k · 1[t − `majority_year` = k]，k = −4 … +4，以 k = −1 为基准。
- **解读**：把 δ_k 作图。k < 0 的系数检验采用前是否已有差异趋势；k ≥ 0 的系数为采用后的效应。
- **估计量**：处理时间交错且效应可能随时间变化时，普通双向固定效应估计会以较早采用者作为较晚采用者的对照，可能产生偏误。采用 Callaway & Sant'Anna 2021 的估计量，以尚未采用和从未采用的 banner 作对照（Stata `csdid`；R `did` 包）。
- **标准误**：按母集团聚类。

### M4 调节效应
- 按调节变量分组分别估计 M3，比较各组效应（如 Hi-Lo 与 EDLP、仅生鲜与全店、高普及国家与低普及国家）。
- 分组估计比在交错 DiD 中加入交互项更易解释。

### M5 匹配度（可选）
- 用 M1 预测每个 banner 每年的采用概率，识别预测概率高而未采用、以及预测概率低而采用的 banner。
- 检验这两类 banner 的后续销售表现是否较差（Keller et al. 2016；Gielens & Dekimpe 2007）。

### 自选择的稳健性检验
- **问题**：表现较好的 banner 可能较早采用。
- **检验**：
  1. M3 中采用前系数的检验。
  2. 匹配样本：按规模与采用前增长率为每个采用者匹配一个未采用者，再估计 M3（Basker & Simcoe）。
  3. Heckman 两步法：第一步为 M1，以 C2 邻国竞争者采用比例作排他变量，其合理性需论证；第二步加入逆米尔斯比。做法参照 Bombaij & Dekimpe 2020、2022 与 Geyskens et al. 2015。校正项不显著时，报告未校正的主模型（同 Bombaij & Dekimpe 2020 的处理）。

---

## 7. 描述性报告与监管背景
- **定位**：现有 ESL 证据均来自单一零售商（见 §1(1)）。本数据提供跨 15 国、banner 层面的采用记录。
- **可呈现内容**：各国首次采用年份分布、扩散曲线、业态比较、供应商份额、采用范围。
- **监管对比**：
  - 美国：联邦层面与 14 个州提出禁止或限制 ESL 的法案（Stamatopoulos et al. 2026，表 1）。
  - 欧盟：GDPR 约束涉及个人数据的个性化定价（Zuiderveen Borgesius & Poort 2017）；Article 6a 规范降价的标示方式；目前没有针对 ESL 本身的限制。数字市场法与数字服务法对算法定价仅有零星涉及（Spann et al. 2024）。

---

## 8. 待办
- [ ] 采用范围编码：确定 4 条分歧与 7 条存疑记录的处理规则（结果尚未写入 CSV）。
- [ ] 确定 `follows parent` 的处理方式。
- [ ] 手工编码 B5 定价策略、B10 所有权结构、B11 会员计划。
- [ ] 核实 D2、D4、D5 的各国日期。
- [ ] 确认 B7 是否随时间变化，以及 Flywheel 各字段中哪些为实测值。
- [ ] 将以下文献加入 Zotero：Levin et al. 1987、1992；Beck et al. 2011；Das et al. 2009；Stamatopoulos et al. 2021；Callaway & Sant'Anna 2021。

---

## 来源（网络检索部分）
- Levin, Levin & Meisel 1987：[IDEAS](https://ideas.repec.org/a/tpr/restat/v69y1987i1p12-17.html)
- Levin, Levin & Meisel 1992：[IDEAS](https://ideas.repec.org/a/tpr/restat/v74y1992i2p345-50.html)
- Beck, Grajek & Wey 2011：[EconPapers](https://econpapers.repec.org/RePEc:taf:applec:v:43:y:2011:i:14:p:1737-1748)、[DIW 工作论文](https://econpapers.repec.org/RePEc:diw:diwwpp:dp523)
- Basker 关于扫描仪扩散的综述：[NBER w17825](https://www.nber.org/papers/w17825.pdf)
- Stamatopoulos, Bassamboo & Moreno 2021：[Kellogg](https://www.kellogg.northwestern.edu/academics-research/research/detail/2021/the-effects-of-menu-costs-on-retail-performance-evidence/)、[INFORMS](https://pubsonline.informs.org/doi/fpi/10.1287/mnsc.2019.3551)
- Stamatopoulos, Sanders & Bray：[SSRN 5271491](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5271491)
- Omnibus / Article 6a：[EUR-Lex 98/6 合并版](https://eur-lex.europa.eu/eli/dir/1998/6/2022-05-28/eng)、[比利时实施（DLA Piper）](https://www.dlapiper.com/en-be/insights/publications/2022/05/belgium-adopts-law-implementing-the-omnibus-directive)、[欧盟法院 Aldi Süd 案（Baker McKenzie）](https://insightplus.bakermckenzie.com/bm/international-commercial-trade/european-union-the-cjeu-confirms-that-a-price-reduction-must-be-calculated-based-on-the-lowest-price-in-the-last-30-days)
- Nutri-Score：[OECD](https://www.oecd.org/en/publications/healthy-eating-and-active-lifestyles_40f65568-en/full-report/component-7.html)、[卢森堡 2021 报告](https://mpc.gouvernement.lu/dam-assets/le-minist%C3%A8re/consodur/Report-2021-Steering-committee-VF2.pdf)
- Eurostat 人工成本：[Labour cost index – recent trends](https://ec.europa.eu/eurostat/statistics-explained/index.php/Labour_cost_index_-_recent_trends)

相关：[[ESL顾客层面]] · [[2026-10-20 Meeting]] · [[2026-11-20 Meeting]] · [[防备成本 low-effort shopping & cost]]
