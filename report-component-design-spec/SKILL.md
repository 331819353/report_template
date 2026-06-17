---
name: report-component-design-spec
aliases: ["时间序列KPI卡规范", "趋势卡规范", "变化卡规范", "同环比卡规范", "周期卡规范", "波动卡规范", "预测卡规范", "对比分析卡规范", "分组对比卡规范", "竞品对比卡规范", "标杆卡规范", "差异卡规范", "占比卡规范", "构成卡规范", "结构卡规范", "份额卡规范", "指标拆解卡规范", "归因拆解卡规范", "贡献卡规范", "层级拆解卡规范", "分布卡规范", "区间卡规范", "密度卡规范", "分位数卡规范", "箱线卡规范", "异常分析卡规范", "风险卡规范", "预警卡规范", "离群点卡规范"]
description: "用于创建、审计、合并或沉淀可复用的报表组件设计规范/组件规范/组件设计标准。用户提到组件设计规范、组件规范、图表规范、表格规范、KPI卡规范、KPI总览卡/多指标总览卡规范、单指标KPI卡规范、状态卡/健康度卡/评分卡/仪表盘卡/指标判断卡规范、目标执行卡/目标达成卡/差距卡/进度卡/里程碑卡规范、时间序列KPI卡/趋势卡/变化卡/同环比卡/周期卡/波动卡/预测卡规范、对比分析KPI卡/对比卡/分组对比卡/竞品对比卡/标杆卡/差异卡/偏差卡规范、排名卡/榜单卡/Top N卡/排行榜/帕累托卡规范、占比卡/构成卡/结构卡/份额卡/市场份额卡/集中度卡规范、指标拆解卡/归因拆解卡/贡献卡/层级拆解卡/驱动因素拆解/路径贡献/瀑布拆解规范、分布卡/区间卡/密度卡/分位数卡/箱线卡/直方分布/KDE密度/分布热力图规范、异常分析卡/异常卡/风险卡/预警卡/离群点卡/波动异常卡/阈值预警卡/风险矩阵卡/异常影响评估卡规范、横向指标卡/横版KPI/宽指标卡规范、横向折线KPI/坐标折线诊断卡规范、横向柱状KPI/坐标柱状诊断卡规范、横向散点KPI/关系诊断卡规范、横向地图KPI/空间诊断卡规范、双栏VS对比诊断卡规范、筛选控件规范、Analysis & Insight规范、Composite Panel规范、Micro Dashboard Card/微型看板卡规范、状态反馈/空态/loading/error/no-permission/building规范、透视表/复杂表头规范、ECharts组件规范、AntV S2组件规范、组件库沉淀、前端组件设计标准、提高前端设计中的组件规范时触发；不替代单个组件修复、整页布局或完整报表设计系统治理。"
---

# Report Component Design Spec

## Positioning

Use this skill when the output should be a reusable component-family standard, not a one-off component repair. It packages component anatomy, data contract, placement, visual rules, states, interactions, acceptance gates, and implementation handoff into a predictable spec.

When component standards are derived from user-provided visual samples, the target is `100% routable coverage` of those samples: every reusable style must be represented by a controlled pattern field, a composed pattern contract, or a documented extension gap. Component specs must be usable by text-only downstream agents and must not depend on raw screenshots or image embeddings.

It sits between `$report-design-system-governance` and `$report-component-style-design`: governance owns the whole design system; this skill owns component-family standards; component-style owns single component execution and detailed fit rules.

## Reference Map

| Need | Read |
| --- | --- |
| Preflight understanding before implementation/repair/acceptance | `$quality-gate-validation` `references/preflight-understanding-gate.md` |
| Component-family source map | `references/01-component-spec-source-map.md` |
| Reusable component spec template | `references/02-component-spec-template.md` |
| Screenshot/sample-derived style generalization target | `$report-component-style-design` `references/00a-style-generalization-goal.md` and `$artifact-readability-standard` `references/visual-source-abstraction-standard.md` |
| Report design-system baseline | `$report-design-system-governance` relevant references |
| Modern SaaS / BI Dashboard / UI Kit component language | `$report-design-system-governance` `references/12-modern-saas-bi-style-contract.md` when requested |
| Detailed component family rules | `$report-component-style-design` matching references |
| Relationship / correlation / association / influence card standards | `$report-component-style-design` `references/09b-relationship-analysis-card-patterns.md` plus matching chart/table placement and mapping references when implementation-ready |
| Anomaly / risk / warning / outlier analysis card standards | `$report-component-style-design` `references/07f-anomaly-risk-warning-outlier-cards.md` plus mapping and acceptance references when implementation-ready |
| Chart/table/filter standards | `$report-chart-design-spec`, `$report-table-design-spec`, `$report-filter-control-design-spec` |
| Placement and acceptance gates | `$report-component-placement-spec` and `$report-component-style-design` `references/12-component-acceptance-gates.md` |
| Haier/company tokens and base components | `$haier-enterprise-app-ui-design-spec` for Haier/enterprise report and common-app surfaces |
| Readiness/conflict gate | `$quality-gate-validation` |

