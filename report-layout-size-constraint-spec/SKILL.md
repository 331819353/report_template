---
name: report-layout-size-constraint-spec
aliases: ["时间序列KPI卡尺寸", "趋势卡尺寸", "变化卡尺寸", "同环比卡尺寸", "周期卡尺寸", "波动卡尺寸", "预测卡尺寸", "对比分析卡尺寸", "分组对比卡尺寸", "竞品对比卡尺寸", "标杆卡尺寸", "差异卡尺寸", "排名卡尺寸", "榜单卡尺寸", "Top N卡尺寸", "帕累托卡尺寸", "占比卡尺寸", "构成卡尺寸", "结构卡尺寸", "份额卡尺寸", "指标拆解卡尺寸", "归因拆解卡尺寸", "贡献卡尺寸", "层级拆解卡尺寸", "分布卡尺寸", "区间卡尺寸", "密度卡尺寸", "分位数卡尺寸", "箱线卡尺寸"]
description: "用于报表页面区块尺寸、容器尺寸、高度预算、首屏层级、8*N网格、图表/表格容器高度、固定高度卡片、KPI总览卡/多指标总览卡最小尺寸、单指标KPI卡最小尺寸、状态卡/健康度卡/评分卡/仪表盘卡/指标判断卡最小尺寸、目标执行卡/目标达成卡/差距卡/进度卡/里程碑卡最小尺寸、时间序列KPI卡/趋势卡/变化卡/同环比卡/周期卡/波动卡/预测卡最小尺寸、对比分析KPI卡/对比卡/分组对比卡/竞品对比卡/标杆卡/差异卡最小尺寸、排名卡/榜单卡/Top N卡/排行榜/帕累托卡最小尺寸、占比卡/构成卡/结构卡/份额卡/市场份额卡最小尺寸、指标拆解卡/归因拆解卡/贡献卡/层级拆解卡/驱动因素拆解/路径贡献/瀑布拆解最小尺寸、分布卡/区间卡/密度卡/分位数卡/箱线卡最小尺寸、横向指标卡/横版KPI最小尺寸、横向折线KPI/坐标折线诊断卡最小尺寸、横向柱状KPI/坐标柱状诊断卡最小尺寸、横向散点KPI/关系诊断卡最小尺寸、横向地图KPI/空间诊断卡最小尺寸、双栏VS对比诊断卡最小尺寸、Composite Panel/Micro Dashboard Card多组件最小尺寸、状态反馈几何、裁切、溢出、重叠和响应式尺寸约束设计/评审。用户提到区块尺寸、容器尺寸、卡片高度、首屏放不下、图表太挤、表格太矮、KPI总览卡挤压、多指标总览卡挤压、单指标KPI卡挤压、目标执行卡挤压、目标达成卡挤压、差距卡挤压、进度卡挤压、里程碑卡挤压、时间序列KPI卡挤压、趋势卡挤压、对比分析卡挤压、分组对比卡挤压、竞品对比卡挤压、标杆卡挤压、差异卡挤压、排名卡挤压、榜单挤压、Top N卡挤压、帕累托卡挤压、占比卡挤压、构成卡挤压、结构卡挤压、份额卡挤压、指标拆解卡挤压、归因拆解卡挤压、贡献卡挤压、层级拆解卡挤压、分布卡挤压、区间卡挤压、密度卡挤压、分位数卡挤压、箱线卡挤压、分布热力图被压扁、KDE密度图被压扁、箱线图被压扁、桑基拆解被压扁、树状拆解被压扁、瀑布拆解被压扁、矩阵归因被压扁、指标判断卡挤压、状态卡挤压、健康度卡挤压、评分卡挤压、仪表盘卡挤压、横向卡片挤压、坐标折线KPI被压扁、坐标柱状KPI被压扁、坐标散点KPI被压扁、地图KPI被压扁、VS对比卡挤压、多组件组合挤压、1920x1080、1280x768、高度预算、scrollHeight/clientHeight、overflow、裁切、重叠、响应式布局时触发；不负责组件内部图表细节。"
---

# Report Layout Size Constraint Spec

## Positioning

Use this as the direct front door for page/block sizing and viewport fit. It promotes the layout sizing reference that was previously nested under `$report-visual-layout-design`.

Use `$report-visual-layout-design` for full page layout decisions; use this skill for block size budgets, fixed-height risk, parent/child container fit, and responsive overflow checks.

## Reference Map

