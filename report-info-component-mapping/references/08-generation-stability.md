# 08 Generation Stability

Use this reference whenever the output may become a reusable specification, widget config, mock dataset, prototype implementation, or generated file.

## Stability Goal

The same business input should produce the same:

- Primary report type and secondary report-type routing.
- Display theme and selected pattern-card IDs when supplied by the prototype workflow.
- `styleGeneralization` status, canonical pattern reference, and adaptive variables when the style comes from screenshots, visual samples, or reusable pattern libraries.
- `analysisPerspective` and `secondaryAnalysisPerspectives` before answer atoms when the business request is phrased as "看现状/看目标/看趋势/看排名/看原因/看行动" or equivalent.
- Answer atoms and component priorities.
- Sample/source module roles when restoration input exists.
- Component IDs, parent block IDs, sub-block IDs, dataset IDs, filter IDs, and action names.
- `visualType`, control semantics, component schema impact, layout span category, row grain, and required fields.
- `conclusionCardPattern` for conclusion/evidence/action cards when a lead conclusion is combined with KPI evidence, findings, and recommended actions.
- `kpiCardPattern`, `kpiCardOrientation`, `kpiOverviewCardPattern`, `kpiSingleIndicatorLayoutMode`, `kpiJudgmentCardPattern`, `kpiGoalExecutionCardPattern`, `kpiTimeSeriesCardPattern`, `kpiComparisonAnalysisCardPattern`, `kpiComparisonAnalysisEvidenceMode`, `kpiAxisLineEvidenceMode`, `kpiAxisBarEvidenceMode`, `kpiScatterEvidenceMode`, `kpiMapEvidenceMode`, and `kpiComparisonEvidenceMode` for KPI/metric-card variants when a reusable card expression is selected, including KPI overview cards, single-indicator KPI grid cards, KPI judgment cards, KPI goal execution cards, KPI time-series analysis cards, comparison analysis KPI cards, landscape/horizontal KPI cards, horizontal axis-line diagnostic KPI cards, horizontal axis-bar diagnostic KPI cards, horizontal scatter diagnostic KPI cards, spatial-map diagnostic KPI cards, and paired comparison diagnostic KPI cards.
- `targetActualCardPattern` for target/actual comparison card variants when a KPI headline and target comparison bar chart are combined.
- `targetActualTrendCardPattern` for target/actual trend card variants when a KPI headline and target/comparison line chart are combined.
- `targetActualRadarCardPattern` for target/actual radar card variants when a KPI headline and target/comparison radar chart are combined.
- `targetActualDonutCardPattern` for target/actual donut card variants when a KPI headline and actual composition donut chart are combined with target/comparison summary.
- `targetActualScatterCardPattern` for target/actual scatter card variants when a KPI headline and actual/comparison scatter distribution are combined with target/reference line.
- `targetActualTablePattern` for target/actual detail table variants when ranked row evidence, comparison, target, completion rate, and total reconciliation are primary.
- `targetActualPivotTablePattern` for target/actual pivot table variants when row hierarchy, dimension controls, grouped measures, subtotals, grand totals, and completion reconciliation are primary.
- `tableCardPattern` for reusable table card variants when table-specific row grain, header structure, S2/pivot behavior, fixed columns, grouped subtotal, or tree hierarchy behavior is primary.
- `rankingCardPattern` for ranking, leaderboard, and TOP N variants when a bounded ranked list, rank badge, value/share, trend/progress/comparison evidence, and overflow path are primary.
- `paretoCardPattern` for Pareto/key-factor contribution variants when sorted additive values, cumulative share, threshold boundary, and long-tail policy are primary.
- `compositionShareCardPattern` for occupancy/share/composition/structure/market-share/concentration variants when visible denominator, share formula, category identity, exact-value path, and `Top N + 其他` behavior are primary.
- `decompositionAttributionCardPattern` for indicator decomposition, attribution, contribution, variance, hierarchy, path, and matrix variants when a root metric, explanation path, reconciliation policy, and exact-value route are primary.
- `distributionAnalysisCardPattern` for distribution, interval, density, quantile, and boxplot variants when sample grain/count, bucket/quantile/statistical fields, exact-value path, and missing/zero/out-of-range policy are primary.
- `anomalyAnalysisCardPattern` for anomaly, risk, warning, outlier, volatility abnormality, threshold warning, risk matrix, impact assessment, relation influence, geography, and response-status cards when severity/status, baseline/threshold/time, impact/object, exact-value path, and action context are primary.
- `basicChartCardPattern` for reusable basic chart card variants when a card-level chart needs stable title/legend/control/tooltip composition.
- `specializedChartCardPattern` for reusable specialized chart card variants when gauge, map, heatmap, K-line, boxplot, parallel, or bubble geometry is required by the data shape.
- `flowHierarchyDiagramCardPattern` for reusable flow/hierarchy diagram card variants when process, flow, relation, hierarchy, or path geometry is required by the data shape.
- `relationshipAnalysisCardPattern` for reusable relationship, correlation, association, influence, and relation-network cards when the analysis perspective is `relationshipInfluence`.
- `listStatusPattern` for reusable information list, task list, alert list, exception list, status chip, timeline, user/object list, and mixed work-item list variants.
- `filterControlPattern` for visible filter selector variants when the filter surface itself is part of the reusable design.
- `overlayPanelPattern` for reusable overlay, drawer, modal, action sheet, notification, navigation, and detail panel variants.
- `microDashboardCardPattern` for large single-topic mini dashboard cards that combine KPI strip, multiple bounded child sections, and exact-value/status evidence.
- `stateFeedbackPattern` for reusable empty, loading, error, no-permission, building, stale, partial, disabled, and success states.
- Binding matrix columns and validation cases.

If a later revision changes these, it must be because the business question, data shape, template capability, or user instruction changed.

## Generation Modes

Choose one mode before generating.

- `concept-map`: for design discussion only. Output answer atoms and component bundle; do not invent detailed rows.
- `spec-contract`: default when the user asks for design, optimization, or handoff. Output components, mock/data model, filters, interactions, and binding matrix.
- `prototype-config`: when creating or repairing runnable Vue/template files. Output or implement config-compatible IDs, datasets, filters, actions, and validation cases.

When mode is unclear, use `spec-contract`.

For `prototype-config` targeting bundled dashboard templates, the physical mock-data target is `src/data/dashboard.dataset.json`: filter option datasets go under `filterData`, business/component datasets go under `businessData`, and widgets/filters bind through `widget.data` or `filters[].source`. Do not create generated `*.ts` fixture modules for mock rows, arrays, or payloads.

## Controlled Vocabularies

Use these values unless the target project explicitly defines a different vocabulary.

