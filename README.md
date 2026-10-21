# URBAN5127 — Quantitative Data Analysis：课程与 Lab 学习资料

本文件夹用于整理 URBAN5127 定量数据分析课程的课堂讲义和实验材料，包含 **Lecture 3–11** 的英文原文、中文笔记与 R 语言逐行代码教程，以及 **Tutorial 1–9** 的网页、Markdown、PDF 和配套 R Markdown 练习。

资料覆盖描述统计、可视化、假设检验、回归建模与模型诊断。Lecture 中的工资分析主要使用英国劳动力调查（LFS）的 `lfs` 对象，Lab 练习主要使用爱丁堡 Airbnb 房源数据。建议先阅读相关 Lecture 理解概念，再按 Tutorial 1 → 9 完成实验。

## 1. 目录结构

```text
Lab/
├── README.md                         本说明文件与资料导航
├── Lec/                              课堂讲义、中文笔记和逐行代码教程
│   ├── Lec03/                        描述统计
│   ├── Lec04/                        ggplot2 与数值分布可视化；附参考 PDF
│   ├── Lec05/                        分组与多变量可视化
│   ├── Lec06/                        统计推断、t 检验与简单回归
│   ├── Lec07/                        ANOVA、相关与简单线性回归
│   ├── Lec08/                        多元回归与影响点；含独立补充课件
│   ├── Lec09/                        对数变换、函数形式与回归诊断
│   ├── Lec10/                        共线性、模型迭代与稳健标准误
│   └── Lec11/                        观测独立性、聚类稳健标准误等
├── Code/                             R 项目、数据、练习代码和课堂材料
│   ├── Tutorial_Project.Rproj        RStudio 项目文件，使用 UTF-8 编码
│   ├── listings_edinburgh.csv         各节实验使用的 Airbnb 数据
│   ├── Lab_1.Rmd … Lab_9.Rmd          9 份主要练习代码
│   ├── 注释_Lab_1.Rmd … 注释_Lab_9.Rmd
│   │                                 9 份逐代码块中英文注释版
│   ├── Plamena_Lab_1.rmd              教师示例：Lab 1
│   ├── Plamena_Lab_2.Rmd              教师示例：Lab 2
│   ├── Plamena_Lab_3.Rmd              教师示例：Lab 3
│   ├── QDA_Lab_1_2026-27.pptx         Lab 1 课堂幻灯片
│   ├── QDA_Lab_2_2026-27.pptx         Lab 2 课堂幻灯片
│   ├── QDA_Lab_3_2026-27.pptx         Lab 3 课堂幻灯片
│   ├── .RData / .RDataTmp             本地 R 工作空间及临时状态文件
│   ├── .Rhistory                     本地 R 命令历史
│   └── .Rproj.user/                  本地 RStudio 项目状态（隐藏文件夹）
├── Tutorial/                         同一组实验教程的三种阅读格式
│   ├── HTML/
│   │   └── Tutorial_1/ … Tutorial_9/
│   │       ├── Chapter … .html        保存的 QDA Lab Workbook 教程网页
│   │       └── Chapter … _files/      网页配套图片、样式和脚本资源
│   ├── Markdown/
│   │   ├── Tutorial_1.md … Tutorial_9.md
│   │   │                             从网页正文转换的 Markdown 阅读版
│   │   └── assets/                   Markdown 引用的本地插图
│   └── PDF/
│       └── Tutorial_1.pdf … Tutorial_9.pdf
│                                     从网页正文生成的独立 PDF 阅读版
└── .git/                             Git 版本控制元数据（隐藏文件夹）
```

当前资料数量：

- **Lecture**：`Lec03`–`Lec11` 共 9 个讲次，包含 61 个主要阅读文件：20 份 HTML、10 份 Markdown、31 份 PDF。额外材料位于 Lec04 和 Lec08。
- **Tutorial**：Tutorial 1–9 各有 HTML、Markdown、PDF，合计 27 份主要阅读文件，另附网页和 Markdown 所需的资源文件。
- **Code**：21 份 R Markdown 文件（9 份普通练习、9 份注释版、3 份教师示例），另有 3 份课堂 PPT、1 份 CSV 数据和 1 份 RStudio 项目文件，以及本地会话状态文件。

