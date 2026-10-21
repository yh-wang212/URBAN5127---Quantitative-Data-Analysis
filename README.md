# URBAN5127 — Quantitative Data Analysis：Lab 学习资料

本文件夹用于整理 URBAN5127 定量数据分析课程的实验材料，包含 Tutorial 1–9 的网页教程、Markdown 阅读版、PDF 打印版，以及相应的 R Markdown 练习代码、详细中英文注释、教师示例和课堂幻灯片。

课程以爱丁堡 Airbnb 房源数据为例，依次学习数据读取与清理、描述统计、可视化、假设检验、回归建模和模型诊断。建议按照 Tutorial 1 → 9 的顺序学习。

## 1. 目录结构

```text
Lab/
├── README.md                         本说明文件与资料导航
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
└── Tutorial/                         同一组教程的三种阅读格式
    ├── HTML/
    │   ├── Tutorial_1/ … Tutorial_9/
    │   │   ├── Chapter … .html        保存的 QDA Lab Workbook 教程网页
    │   │   └── Chapter … _files/      网页配套图片、样式和脚本资源
    ├── Markdown/
    │   ├── Tutorial_1.md … Tutorial_9.md
    │   │                             从网页正文转换的 Markdown 阅读版
    │   └── assets/                   Markdown 引用的本地插图
    └── PDF/
        └── Tutorial_1.pdf … Tutorial_9.pdf
                                      从网页正文生成的独立 PDF 阅读版
```

当前共有 21 份 R Markdown 文件：9 份普通练习、9 份注释版、3 份教师示例；教程则各有 9 份 HTML、Markdown 和 PDF。

## 2. 不同材料的用途与关系

| 材料 | 主要内容 | 适合怎样使用 |
| --- | --- | --- |
| `Tutorial/HTML/` | 原教程的详细讲解、示例代码、运行输出、练习和插图。 | 理解实验背景、概念和每一步操作的目的。 |
| `Tutorial/Markdown/` | 从 HTML 正文转换而来，保留标题、代码、输出、表格和插图。 | 在 Markdown 阅读器或编辑器中查阅、搜索和做笔记。 |
| `Tutorial/PDF/` | 从 HTML 正文排版生成，包含页眉、页码、表格和插图。 | 离线阅读、批注或打印。 |
| `Code/Lab_n.Rmd` | 对应第 n 次实验的主要练习代码。 | 在 RStudio 中逐块运行并观察输出。 |
| `Code/注释_Lab_n.Rmd` | 以对应练习为基础，添加详细的中文和英文解释。 | 学习函数、参数、代码执行顺序、结果解读和统计注意事项。 |
| `Code/Plamena_Lab_n.Rmd` | Plamena Panayotova 的教师示例，当前覆盖 Lab 1–3。 | 对照课堂讲解，学习补充写法和扩展操作。 |
| `Code/QDA_Lab_n_2026-27.pptx` | Lab 1–3 的课堂幻灯片。 | 复习课堂介绍和操作演示。 |

这里的 `n` 表示实验编号。`Lab_6` 对应 `Tutorial_6`，其他编号以此类推。原网页中还有 Workbook 的章节编号：由于第 1 章是 Introduction，所以 **Tutorial 1 是 Chapter 2，Tutorial 9 是 Chapter 10**，并不是文件配错了。

HTML、Markdown 和 PDF 是同一教程的不同阅读格式；Rmd 是可以编辑和执行的分析文档。现有 PDF 来自教程网页，并不是运行 `Lab_n.Rmd` 后生成的报告。教师版与普通练习版也不是完全相同的代码副本，可能包含额外步骤、不同的数据对象和不同的组织方式。

## 3. Tutorial 1–9 内容与快速导航

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

## 4. 数据文件

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

## 5. 建议的使用方法

