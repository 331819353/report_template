# Analysis Perspective Card Taxonomy

Use this reference before choosing charts or card styles. It converts a vague business request into a stable analytical perspective, then into answer atoms, card families, and candidate components.

The goal is not to force every report into one perspective. A good report usually has one primary perspective and `1-3` secondary perspectives that form a decision path, such as `currentStatus -> targetProgress -> trendMovement -> causeDiagnosis -> actionRecommendation`.

## How To Use

1. Identify the user's verb: 看现状, 看目标, 看趋势, 看排名, 看原因, 看行动, and so on.
2. Select one `analysisPerspective` as primary. Add secondary perspectives only when they answer a different decision question.
3. Map each perspective to answer atoms and component bundles. Do not jump directly from the perspective to a decorative chart.
4. If a perspective switch is exposed in the UI, classify it as `controlSemantics: perspective-switch`, not an ordinary filter, because it may change metric names, component set, table headers, dimensions, or business vocabulary.
5. Keep exact-value, detail, source, and action paths near the perspective that needs them.

## Controlled Perspective Map

| `analysisPerspective` | Chinese label | Card families | Main question | Common answer atoms | Common component fit |
| --- | --- | --- | --- | --- | --- |
| `currentStatus` | 看现状 | KPI卡, 指标总览卡, 状态卡, 健康度卡, 评分卡, 仪表盘卡 | 当前怎么样? 是否正常? | `status`, `targetGap`, `evidence` | metric card with `kpiJudgmentCardPattern`, gauge, progress bar, status chip, scorecard |
| `targetProgress` | 看目标 | 目标达成卡, 进度卡, 差距卡, 里程碑卡 | 距离目标还差多少? 完成到哪一步了? | `targetGap`, `variance`, `trend` | metric card with `kpiGoalExecutionCardPattern`, gauge, progress bar, bullet/progress bar, target/actual bar, line |
| `trendMovement` | 看趋势 | 趋势卡, 变化卡, 同环比卡, 波动卡, 周期卡, 预测卡 | 过去怎么变? 未来可能怎么走? | `trend`, `variance`, `anomaly` | metric card with `kpiTimeSeriesCardPattern` for card-level trend/change/YoY-MoM/cycle/volatility/forecast, line, area, theme-river only with real stream data, calendar/heatmap for time pattern |
| `comparisonDifference` | 看对比 | 对比卡, 分组对比卡, 差异卡, 标杆卡, 竞品对比卡 | 谁更高? 谁更低? 差异有多大? | `variance`, `ranking`, `evidence` | metric card with `kpiComparisonAnalysisCardPattern`, bar/horizontal bar, radar for multi-metric profile, comparison table, matrix |
| `rankingContribution` | 看排名 | 排名卡, Top N卡, Bottom N卡, 榜单卡, 帕累托卡 | 谁排前面? 主要贡献来自谁? | `ranking`, `structure`, `cause` | ranking/leaderboard/Top N card with `rankingCardPattern`, Pareto card with `paretoCardPattern` when contribution is additive, horizontal bar, column bar, ranking table |
| `compositionShare` | 看占比 | 占比卡, 结构卡, 构成卡, 份额卡, 市场份额卡, 集中度卡 | 各部分占多少? 结构是否合理? | `structure`, `evidence` | card with `compositionShareCardPattern`, donut/detail, percent bars, treemap, sunburst, stacked share trend, share ranking, map structure |
| `decompositionDriver` | 看拆解 | 指标拆解卡, 归因拆解卡, 层级拆解卡, 贡献卡, 驱动因素卡, 路径贡献卡 | 指标由哪些部分组成? 谁贡献最大? | `cause`, `structure`, `ranking` | card with `decompositionAttributionCardPattern`, formula, tree, Sankey, waterfall, matrix/table |
| `distributionSpread` | 看分布 | 分布卡, 区间卡, 密度卡, 分位数卡, 离散卡, 箱线卡 | 数据集中在哪? 是否分散? | `structure`, `anomaly`, `evidence` | card with `distributionAnalysisCardPattern`, histogram/interval, CDF/quantile, KDE/density, boxplot, calendar/heatmap, population pyramid, detail table |
| `anomalyRisk` | 看异常 | 异常卡, 预警卡, 风险卡, 离群点卡, 波动异常卡 | 哪里不正常? 是否需要关注? | `anomaly`, `action`, `evidence` | card with `anomalyAnalysisCardPattern`, line with threshold, scatter outlier, boxplot, heatmap/matrix, alert list, relation influence, map, response status |
| `relationshipInfluence` | 看关系 | 相关性卡, 关系卡, 关联卡, 影响因素卡, 关系网络卡 | A 和 B 有没有关系? 谁和谁相关? 哪些因素有关联或影响? | `cause`, `evidence`, `structure` | card with `relationshipAnalysisCardPattern`, scatter/quadrant, correlation heatmap, relation graph, Sankey when directed flow exists, tree when hierarchy exists, line when relation changes over time, ranking/table for factor strength and audit |
| `flowTransfer` | 看流转 | 流向卡, 路径卡, 迁移卡, 流量分布卡 | 数据/用户/资金从哪来, 到哪去? | `process`, `structure`, `evidence` | Sankey, path chart, map only for geography, chord only with pair flows |
| `processBottleneck` | 看流程 | 流程卡, 步骤卡, 节点卡, 瓶颈卡 | 流程经过哪些环节? 哪里卡住了? | `process`, `anomaly`, `action` | process chart, path chart, funnel, Sankey |
| `conversionRetention` | 看转化 | 漏斗卡, 转化卡, 流失卡, 留存卡, 阶段转化卡 | 每一步转化率多少? 哪里流失最多? | `process`, `ranking`, `trend` | funnel, line, bar, Sankey when branches exist |
| `spatialDistribution` | 看空间 | 地图卡, 区域分布卡, 地理热区卡, 网点覆盖卡, 迁徙卡 | 哪些地区表现好? 空间上如何分布? | `structure`, `location`, `ranking` | map, geo coordinate, heatmap, path chart |
| `timePattern` | 看时间规律 | 日历卡, 周期卡, 时段分布卡, 峰谷卡 | 哪些日期/时间段更突出? | `trend`, `structure`, `anomaly` | calendar heatmap, heatmap, line, cycle/period KPI time-series card |
| `multiDimensionalProfile` | 看多维特征 | 画像卡, 雷达卡, 多维对比卡, 标签卡 | 一个对象有哪些特征? 优势短板是什么? | `structure`, `comparison`, `evidence` | radar, parallel coordinates, tag group |
| `populationObject` | 看人群/对象 | 用户画像卡, 客户分群卡, 客群对比卡, 对象详情卡 | 不同人群/对象有什么差异? | `structure`, `comparison`, `detail` | radar, bar, scatter, detail table |
| `matrixDecision` | 看矩阵判断 | 象限卡, 矩阵卡, 优先级卡, 策略分层卡 | 应该重点关注谁? 放在哪个象限? | `ranking`, `cause`, `action` | scatter quadrant, matrix coordinate, bubble |
| `marketMovement` | 看行情 | 行情卡, K线卡, 波动卡, 涨跌卡 | 价格/指数如何变化? | `trend`, `anomaly`, `detail` | candlestick/K-line, line, volume bar |
| `definitionHelp` | 看说明 | 说明卡, 注释卡, 定义卡, 口径卡, 帮助卡 | 这个指标什么意思? 怎么算的? | `narrative`, `dataTrust`, `evidence` | text, icon, tooltip, definition panel |
| `conclusionInsight` | 看结论 | 结论卡, 洞察卡, 摘要卡, 解读卡 | 这组数据说明了什么? | `narrative`, `status`, `evidence` | text summary, key metrics, conclusion/evidence/action card |
| `causeDiagnosis` | 看原因 | 归因卡, 诊断卡, 原因分析卡, 影响因素卡 | 为什么变好/变差? 主要原因是什么? | `cause`, `variance`, `evidence` | decomposition chart, contribution chart, scatter, table |
| `actionRecommendation` | 看行动 | 建议卡, 策略卡, 待办卡, 下一步卡 | 接下来该做什么? | `action`, `anomaly`, `detail` | text, button, task list, status chip |
| `reviewImpact` | 看复盘 | 复盘卡, 事件卡, 前后对比卡, 影响评估卡 | 某个动作/活动带来了什么变化? | `trend`, `variance`, `narrative` | line, before/after comparison, timeline |
| `dataQualityTrust` | 看质量 | 数据质量卡, 完整性卡, 准确性卡, 异常数据卡 | 数据靠不靠谱? 有没有缺失或错误? | `dataTrust`, `anomaly`, `detail` | KPI, table, status card, exception list |
| `detailEvidence` | 看明细 | 明细卡, 列表卡, 样本卡, 日志卡 | 具体数据是什么? 能否下钻查看? | `detail`, `evidence`, `record` | detail table, list, timeline, drawer |
| `filterExploration` | 看筛选探索 | 筛选卡, 钻取卡, 联动卡, 条件分析卡 | 按不同条件看结果会怎样? | `evidence`, `detail`, `trend` | filter controls, tags, dropdowns, linked charts |