## 2. 不同材料的用途与关系

| 材料 | 主要内容 | 适合怎样使用 |
| --- | --- | --- |
| `Lec/LecNN/` 中编号 `1`、`2` 的文件 | 第 NN 讲的英文原始课堂讲义，分别为 HTML 和 PDF。 | 阅读课程概念、原始代码、输出与老师的解释。 |
| `Lec/LecNN/` 中编号 `3`、`4` 的文件 | 对应的中文课堂笔记，分别为 HTML 和 PDF。 | 对照英文原文理解统计概念和术语。 |
| `Lec/LecNN/` 中编号 `5`、`6` 的文件 | 面向初学者的 R 代码逐行教程，分别为 Markdown 和 PDF。 | 逐段理解课堂代码；原代码、输出和补充讲解在文档中分别标明。 |
| `Tutorial/HTML/` | 原教程的详细讲解、示例代码、运行输出、练习和插图。 | 理解实验背景、概念和每一步操作的目的。 |
| `Tutorial/Markdown/` | 从 HTML 正文转换而来，保留标题、代码、输出、表格和插图。 | 在 Markdown 阅读器或编辑器中查阅、搜索和做笔记。 |
| `Tutorial/PDF/` | 从 HTML 正文排版生成，包含页眉、页码、表格和插图。 | 离线阅读、批注或打印。 |
| `Code/Lab_n.Rmd` | 对应第 n 次实验的主要练习代码。 | 在 RStudio 中逐块运行并观察输出。 |
| `Code/注释_Lab_n.Rmd` | 以对应练习为基础，添加详细的中文和英文解释。 | 学习函数、参数、代码执行顺序、结果解读和统计注意事项。 |
| `Code/Plamena_Lab_n.Rmd` | Plamena Panayotova 的教师示例，当前覆盖 Lab 1–3。 | 对照课堂讲解，学习补充写法和扩展操作。 |
| `Code/QDA_Lab_n_2026-27.pptx` | Lab 1–3 的课堂幻灯片。 | 复习课堂介绍和操作演示。 |

这里的 `n` 表示实验编号。`Lab_6` 对应 `Tutorial_6`，其他编号以此类推。**Lecture 讲次和 Tutorial/Lab 编号是两套序列，应按主题对照，不能按相同数字直接配对。** 原网页中还有 Workbook 的章节编号：由于第 1 章是 Introduction，所以 Tutorial 1 是 Chapter 2，Tutorial 9 是 Chapter 10。

`Tutorial/` 中的 HTML、Markdown 和 PDF 是同一实验教程的不同阅读格式；`Lec/` 中的英文讲义、中文笔记和逐行代码教程则有不同的讲解深度与用途。Rmd 是可以编辑和执行的分析文档，`Tutorial/PDF/` 中的文件来自教程网页。教师版与普通练习版也可能包含额外步骤、不同的数据对象和不同的组织方式。

## 3. Lecture 3–11 内容与快速导航

每个讲次的基础材料按 `1`–`6` 编号组织：`1/2` 为英文讲义 HTML/PDF，`3/4` 为中文笔记 HTML/PDF，`5/6` 为 R 代码逐行教程 Markdown/PDF。文件名前的数字表示**同一讲次内的材料类别**。