- `answerAtom`: `status`, `targetGap`, `variance`, `trend`, `structure`, `ranking`, `process`, `cause`, `anomaly`, `detail`, `action`, `evidence`, `dataTrust`, `narrative`.
- `analysisPerspective`: `currentStatus`, `targetProgress`, `trendMovement`, `comparisonDifference`, `rankingContribution`, `compositionShare`, `decompositionDriver`, `distributionSpread`, `anomalyRisk`, `relationshipInfluence`, `flowTransfer`, `processBottleneck`, `conversionRetention`, `spatialDistribution`, `timePattern`, `multiDimensionalProfile`, `populationObject`, `matrixDecision`, `marketMovement`, `definitionHelp`, `conclusionInsight`, `causeDiagnosis`, `actionRecommendation`, `reviewImpact`, `dataQualityTrust`, `detailEvidence`, `filterExploration`. Use this before `answerAtom` when selecting card families from a business intent.
- `semanticRole`: `judgment`, `comparison`, `movement`, `location`, `rank`, `conversion`, `driver`, `risk`, `record`, `operation`, `proof`, `trust`, `story`.
- `block`: `header`, `filter`, `summary`, `kpi`, `targetVariance`, `trend`, `structure`, `ranking`, `process`, `decomposition`, `alert`, `detail`, `taskAction`, `evidence`, `dataTrust`, `footer`.
- `priority`: `must-have`, `should-have`, `optional`.
- `componentType`: `card`, `chart`, `table`, `text-summary`, `drawer`, `task`, `action`, `custom`.
- `visualType`: `line`, `bar`, `combo`, `candlestick`, `heatmap`, `pie`, `radar`, `path`, `sunburst`, `gauge`, `scatter`, `boxplot`, `parallel`, `map`, `graph`, `tree`, `treemap`, `sankey`, `funnel`, `metric-card`, `text-summary`, `table`, `pivot`, `ranking-list`, `composition-card`, `decomposition-card`, `distribution-card`, `anomaly-card`, `operational-list`, `overlay-panel`, `composite-panel`, `micro-dashboard`, `state-feedback`, `other`.
- `conclusionCardPattern`: `metric-evidence-conclusion`, `finding-action-conclusion`, `compact-conclusion-summary`. Use inside `analysisInsightContract` with `subtype: conclusion-card` and `visualType: text-summary`.
- `kpiCardPattern`: `plain-metric`, `target-wave`, `mini-bar-trend`, `highlight-line-trend`, `horizontal-trend-compare`, `horizontal-axis-line-trend`, `horizontal-axis-bar-compare`, `horizontal-axis-scatter-diagnostic`, `horizontal-spatial-map-diagnostic`, `paired-comparison-diagnostic`, `horizontal-ring-progress`, `horizontal-target-progress`, `horizontal-status-trend-compare`, `horizontal-grain-bar-switch`, `horizontal-period-summary-strip`, `horizontal-pp-assist-info`, `horizontal-warning-status-band`. Use only with `visualType: metric-card`.
- `kpiCardOrientation`: `portrait`, `landscape`, `compact-row`, `wide-banner`. Use with `visualType: metric-card`; set `landscape`, `compact-row`, or `wide-banner` when a horizontal KPI pattern is selected.
- `kpiAxisLineEvidenceMode`: `basic-compare-line`, `filled-baseline-line`, `target-reference-line`, `phase-annotated-line`, `unit-axis-line`, `grain-switch-line`, `dual-comparison-line`, `threshold-band-line`. Use only with `kpiCardPattern: horizontal-axis-line-trend`.
- `kpiAxisBarEvidenceMode`: `basic-horizontal-bar`, `period-comparison-bar`, `target-reference-bar`, `category-change-sidebar-bar`, `time-series-horizontal-bar`, `grain-switch-horizontal-bar`, `dual-series-horizontal-bar`, `threshold-warning-bar`. Use only with `kpiCardPattern: horizontal-axis-bar-compare`.
- `kpiScatterEvidenceMode`: `correlation-trendline-scatter`, `mean-reference-scatter`, `target-crosshair-scatter`, `distribution-change-band-scatter`, `threshold-quadrant-scatter`, `dual-series-trendline-scatter`, `change-callout-scatter`, `category-quadrant-scatter`. Use only with `kpiCardPattern: horizontal-axis-scatter-diagnostic`.
- `kpiMapEvidenceMode`: `choropleth-heat-map`, `graded-choropleth-map`, `bubble-target-gap-map`, `distribution-change-marker-map`, `column-symbol-map`, `annotated-interval-map`, `yoy-change-zone-map`, `point-category-summary-map`. Use only with `kpiCardPattern: horizontal-spatial-map-diagnostic`.
- `kpiComparisonEvidenceMode`: `metric-yoy-vs`, `progress-mom-vs`, `target-gap-progress-vs`, `improvement-dot-matrix-vs`, `trend-yoy-vs`, `structure-breakdown-vs`, `percentage-ring-vs`, `trend-mom-vs`. Use only with `kpiCardPattern: paired-comparison-diagnostic`.
- `kpiOverviewCardPattern`: `lead-metric-comparison-sparkline-overview`, `multi-metric-strip-progress-overview`, `domain-metric-cluster-progress-overview`. Use with `visualType: metric-card` for wide domain/topic overview cards with `2-5` visible metrics, one local control group, and at most one compact evidence visual.
- `kpiSingleIndicatorLayoutMode`: `dropdown-sparkline-progress`, `unit-toggle-ring-progress`, `dropdown-minibar-progress`, `grain-switch-minibar-progress`, `dropdown-area-sparkline-progress`, `scale-toggle-area-progress`, `dropdown-gauge-progress`. Use with `visualType: metric-card` for peer grids of one-metric KPI cards that share header/value/comparison/evidence/footer grammar.
- `kpiJudgmentCardPattern`: `semantic-status-icon-card`, `progress-status-ring-card`, `health-score-ring-card`, `health-threshold-bullet-card`, `health-dimension-breakdown-card`, `rating-score-summary-card`, `rating-distribution-card`, `semicircle-gauge-target-card`. Use with `visualType: metric-card` for status, health, score, rating, risk, progress, and gauge judgment cards with explicit status/range/threshold semantics.
- `kpiGoalExecutionCardPattern`: `attainment-ring-summary-card`, `attainment-gauge-deadline-card`, `attainment-linear-target-card`, `attainment-unit-progress-card`, `gap-gauge-deficit-card`, `gap-target-actual-compare-card`, `progress-plan-actual-card`, `milestone-timeline-card`. Use with `visualType: metric-card` for target attainment, gap, plan-vs-actual progress, remaining work, deadline, and milestone execution cards with explicit actual/target/gap/progress/milestone fields.
- `kpiTimeSeriesCardPattern`: `trend-line-target-card`, `change-baseline-delta-card`, `yoy-mom-comparison-card`, `cycle-period-progress-card`, `volatility-stat-card`, `forecast-interval-card`. Use with `visualType: metric-card` for trend movement, named-baseline change, YoY/MoM comparison, cycle/period state, volatility/stability, and forecast uncertainty cards with explicit ordered series and baseline/cycle/volatility/forecast fields.
- `kpiComparisonAnalysisCardPattern`: `direct-value-compare-card`, `group-segment-compare-card`, `competitor-position-card`, `benchmark-position-card`, `variance-gap-card`. Use with `visualType: metric-card` for direct comparison, group/segment comparison, competitor position, benchmark distance, and variance/gap diagnosis cards with explicit comparable subject grain, role labels, shared metric/unit/grain, benchmark or variance fields, sort rules, and exact values.
- `kpiComparisonAnalysisEvidenceMode`: `side-by-side-values`, `grouped-bars`, `stacked-distribution`, `multi-series-trend`, `market-share-donut`, `radar-profile`, `benchmark-ruler`, `variance-gauge`, `nps-score-scale`, `comparison-table`, `map-table-compare`. Use only with `kpiComparisonAnalysisCardPattern`.
- `targetActualCardPattern`: `standard-summary-panel`, `emphasis-header-summary`, `soft-chip-summary`. Use with `visualType: bar` and `chartSubtype: target-actual-comparison`.
- `targetActualTrendCardPattern`: `emphasis-wave-trend`, `standard-summary-trend`, `soft-chip-trend`. Use with `visualType: line` and `chartSubtype: target-actual-trend`.
- `targetActualRadarCardPattern`: `emphasis-wave-radar`, `standard-action-radar`. Use with `visualType: radar` and `chartSubtype: target-actual-radar`.
- `targetActualDonutCardPattern`: `emphasis-filter-donut`, `standard-filter-donut`. Use with `visualType: pie` and `chartSubtype: target-actual-donut`.
- `targetActualScatterCardPattern`: `emphasis-filter-scatter`, `standard-filter-scatter`. Use with `visualType: scatter` and `chartSubtype: target-actual-scatter`.
- `tableSubtype`: `target-actual-detail`, `target-actual-pivot`. Use with `componentType: table` for target/actual table cards.
- `targetActualTablePattern`: `standard-audit-table`, `compact-audit-table`. Use with `visualType: table` and `tableSubtype: target-actual-detail`.
- `targetActualPivotTablePattern`: `standard-hierarchy-pivot`, `share-matrix-pivot`, `tree-expand-pivot`. Use with `visualType: pivot` and `tableSubtype: target-actual-pivot`.
- `tableCardPattern`: `plain-detail-ledger-table`, `filtered-operational-status-table`, `grouped-header-summary-table`, `metric-matrix-table`, `s2-cross-pivot-table`, `fixed-column-scroll-table`, `grouped-subtotal-summary-table`, `tree-hierarchy-table`. Use with `componentType: table` and `visualType: table` or `pivot`.
- `rankingCardPattern`: `basic-rank-list-card`, `trend-delta-rank-list-card`, `progress-bar-rank-list-card`, `podium-rank-card`, `yoy-microbar-rank-list-card`, `radar-comparison-rank-card`, `metric-summary-rank-card`, `time-switch-rank-card`, `share-donut-rank-card`, `map-distribution-rank-card`, `topn-bar-rank-card`, `topn-comparison-rank-card`, `topn-waterfall-strip-card`, `topn-sparkline-rank-list-card`, `topn-bubble-rank-card`, `topn-icon-card-grid`, `medal-horizontal-ranking`, `bar-progress-ranking`, `compact-list-ranking`. Use with `componentType: card` and `visualType: ranking-list`.
- `paretoCardPattern`: `pareto-basic-card`, `pareto-table-chart-card`, `pareto-dual-axis-card`, `pareto-cumulative-fill-card`, `pareto-stacked-share-card`, `pareto-bubble-card`, `pareto-zone-card`, `pareto-ring-list-card`. Use with `componentType: card`, `visualType: ranking-list`, and `paretoEvidenceBinding`.
- `compositionShareCardPattern`: `basic-donut-share-card`, `donut-detail-share-card`, `percent-bar-share-card`, `multi-ring-hierarchy-share-card`, `share-trend-stack-card`, `share-ranking-topn-card`, `treemap-composition-card`, `share-metrics-summary-card`, `stacked-strip-composition-card`, `stacked-column-trend-composition-card`, `funnel-composition-card`, `bubble-composition-card`, `market-share-overview-card`, `market-share-concentration-card`, `share-distribution-interval-card`, `map-structure-card`, `sunburst-structure-card`. Use with `componentType: card`, `visualType: composition-card`, and `compositionShareEvidenceBinding`.
- `decompositionAttributionCardPattern`: `formula-decomposition-card`, `funnel-decomposition-card`, `tree-decomposition-card`, `sankey-decomposition-card`, `driver-factor-decomposition-card`, `variance-waterfall-decomposition-card`, `combined-decomposition-card`, `multilevel-metric-decomposition-card`, `total-attribution-card`, `funnel-attribution-card`, `channel-attribution-donut-card`, `touchpoint-attribution-list-card`, `segment-attribution-card`, `feature-attribution-bar-card`, `time-attribution-waterfall-card`, `multidimensional-attribution-matrix-card`, `overall-contribution-card`, `contribution-waterfall-card`, `contribution-structure-card`, `contribution-comparison-card`, `contribution-trend-card`, `contribution-tree-card`, `key-contribution-topn-card`, `contribution-heatmap-card`, `progressive-hierarchy-decomposition-card`, `hierarchy-tree-decomposition-card`, `hierarchy-waterfall-card`, `indented-hierarchy-table-card`, `hierarchy-share-card`, `path-contribution-card`, `multilevel-comparison-hierarchy-card`, `target-attainment-hierarchy-attribution-card`. Use with `componentType: card`, `visualType: decomposition-card`, and `decompositionAttributionEvidenceBinding`.
- `distributionAnalysisCardPattern`: `numeric-histogram-distribution-card`, `interval-donut-distribution-card`, `percentile-cdf-distribution-card`, `geographic-distribution-card`, `time-distribution-card`, `distribution-comparison-card`, `calendar-heatmap-distribution-card`, `multidimensional-population-distribution-card`, `interval-histogram-card`, `interval-share-donut-card`, `interval-boxplot-card`, `interval-comparison-card`, `interval-stacked-trend-card`, `cumulative-interval-card`, `interval-scatter-strip-card`, `interval-detail-table-card`, `univariate-density-curve-card`, `interval-density-curve-card`, `grouped-density-comparison-card`, `density-heatmap-card`, `kde-cumulative-density-card`, `bivariate-density-hexbin-card`, `quantile-band-density-card`, `density-overview-card`, `boxplot-kpi-summary-card`, `time-series-boxplot-card`, `grouped-boxplot-comparison-card`, `boxplot-overview-card`, `boxplot-side-summary-card`, `weekday-boxplot-card`, `anomaly-boxplot-card`, `boxplot-detail-table-card`. Use with `componentType: card`, `visualType: distribution-card`, and `distributionAnalysisEvidenceBinding`.
- `anomalyAnalysisCardPattern`: `anomaly-overview-card`, `anomaly-trend-compare-card`, `anomaly-distribution-structure-card`, `anomaly-interval-threshold-card`, `anomaly-timeline-card`, `anomaly-ranking-top-card`, `anomaly-impact-assessment-card`, `anomaly-baseline-compare-card`, `anomaly-summary-table-card`, `anomaly-multi-metric-monitor-card`, `risk-matrix-card`, `risk-response-status-card`, `anomaly-relation-influence-card`, `anomaly-geographic-distribution-card`, `outlier-scatter-card`, `warning-progress-donut-card`. Use with `componentType: card`, `visualType: anomaly-card`, `analysisPerspective: anomalyRisk`, and `anomalyAnalysisEvidenceBinding`.
- `basicChartCardPattern`: `single-series-bar-card`, `comparison-line-trend-card`, `area-trend-card`, `bar-line-combo-card`, `pie-composition-card`, `donut-composition-card`, `stacked-bar-composition-card`, `multi-metric-combo-card`, `filtered-bar-card`, `tooltip-line-trend-card`. Use with `componentType: chart` and a real chart-family `visualType`.
- `specializedChartCardPattern`: `gauge-progress-card`, `choropleth-ranking-map-card`, `time-heatmap-card`, `candlestick-volume-card`, `boxplot-distribution-card`, `parallel-profile-card`, `bubble-opportunity-card`. Use with `componentType: chart` and a real specialized chart-family `visualType`.
- `flowHierarchyDiagramCardPattern`: `conversion-funnel-card`, `multi-stage-sankey-card`, `journey-stage-map-card`, `hierarchy-tree-card`, `hub-relation-network-card`, `sunburst-composition-card`, `treemap-composition-card`, `path-conversion-flow-card`. Use with `componentType: chart` and a real flow/hierarchy diagram `visualType`.
- `relationshipAnalysisCardPattern`: `relation-overview-hub-card`, `relation-strength-matrix-card`, `relation-flow-sankey-card`, `relation-community-network-card`, `relation-pair-compare-card`, `relation-trend-card`, `relation-hierarchy-tree-card`, `relation-bubble-quadrant-card`, `relation-factor-ranking-card`, `relation-evolution-snapshot-card`, `relation-bipartite-attribute-card`, `relation-detail-table-card`. Use with `analysisPerspective: relationshipInfluence`; keep `visualType` as the actual renderer such as scatter, heatmap, graph, Sankey, tree, line, bar, or table.
- `listStatusPattern`: `simple-info-list`, `progress-task-list`, `severity-alert-list`, `exception-record-list`, `status-chip-set`, `event-timeline`, `user-object-list`, `mixed-info-list`. Use with `visualType: operational-list`.
- `overlayPanelPattern`: `right-filter-drawer`, `bottom-action-sheet`, `center-confirmation-modal`, `fullscreen-detail-modal`, `top-notification-bar`, `left-navigation-drawer`, `side-detail-drawer`, `large-detail-side-panel`. Use with `visualType: overlay-panel`.
- `microDashboardCardPattern`: `sales-fresh-analysis-board`, `user-operations-purple-board`, `supply-chain-orange-monitoring-board`, `finance-blue-analysis-board`. Use with `visualType: micro-dashboard`.
- `stateFeedbackPattern`: `fresh-line-state-set`, `soft-illustration-state-set`, `minimal-line-state-set`, `dark-tech-state-set`, `glass-card-state-set`, `playful-healing-state-set`, `business-blue-state-set`, `immersive-fullscreen-state-set`. Use with `visualType: state-feedback`.
- `stateFeedbackKind`: `empty`, `filtered-empty`, `loading`, `error`, `no-permission`, `building`, `stale`, `partial-data`, `disabled`, `success`.
- `actionType`: `openModal`, `closeModal`, `setFilters`, `resetFilters`, `navigateUrl`, `print`, `fullscreen`, `refresh`, or `custom` with `customActionId` registered in the project.
- `filterValueType`: `single`, `multiple`, `range`, `keyword`, `date`, `treePath`, `enum`, `toggle`, `mixed`.
- `filterControlPattern`: `single-select-dropdown`, `multi-tag-select`, `date-range-selector`, `searchable-select`, `tree-path-selector`, `advanced-filter-drawer`, `combined-filter-chipbar`. Use with visible page/global, component-local, table-toolbar, or drawer-internal filters.
- `controlSemantics`: `perspective-switch`, `global-filter`, `local-filter`, `drilldown-param`.
- `componentSchemaImpact`: `none`, `row-scope-only`, `metric-name`, `metric-set`, `component-set`, `table-schema`, `dimension-set`, `definition-change`, `domain-vocabulary`, `mixed`.
- `navigationMetricKind`: `percentage`, `ranking`, `status-light`.
- `periodBehavior`: `selected-period`, `current-period`, `comparison-period`, `rolling-window`, `latest-snapshot`, `static-display-copy`.
- `filterExecutionStage`: `sql-where`, `source-query`, `provider-query`, `repository-query`, `resolver-param`, `redis-cache`, `precompute-cache`, `component-local`, `bounded-local`, `blocked`.
- `dataPolicy`: `bound`, `static`, `external`. Prefer `bound`.
- `sampleModuleRole`: `businessRequired`, `sampleStructure`, `optionalEnhancement`.
- `subBlockRole`: `summary`, `evidence`, `primaryEvidence`, `secondaryEvidence`, `detail`, `control`, `peer`, `state`, `feedback`, `status`, `kpiStrip`, `exactValuePath`, `microGroup`.
- `displayTheme`: `detail-table`, `summary-stat`, `business-dashboard`, `exploratory-analysis`, `management-report`, `monitoring-alert`.
- `patternRole`: `primary-structure`, `supporting-evidence`, `interaction`, `state`, `export`, `governance`, `acceptance-only`.
- `visualSourceRole`: `temporary-evidence`, `exact-restoration-source`, `visual-regression-baseline`, `runtime-asset`, `audit-evidence`, `reusable-inspiration`.
- `styleGeneralizationStatus`: `covered-by-existing-pattern`, `covered-by-composed-patterns`, `requires-pattern-extension`, `out-of-scope-one-off`.