## Composition Rules

- `currentStatus` without `targetProgress`, `trendMovement`, `detailEvidence`, or `actionRecommendation` often becomes a shallow dashboard. Add one evidence path when the surface is decision-facing.
- `targetProgress` should carry target formula, denominator, time progress, missing-target state, and `kpiGoalExecutionCardPattern` when the answer is a card-level target attainment, gap, progress, or milestone execution judgment before visual styling.
- `trendMovement` and `reviewImpact` must declare time grain, baseline/event date, and missing-period behavior. Use `kpiTimeSeriesCardPattern` when the answer is a compact card-level trend, change, YoY/MoM, cycle, volatility, or forecast judgment; split to a full chart/table when the time-series evidence needs dense audit.
- `comparisonDifference` must declare the comparable subject grain, role labels, shared metric/unit/grain/filter scope, direction semantics, deterministic sort, and exact-value tooltip/detail. Use `kpiComparisonAnalysisCardPattern` when the answer is a compact card-level direct comparison, group/segment comparison, competitor position, benchmark distance, or variance/gap diagnosis; split to full chart/table when the comparison requires dense audit.
- `rankingContribution` must declare `rankingCardPattern`, `rankingEvidenceBinding`, deterministic sort, Top N/`其他` rules, visible-row/slot budget, tie-break fields, and exact-value tooltip/detail. When it becomes Pareto, also declare `paretoCardPattern`, `paretoEvidenceBinding`, additive value, cumulative share, threshold boundary, and long-tail policy.
- `compositionShare` must declare `compositionShareCardPattern`, `compositionShareEvidenceBinding`, denominator policy, `Top N + 其他` or small-slice merge rules, share formula, color/category identity, exact-value tooltip/detail, and fallback when the denominator or share reconciliation is invalid.
- `decompositionDriver` must declare `decompositionAttributionCardPattern`, `decompositionAttributionEvidenceBinding`, root metric, formula/node/link/stage/matrix fields as required by the selected pattern, sign rule, reconciliation policy, residual/other policy, exact-value tooltip/detail, and fallback before formula, tree, Sankey, waterfall, or matrix evidence is squeezed. Do not claim attribution or causality without an attribution method or diagnostic model.
- `distributionSpread` must declare `distributionAnalysisCardPattern`, `distributionAnalysisEvidenceBinding`, sample grain/count, metric/unit, selected bucket/density/quantile/boxplot/heatmap/geography fields, interval/density policy, missing/zero/out-of-range policy, exact-value tooltip/detail, and fallback before histogram, density, boxplot, heatmap, or interval evidence is squeezed. Do not claim density, quartiles, or outliers without statistical fields or a named estimator/rule.
- `anomalyRisk` must declare `anomalyAnalysisCardPattern`, `anomalyAnalysisEvidenceBinding`, one diagnostic lens, severity/status dictionary, baseline or threshold evidence, occurrence/update/freshness time, affected object or impact fields when visible, exact-value/detail/action route, and fallback before trend, donut, matrix, map, relation, scatter, gauge, timeline, list, or table evidence is squeezed. Use `visualType: anomaly-card` when the card owns abnormality context; use stricter chart/list/table/KPI patterns only for bare evidence bodies.
- `causeDiagnosis` is not valid without either additive contribution, driver evidence, comparison deltas, or a diagnostic table.
- `processBottleneck`, `conversionRetention`, and `flowTransfer` require ordered stages or directed links. Use bar/table instead when the data is only category comparison.
- `relationshipInfluence` must declare `relationshipAnalysisCardPattern`, `relationshipAnalysisEvidenceBinding`, the relation task, method wording, source/target or pair/node/edge fields, strength/direction/threshold rules when visible, density limits, exact-value tooltip/detail, and fallback. Do not claim influence or causality when the evidence is only correlation, co-occurrence, or similarity.
- `matrixDecision` and `multiDimensionalProfile` require explicit metric axes/dimensions and a table/detail fallback for exact object values.
- `spatialDistribution` requires real geography fields. Do not use a map when region is only an organization label.
- `definitionHelp`, `dataQualityTrust`, and `detailEvidence` are trust/evidence perspectives. They can be secondary but should not be removed from implementation-ready analytical pages when metric口径, source, row proof, or export matter.
- `filterExploration` changes how users explore the report. Treat its controls as `perspective-switch`, `global-filter`, `local-filter`, or `drilldown-param` according to schema impact.

## Contract Notes

For every mapped component, add:

```text
analysisPerspective: controlled value from this file
businessQuestion: concrete question in user language
answerAtom: controlled answer atom
semanticRole: controlled semantic role
componentType / visualType / pattern field
data grain, required fields, formula or source proof
interaction or evidence path
```

When a single component supports multiple perspectives, use one primary `analysisPerspective` and put secondary perspectives in `secondaryAnalysisPerspectives`. Do not duplicate the component only to represent each perspective separately.