| 讲次 | 主题与主要内容 | 英文讲义 | 中文笔记 | R 代码逐行教程 |
| --- | --- | --- | --- | --- |
| Lecture 3 | **描述统计**：均值、中位数、方差、标准差、分位数、频数、百分比与分组汇总。 | [HTML](Lec/Lec03/1.lecture3_notes.html) · [PDF](Lec/Lec03/2.Lecture%203%20Notes.pdf) | [HTML](Lec/Lec03/3.中文版lecture3_notes.html) · [PDF](Lec/Lec03/4.中文版%20Lecture%203%20Notes.pdf) | [Markdown](Lec/Lec03/5.Lecture3_R语言零基础代码逐行教程.md) · [PDF](Lec/Lec03/6.Lecture3_R语言零基础代码逐行教程.pdf) |
| Lecture 4 | **ggplot2 与数值分布**：图层、直方图、箱宽、标签、主题、对数坐标、密度图与分组填色。 | [HTML](Lec/Lec04/1.lecture4_notes.html) · [PDF](Lec/Lec04/2.Lecture%204%20Notes.pdf) | [HTML](Lec/Lec04/3.第四讲课堂笔记｜定量数据分析.html) · [PDF](Lec/Lec04/4.第四讲课堂笔记｜定量数据分析.pdf) | [Markdown](Lec/Lec04/5.Lecture%204：R语言%20ggplot2%20数据可视化逐行教程.md) · [PDF](Lec/Lec04/6.Lecture%204：R语言%20ggplot2%20数据可视化逐行教程.pdf) |
| Lecture 5 | **分组与多变量可视化**：箱线图、小提琴图、抖动点、散点图、分面、热力图及各类条形图。 | [HTML](Lec/Lec05/1.lecture5_notes.html) · [PDF](Lec/Lec05/2.Lecture%205%20Notes.pdf) | [HTML](Lec/Lec05/3.第五讲笔记.html) · [PDF](Lec/Lec05/4.第五讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec05/5.Lecture%205%20Notes｜R语言数据可视化零基础逐行教程.md) · [PDF](Lec/Lec05/6.Lecture%205%20Notes｜R语言数据可视化零基础逐行教程.pdf) |
| Lecture 6 | **统计推断与均值比较**：抽样误差、正态概率、置信区间、Welch t 检验与虚拟变量回归。 | [HTML](Lec/Lec06/1.lecture6_notes.html) · [PDF](Lec/Lec06/2.Lecture%206%20Notes.pdf) | [HTML](Lec/Lec06/3.第六讲笔记.html) · [PDF](Lec/Lec06/4.第6讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec06/5.Lecture6_R语言零基础逐行代码详细教程.md) · [PDF](Lec/Lec06/6.Lecture6_R语言零基础逐行代码详细教程.pdf) |
| Lecture 7 | **ANOVA、相关与简单线性回归**：分类解释变量、组均值、F 检验、Pearson 相关与回归解释。 | [HTML](Lec/Lec07/1.lecture7_notes.html) · [PDF](Lec/Lec07/2.Lecture%207%20Notes.pdf) | [HTML](Lec/Lec07/3.第七讲笔记.html) · [PDF](Lec/Lec07/4.第7讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec07/5.Lecture7_R语言零基础逐行代码详细教程.md) · [PDF](Lec/Lec07/6.Lecture7_R语言零基础逐行代码详细教程.pdf) |
| Lecture 8 | **多元回归与影响点**：建模与估计假设、变量选择、R²、异常值、杠杆值和 Cook 距离。 | [HTML](Lec/Lec08/1.lecture8_notes.html) · [PDF](Lec/Lec08/2.Lecture%208%20Notes.pdf) | [HTML](Lec/Lec08/3.第八讲笔记.html) · [PDF](Lec/Lec08/4.第8讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec08/5.Lecture8_R语言零基础逐行代码详细教程.md) · [PDF](Lec/Lec08/6.Lecture8_R语言零基础逐行代码详细教程.pdf) |
| Lecture 9 | **对数变换与回归诊断**：线性、半对数、双对数模型，函数形式、RESET、BP 检验与残差 QQ 图。 | [HTML](Lec/Lec09/1.lecture9_notes.html) · [PDF](Lec/Lec09/2.Lecture%209%20Notes.pdf) | [HTML](Lec/Lec09/3.第九讲笔记.html) · [PDF](Lec/Lec09/4.第9讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec09/5.Lecture9_R语言零基础逐行代码详细教程.md) · [PDF](Lec/Lec09/6.Lecture9_R语言零基础逐行代码详细教程.pdf) |
| Lecture 10 | **共线性与模型迭代**：VIF/GVIF、分类重编码、参照组、变量调整及异方差稳健标准误。 | [HTML](Lec/Lec10/1.lecture10_notes.html) · [PDF](Lec/Lec10/2.Lecture%2010%20Notes.pdf) | [HTML](Lec/Lec10/3.第十讲笔记.html) · [PDF](Lec/Lec10/4.第10讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec10/5.Lecture10_R语言零基础逐行代码详细教程.md) · [PDF](Lec/Lec10/6.Lecture10_R语言零基础逐行代码详细教程.pdf) |
| Lecture 11 | **观测独立性与聚类推断**：家庭内相关、聚类稳健标准误、一般到具体建模及其他模型概览。 | [HTML](Lec/Lec11/1.lecture11_notes.html) · [PDF](Lec/Lec11/2.Lecture%2011%20Notes.pdf) | [HTML](Lec/Lec11/3.第十一讲笔记.html) · [PDF](Lec/Lec11/4.第11讲笔记｜定量数据分析（中文版）.pdf) | [Markdown](Lec/Lec11/5.Lecture11_R语言零基础逐行代码详细教程.md) · [PDF](Lec/Lec11/6.Lecture11_R语言零基础逐行代码详细教程.pdf) |

