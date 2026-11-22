# Khalifa CS PhD WQE

## 项目简介

哈利法大学（Khalifa University）CS PhD 书面资格考试（WQE）离线复习笔记静态站点。仓库直接维护发布态单页 HTML（无上游 Markdown 或构建脚本），所有 KaTeX、highlight.js 与教材配图均打包在各科 `notes/` 下，打开 `index.html` 或单科 HTML 即可离线阅读。

> **核心痛点与优先目标**：现有笔记由 AI 初稿生成，存在碎句堆砌、机器翻译腔、长段密集、缺直觉铺垫等问题，读起来很累。后续所有修订与重写须在**保证考点准确、英文可直接用于作答**的前提下，优先优化**语言流畅度、理解门槛与视觉可读性**。

## 科目速查

各科目录结构统一为 `<Dir>/<Short>_WQE_notes.html` + `<Dir>/notes/{assets/{katex,hljs}, img/<BOOK>/fig_<ch>.<num>.png}`。

| 科目 | 笔记文件 | 对标课程 | 主要教材（配图目录） | 章节 | `localStorage` 键 |
| --- | --- | --- | --- | --- | --- |
| Software Engineering | `Software-Engineering/SE_WQE_notes.html` | COSC 336 | Sommerville 10e (`SOM/`), Valente | `c01`–`c12` | `wqe-se-zh` |
| Artificial Intelligence | `Artificial-Intelligence/AI_WQE_notes.html` | COSC 330, 434 | AIMA 4e (`AIMA/`), Lindholm (`LIND/`) | `c01`–`c12` | `wqe-ai-zh` |
| Operating Systems | `Operating-Systems/OS_WQE_notes.html` | COSC 354 | Silberschatz OSC 10e (`OSC/`) | `c01`–`c07` | `wqe-os-zh` |
| Algorithms | `Algorithms/Algorithms_WQE_notes.html` | COSC 312 | CLRS 4e (`CLRS/`) | `c01`–`c21` | `wqe-alg-zh` |
| Security | `Computer-and-Network-Security/Security_WQE_notes.html` | COSC 340, CCEN 446 | Stallings CSPP 5e (`CSPP/`), CNS 8e (`CNS/`) | `c01`–`c24` | `wqe-sec-zh` |

考试规则：5 科均闭卷且允许基础科学计算器；仅 **AI** 额外允许携带 1 张双面 A4 纯公式纸。

## 语言表达与可读性准则（重点）

1. **消除碎句连珠炮，写连贯自然的英文**：避免把一个逻辑拆成七八个无衔接的短平句（staccato style）；用恰当的因果、转折、对比连接句子，同时避免过度嵌套的学术长难句，使英文既顺滑易读，又适合考场直接作答。
2. **先立直觉，再讲定义与步骤**：引入新概念、算法或机制时，先用 1–2 句说清「解决什么问题 / 为什么需要它 / 核心思路是什么」，再展开形式化定义、流程或分类，不干巴巴堆砌条款。
3. **彻底去掉机器翻译腔**：
   - `<span class="zh" lang="zh-CN">` 按自然中文重整语序意译，**严禁逐词直译英文句式**（如生硬的「用文字表述：」「（循环地）」「与……相与」及英文倒装）。
   - 同科内同一术语保持统一译名（例如 `critic`、`performance element` 等不前后混译）。
   - `<aside class="callout cn">` 用来补充直白类比、底层直觉或记忆抓手，不要与正文译文重复复读。
4. **打破「文字墙」，强化扫读层次**：
   - 正文单段尽量控制在 2–4 句，每段只讲一个核心点。
   - 多步演算（trace / 推导）、多条特征对比及较长的参考答案（Practice / Exam-style），须拆分为编号步骤、要点列表、短段或表格，并用 `<strong>` 突出关键词，禁止把整道大题答案或整段演算挤成一坨。
5. **精简套话，提高信息密度**：删去机械重复的过渡语和冗余解释，每一句都服务于「理解概念」或「考场得分」。

## HTML 与格式底线

- **双语结构**：正文、例题与答案以英文为主；中文译文统一放在对应块级元素（`<p>`、`<li>`、`<td>`、`<th>`、`<h1-h4>`、`<figcaption>`、`<summary>`）末尾的 `<span class="zh" lang="zh-CN">...</span>` 内，保证「隐藏中文」生效。英文首次出现核心术语可括注中文，如 `<strong>software process</strong>（软件过程）`。
- **公式（KaTeX）**：行内 `<span class="math">\(...\)</span>`，块级 `<p><span class="math display">\[...\]</span></p>`。**严禁 `$...$` / `$$...$$`**；公式内 `<`、`>`、`&` 须转义为 `&lt;`、`&gt;`、`&amp;`。
- **代码、表格与配图**：代码用 `<pre><code class="language-xxx">`（伪代码用 `language-text`）；表格外包 `<div class="tw">`；配图用 `.figs.n1`（单图）/ `.figs.n2`（双图）+ `<a class="zoom" href="...">` + `<figcaption>`。

## Agent 工作准则

1. **按锚点局部编辑**：各科 HTML 约 14,000–27,000 行，先按 `id`（如 `id="c04-s2"`）或关键词定位行号，仅读写局部上下文。
2. **严守离线约束**：不得引入任何 `http://` / `https://` 外部资源；新增配图落盘到对应科目 `notes/img/<BOOK>/`。
3. **多处联动一致**：改动章节/优先级、公式卡或易错点时，同步更新 TOC、导读 `#c00`、文末 `#app-formulas`/`#app-exam` 及更新日期；改共用样式/脚本时同步 5 科并保留各自 `localStorage` 键。
4. **改后校验与提交**：用轻量脚本检查 `id` 唯一与锚点有效、本地资源存在无外链、KaTeX 与 `.zh` 标签闭合；保持 diff 聚焦，不对未涉及章节做无关格式化。