| Need | Read |
| --- | --- |
| Preflight understanding before implementation/repair/acceptance | `$quality-gate-validation` `references/preflight-understanding-gate.md` |
| Size source map | `references/01-size-reference-map.md` |
| Parent layout references | `$report-visual-layout-design` references: `block-size-constraints.md`, `grid-containers.md`, `block-composition.md`, `layout-acceptance-gates.md` |
| Modern SaaS / BI Dashboard / UI Kit pileup and hierarchy constraints | `$report-design-system-governance` `references/12-modern-saas-bi-style-contract.md` when requested |
| KPI time-series card minimums for trend/change/YoY-MoM/cycle/volatility/forecast cards | `$report-visual-layout-design` `references/block-size-constraints-02-component-requirements.md` |
| Component minimums for KPI overview cards, single-indicator KPI cards, KPI judgment cards, KPI goal execution / target attainment / gap / progress / milestone cards, KPI comparison analysis / comparison / group comparison / competitor / benchmark / variance cards, ranking / leaderboard / Top N / Pareto cards, composition / share / structure / market-share cards, decomposition / attribution / contribution / hierarchy cards, distribution / interval / density / quantile / boxplot cards, horizontal KPI cards, axis-line diagnostic KPI cards, axis-bar diagnostic KPI cards, axis-scatter diagnostic KPI cards, spatial-map diagnostic KPI cards, paired comparison diagnostic KPI cards, Composite Panel, Micro Dashboard Card, state feedback, dense tables/charts | `$report-visual-layout-design` `references/block-size-constraints-02-component-requirements.md` |

## Anti-Laziness Gate

For non-trivial work, apply `$quality-gate-validation` `references/anti-laziness-execution-gate.md` before final output, handoff, or readiness. Do not mark the result ready while `LAZY-*` findings remain open, when available local evidence was not inspected, when owning skills were skipped, or when proof is limited to generic statements such as "checked", "optimized", "looks good", or "implemented".

## Workflow

1. Run the Preflight understanding gate for implementation, repair, or acceptance work; name affected blocks, child component families, viewport targets, hard constraints, missing evidence, and start decision.
2. Identify viewport targets, grid system, parent blocks, child components, fixed-height surfaces, and density.
3. Calculate usable width/height for the block before deciding chart/table/KPI composition.
4. Check row count, header/filter/toolbar/legend/footer/state masks, child-component minimums, gaps, padding, line-height, and scroll areas.
5. Decide whether to enlarge, split, move to drawer/fullscreen, paginate, scroll, or reduce component density.
6. Require DOM overflow checks when code or URL exists: fixed-height cards, summary/ranking blocks, KPI tiles, nav items, Composite Panels, table bodies, and compact controls must pass `scrollHeight <= clientHeight + 2` and `scrollWidth <= clientWidth + 2`, or declare an intentional visible scroll, expand/collapse, drawer/fullscreen, pagination, or split strategy.
7. Inspect `overflow: hidden` on parent/root containers. It is allowed for decorative masks or known non-content regions, but fails acceptance when it hides decision-critical text, ranking rows, controls, legends, values, or table content without a declared disclosure path.

## Required Output

- Preflight understanding result when the work is implementation/repair/acceptance, plus target viewport and block/container size budget.
- Fit decision for each dense block: fit, enlarge, split, scroll, drawer/fullscreen, or blocked.
- Overflow/cropping risks and required DOM/runtime checks, including selectors, target viewports, `scrollHeight/clientHeight`, `scrollWidth/clientWidth`, overflow CSS, and pass/fail result when code or URL exists.
- Handoff to component/table/chart skills when internal fit rules are needed.

## Quality Gate

- Do not approve a block only because it looks acceptable at one viewport.
- Do not approve or edit a layout before identifying affected child component families and their owning chart/table/filter/placement skills.
- Fixed-height KPI/card/navigation/table areas need explicit padding, line-height, gap, and overflow checks.
- Fixed-height summary/ranking/composite cards cannot pass with hidden overflow. They must prove content budget, pass DOM overflow checks within the `+2px` tolerance, or expose usable visible scroll, expand/collapse, pagination, drawer/fullscreen, or split behavior.
- Dense charts, tables, KPI Overview Cards, Micro Dashboard Cards, Composite Panels, and state feedback surfaces need enough reserved area for labels, axes, legends, pagination, child minimums, metric-cell minimums, and states.
- Do not solve a modern SaaS/BI visual request by shrinking more components into the same viewport. If the page needs extra cards or charts beyond the hierarchy budget, split, tab, drawer, fullscreen, or route to detail instead of accepting `VIS-COMPONENT-PILEUP` or `VIS-CHART-OVERWEIGHT`.