### 3.1 Lecture 4 补充参考

[Data visualization with ggplot2](Lec/Lec04/7.Data%20visualization%20with%20ggplot2.pdf) 是 Lec04 中编号 `7` 的可视化补充参考 PDF，单独列于基础材料之外。

### 3.2 Lecture 8 多元线性回归补充课件

Lec08 的编号 `7`–`12` 是独立的 **Multiple linear regression** 补充材料。它以 LFS 小时工资与性别的关联为线索，逐步加入控制变量，展示 11 个回归模型；应与编号 `1`–`6` 的主讲义配合阅读。

| 资料 | 链接 |
| --- | --- |
| 英文补充讲义 | [HTML](Lec/Lec08/7.lecture8_regressions.html) · [PDF](Lec/Lec08/8.lecture8_regressions.pdf) |
| 中文补充笔记 | [HTML](Lec/Lec08/9.第8讲笔记｜多元线性回归｜课堂讲义中文版.html) · [PDF](Lec/Lec08/10.第讲笔记｜多元线性回归｜课堂讲义中文版.pdf) |
| 补充课件的 R 代码逐行教程 | [Markdown](Lec/Lec08/11.Lecture%208%20补充课件：多元线性回归——R语言完全零基础逐行代码教程.md) · [PDF](Lec/Lec08/12.Lecture%208%20补充课件：多元线性回归——R语言完全零基础逐行代码教程.pdf) |

## 4. Tutorial 1–9 内容与快速导航