Do not create near-synonyms such as `trendLine`, `line-chart`, `metricCard`, or `dataTable` in contract fields. Put display labels in titles, not enum fields.

## Naming Rules

- Component IDs: lowerCamelCase, semantic and stable, such as `attritionTrend`, `riskEmployeeTable`, `revenueGapWaterfall`.
- Parent block IDs: lowerCamelCase ending with `Block`, such as `attritionOverviewBlock` or `riskEvidenceBlock`.
- Sub-block IDs: lowerCamelCase ending with `SubBlock`, such as `trendChartSubBlock` or `topRiskListSubBlock`.
- Dataset IDs: lower_snake_case with prefixes: `dim_`, `fact_`, `agg_`, `ref_`, `log_`.
- Filter IDs: lowerCamelCase and scope-oriented, such as `period`, `orgId`, `jobFamily`, `severity`, `ownerId`.
- Perspective IDs: lowerCamelCase and view-oriented, such as `businessDomain`, `reportTheme`, `managementObject`, or `analysisPerspective`. Do not reuse ordinary filter IDs for first-level perspective switching.
- Action event names: lowerCamelCase plus event type, such as `barClick`, `rowClick`, `stageClick`, `taskSubmit`.
- Modal IDs and drawer IDs: lowerCamelCase ending with `Modal` or `Drawer`.
- Field names in mock datasets: lower_snake_case unless the existing project already uses camelCase.
- Display labels may be Chinese; IDs and field names should stay ASCII.
- Source pattern IDs: `<displayTheme>-NN`, such as `detail-table-01`, `summary-stat-05`, or `monitoring-alert-12`.

When revising an existing mapping, preserve IDs unless the component's semantic role changes. Add new components instead of renaming existing ones.

## Quantity Bounds

Use these default bounds to reduce random output drift.

- First viewport: 3-7 meaningful components.
- Full report page: 6-14 components unless the user asks for a dense suite.
- Must-have components: 3-8.
- Main filter surface: 3-6 global/page filters. In bundled templates this is `filters[]` plus native trigger/panel/popover/drawer, not a visual toolbar.
- Advanced filters: 0-12 filters.
- KPI strip: 3-8 cards.
- Top/Bottom lists: default Top 5 or Top 10; state which one.
- Detail table: 5-8 visible columns by default, 8-12 only in large blocks, with row drawer/export/column settings for full fields.
- Mock time coverage: 12-13 months for monthly trend, 30 days for daily rolling view, selected + previous period for MoM, selected + prior-year comparable period for YoY.

If more components are needed, group them into tabs, drawers, secondary sections, or follow-up pages rather than flattening them into one screen.

## Deterministic Selection Order

Before choosing components, choose the stable `analysisPerspective` from `00-analysis-perspective-card-taxonomy.md`:

