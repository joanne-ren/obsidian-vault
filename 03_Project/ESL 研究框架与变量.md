---
created: 2026-11-24
updated: 2026-11-25
tags: [project, ESL, 研究设计, 变量, 计量]
---

# ESL 研究框架与变量


---

## 1. 文献脉络

逐篇的数据、方法与发现见 [[ESL 文献综述]]。本研究涉及三支文献：

**1.1 ESL 的实证研究**

现有研究都在单一零售商、少数门店内识别 ESL 的效应。

- **Ray et al. 2019**：意大利两家超市，一家 EDLP、一家 Hi-Lo，DiD。
  - 合并估计：营收 +7.3%，销量 +9.8%。
  - EDLP 店用 ESL 稳定价格，平均价格变动幅度由 45.3% 降至 11.7%，并用于生鲜减损。
  - Hi-Lo 店用 ESL 更快调整价格，价格对过去价格的依赖由 3.21 周降至 2.13 周。
  - 意义：ESL 的作用随定价策略而不同（B5、G1）。
- **Stamatopoulos, Bassamboo & Moreno 2021**：英国某国际零售商的 2 家处理店与 2 家对照店，2015 年上线，DiD；门店经理有定价自主权。
  - 毛利 +8.5% 至 +11.2%，销量约 +5.5%。
  - 改价次数增加，以降价为主，单次幅度变小。
  - 保质期越短的品类，毛利效应越大。
  - 意义：ESL 的主要收益来自生鲜降价（用途②）。作者把「多个零售商采用 ESL 后的竞争效应」列为未来研究方向。
- **Chehrazi, Sanders & Stamatopoulos 2025**：理论模型加两个单店试点。
  - 英国门店只装 ESL，每周改价次数 +54%。
  - 欧盟门店同时装 ESL 与可记录保质期的扩展条码，每周改价次数 +853%。
  - 结论：生鲜价格刚性主要来自库存信息不准，物理菜单成本是次要原因；ESL 的价值依赖库存信息能力（B13）。
- **Stamatopoulos, Sanders & Bray 2026**：美国一家连锁的 128 家门店，2022–2024 年分 37 波安装；在同一价格区内比较已装与未装门店。
  - 未发现涨价式 surge pricing：变化 +0.0006 个百分点，p = 0.90。
  - 改价频率与 NielsenIQ 中同州 32 家连锁无差异。
  - 意义：美国监管争议的背景；零效应的报告方式可作参照。
- **Vandevijvere & Berger 2021**：比利时 Delhaize 用 ESL 展示 Nutri-Score，43 家门店与匹配对照店，DiD。
  - 对购买营养构成的影响有正有负。
  - 意义：ESL 的信息展示用途（用途⑤、D5）。
- **行业报告（Coresight 2021、2024）**：
  - 价签单价、市场规模与供应商自报效果（营收 +2–5%，偏乐观）；
  - 零售商「只降不涨」的承诺；
  - 美国消费者调查：22% 表示会少去或不去用 ESL 的门店，净值 −2%。

这些研究说明了 ESL 的用途（§2），但无法回答哪些零售商、在什么条件下采用，也无法比较零售商与国家之间的效应差异。

**1.2 消费者对动态定价的反应**
- 动态定价降低信任、延长比价；做法成为市场惯例后，负面反应减弱（Vomberg et al. 2025）。
- 个人化价格比所有顾客同价更被视为不公平（Priester et al. 2020）。ESL 本身只能实现后者。
- 证据来自线上情境或实验，外推到实体店需要说明。

**1.3 多国 banner 面板研究**
- Bombaij & Dekimpe 2020、Bombaij et al. 2022、Gielens & Dekimpe 2001、2007、Keller et al. 2016、Geyskens et al. 2015 研究的对象分别是会员计划、自有品牌、采购联盟与国际进入，都采用「多国 banner × 年」的设计。
- 提供的模板：样本构造（各国前 15 大 banner）、变量编码（Hi-Lo、业态、规模、CR5、国家文化）、竞争者先前决策的作用、自选择的处理、匹配度检验。

**1.4 本研究的位置**：把 1.3 的设计用于 ESL 的跨国 banner 数据，并用 1.1、1.2 的机制解释采用的前因与效应差异。

---

## 2. ESL 的六种用途

前因变量由下表推导。现有实证多把 ESL 视为降低改价成本的技术；零售商公开说明的用途更多样，各用途的重要性随零售商与国家而异。