| 编号 | 主题与主要内容 | HTML | Markdown | PDF | R Markdown 代码 |
| --- | --- | --- | --- | --- | --- |
| 1 | **读取与检查数据**：R/RStudio 项目、`read_csv()`、`glimpse()`、变量类型与因子转换。 | [网页](Tutorial/HTML/Tutorial_1/Chapter%202%20Tutorial%201_%20Reading%20in%20our%20data%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_1.md) | [打印版](Tutorial/PDF/Tutorial_1.pdf) | [练习](Code/Lab_1.Rmd) · [注释](Code/注释_Lab_1.Rmd) |
| 2 | **描述统计与清理**：缺失值、排序、筛选、频数与百分比、分组汇总。 | [网页](Tutorial/HTML/Tutorial_2/Chapter%203%20Tutorial%202_%20Descriptive%20Statistics%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_2.md) | [打印版](Tutorial/PDF/Tutorial_2.pdf) | [练习](Code/Lab_2.Rmd) · [注释](Code/注释_Lab_2.Rmd) |
| 3 | **数值变量可视化**：ggplot 图层、直方图、密度图、箱线图与分组分布。 | [网页](Tutorial/HTML/Tutorial_3/Chapter%204%20Tutorial%203_%20Data%20Visualisation%20-%20Numeric%20variables%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_3.md) | [打印版](Tutorial/PDF/Tutorial_3.pdf) | [练习](Code/Lab_3.Rmd) · [注释](Code/注释_Lab_3.Rmd) |
| 4 | **数值与分类变量可视化**：散点图、抖动点、平滑线、因子排序、条形图及图形组合。 | [网页](Tutorial/HTML/Tutorial_4/Chapter%205%20Tutorial%204_%20Data%20Visualisation%20-%20Numeric%20and%20Factor%20variables%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_4.md) | [打印版](Tutorial/PDF/Tutorial_4.pdf) | [练习](Code/Lab_4.Rmd) · [注释](Code/注释_Lab_4.Rmd) |
| 5 | **t 检验**：筛选两组房型、检查分布、比较组均值与标准差、运行 Welch t 检验。 | [网页](Tutorial/HTML/Tutorial_5/Chapter%206%20Tutorial%205_%20Inference%20-%20the%20t-test%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_5.md) | [打印版](Tutorial/PDF/Tutorial_5.pdf) | [练习](Code/Lab_5.Rmd) · [注释](Code/注释_Lab_5.Rmd) |
| 6 | **ANOVA 与相关分析**：比较多个房型的价格均值，检验价格与评分的 Pearson 相关。 | [网页](Tutorial/HTML/Tutorial_6/Chapter%207%20Tutorial%206_%20Inference%20-%20ANOVA%20and%20Correlation%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_6.md) | [打印版](Tutorial/PDF/Tutorial_6.pdf) | [练习](Code/Lab_6.Rmd) · [注释](Code/注释_Lab_6.Rmd) |
| 7 | **回归模型建立与比较**：逐步加入解释变量、参照类别、类别合并与回归结果表。 | [网页](Tutorial/HTML/Tutorial_7/Chapter%208%20Tutorial%207_%20Model%20Building%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_7.md) | [打印版](Tutorial/PDF/Tutorial_7.pdf) | [练习](Code/Lab_7.Rmd) · [注释](Code/注释_Lab_7.Rmd) |
| 8 | **模型诊断 I**：影响点、残差图、非线性、正态性、异方差与多重共线性。 | [网页](Tutorial/HTML/Tutorial_8/Chapter%209%20Tutorial%208_%20Diagnostics%20I%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_8.md) | [打印版](Tutorial/PDF/Tutorial_8.pdf) | [练习](Code/Lab_8.Rmd) · [注释](Code/注释_Lab_8.Rmd) |
| 9 | **模型诊断 II**：对价格取对数、重新诊断模型、调整模型与异方差稳健标准误。 | [网页](Tutorial/HTML/Tutorial_9/Chapter%2010%20Tutorial%209_%20Diagnostics%20II%20_%20QDA%20Lab%20Workbook.html) | [阅读版](Tutorial/Markdown/Tutorial_9.md) | [打印版](Tutorial/PDF/Tutorial_9.pdf) | [练习](Code/Lab_9.Rmd) · [注释](Code/注释_Lab_9.Rmd) |

教师示例：[Lab 1](Code/Plamena_Lab_1.rmd) · [Lab 2](Code/Plamena_Lab_2.Rmd) · [Lab 3](Code/Plamena_Lab_3.Rmd)。

课堂幻灯片：[Lab 1](Code/QDA_Lab_1_2026-27.pptx) · [Lab 2](Code/QDA_Lab_2_2026-27.pptx) · [Lab 3](Code/QDA_Lab_3_2026-27.pptx)。

## 5. 数据文件与示例对象

### 5.1 Lab 使用的 Airbnb 数据