## Anti-Laziness Gate

For non-trivial work, apply `$quality-gate-validation` `references/anti-laziness-execution-gate.md` before final output, handoff, or readiness. Do not mark the result ready while `LAZY-*` findings remain open, when available local evidence was not inspected, when owning skills were skipped, or when proof is limited to generic statements such as "checked", "optimized", "looks good", or "implemented".

## Workflow

1. Run the Preflight understanding gate for implementation, repair, or acceptance work; name component-family scope, source-of-truth hierarchy, inherited baselines, affected surfaces, hard constraints, missing evidence, and start decision.
2. Define component-standard scope: component families, target report types, surfaces, libraries, devices, and source-of-truth hierarchy.
3. For screenshot/sample-derived component families, run the style generalization goal and record whether each sample is covered by an existing pattern, composed patterns, requires an extension, or is out of scope.
4. Load the report/common-app baseline and the smallest matching component-family references.
5. For each component family, define anatomy, required/optional slots, data contract, metric/formula/unit/source needs, interaction contract, states, accessibility, responsive behavior, and exact-value disclosure.
6. Define placement rules through `$report-component-placement-spec`: coordinate variables, slot ownership, main visual center, local-filter geometry, size tiers, fallback order, and state geometry.
7. Define visual tokens and variants as semantic rules, not one-off colors or decorative effects. When modern SaaS / BI Dashboard / UI Kit language is requested, map component surfaces, borders, radius, shadow, UI controls, hierarchy, and chart-lightness constraints to the positive style contract.
8. Classify normative rules: `MUST/fail` for data contract, renderer ownership, metric display, filter scope, layout fit, accessibility, state coverage, and readiness evidence; `SHOULD/exception-required` for recommended visual defaults or density choices; `MAY/optional` for enhancements.
9. Add implementation handoff: ECharts/S2/Element Plus usage, config fields, API/view-model expectations, DOM/CSS/option proof hooks, QA crops, DOM overflow checks, and version/adoption notes.
10. Run component acceptance gates and list any gaps, deprecated patterns, or project exceptions.

## Required Output

- Preflight understanding result when the work is implementation/repair/acceptance, plus scope, source-of-truth hierarchy, and inherited Haier/report baselines.
- Component-family standard matrix.
- Style generalization coverage matrix for sample-derived standards: sample role, selected pattern field, status, adaptive variables, fallback, and extension decision.
- Per-family spec: purpose, anatomy, data contract, placement, visual tokens, states, interactions, responsive behavior, accessibility, and implementation notes.
- Rule strength and proof matrix: `MUST/fail`, `SHOULD/exception-required`, and `MAY/optional` rules with proof method, failure ID, and exception condition.
- Acceptance gates and QA evidence requirements.
- Governance fields: owner, version, status, allowed variants, deprecated patterns, exceptions, and migration notes.

## Quality Gate