1. Use `currentStatus` for "当前怎么样/是否正常/健康度/评分".
2. Use `targetProgress` for "目标达成/进度/差距/里程碑".
3. Use `trendMovement` for "过去怎么变/未来可能怎么走/波动/预测".
4. Use `comparisonDifference` for "谁更高更低/差异/标杆/竞品".
5. Use `rankingContribution` for "Top N/Bottom N/谁贡献最大/主要来自谁".
6. Use `compositionShare` for "占比/结构/构成/份额".
7. Use `decompositionDriver` or `causeDiagnosis` for "由什么组成/为什么变化/归因/贡献". Use `decompositionDriver` when structure is primary; use `causeDiagnosis` when explanation is primary.
8. Use `distributionSpread` for "集中在哪/是否分散/区间/离散/箱线".
9. Use `anomalyRisk` for "哪里不正常/预警/风险/离群/波动异常".
10. Use `relationshipInfluence` for "A 和 B 有没有关系/谁影响谁/关联网络". Then choose `relationshipAnalysisCardPattern`: hub card for one selected subject, matrix card for pairwise strength/correlation, graph card for node-edge networks or communities, Sankey only for directed source-target-value flow, tree only for parent-child relation, scatter/bubble for two numeric variables, trend for relationship over time, factor ranking for ordered relationship strength, and table for exact pair audit. Do not claim influence/causality unless method evidence exists.
11. Use `flowTransfer`, `processBottleneck`, or `conversionRetention` only when the data has directed links, ordered stages, or a shared conversion cohort. If not, route to comparison, ranking, composition, or detail.
12. Use `spatialDistribution` only when geography itself is the decision dimension; organization/区域 labels without geography route to ranking/comparison.
13. Use `timePattern` when day/hour/week seasonality or peak-valley pattern is the question, not merely a time trend.
14. Use `multiDimensionalProfile` for one object's multi-metric feature profile; use `populationObject` when the object/person/customer group comparison is primary.
15. Use `matrixDecision` when the output needs quadrant, priority, strategy tier, or two-axis decision placement.
16. Use `marketMovement` only for OHLC/price/index/market movement tasks; otherwise use ordinary trend/comparison.
17. Use `definitionHelp`, `conclusionInsight`, `actionRecommendation`, `reviewImpact`, `dataQualityTrust`, `detailEvidence`, and `filterExploration` as evidence/trust/action/exploration perspectives; they often appear as secondary perspectives supporting a primary analytical perspective.

When several components are plausible, choose in this order:

1. KPI/status card for current judgment.
2. Target/variance card or bullet/progress when target exists.
3. Gauge only when one bounded status/progress metric needs range and threshold judgment.
4. Combo chart only when scale + rate/trend/target must be read together on one shared category/time axis.
5. Trend chart when time movement matters or period filters exist.
6. Structure/ranking chart when the user must locate objects.
7. Process/funnel only when ordered stages, shared population/cohort logic, and conversion/drop formulas exist.
8. Decomposition/waterfall only when cause or additive contribution exists.
9. Detail table/drawer when exact records or evidence matter.
10. Task/action block when closure or responsibility matters.
11. Data-trust block when sources, versions, or differences matter.

If two components answer the same atom, keep the one earlier in this order unless the later one provides necessary evidence or action.

For screenshot/sample-derived style generation, first run the shared style generalization target from `$report-component-style-design` `references/00a-style-generalization-goal.md`:

1. Choose `covered-by-existing-pattern` when one controlled pattern field matches the business task, data shape, and component family.
2. Choose `covered-by-composed-patterns` when the desired design is a valid composition, such as KPI headline + chart card + local filter + bottom evidence strip, and every child pattern remains valid.
3. Choose `requires-pattern-extension` when the sample is reusable but no controlled field or safe composition covers the business/data trigger.
4. Choose `out-of-scope-one-off` only when the visual is audit evidence, exact restoration, runtime asset, or a non-reusable project exception.

Preserve the selected status, `canonicalPatternRef`, and `patternFields` across runs unless the business question, data shape, template capability, or user instruction changes.

For conclusion/evidence/action cards, keep `componentType: text-summary`, `visualType: text-summary`, set `analysisInsightContract.subtype: conclusion-card`, and choose `conclusionCardPattern` from `$report-component-style-design` `references/03a-conclusion-evidence-action-cards.md`:

1. `metric-evidence-conclusion` when the card is a standalone executive conclusion with visible KPI evidence, findings, and actions.
2. `finding-action-conclusion` when KPI/chart/table evidence already exists nearby and the card should focus on interpretation and next steps.
3. `compact-conclusion-summary` when the card is constrained and can show only a conclusion plus one evidence/action line.

For KPI cards, choose the stable `kpiCardPattern` from `$report-component-style-design` `references/04a-kpi-card-patterns.md`:

1. When one card judges status, health, score, rating, risk, progress, or gauge state, set `kpiJudgmentCardPattern` before treating it as an ordinary KPI. Use `semantic-status-icon-card` for categorical states, `progress-status-ring-card` for completion/progress, `health-score-ring-card` for bounded health scores, `health-threshold-bullet-card` for multi-band thresholds, `health-dimension-breakdown-card` for dimension health, `rating-score-summary-card` for score/level summaries, `rating-distribution-card` for rating buckets, and `semicircle-gauge-target-card` for bounded gauge targets. Require `W >= 360px`, `H >= 240px`, status/range/threshold semantics, exactly one hero visual, comparison strip fields, and footer evidence.
2. When one card manages target attainment, target gap, plan-vs-actual progress, remaining work, deadline, or milestone state, set `kpiGoalExecutionCardPattern` before treating it as an ordinary gauge, progress bar, timeline, or target/actual chart. Use attainment patterns for "达成率/超额达成", gap patterns for "差距/缺口/落后/超支", progress patterns for "计划进度 vs 实际进度", and milestone patterns for "阶段/节点/倒计时/里程碑". Require `W >= 360px`, `H >= 240px`, `kpiEvidenceBinding.goalExecution`, actual/target fields, formula/denominator behavior, one execution hero visual, comparison strip fields, and footer evidence.
3. When one card answers trend movement, named-baseline change, YoY/MoM comparison, cycle/period state, volatility/stability, or forecast uncertainty, set `kpiTimeSeriesCardPattern` before treating the line, bar, ring, or forecast band as an ordinary mini chart. Use trend patterns for "趋势/走势", change patterns for "变化/较上期", YoY/MoM patterns for "同比/环比", cycle patterns for "周期/第几周/阶段", volatility patterns for "波动/稳定", and forecast patterns for "预测/置信区间". Require `W >= 360px`, `H >= 240px`, `kpiEvidenceBinding.timeSeries`, ordered x/y fields, grain, latest period, direction semantics, footer evidence, and the selected pattern's baseline/cycle/volatility/forecast fields.
4. When one card answers direct value comparison, group/segment comparison, competitor position, benchmark distance, or variance/gap diagnosis, set `kpiComparisonAnalysisCardPattern` before treating bars, radar, donut, table, map, or VS panes as ordinary chart variety. Use `direct-value-compare-card` for two-period/two-object value comparison, `group-segment-compare-card` for segments/groups/categories, `competitor-position-card` for competitor/peer/industry comparisons, `benchmark-position-card` for P50/P75/P90/industry-standard/best-practice positioning, and `variance-gap-card` for actual-vs-reference gaps. Require `W >= 360px`, `H >= 240px`, `kpiEvidenceBinding.comparisonAnalysis`, shared metric/unit/grain/filter scope, comparable subject roles, direction semantics, selected evidence mode, sort/visible-limit rules, footer evidence, and exact values.
5. For a wide domain/topic card with `2-5` visible metrics, one local control group, and at most one compact evidence visual, set `kpiOverviewCardPattern` before considering single-indicator layout. Use `lead-metric-comparison-sparkline-overview` when one lead metric anchors comparison, target, and sparkline evidence; use `multi-metric-strip-progress-overview` when `3-5` sibling metrics have equal weight; use `domain-metric-cluster-progress-overview` when one lead metric has `2-3` companion metrics and one target/progress summary. Require `W >= 720px`, `H >= 220px`, and `kpiEvidenceBinding.overview`.
6. For landscape, wide, or row-based KPI cards with `W >= 360px`, choose a horizontal pattern first when the evidence can fit inside one KPI card.
7. When the design is a peer grid of one-metric cards with a local period/unit/grain/scale control, compact evidence visual, and target/progress footer, set `kpiSingleIndicatorLayoutMode` after choosing the closest `kpiCardPattern`. Use `dropdown-sparkline-progress` for period dropdown + sparkline, `unit-toggle-ring-progress` for unit/rate toggle + ring, `dropdown-minibar-progress` for period dropdown + mini bars, `grain-switch-minibar-progress` for grain switch + mini bars, `dropdown-area-sparkline-progress` for period dropdown + soft area sparkline, `scale-toggle-area-progress` for value-scale switch + area sparkline, and `dropdown-gauge-progress` for period dropdown + semi-gauge. Require `W >= 360px`, `H >= 220px`, exactly one evidence visual, and target/attainment fields when the footer is visible.
8. Use `horizontal-axis-line-trend` only when the KPI card needs a readable line body with axes, gridlines, target/reference lines, threshold bands, phase annotations, local grain switching, or dual-series comparison and the candidate size can satisfy `W >= 420px`, `H >= 260px`, chart body `>=180px`, and plot height `>=130px`. Set `kpiAxisLineEvidenceMode` according to the evidence: basic comparison, filled baseline, target reference, phase annotation, unit axis, grain switch, dual comparison, or threshold band.
9. Use `horizontal-axis-bar-compare` only when the KPI card needs readable horizontal bars for ranked/time/category comparison, target/reference lines, threshold warning, local grain switching, dual-series comparison, or category change-rate evidence and the candidate size can satisfy `W >= 420px`, `H >= 260px`, chart body `>=180px`, plot height `>=140px`, row height `>=22px`, and visible bars `<=8`. Set `kpiAxisBarEvidenceMode` according to the evidence: basic bar, period comparison, target reference, category change sidebar, time-series bar, grain switch, dual series, or threshold warning.
10. Use `horizontal-axis-scatter-diagnostic` only when the KPI card needs relationship, distribution, outlier, threshold, target-crosshair, quadrant, or category-zone diagnosis with two numeric fields and object grain, and the candidate size can satisfy `W >= 420px`, `H >= 300px`, chart body `>=200px`, plot height `>=160px`, and managed point density. Set `kpiScatterEvidenceMode` according to the evidence: correlation trendline, mean reference, target crosshair, distribution/change band, threshold quadrant, dual series, change callout, or category quadrant.
11. Use `horizontal-spatial-map-diagnostic` only when geography is the decision dimension and the candidate size can satisfy `W >= 460px`, `H >= 320px`, map body `>=220px`, map viewport shorter side `>=180px`, map resource/projection, and visualMap/legend budget. Set `kpiMapEvidenceMode` according to the evidence: choropleth heat, graded choropleth, bubble target gap, distribution/change marker, column symbol, annotation interval, YoY change zone, or point category summary.
12. Use `paired-comparison-diagnostic` only when two panes compare the same metric definition, unit, grain, period/filter scope, and baseline logic, and the candidate size can satisfy `W >= 420px`, `H >= 260px`, pane width `>=140px`, `VS` rail `32-44px`, and bottom conclusion band `>=36px`. Set `kpiComparisonEvidenceMode` according to the evidence: metric YoY, progress MoM, target gap, improvement dot matrix, trend YoY, structure breakdown, percentage ring, or trend MoM.
13. Use `horizontal-trend-compare` when current value plus prior/baseline comparison and a compact sparkline-like trend are the job and axes/thresholds are not needed.
14. Use `horizontal-ring-progress` when one bounded status/progress metric such as OEE, utilization, SLA, or completion is best read through a ring or semi-gauge.
15. Use `horizontal-target-progress` when target attainment and distance to target are best read through a linear track.
16. Use `horizontal-status-trend-compare` for business-negative metrics such as defect, complaint, overdue, risk, cost, or failure where lower-is-better semantics are declared.
17. Use `horizontal-grain-bar-switch` when one local time-grain switch and mini bars are required.
18. Use `horizontal-period-summary-strip` when current, previous, and target values are the complete evidence and a chart would be unnecessary.
19. Use `horizontal-pp-assist-info` when the visible delta is percentage points (`currentRate - baselineRate`), not percent growth.
20. Use `horizontal-warning-status-band` when the KPI has a threshold warning, status badge, and warning reason/action path.
21. Use `target-wave` when target attainment or bounded progress is the main judgment and target data exists but the card is portrait or narrow.
22. Use `highlight-line-trend` when one KPI is the lead card and trend movement is part of the first-viewport answer.
23. Use `mini-bar-trend` when recent period volatility is supporting evidence inside a peer KPI card.
24. Use `plain-metric` when the card only needs current value, comparison, and compact status.