数据位于 [Code/listings_edinburgh.csv](Code/listings_edinburgh.csv)，当前文件包含 **14,014 条房源记录、10 个变量**。读取后一般保存为 `listings`；筛选和删除缺失记录后的样本量会发生变化。

| 变量 | 含义 |
| --- | --- |
| `name` | 房源名称。 |
| `neighbourhood_cleansed` | 房源所在社区或区域。 |
| `property_type` | 物业类型，例如 Apartment、House、Hotel。 |
| `room_type` | 房间类型，例如 Entire home/apt、Private room、Shared room。 |
| `accommodates` | 可容纳人数。 |
| `bathrooms` | 浴室数量或数据中记录的相应数值。 |
| `bedrooms` | 卧室数量。 |
| `beds` | 床位数量。 |
| `price` | 价格；具体币种和计价周期应以数据来源说明为准。 |
| `review_scores_rating` | 房源评分；教程图示按 100 分制解释。 |

教程中会把 `room_type`、`property_type` 转换为因子，并在许多练习中保留 `25 ≤ price ≤ 1000`、`bathrooms ≤ 5`，再删除价格、卧室数和浴室数缺失的记录。这些是课程示范所采用的分析规则；原 CSV 不会因为在 R 中给对象重新赋值而自动改变。

### 5.2 Lecture 使用的 LFS 等示例

Lecture 的工资示例主要使用英国劳动力调查数据，常见对象为 `lfs`，变量包括 `HOURPAY`（小时工资）、`SEX`（性别）、`AGE`（年龄）和 `HIQUL22D`（学历类别）。Lecture 11 还使用家庭标识 `HSERIALP` 进行聚类推断；Lecture 9 的部分变换示例使用 R 内置的 `mtcars` 数据，Lecture 8 也有构造数据的演示。

当前单独存放的原始表格数据文件为 `Code/listings_edinburgh.csv`，它是 Airbnb 数据。Lecture 所需的 `lfs` 应按照课程提供的 LFS 数据与前序清理步骤另行准备，不能把 Airbnb CSV 直接代入工资分析。部分 Lecture 代码还依赖之前创建的模型对象，逐行教程中有相应的运行前提说明。

## 6. 建议的使用方法

1. **先理解课堂概念**：在 `Lec/` 中阅读相关讲次的英文讲义或中文笔记；刚接触 R 时，可同时查阅该讲编号 `5/6` 的逐行代码教程。
2. **打开 Lab 项目**：[Code/Tutorial_Project.Rproj](Code/Tutorial_Project.Rproj)。项目根目录是 `Code/`，实验代码中的 `read_csv("listings_edinburgh.csv")` 因此可以找到同目录的数据文件。
3. **阅读对应实验教程**：在 `Tutorial/` 中选择 HTML、Markdown 或 PDF，了解实验的目的和操作步骤。
4. **逐块运行注释版**：打开 `注释_Lab_n.Rmd`，从上到下阅读说明、运行代码，并检查每一步的实际输出。
5. **用普通版复习或练习**：打开 `Lab_n.Rmd`，尝试解释每一行；Lab 1–3 还可以对照教师示例和课堂幻灯片。
6. **需要报告时再 Knit**：这些 Rmd 主要配置为输出 HTML。Knit 会重新运行文档代码，结果与直接阅读已经保存的教程 PDF 不同。Lecture 的 Markdown 逐行教程是阅读材料，其中的代码应按其数据和对象前提分段运行。

运行分析需要 R 和 RStudio；渲染 R Markdown HTML 报告还需要 `rmarkdown`、`knitr`。代码按章节使用的主要包如下：

| 用途 | 包 |
| --- | --- |
| 数据读取、整理与绘图 | `tidyverse`，其中包括 `readr`、`dplyr`、`tidyr`、`ggplot2`、`forcats` 等。 |
| 刻度格式与组合绘图 | `scales`、`gridExtra`。 |
| R Markdown 与表格 | `rmarkdown`、`knitr`、`texreg`。 |
| 回归诊断与稳健推断 | `car`、`lmtest`、`sandwich`。 |
| Lecture 11 的聚类回归 | `miceadds`，提供 `lm.cluster()`。 |
| 教师示例中的其他数据格式 | `haven`。 |