- Do not write a component spec that only lists colors, font sizes, radius, and shadows.
- Do not accept a modern SaaS / BI Dashboard / UI Kit component standard that lacks semantic white-card/UI Kit token mapping, display-budget limits, and component-pileup/chart-overweight failure handling.
- Do not create or accept a reusable component standard before component-family scope, source-of-truth hierarchy, inherited baseline, and implementation surface are clear.
- Do not accept a component family without business purpose, data grain, exact-value path, states, and placement rules.
- Do not accept KPI overview / multi-metric overview standards without `kpiOverviewCardPattern`, one shared `overviewTopic`, `2-5` metric cells, lead-metric ownership when present, local-control scope, exact-value/detail path, `kpi_overview_card` minimum size, and fallback before metric cells or evidence visuals are squeezed.
- Do not accept status/health/rating/gauge judgment card standards without `kpiJudgmentCardPattern`, status/score/range/threshold semantics, one hero visual, comparison strip, footer evidence, `kpi_judgment_card` minimum `360x240`, and fallback before icon/ring/gauge/bars are squeezed.
- Do not accept target attainment / gap / progress / milestone goal execution card standards without `kpiGoalExecutionCardPattern`, `goalExecutionKind`, actual/target fields, required gap/progress/milestone fields, formula/denominator and direction semantics, exact-value/detail path, `kpi_goal_execution_card` minimum `360x240`, execution hero family minimums, comparison strip, footer evidence/deadline, and fallback before execution visuals are squeezed.
- Do not accept trend / change / YoY-MoM / cycle / volatility / forecast time-series KPI card standards without `kpiTimeSeriesCardPattern`, `temporalAnalysisKind`, ordered x/y fields, grain/latest period, direction semantics, required baseline/cycle/volatility/forecast fields, exact-value/detail path, `kpi_time_series_card` minimum `360x240`, time-series evidence zone `>=112px`, footer evidence, and fallback before temporal evidence is squeezed.
- Do not accept direct comparison / group comparison / competitor comparison / benchmark / variance KPI card standards without `kpiComparisonAnalysisCardPattern`, `comparisonAnalysisKind`, comparable subject roles, shared metric/unit/grain/filter scope, benchmark or variance fields when required, selected evidence mode, exact-value/detail path, `kpi_comparison_analysis_card` minimum `360x240`, comparison evidence zone `>=112px`, footer evidence, and fallback before radar/donut/table/chart evidence is squeezed.
- Do not accept composition / share / structure / market-share card standards without `compositionShareCardPattern`, `compositionShareEvidenceBinding`, denominator policy, category/value/total/share fields, `Top N + 其他` or merge policy, exact-value/detail path, size family, and fallback before donut, treemap, ring, stacked chart, funnel, bubble, or map evidence is squeezed.
- Do not accept indicator decomposition / attribution decomposition / contribution / hierarchy decomposition card standards without `decompositionAttributionCardPattern`, `decompositionAttributionEvidenceBinding`, explanation mode, root metric/unit/value fields, selected-pattern formula/node/link/stage/time/matrix fields, sign rule, reconciliation policy, residual/other visibility, attribution method when causal attribution is claimed, exact-value/detail path, size family, and fallback before formula, Sankey, tree, waterfall, matrix, or heatmap evidence is squeezed.
- Do not accept distribution / interval / density / quantile / boxplot card standards without `distributionAnalysisCardPattern`, `distributionAnalysisEvidenceBinding`, distribution mode, metric id/name/unit, sample grain and count, selected bucket/density/quantile/boxplot/heatmap/geography/comparison fields, interval policy, density/estimator policy when used, missing/zero/out-of-range policy, exact-value/detail path, size family, and fallback before histogram, CDF, KDE, heatmap, boxplot, scatter-strip, map, population distribution, or exact-stat table evidence is squeezed.
- Do not accept anomaly / risk / warning / outlier card standards without `anomalyAnalysisCardPattern`, `anomalyAnalysisEvidenceBinding`, one diagnostic lens, severity/status dictionary, current/baseline or threshold evidence, occurrence/update/freshness time, affected-object or impact fields when visible, exact-value/detail/action path, size family, and fallback before trend, donut, matrix, map, relation, scatter, gauge, timeline, list, or table evidence is squeezed.
- Do not accept relationship / correlation / association / influence card standards without `relationshipAnalysisCardPattern`, `relationshipAnalysisEvidenceBinding`, a declared relationship task, source/target or pair/node/edge fields, method wording, strength/direction/threshold rules when visible, exact-value/detail path, size family, renderer ownership, and fallback before matrix, network, Sankey, tree, scatter, trend, ranking, or table evidence is squeezed.
- Do not accept sample-derived reusable component standards when any reusable sample remains image-only, lacks a controlled pattern field, or cannot be reproduced from text by a non-multimodal downstream model.
- Do not leave implementation-critical component rules as advice. Renderer ownership, data contracts, metric display, filter scope, overflow/layout fit, accessibility, and state coverage must be written as `MUST/fail` with evidence requirements.
- Do not accept Haier/enterprise report component standards that define report-specific rules but omit inherited Haier typography, color, spacing, radius, shadow, state, and base-control tokens.
- Do not duplicate Haier or report design-system tokens; inherit them and state only component-specific extensions.
- Do not merge page layout rules into component specs except for the component's own parent/container assumptions.
- Load `references/02-component-spec-template.md` before delivering a reusable component design spec.