For target/actual comparison cards, keep `visualType: bar`, set `chartSubtype: target-actual-comparison`, and choose `targetActualCardPattern` from `$report-component-style-design` `references/04b-target-actual-comparison-cards.md`:

1. `emphasis-header-summary` when one comparison card is the lead first-read object.
2. `standard-summary-panel` when enterprise audit clarity or bottom reconciliation is most important.
3. `soft-chip-summary` when the card is secondary, mobile-friendly, or intentionally softer.

For target/actual trend cards, keep `visualType: line`, set `chartSubtype: target-actual-trend`, and choose `targetActualTrendCardPattern` from `$report-component-style-design` `references/04c-target-actual-trend-cards.md`:

1. `emphasis-wave-trend` when one trend card is the lead first-read object and brand emphasis is allowed.
2. `standard-summary-trend` when enterprise audit clarity, target reconciliation, or dense dashboard rhythm is most important.
3. `soft-chip-trend` when the card is secondary, mobile-friendly, or intentionally softer.

For target/actual radar cards, keep `visualType: radar`, set `chartSubtype: target-actual-radar`, and choose `targetActualRadarCardPattern` from `$report-component-style-design` `references/04d-target-actual-radar-cards.md`:

1. `emphasis-wave-radar` when one radar card is the lead first-read object and brand emphasis is allowed.
2. `standard-action-radar` when enterprise audit clarity, detail action, or multi-card consistency is more important.

For target/actual donut cards, keep `visualType: pie`, set `chartSubtype: target-actual-donut`, and choose `targetActualDonutCardPattern` from `$report-component-style-design` `references/04e-target-actual-donut-cards.md`:

1. `emphasis-filter-donut` when one composition card is the lead first-read object and brand emphasis is allowed.
2. `standard-filter-donut` when enterprise audit clarity, local period switching, or multi-card consistency is more important.

For target/actual scatter cards, keep `visualType: scatter`, set `chartSubtype: target-actual-scatter`, and choose `targetActualScatterCardPattern` from `$report-component-style-design` `references/04f-target-actual-scatter-cards.md`:

1. `emphasis-filter-scatter` when one relationship/distribution card is the lead first-read object and brand emphasis is allowed.
2. `standard-filter-scatter` when enterprise audit clarity, local period switching, or multi-card consistency is more important.

For target/actual detail table cards, keep `componentType: table`, `visualType: table`, set `tableSubtype: target-actual-detail`, and choose `targetActualTablePattern` from `$report-component-style-design` `references/06a-target-actual-detail-tables.md`:

1. `standard-audit-table` when exact ranked row evidence, target reconciliation, total row, export, or audit clarity is the main task.
2. `compact-audit-table` when the card is narrow, mobile, embedded, or only a Top N evidence preview.

For target/actual pivot table cards, keep `componentType: table`, `visualType: pivot`, set `tableSubtype: target-actual-pivot`, and choose `targetActualPivotTablePattern` from `$report-component-style-design` `references/06b-target-actual-pivot-tables.md`:

1. `standard-hierarchy-pivot` when a clean two-dimension target/actual pivot with subtotals and grand total is the main task.
2. `share-matrix-pivot` when amount plus share/contribution columns are required under comparison, actual, or target groups.
3. `tree-expand-pivot` when compact row hierarchy, expand/collapse, or many row groups are required.

For reusable table card patterns, keep `componentType: table`, keep `visualType` as `table` or `pivot`, and choose `tableCardPattern` from `$report-component-style-design` `references/06c-table-card-patterns.md`:

1. `plain-detail-ledger-table` when row-level audit, order ledger, customer list, transaction list, or exact detail evidence is primary.
2. `filtered-operational-status-table` when local filters, status badges, row detail, export, or operational scanning are primary.
3. `grouped-header-summary-table` when fields naturally group by metric family, period, actual/target, amount/share, or business domain.
4. `metric-matrix-table` when indicator families, target/actual/score/weight, or multidimensional metrics need matrix comparison.
5. `s2-cross-pivot-table` when row dimension by column dimension aggregate summaries need S2-class pivot behavior.
6. `fixed-column-scroll-table` when a wide schedule, progress, or period table requires frozen key columns and horizontal scroll.
7. `grouped-subtotal-summary-table` when grouped rows, subtotals, and grand-total reconciliation are primary.
8. `tree-hierarchy-table` when parent-child rows, expandable hierarchy, and row-level metrics are primary.

For ranking, leaderboard, and Top N cards, keep `componentType: card`, `visualType: ranking-list`, choose `rankingCardPattern` from `$report-component-style-design` `references/07a-top-ranking-cards.md`, and declare `rankingEvidenceBinding`:

1. `basic-rank-list-card` for the cleanest Top 5 rows with rank, object, secondary label, and value.
2. `trend-delta-rank-list-card` or `topn-sparkline-rank-list-card` when ranking movement or per-row trend proof is visible.
3. `progress-bar-rank-list-card` or legacy `bar-progress-ranking` when value gaps should be read through shared bar tracks.
4. `podium-rank-card` or legacy `medal-horizontal-ranking` when a broad card should stage top winners.
5. `yoy-microbar-rank-list-card` when row-level micro bars and YoY/MoM deltas are the evidence.
6. `radar-comparison-rank-card` when ranking is based on multi-dimensional score/profile comparison.
7. `metric-summary-rank-card` when 2-3 summary metrics must sit above the rank list.
8. `time-switch-rank-card` when the card owns a local day/week/month/period switch.
9. `share-donut-rank-card` when Top N share/concentration is visible through a donut plus list.
10. `map-distribution-rank-card` when geography itself is the ranked object and map evidence is needed.
11. `topn-bar-rank-card`, `topn-comparison-rank-card`, `topn-waterfall-strip-card`, `topn-bubble-rank-card`, or `topn-icon-card-grid` for compact Top N cards in a grid where bars, comparison columns, contribution strips, bubbles, or icon/entity cards are the primary evidence.
12. `compact-list-ranking` remains a legacy/narrow fallback when only rank, object, and value can fit.

For Pareto cards, keep `componentType: card`, `visualType: ranking-list`, choose `paretoCardPattern`, and declare `paretoEvidenceBinding`:

1. `pareto-basic-card` for sorted bars + cumulative line + threshold.
2. `pareto-table-chart-card` when a small exact rank table must sit with the Pareto chart.
3. `pareto-dual-axis-card` when value and cumulative share both need axes.
4. `pareto-cumulative-fill-card` when cumulative contribution region is emphasized.
5. `pareto-stacked-share-card` when single-item share and cumulative share should be compared together.
6. `pareto-bubble-card` when key factors should read as scale objects plus cumulative progression.
7. `pareto-zone-card` when key vs secondary factors need colored threshold zones.
8. `pareto-ring-list-card` when a compact summary ring plus ranked factor list is enough.

For composition, share, structure, and market-share cards, keep `componentType: card`, `visualType: composition-card`, choose `compositionShareCardPattern`, and declare `compositionShareEvidenceBinding`:

1. `basic-donut-share-card` or `donut-detail-share-card` when 2-6 categories need one denominator, a center total, and exact side or tooltip values.
2. `percent-bar-share-card` when close percentages must be compared precisely.
3. `multi-ring-hierarchy-share-card`, `sunburst-structure-card`, or `treemap-composition-card` when parent-child structure and share are both decision evidence.
4. `share-trend-stack-card`, `stacked-strip-composition-card`, or `stacked-column-trend-composition-card` when share movement across time or groups is primary and each bucket reconciles to 100%.
5. `share-ranking-topn-card` when the largest shares and their rank order are the primary task; combine with `rankingEvidenceBinding` only when row order itself is a ranking decision.
6. `funnel-composition-card` only when categories have a natural ordered level or stage-like structure but no cohort conversion logic; use conversion funnel contracts for true stage conversion.
7. `bubble-composition-card` when approximate share magnitude and grouping are more important than exact rank.
8. `market-share-overview-card`, `market-share-concentration-card`, or `share-distribution-interval-card` when external market denominator, CR metrics, or share buckets are primary.
9. `map-structure-card` only when geography is the structure dimension with region codes or coordinates.
10. `share-metrics-summary-card` when one share visual must be paired with total amount/count/average strips under the same denominator.