| 用途 | 证据 | 相关因素 |
|---|---|---|
| ① 节省换签人工 | Levy et al. 1997：换签成本约占营收 0.7%、净利 35%（Stamatopoulos et al. 2026 转引）；Spann et al. 2024：合作零售商在 ESL 前规定每年只改价两次 | 人工成本、门店数、SKU 数 |
| ② 生鲜与临期降价 | Stamatopoulos et al. 2021：毛利效应随保质期缩短而增大（果蔬 0.23，罐装蔬菜 0.02）；Chehrazi et al. 2025：收益依赖实时库存与保质期信息；Ray et al. 2019：EDLP 店用于减损 | 生鲜占比、业态、库存信息能力 |
| ③ 试价与价格学习 | Ray et al. 2019：Hi-Lo 店价格对过去价格的依赖由 3.21 周降至 2.13 周 | Hi-Lo、促销强度 |
| ④ 分店差异定价 | Ray et al. 2019 引 DellaVigna & Gentzkow 2019：统一定价平均损失约 7% 利润 | 门店数、地域分散度 |
| ⑤ 信息展示与合规 | Ray et al. 2019：意大利生鲜产地标示法；Vandevijvere & Berger 2021：Nutri-Score；欧盟 30 天最低价规则（见 D4） | 标签法规、Nutri-Score、Omnibus |
| ⑥ 门店运营 | Coresight 2021：价签闪灯辅助线上订单拣货与补货 | 线上全渠道占比 |

---

---

变量

图例：✅ `supermarket_all.csv` 已有且随时间变化 · 🟡 已有但多数序列历年不变 · 🔧 可由已有数据计算 · 🔍 需另行收集


### banner 层面

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
| B13 库存信息能力 | 是否采用可记录保质期的扩展条码（GS1 DataBar / DataMatrix）、实时库存系统或临期定价软件 | + | Chehrazi et al. 2025：ESL 对生鲜定价的价值取决于实时库存与保质期信息，两类技术互为补充 | 🔍 年报、新闻稿、供应商案例；可能只覆盖部分 banner |

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
| Stamatopoulos et al. 2021（两家处理店） | 毛利 +8.5% 至 +11.2%；销量 +5.5% 至 +5.7% |
| Chehrazi et al. 2025（单店试点） | 只装 ESL：每周改价次数 +54%；ESL + 扩展条码：+853% |
| Stamatopoulos et al. 2026（100 余家门店） | 定价行为无显著变化 |

在 banner × 年的年度数据上，可预期的效应在几个百分点以内。可用的处理组为约 51 个达到多数铺开的 banner（晚于 2025 年者需剔除）。估计前应做功效分析；若结果不显著，应报告最小可检测效应（参照 Stamatopoulos et al. 2026）。

### G. 后果模型的调节变量
- **G1 定价策略**（B5）：Ray et al. 2019 显示 EDLP 与 Hi-Lo 从 ESL 获益的方式不同。
- **G2 业态**（B4）：Bombaij & Dekimpe 2020 发现会员计划对折扣店的效果较弱，ESL 可能存在类似差异。
- **G3 采用范围**（`ESL_scope`）：仅生鲜对应用途②；全店采用更易被顾客察觉，对应 [[ESL顾客层面]] 中的信号渠道。
- **G4 国内普及度**（C1 在铺开当年的取值）：Vomberg et al. 2025 的习惯化效应意味着，普及度高时顾客的负面反应较小。
- **G5 会员计划**（B11）：具备个性化定价能力的零售商，更可能引起 Priester et al. 2020 所述的公平性顾虑。
- **G6 定价权集中程度**：门店能否自主改价，还是由总部统一定价。Stamatopoulos et al. 2021 的门店经理有完全的定价自主权；Ray et al. 2019 引 DellaVigna & Gentzkow 2019 指出，美国连锁多为统一定价。定价越集中，ESL 用于门店层面临期降价的空间越小。需手工编码，可能只能区分「合作社 / 加盟」与「直营」（与 B10 相关）。

---




## 5. 模型

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

## 6. 描述性报告与监管背景
- **定位**：现有 ESL 证据均来自单一零售商（见 §1.1）。本数据提供跨 15 国、banner 层面的采用记录。
- **可呈现内容**：各国首次采用年份分布、扩散曲线、业态比较、供应商份额、采用范围。
- **监管对比**：
  - 美国：联邦层面与 14 个州提出禁止或限制 ESL 的法案（Stamatopoulos et al. 2026，表 1）。
  - 欧盟：GDPR 约束涉及个人数据的个性化定价（Zuiderveen Borgesius & Poort 2017）；Article 6a 规范降价的标示方式；目前没有针对 ESL 本身的限制。数字市场法与数字服务法对算法定价仅有零星涉及（Spann et al. 2024）。

---

## 7. 待办
- [ ] 采用范围编码：确定 4 条分歧与 7 条存疑记录的处理规则（结果尚未写入 CSV）。
- [ ] 确定 `follows parent` 的处理方式。
- [ ] 手工编码 B5 定价策略、B10 所有权结构、B11 会员计划。
- [ ] 核实 D2、D4、D5 的各国日期。
- [ ] 确认 B7 是否随时间变化，以及 Flywheel 各字段中哪些为实测值。
- [ ] 将 Callaway & Sant'Anna 2021 加入 Zotero；决定 Levin et al. 1987、1992，Beck et al. 2011，Das et al. 2009 是否纳入（§1 暂未收录，§4 变量依据中仍有引用）。

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