首次使用时安装相应包，在每次新的 R 会话中按文档需要加载。`lm()`、`aov()`、`t.test()` 和 `cor.test()` 来自 R 自带的统计工具。

## 7. 运行前需要了解的现有依赖

- **Lecture 和 Lab 需要分别准备数据。** Lecture 中的 `lfs`、已有模型及相关包不一定在文档开头完整创建；先阅读对应逐行教程的前提说明。`Code/Tutorial_Project.Rproj` 主要服务于 Airbnb 实验，其路径与数据设置不会自动完成 Lecture 的 LFS 准备。
- **Lab 6 和 Lab 7 依赖前面的数据准备。** 普通版及注释版没有完整加载 `tidyverse`、读取 CSV 和重建 `listings` 的步骤。交互运行时需先在同一会话准备数据；如果要单独 Knit，需要把必要的包加载和数据准备步骤放入文档，不能依赖之前交互会话中的对象。
- **部分 setup 会安装包。** Lab 4 含可执行的 `install.packages("gridExtra")`，Lab 7 含 `install.packages("texreg")`，因此运行这些设置块时会再次尝试安装。注释版已经解释了这一行为。
- **Lab 7 有需要留意的代码顺序。** 原代码在合并物业类别之前使用小写 `ref = "apartment"`；原始水平为 `"Apartment"` 时，此处会报错。另外，后续代码会重新定义 `m3`，解释模型时应核对最后实际使用的公式。对应注释版提供了详细说明。
- **教师版 Lab 3 读取上一节生成的数据。** [Plamena_Lab_3.Rmd](Code/Plamena_Lab_3.Rmd) 使用 `readRDS("listings_clean.rds")`；当前文件夹未包含这个 RDS。需要先运行教师版 Lab 2 中相关清理和 `saveRDS()` 步骤，再运行教师版 Lab 3。
- **会话文件不能替代分析脚本。** `.RData`、`.RDataTmp`、`.Rhistory` 和 `.Rproj.user/` 记录本地工作状态或历史，复现分析应以 CSV 和 Rmd 中明确的数据准备步骤为依据。

## 8. 阅读与文件维护说明

- `Tutorial/HTML/` 中的网页应与同目录下的 `*_files/` 资源文件夹一起保留，否则可能无法显示样式或插图。
- `Tutorial/Markdown/` 的插图由其 `assets/` 提供；移动或分享这些 Markdown 时，应一起保留这个文件夹。Lecture 的逐行教程保存在各自的 `LecNN/` 目录中。
- PDF 可直接单独阅读或分享，不依赖旁边的 HTML 资源目录。
- Tutorial 8 的原始保存文件缺少 `Diagnostics 1_ Influential Outliers-1.png`，Markdown 和 PDF 已在原位置注明缺图；其余现有插图已保留。
- 当前资料已统一放在 `Tutorial/HTML`、`Tutorial/Markdown`、`Tutorial/PDF` 下。部分早期材料正文中的相对链接仍指向整理前的位置；请优先使用本 README 中按现有结构编写的导航链接。
- 文件名与 Rmd 的 YAML `title` 是两个字段。部分文件改名后，报告标题仍保留原有名称，这是文档标题设置，并不表示文件缺失。
- `.git/` 保存 Git 版本控制元数据，属于仓库管理文件；查阅课程材料时使用上面的资料目录和导航即可。

Tutorial 原始资料来自 **QDA Lab Workbook**，教师示例文件署名 **Plamena Panayotova**。`Lec/` 中另保留课堂英文讲义、中文笔记及逐行代码讲解，Lecture 8 的多元回归补充原文署名 **Dr. David McArthur**。各种阅读版和注释版用于配合课程材料学习；实际统计结论应根据所运行代码、所用数据和输出进行解释。