For decomposition, attribution, contribution, and hierarchy cards, keep `componentType: card`, `visualType: decomposition-card`, choose `decompositionAttributionCardPattern`, and declare `decompositionAttributionEvidenceBinding`:

1. Use `formula-decomposition-card` when the visible explanation is a formula and all factors/operators reconcile to the root.
2. Use `funnel-decomposition-card` when ordered stages explain the root but the primary question is metric structure rather than cohort conversion.
3. Use `tree-decomposition-card` or `multilevel-metric-decomposition-card` when parent-child metric nodes explain the root; choose multilevel when `3+` levels must remain visible.
4. Use `sankey-decomposition-card` or `path-contribution-card` when source-target-value links or named paths explain where the root value flows.
5. Use `driver-factor-decomposition-card` when drivers explain growth/change but the math is not a signed additive bridge.
6. Use `variance-waterfall-decomposition-card`, `contribution-waterfall-card`, or `time-attribution-waterfall-card` when signed additive values bridge baseline to current/target by factor or period.
7. Use `combined-decomposition-card` when one compact card needs root metric plus `2-3` bounded explanation visuals and every child stays above its minimum.
8. Use `total-attribution-card` only when an attribution method is declared; otherwise use contribution or driver wording.
9. Use `channel-attribution-donut-card`, `touchpoint-attribution-list-card`, `segment-attribution-card`, or `feature-attribution-bar-card` according to the primary attribution dimension.
10. Use `multidimensional-attribution-matrix-card` when two dimensions cross to explain the result and the visible matrix is bounded.
11. Use `overall-contribution-card`, `contribution-structure-card`, `contribution-comparison-card`, `contribution-trend-card`, `contribution-tree-card`, `key-contribution-topn-card`, or `contribution-heatmap-card` according to whether the main reading task is summary, structure, comparison, movement, hierarchy, top factors, or dense time/dimension cells.
12. Use `progressive-hierarchy-decomposition-card`, `hierarchy-tree-decomposition-card`, `hierarchy-waterfall-card`, `indented-hierarchy-table-card`, `hierarchy-share-card`, `multilevel-comparison-hierarchy-card`, or `target-attainment-hierarchy-attribution-card` according to whether the hierarchy is step rollup, tree structure, signed level change, dense rows, share by level, current-vs-baseline comparison, or target-gap attribution.

For distribution, interval, density, quantile, and boxplot cards, keep `componentType: card`, `visualType: distribution-card`, choose `distributionAnalysisCardPattern`, and declare `distributionAnalysisEvidenceBinding`:

1. Use `numeric-histogram-distribution-card` or `interval-histogram-card` when bounded interval counts are primary and each bucket has lower/upper bounds, count, share, and sort order.
2. Use `interval-donut-distribution-card` or `interval-share-donut-card` when interval composition is primary and the denominator reconciles to the sample count.
3. Use `percentile-cdf-distribution-card`, `cumulative-interval-card`, or `quantile-band-density-card` when percentile position, P25/P50/P75/P90, or cumulative coverage is the decision evidence.
4. Use `univariate-density-curve-card`, `interval-density-curve-card`, `grouped-density-comparison-card`, `density-heatmap-card`, `kde-cumulative-density-card`, `bivariate-density-hexbin-card`, or `density-overview-card` only when the density estimator or precomputed density field, sample count, and smoothing/binning policy are declared.
5. Use `boxplot-kpi-summary-card`, `time-series-boxplot-card`, `grouped-boxplot-comparison-card`, `boxplot-overview-card`, `boxplot-side-summary-card`, `weekday-boxplot-card`, `anomaly-boxplot-card`, or `boxplot-detail-table-card` only when Q1, median, Q3, whisker min/max, sample count, and outlier/whisker rule are declared.
6. Use `geographic-distribution-card` only when geography fields or a map resource exist; otherwise route to interval/ranking/table.
7. Use `time-distribution-card` or `calendar-heatmap-distribution-card` when the distribution is over hour/day/week and missing cells versus zero cells are explicitly different.
8. Use `distribution-comparison-card` when groups or periods share the same bucket/statistic definition and comparable sample counts are visible or available through tooltip.
9. Use `multidimensional-population-distribution-card` when two population sides or dimensions share aligned intervals and the visual answers "who is concentrated where".
10. Use `interval-detail-table-card` or `boxplot-detail-table-card` when exact audit of buckets/statistics is primary or when the chart body cannot fit without hiding statistical proof.

For anomaly, risk, warning, and outlier analysis cards, keep `componentType: card`, `visualType: anomaly-card`, choose `anomalyAnalysisCardPattern`, and declare `anomalyAnalysisEvidenceBinding`:

1. Use `anomaly-overview-card` when current abnormal/risk/warning state, severity, value, comparison, and freshness are the first-read answer.
2. Use `anomaly-trend-compare-card` or `anomaly-baseline-compare-card` when time movement or current-vs-baseline proof is the diagnostic lens.
3. Use `anomaly-distribution-structure-card`, `warning-progress-donut-card`, or `anomaly-interval-threshold-card` when severity/share, status progress, interval, or threshold bands are primary.
4. Use `anomaly-timeline-card`, `anomaly-ranking-top-card`, or `anomaly-summary-table-card` when ordered events, Top affected objects, or compact row evidence is primary.
5. Use `anomaly-multi-metric-monitor-card` when a bounded set of metrics share one warning context and every visible metric has threshold/status fields.
6. Use `risk-matrix-card` when likelihood and impact cross to form the decision; use `risk-response-status-card` when processing closure, owner, SLA, or unresolved count is primary.
7. Use `anomaly-impact-assessment-card` when affected users/orders/services, loss, duration, or impact score is the answer.
8. Use `anomaly-relation-influence-card`, `anomaly-geographic-distribution-card`, or `outlier-scatter-card` only when relation, geography, or outlier point fields are present and density/fallback rules are declared.

For basic chart cards, keep `componentType: chart`, keep `visualType` as the real chart family, and choose `basicChartCardPattern` from `$report-component-style-design` `references/05d-basic-chart-card-patterns.md`:

1. `single-series-bar-card` when one metric compares a small set of categories.
2. `comparison-line-trend-card` when two or more comparable series share one time grain.
3. `area-trend-card` when one continuous volume trend should read as movement over time.
4. `bar-line-combo-card` when one scale metric and one related count/rate need the same x-axis.
5. `pie-composition-card` when part-to-whole composition is small and no center total is needed.
6. `donut-composition-card` when composition needs a center total or selected summary.
7. `stacked-bar-composition-card` when category totals and segment composition must be read together.
8. `multi-metric-combo-card` when two scale metrics and one rate/efficiency metric share a time/category axis.
9. `filtered-bar-card` when a simple bar comparison owns a compact local period/range selector.
10. `tooltip-line-trend-card` when dense daily/rolling trend values should be inspected through tooltip focus.

For specialized chart cards, keep `componentType: chart`, keep `visualType` as the real chart family, and choose `specializedChartCardPattern` from `$report-component-style-design` `references/05e-specialized-chart-card-patterns.md`:

1. `gauge-progress-card` when one bounded progress, completion, or status metric needs range and target judgment.
2. `choropleth-ranking-map-card` when geography is the decision dimension and a side ranking helps exact Top regions.
3. `time-heatmap-card` when two ordered dimensions, usually time by time or category by time, need hotspot pattern reading.
4. `candlestick-volume-card` when OHLC plus volume and moving-average context are primary.
5. `boxplot-distribution-card` when distribution, median, IQR, spread, or outliers across categories are primary.
6. `parallel-profile-card` when `3+` metrics describe object profiles and users need similarity, anomaly, or multi-factor screening.
7. `bubble-opportunity-card` when x/y relationship plus non-negative size metric is the primary opportunity or portfolio question.

For flow/hierarchy diagram cards, keep `componentType: chart`, keep `visualType` as the real diagram family, and choose `flowHierarchyDiagramCardPattern` from `$report-component-style-design` `references/09a-flow-hierarchy-diagram-card-patterns.md`:

1. `conversion-funnel-card` when ordered stages, shared population/cohort, conversion, drop, or retention are primary.
2. `multi-stage-sankey-card` when source-target-value links distribute across multiple stages or outcomes.
3. `journey-stage-map-card` when a staged user/business journey needs goals, behaviors, touchpoints, emotions, and opportunities.
4. `hierarchy-tree-card` when parent-child structure, organization, category, ownership, lineage, or decomposition is primary.
5. `hub-relation-network-card` when one central object and surrounding relationship clusters are primary.
6. `sunburst-composition-card` when hierarchy path plus composition share should be read through radial rings.
7. `treemap-composition-card` when hierarchy contribution and relative area comparison are primary.
8. `path-conversion-flow-card` when start-to-end branches, edge ratios, and terminal success/loss outcomes are primary.

For operational lists, keep `visualType: operational-list` and choose `listStatusPattern` from `$report-component-style-design` `references/07b-operational-list-status-patterns.md`:

1. `simple-info-list` when ordinary records need title/name, owner, status, update time, and a trailing action.
2. `progress-task-list` when task closure, owner/deadline, status, and completion percent are the main evidence.
3. `severity-alert-list` when alert severity, threshold/current value, and occurrence time are primary.
4. `exception-record-list` when failures or incidents need error code, occurrence time, and handling state.
5. `status-chip-set` when the component is a reusable status tag set rather than record rows.
6. `event-timeline` when ordered workflow, event, approval, release, or operation history is primary.
7. `user-object-list` when people, members, owners, customers, or contacts require avatar/identity and availability status.
8. `mixed-info-list` when work items combine title, subtitle, status, priority, owner, and update time but do not require a full table.