1. **先打开项目**：[Code/Tutorial_Project.Rproj](Code/Tutorial_Project.Rproj)。项目根目录是 `Code/`，代码中的 `read_csv("listings_edinburgh.csv")` 因此可以找到同目录的数据文件。
2. **阅读对应教程**：选择 HTML、Markdown 或 PDF，了解本次实验的目的和统计概念。
3. **逐块运行注释版**：打开 `注释_Lab_n.Rmd`，从上到下阅读说明、运行代码，并检查每一步的实际输出。
4. **用普通版复习或练习**：打开 `Lab_n.Rmd`，尝试解释每一行；Lab 1–3 还可以对照教师示例和课堂幻灯片。
5. **需要报告时再 Knit**：这些 Rmd 主要配置为输出 HTML。Knit 会重新运行文档代码，结果与直接阅读已经保存的教程 PDF 不同。

运行分析需要 R 和 RStudio；渲染 R Markdown HTML 报告还需要 `rmarkdown`、`knitr`。代码按章节使用的主要包如下：

| 用途 | 包 |
| --- | --- |
| 数据读取、整理与绘图 | `tidyverse`，其中包括 `readr`、`dplyr`、`tidyr`、`ggplot2`、`forcats` 等。 |
| 刻度格式与组合绘图 | `scales`、`gridExtra`。 |
| R Markdown 与表格 | `rmarkdown`、`knitr`、`texreg`。 |
| 回归诊断与稳健推断 | `car`、`lmtest`、`sandwich`。 |
| 教师示例中的其他数据格式 | `haven`。 |

首次使用时安装相应包，在每次新的 R 会话中按文档需要加载。`lm()`、`aov()`、`t.test()` 和 `cor.test()` 来自 R 自带的统计工具。

## 6. 运行前需要了解的现有依赖

- **Lab 6 和 Lab 7 依赖前面的数据准备。** 普通版及注释版没有完整加载 `tidyverse`、读取 CSV 和重建 `listings` 的步骤。交互运行时需先在同一会话准备数据；如果要单独 Knit，需要把必要的包加载和数据准备步骤放入文档，不能依赖之前交互会话中的对象。
- **部分 setup 会安装包。** Lab 4 含可执行的 `install.packages("gridExtra")`，Lab 7 含 `install.packages("texreg")`，因此运行这些设置块时会再次尝试安装。注释版已经解释了这一行为。
- **Lab 7 有需要留意的代码顺序。** 原代码在合并物业类别之前使用小写 `ref = "apartment"`；原始水平为 `"Apartment"` 时，此处会报错。另外，后续代码会重新定义 `m3`，解释模型时应核对最后实际使用的公式。对应注释版提供了详细说明。
- **教师版 Lab 3 读取上一节生成的数据。** [Plamena_Lab_3.Rmd](Code/Plamena_Lab_3.Rmd) 使用 `readRDS("listings_clean.rds")`；当前文件夹未包含这个 RDS。需要先运行教师版 Lab 2 中相关清理和 `saveRDS()` 步骤，再运行教师版 Lab 3。
- **会话文件不能替代分析脚本。** `.RData`、`.RDataTmp`、`.Rhistory` 和 `.Rproj.user/` 记录本地工作状态或历史，复现分析应以 CSV 和 Rmd 中明确的数据准备步骤为依据。

## 7. 阅读与文件维护说明

- HTML 文件应与同目录下的 `*_files/` 资源文件夹一起保留，否则可能无法显示样式或插图。
- Markdown 的插图由同级 `assets/` 提供；移动或分享 Markdown 时，应一起保留这个文件夹。
- PDF 可直接单独阅读或分享，不依赖旁边的 HTML 资源目录。
- Tutorial 8 的原始保存文件缺少 `Diagnostics 1_ Influential Outliers-1.png`，Markdown 和 PDF 已在原位置注明缺图；其余现有插图已保留。
- 当前资料已统一放在 `Tutorial/HTML`、`Tutorial/Markdown`、`Tutorial/PDF` 下。部分早期材料正文中的相对链接仍指向整理前的位置；请优先使用本 README 中按现有结构编写的导航链接。
- 文件名与 Rmd 的 YAML `title` 是两个字段。部分文件改名后，报告标题仍保留原有名称，这是文档标题设置，并不表示文件缺失。

教程资料来源为 **QDA Lab Workbook**，教师示例文件署名 **Plamena Panayotova**。Markdown、PDF 和中英文注释版用于配合这些课程材料阅读与练习；实际统计结论应根据所运行代码、所用数据和输出进行解释。