For visible filter controls, choose `filterControlPattern` from `$report-filter-control-design-spec` `references/02-filter-selector-patterns.md`:

1. `single-select-dropdown` for ordinary one-value dimensions with small or medium option sets.
2. `multi-tag-select` when selected multiple values should remain visible as removable tags.
3. `date-range-selector` when the control selects an exact period or shortcut period.
4. `searchable-select` when option volume is large or keyword lookup is expected.
5. `tree-path-selector` when organization, region, category, or product hierarchy must stay visible.
6. `advanced-filter-drawer` when multiple low-frequency or expensive conditions should be grouped behind one trigger.
7. `combined-filter-chipbar` when the surface should summarize active filters and open the full filter set on click.

For reusable overlays, keep `visualType: overlay-panel` and choose `overlayPanelPattern` from `$report-component-style-design` `references/08a-overlay-drawer-modal-patterns.md`:

1. `right-filter-drawer` when multiple table/report filters need a right-side configuration surface.
2. `bottom-action-sheet` when a small operation menu should slide from the bottom.
3. `center-confirmation-modal` when a focused confirmation, especially destructive or irreversible, is required.
4. `fullscreen-detail-modal` when a full object record needs tabs, grouped fields, and sticky actions.
5. `top-notification-bar` when a success/warning/info message should appear without blocking work.
6. `left-navigation-drawer` when temporary module navigation should preserve page context.
7. `side-detail-drawer` when a selected row/card needs compact detail while the source list stays visible.
8. `large-detail-side-panel` when analytical detail requires KPI, tabs, chart/table evidence, and a wide side panel.

For Micro Dashboard Cards, keep `componentType: custom`, set `visualType: micro-dashboard`, and choose `microDashboardCardPattern` from `$report-component-style-design` `references/12f6-placement-micro-dashboard-card.md`:

1. `sales-fresh-analysis-board` when sales, revenue, orders, target attainment, channel mix, region ranking, and Top object detail are the shared topic.
2. `user-operations-purple-board` when user acquisition, active users, retention, conversion, funnel, heatmap, and product-operation signals are the shared topic.
3. `supply-chain-orange-monitoring-board` when procurement, supplier delivery, inventory, logistics, warnings, shortages, or exceptions are the shared topic.
4. `finance-blue-analysis-board` when revenue, profit, cost, expense, cash, accounts, or reconciliation is the shared topic.

Use `micro-dashboard` only when the parent can meet `680x620` minimum and every visible child meets its declared minimum. Otherwise choose a normal `composite-panel`, split blocks, tabs, drawer, or fullscreen.

For state feedback components, keep `componentType: custom`, set `visualType: state-feedback`, and choose `stateFeedbackPattern` from `$report-component-style-design` `references/13-state-feedback-patterns.md`:

1. `fresh-line-state-set` for default professional report states.
2. `minimal-line-state-set` for dense admin, audit, or low-distraction states.
3. `business-blue-state-set` for enterprise portal and management-app defaults.
4. `soft-illustration-state-set` for guided self-service or friendly product states.
5. `glass-card-state-set` for card-based state galleries or template-library displays.
6. `dark-tech-state-set` only inside a dark monitoring, security, or ops-center template.
7. `playful-healing-state-set` only when brand and risk context allow a playful state.
8. `immersive-fullscreen-state-set` for page-level blocking scenes, not small chart/table states.

## Fallback Rules

- Missing ordered stages, shared population/cohort logic, or conversion/drop formulas: do not use funnel; use structure bar, ranking table, process table, path chart, or Sankey according to the actual question.
- Missing Gauge min/max range, status/threshold rule, or bounded metric semantics: do not use Gauge; use KPI card, progress bar, target card, bar/table, or line chart according to the actual question.
- Missing paired business relationship, shared ordered category/time grain, axis units, or valid series limit: do not use Combo; use separate bar and line charts, target/variance card, trend chart, or table according to the actual question.
- Missing row grain, primary key, default sort, visible column priority, or pagination/search/export scope: do not finalize a Detail Table; use a bounded list/summary card while row evidence is pending, or mark the table contract as a data gap.
- Missing additive contribution: do not use waterfall; use driver table, contribution bar, or narrative explanation.
- Missing geographic meaning: do not use map; use organization bar/matrix.
- Missing stable row IDs: do not create click-through drawer; use tooltip/popover until IDs are defined.
- Missing time coverage: do not expose multi-period filter or trend claim; mark fixed period.
- Missing permission model: include `permission_scope` placeholder and no-permission validation case.
- Missing API contract: produce mock dataset contract and mark data source as mock/resolver candidate.
- Unknown template support: use `other` only with a named custom widget and explicit reason; otherwise choose from known `visualType` values.
- Unknown screenshot/sample style: do not store the image as the durable standard. Try existing controlled patterns, then composed patterns; if neither fits, set `styleGeneralization.generalizationStatus: requires-pattern-extension` and route to the owning component-family reference before implementation. Use `out-of-scope-one-off` only when the surface is explicitly non-reusable or kept for exact restoration/audit/runtime asset purposes.
- Unknown or unsupported conclusion card pattern: keep `componentType: text-summary`, `visualType: text-summary`, use `analysisInsightContract.subtype: conclusion-card`, choose `conclusionCardPattern: compact-conclusion-summary`, and move unsupported KPI evidence, findings, or actions to tooltip/detail.
- Unknown or unsupported KPI card pattern: keep `visualType: metric-card`, use `kpiCardPattern: plain-metric`, set `kpiCardOrientation: portrait` unless a project contract requires a row card, and move unsupported visual evidence to tooltip, drawer, or a full chart block. If the unsupported pattern is a KPI overview card but `kpiOverviewCardPattern` cannot meet `720x220`, `2-5` metrics, one local-control group, one compact evidence visual, or overview binding rules, reduce visible metrics to Top3, hide compact evidence, split into separate KPI cards, or route to Micro Dashboard Card only when the business topic needs multiple child sections. If the unsupported pattern is a KPI goal execution card but `kpiGoalExecutionCardPattern` cannot meet `360x240`, required actual/target/gap/progress/milestone binding, execution hero minimum, comparison strip, or deadline/footer evidence rules, keep the actual/target/remaining values and downgrade to a linear progress summary before splitting to a full chart/table/timeline/detail block. If the unsupported pattern is a KPI time-series card but `kpiTimeSeriesCardPattern` cannot meet `360x240`, ordered series, time evidence floor, footer evidence, or baseline/cycle/volatility/forecast binding rules, keep the current value and most important baseline/change result, downgrade to `horizontal-trend-compare` or a plain metric with tooltip evidence, or split to a full chart/table before using decorative sparklines. If the unsupported pattern is a KPI comparison analysis card but `kpiComparisonAnalysisCardPattern` cannot meet `360x240`, comparable subject roles, shared metric/unit/grain, benchmark/variance fields required by the pattern, evidence minimums, footer evidence, or exact-value rules, keep the comparison conclusion and top `2-3` values, reduce subjects or evidence mode, then split to a full bar/radar/table/map/chart block before squeezing. If the unsupported pattern is a single-indicator KPI grid card but `kpiSingleIndicatorLayoutMode` cannot meet `360x220`, one-evidence-visual, target/footer, or local-control binding rules, keep the value/comparison/target and drop the mini evidence first. If the unsupported pattern is a KPI plus readable axis line but `horizontal-axis-line-trend` cannot meet the `420x260` and chart-body floors, use `horizontal-trend-compare` without axes or split to a full `comparison-line-trend-card`. If the unsupported pattern is a KPI plus readable horizontal bar body but `horizontal-axis-bar-compare` cannot meet the `420x260`, chart-body, row-height, or `<=8` visible-bar floors, use a mini bar KPI without axes or split to a full `single-series-bar-card`, `filtered-bar-card`, target/actual bar card, or table. If the unsupported pattern is a KPI plus readable scatter body but `horizontal-axis-scatter-diagnostic` cannot meet the `420x300`, chart-body, plot-height, or point-density floors, use a simpler KPI plus tooltip/detail or split to a full scatter/table block. If the unsupported pattern is a KPI plus map body but `horizontal-spatial-map-diagnostic` cannot meet the `460x320`, map-body, viewport, or projection floors, use ranking/bar/table or split to a full map block. If the unsupported pattern is a KPI plus two-pane comparison but `paired-comparison-diagnostic` cannot meet pane and conclusion floors, use a single KPI plus delta or split to a full comparison chart/table.
- Unknown or unsupported target/actual card pattern: keep `visualType: bar`, use `chartSubtype: target-actual-comparison`, choose `targetActualCardPattern: standard-summary-panel`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported target/actual trend card pattern: keep `visualType: line`, use `chartSubtype: target-actual-trend`, choose `targetActualTrendCardPattern: standard-summary-trend`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported target/actual radar card pattern: keep `visualType: radar`, use `chartSubtype: target-actual-radar`, choose `targetActualRadarCardPattern: standard-action-radar`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported target/actual donut card pattern: keep `visualType: pie`, use `chartSubtype: target-actual-donut`, choose `targetActualDonutCardPattern: standard-filter-donut`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported target/actual scatter card pattern: keep `visualType: scatter`, use `chartSubtype: target-actual-scatter`, choose `targetActualScatterCardPattern: standard-filter-scatter`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported target/actual table pattern: keep `componentType: table`, `visualType: table`, use `tableSubtype: target-actual-detail`, choose `targetActualTablePattern: standard-audit-table`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported target/actual pivot table pattern: keep `componentType: table`, `visualType: pivot`, use `tableSubtype: target-actual-pivot`, choose `targetActualPivotTablePattern: standard-hierarchy-pivot`, and move decorative variants to project-specific style tokens.
- Unknown or unsupported table card pattern: keep `componentType: table`, keep `visualType` as `table` for row-level records or `pivot` for cross summaries, choose `plain-detail-ledger-table` for ordinary details, `filtered-operational-status-table` for local filter/status workflows, `grouped-header-summary-table` for natural grouped headers, `s2-cross-pivot-table` for cross summaries, or `tree-hierarchy-table` for parent-child rows, and document the fallback.
- Unknown or unsupported ranking card pattern: keep `componentType: card`, `visualType: ranking-list`, choose `rankingCardPattern: basic-rank-list-card` for narrow/embedded usage or `progress-bar-rank-list-card` when width allows value-gap comparison, and move award, map, donut, radar, bubble, or icon decoration to project-specific style tokens unless the corresponding data contract is present.
- Unknown or unsupported Pareto card pattern: keep `componentType: card`, `visualType: ranking-list`, choose `paretoCardPattern: pareto-basic-card` only when additive sorted values, total, cumulative share, threshold, and long-tail policy are available; otherwise downgrade to `progress-bar-rank-list-card` or a table and record why Pareto was rejected.
- Unknown or unsupported composition/share/structure card pattern: keep `componentType: card`, `visualType: composition-card`, choose `basic-donut-share-card` only when category, value, total, share, denominator, and `otherPolicy` are valid. Choose `percent-bar-share-card` for exact close-share comparison; choose `treemap-composition-card` or `sunburst-structure-card` only with parent-child non-negative additive fields; otherwise downgrade to bar/table/ranking and record why the composition card was rejected.
- Unknown or unsupported decomposition/attribution/contribution/hierarchy card pattern: keep `componentType: card`, `visualType: decomposition-card`, choose `overall-contribution-card` when a root metric plus contributor values are valid, `variance-waterfall-decomposition-card` when signed additive deltas reconcile, `tree-decomposition-card` when stable parent-child nodes exist, or `indented-hierarchy-table-card` when exact hierarchy rows are more important than shape. If root metric, formula/node/link/stage/matrix fields, sign rule, attribution method when claimed, or reconciliation policy are missing, downgrade to a detail table, ranking card, or analysis text and record why the decomposition claim was rejected.
- Unknown or unsupported distribution/interval/density/boxplot card pattern: keep `componentType: card`, `visualType: distribution-card`, choose `numeric-histogram-distribution-card` when valid bucket fields exist, `density-overview-card` when valid density fields and estimator policy exist, `boxplot-detail-table-card` when valid boxplot statistics exist but the plot cannot fit, or `interval-detail-table-card` when exact bucket audit is primary. If sample count, metric/unit, bucket/statistic fields, interval/density policy, missing/zero/out-of-range policy, or exact-value route are missing, downgrade to a bar chart, table, KPI, or text explanation and record why the statistical distribution claim was rejected.
- Unknown or unsupported anomaly/risk/warning/outlier card pattern: keep `componentType: card`, `visualType: anomaly-card`, choose `anomaly-overview-card` only when severity/status, current value, baseline or threshold, time/freshness, and detail/action fields exist. Choose `anomaly-summary-table-card` or `anomaly-timeline-card` when exact row or event evidence is primary; choose `risk-response-status-card` when closure state is primary. If severity/status, diagnostic lens, baseline/threshold, time, impact/object, or exact-value/action route is missing, downgrade to KPI, operational list, table, or analysis text and record why the anomaly card was rejected.
- Unknown or unsupported basic chart card pattern: keep `componentType: chart`, keep the real `visualType`, choose `single-series-bar-card` for one-metric category comparison, `comparison-line-trend-card` for multi-series trends, `area-trend-card` for one filled trend, `bar-line-combo-card` for scale-plus-rate pairs, `pie-composition-card` or `donut-composition-card` for small composition, and document the fallback.
- Unknown or unsupported specialized chart card pattern: keep `componentType: chart`, keep the real `visualType`, choose the closest supported specialized pattern only when the data shape satisfies its required fields, otherwise fall back to a basic chart card, KPI card, table, drawer, or fullscreen detail and document why the specialized geometry was rejected.
- Unknown or unsupported flow/hierarchy diagram card pattern: keep `componentType: chart`, keep the real `visualType`, choose the closest supported flow/hierarchy pattern only when the data shape satisfies its required nodes, links, stages, hierarchy, or path fields, otherwise fall back to a basic chart card, table, tree list, detail drawer, or fullscreen-first diagram and document why the diagram geometry was rejected.
- Unknown or unsupported operational list pattern: keep `visualType: operational-list`, choose `simple-info-list` for ordinary records, `progress-task-list` for tasks with progress, `severity-alert-list` for monitoring alerts, `exception-record-list` for incidents/errors, `event-timeline` for ordered events, or `mixed-info-list` for work items with title/status/owner/time; use table fallback when exact audit fields exceed the list budget.
- Unknown or unsupported filter control pattern: keep the filter contract, choose `single-select-dropdown` for one-value dimensions, `combined-filter-chipbar` for summarized active filters, or `advanced-filter-drawer` for multi-condition filters, and document the visual fallback.
- Unknown or unsupported overlay panel pattern: keep `visualType: overlay-panel`, choose `center-confirmation-modal` for focused decisions, `right-filter-drawer` for filter configuration, `side-detail-drawer` for compact row detail, or `large-detail-side-panel` for dense analytical detail, and document the fallback.
- Unknown or unsupported Micro Dashboard Card pattern: use `micro-dashboard` only if one shared topic, child priorities, parent minimum size, and child minimum sizes are proven. If not, choose `composite-panel` for `2-4` related children, tabs for alternate views, split blocks for unrelated children, or fullscreen/drawer for dense detail.
- Unknown or unsupported state feedback pattern: keep `visualType: state-feedback`, choose `fresh-line-state-set` for ordinary report states, `business-blue-state-set` for enterprise defaults, or `minimal-line-state-set` for dense/admin contexts. Do not store screenshots, image paths, or embeddings as the durable state standard.
- Sample/source module visibility: do not mark as `must-have` unless it directly answers the user's stated report question; otherwise preserve as `sampleStructure` or label as `optionalEnhancement`.

## Output Stability Rules

- Always include a binding matrix for `spec-contract` and `prototype-config` modes.
- Preserve upstream `displayTheme` and `sourcePatternIds` in binding rows unless a pattern is explicitly rejected as out of scope.
- Preserve `styleGeneralization` fields for sample-derived reusable components; do not drop them during prototype config generation, API handoff, or frontend implementation.
- Use the same field name for the same concept across datasets, filters, actions, and matrix rows.
- Classify every user control before placement with `controlSemantics`. A control that changes metric names, metric set, component set, table headers, dimensions, metric definition/口径, report subject, or business-domain vocabulary is `perspective-switch`, not a normal filter.
- Every binding matrix row must include `controlSemantics` and `componentSchemaImpact`. Use `row-scope-only` only when the control keeps the same component schema and only narrows rows or values.
- Every perspective-navigation percentage, ranking, or status light must include stable lineage fields: `sourceDataset`, `field/formula`, `grain`, `affectedFilters`, and `periodBehavior`.
- Filter option `meta` must be treated as static/dimensional only. Do not place dynamic KPI values in `filterData.meta` unless the value is explicitly `static-display-copy`.
- For bundled template prototypes, each mock dataset ID must map to a `dashboard.dataset.json` key or to an explicit API/provider resolver. A generated TS data file is not an acceptable mock dataset target.
- Use a controlled `filterExecutionStage` for primary filters and implementation-handoff components. Global/page filters should prefer `sql-where`, `source-query`, `provider-query`, or `repository-query`; component-internal filters may use `component-local`; `blocked` is required when the current design depends on page/API-level full-materialize-then-filter behavior.
- Do not alternate between `org`, `organization`, `orgId`, and `department` for the same scope. Pick one and map aliases explicitly.
- Do not mix Chinese labels into IDs or query params.
- State assumptions in one section; do not hide assumptions inside component titles.
- Every `must-have` component must have a dataset, fields, filters, interaction state, update trigger, and validation case.
- Every component inside a composed parent block must declare `parentBlockId`, `subBlockId`, `subBlockRole`, local sub-block layout, `subBlockInset:5px`, and `subBlockGap:5px`.
- Use `primaryEvidence`/`secondaryEvidence` for Micro Dashboard or Composite Panel chart/table proof areas, `kpiStrip` for KPI strips, `status` for status strips, `exactValuePath` for table/detail/drilldown proof, and `feedback` for empty/loading/error/no-permission/building state sub-blocks. Do not use generic `state` or `microGroup` when one of these specific roles applies.
- Every selected pattern card must map to at least one component/control/data/API/interaction/export/operations/validation row; otherwise mark it `futurePattern` or remove it from the selected set.
- Every primary filter must list affected components.
- Every primary/global filter must state whether it narrows data through SQL/source/provider/repository/resolver/precompute/cache before component construction; every component-internal filter must state the already fetched component dataset it operates on.
- First-level business domain, report theme, management object, subject area, or analysis perspective must map to navigation, route, tab, segment, or an explicit perspective state. Do not encode it only as a template `filters[]` item unless an accepted local project contract proves it is row-scope-only.
- Every clickable component must list event name, payload fields, target action, and stale-state behavior.

## Acceptance Gate

Before finalizing, answer yes to all:

- Can another agent implement the same component IDs and dataset IDs from this output?
- Can another agent trace every selected pattern card to implemented rows or explicit future/gap status?
- Can every first-screen value be traced to a dataset or static policy?
- Can every primary filter be tested against at least one affected component?
- Can every control be classified as perspective switch, global filter, local filter, or drilldown param without hiding schema-changing behavior inside ordinary filters?
- For every non-default perspective, can QA verify changed metric names, titles/summaries, table dimensions or headers, component set, specialty metrics, and口径 where the contract says they should change?
- Can every navigation percentage, ranking, and status light be traced to `sourceDataset`, `field/formula`, `grain`, `affectedFilters`, and `periodBehavior` instead of filter option metadata?
- Can every global/page-level filter be tested without relying on full-materialize-then-filter behavior, and can every component-internal filter be tested against already fetched component data?
- Can every clickable mark or row produce a stable action payload?
- Can the page still behave predictably when filters return empty data or remove a selected object?
- Are unsupported chart choices explicitly ruled out by fallback rules?
- Are all enums from controlled vocabularies or project-defined local types?
