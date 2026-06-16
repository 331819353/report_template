---
name: report-component-style-design
description: "用于报表组件级设计规范、组件规范、视觉样式、响应式和可读性设计/评审/修复。用户提到提高前端设计、前端设计提升、组件设计规范、组件优化、KPI卡/指标卡、横向指标卡/横版KPI/宽指标卡、文本总结、分析洞察、Composite Panel、多组件组合、Micro Dashboard Card/微型看板卡、状态反馈/空态/loading/error/no-permission/building、筛选控件、按钮/标签/弹窗/抽屉、ECharts图表、AntV S2表格、透视表、复杂表头、图例/标签/tooltip、hover/focus动效、图形变形、组件溢出/裁切/对齐、移动端适配、视觉优化时触发；不负责整页布局或模板工程。"
---

# Report Component Style Design

## Core Positioning

Use this skill for one component or one component family: design, critique, repair, or implementation-ready component guidance for report/dashboard/BI/business-analysis surfaces.

When the user provides screenshots or says a style should be "沉淀为 skill", the primary goal is `100% routable coverage` of the provided component-style universe: convert every reusable sample into a text-only, controlled-pattern contract that can be selected, adapted, implemented, and validated by non-multimodal downstream models. Use `references/00a-style-generalization-goal.md` before choosing or extending pattern references.

Keep this `SKILL.md` as the router. Load only the references for the component family that actually appears in the task. For reusable component-system standards, use `$report-component-design-spec`; for chart-only standards use `$report-chart-design-spec`; for table-only standards use `$report-table-design-spec`; for filter-control standards use `$report-filter-control-design-spec`; for implementation-ready component coordinates use `$report-component-placement-spec`; for page shell/layout use `$report-visual-layout-design`; for whole-system governance use `$report-design-system-governance`.

For Haier/enterprise report, dashboard, cockpit, data-screen, BI, or business-analysis components, load `$haier-enterprise-app-ui-design-spec` for company-level tokens, typography, spacing, base controls, states, and brand rules, then load `$report-design-system-governance` as the report-specific baseline before applying component-specific fit rules.

## Reference Library

Start with `references/00-component-reference-index.md`, then load the smallest matching set.

| Need | Read |
| --- | --- |
| Screenshot-derived, sample-derived, or adaptive reusable component style goal | `references/00a-style-generalization-goal.md` plus `$artifact-readability-standard` `references/visual-source-abstraction-standard.md` |
| Shared viewport, typography, overflow, states | `references/01-shared-foundation.md` |
| Filter bars, query controls, chips, advanced filters | `references/02-filter-controls.md`; use `$report-filter-control-design-spec` `references/02-filter-selector-patterns.md` when selecting reusable filter control patterns such as dropdown, tag multi-select, date range, searchable select, tree path, drawer, or combined chipbar |
| Text summaries, conclusions, Analysis & Insight | `references/03-text-summary.md` |
| Conclusion/evidence/action cards | `references/03a-conclusion-evidence-action-cards.md`, plus `references/03-text-summary.md`, `references/04a-kpi-card-patterns.md`, and `references/12b-placement-insight-kpi.md` |
| KPI cards, metric groups, comparison tiles | `references/04-kpi-metric-cards.md`; use `references/04a-kpi-card-patterns.md` when selecting reusable KPI card expressions such as target completion, mini trend bars, lead trend cards, landscape/horizontal KPI cards, compact KPI rows, wide KPI banners, or anti-AI KPI card generation |
| Target/actual comparison cards | `references/04b-target-actual-comparison-cards.md`, plus `references/05a-echarts-foundation-bars-lines.md` and `references/12c1-placement-target-actual-bars.md` |
| Target/actual trend cards | `references/04c-target-actual-trend-cards.md`, plus `references/05a-echarts-foundation-bars-lines.md` and `references/12c2-placement-line-trends.md` |
| Target/actual radar cards | `references/04d-target-actual-radar-cards.md`, plus `references/05b-echarts-combo-pie-radar-gauge.md` and `references/12d1-placement-radar.md` |
| Target/actual donut cards | `references/04e-target-actual-donut-cards.md`, plus `references/05b-echarts-combo-pie-radar-gauge.md` and `references/12c4-placement-pie-donut.md` |
| Target/actual scatter cards | `references/04f-target-actual-scatter-cards.md`, plus `references/05c-echarts-specialized-and-flow.md` and `references/12d3-placement-scatter-bubble.md` |
| Target/actual detail table cards | `references/06a-target-actual-detail-tables.md`, plus `references/06-analytical-tables.md`, `references/10-in-component-controls.md`, `references/12f4-placement-detail-table.md`, and `$report-table-design-spec` |
| Target/actual pivot table cards | `references/06b-target-actual-pivot-tables.md`, plus `references/06-analytical-tables.md`, `references/10-in-component-controls.md`, `references/12f3-placement-pivot-table.md`, `references/12f2-placement-grouped-table-header.md`, and `$report-table-design-spec` |
| ECharts chart rules and chart-family fit | `references/05-echarts-charts.md`; use `references/05d-basic-chart-card-patterns.md` when selecting reusable basic chart card patterns such as bar card, line trend card, area trend, Combo card, pie/donut composition, stacked bar, local-filter bar, or tooltip line trend; use `references/05e-specialized-chart-card-patterns.md` when selecting specialized chart card patterns such as gauge progress, choropleth ranking map, time heatmap, K-line volume, boxplot distribution, parallel profile, or bubble opportunity |
| ECharts renderer ownership, resize lifecycle, and container-fit proof | `references/05a-echarts-foundation-bars-lines.md` |
| Detail tables, Pivot/S2, complex/grouped headers | `references/06-analytical-tables.md`; use `references/06c-table-card-patterns.md` when selecting reusable table card patterns such as detail ledger, filtered operational table, grouped header summary, metric matrix, S2 cross table, fixed-column scroll table, grouped subtotal table, or tree hierarchy table |
| Cards, lists, task/status blocks | `references/07-cards-lists-tasks.md`; use `references/07b-operational-list-status-patterns.md` when selecting reusable information list, task list, alert list, exception list, status chip, timeline, user/object list, or mixed work-item list patterns |
| Top ranking cards / leaderboard cards | `references/07a-top-ranking-cards.md`, plus `references/07-cards-lists-tasks.md`, `references/10-in-component-controls.md`, and `references/03-text-summary.md` |
| Drawers, modals, evidence/detail panels | `references/08-drawers-detail-panels.md`; use `references/08a-overlay-drawer-modal-patterns.md` when selecting reusable overlay patterns such as right filter drawer, bottom action sheet, confirmation modal, fullscreen detail, notification bar, left navigation drawer, side detail drawer, or large detail panel |
| Flow, tree, relation, Sankey, hierarchy diagrams | `references/09-complex-diagrams.md`; use `references/09a-flow-hierarchy-diagram-card-patterns.md` when selecting reusable flow/hierarchy diagram card patterns such as funnel, Sankey, journey map, tree, relation network, sunburst, treemap, or path conversion flow |
| Component-internal local filters and controls | `references/10-in-component-controls.md` |
| Empty/loading/error/no-permission/building state components | `references/13-state-feedback-patterns.md`, plus `references/01-shared-foundation.md` |
| Legacy detailed rules not yet migrated | `references/11-detailed-style-rules.md` |
| Placement routing index | `references/12-internal-placement-algorithms.md` |
| Local-filter coordinate rules | `references/12a-placement-foundation-controls.md` |
| Analysis & Insight and KPI placement | `references/12b-placement-insight-kpi.md` |
| Basic chart placement: bars, trends, combo, donut/pie | `references/12c-placement-basic-charts.md` |
| Specialized chart placement: radar, gauge, scatter, parallel coordinates, map, K-line, boxplot, heatmap | `references/12d-placement-specialized-charts.md` |
| Flow/hierarchy placement: path, sunburst, treemap, tree, relation graph, Sankey, funnel | `references/12e-placement-flow-hierarchy-charts.md` |
| Composite Panel, Micro Dashboard Card, and table placement | `references/12f-placement-composite-tables.md` |
| Implementation-ready acceptance gates | `references/12-component-acceptance-gates.md` |
| Direct chart front door | `$report-chart-design-spec` |
| Direct table front door | `$report-table-design-spec` |
| Direct filter-control front door | `$report-filter-control-design-spec` |
| Direct component-placement front door | `$report-component-placement-spec` |
| Report chart/table/filter/status baseline | `$report-design-system-governance` relevant guideline references |
| Screenshot/image-derived reusable component standards | `$artifact-readability-standard` `references/visual-source-abstraction-standard.md` |
| Cross-stage design reasonableness or readiness | `$quality-gate-validation` |
| Preflight understanding before implementation/repair/acceptance | `$quality-gate-validation` `references/preflight-understanding-gate.md` |

## Anti-Laziness Gate

For non-trivial work, apply `$quality-gate-validation` `references/anti-laziness-execution-gate.md` before final output, handoff, or readiness. Do not mark the result ready while `LAZY-*` findings remain open, when available local evidence was not inspected, when owning skills were skipped, or when proof is limited to generic statements such as "checked", "optimized", "looks good", or "implemented".

## Workflow

1. Run the Preflight understanding gate for implementation, repair, or acceptance work; name component family, parent container, data/decision contract, affected specialty skills, hard constraints, missing evidence, and start decision.
2. For screenshot-derived or reusable style work, load `00a-style-generalization-goal.md` and classify each sample as an existing pattern, composed pattern, extension gap, or out-of-scope one-off.
3. Classify the component family, business purpose, data grain, viewport/container size, interaction state, and priority.
4. Load `00-component-reference-index.md`, shared foundation, the matching component reference, and the matching placement reference only. When the task is purely chart, table, filter, or coordinate placement, prefer the specific front-door skill above.
5. Confirm the data and decision contract before styling: metric/formula, field grain, source/freshness, numeric display contract, filter scope, exact-value path, state set, and next action.
6. Define `Positioning And Alignment Rules`: container variables, slot rectangles, main visual center, local-filter geometry, display budget, overflow strategy, size tiers, fallback order, and state geometry.
7. Apply inherited baseline tokens first, then component-specific typography, color semantics, borders, shadows, spacing, hover/focus, and responsive behavior.
8. Run the component acceptance gates when the output is implementation-ready or when a visual defect may hide decision evidence.
9. Convert component rules into proof obligations before acceptance: DOM semantic roles/selectors, CSS/computed-style checks, ECharts/S2 option fields, browser geometry assertions, screenshot/crop evidence, and source/config anchors for every claimed alignment, overflow, control, legend, renderer, resize behavior, or contract rule.
10. Verify the component inside its real parent block after resize, filter changes, tab switches, drawer/fullscreen changes, loading/empty/error/no-permission states, and data updates. For chart components, distinguish `container-resize-safe` from full page responsiveness; fixed design-width pages may pass chart resize lifecycle but must not claim viewport-adaptive layout unless breakpoints/reflow are proven.

## Required Output

- Preflight understanding result when the work is implementation/repair/acceptance, plus component family and loaded reference files.
- Business/data contract: purpose, grain, key fields, formulas/units, numeric display contract, source/freshness, filters, exact-value path, and owner/action path.
- Placement rules: container variables, slots, alignment, size tiers, display budget, responsive degradation, and state geometry.
- Visual and interaction rules: tokens, labels, legends, tooltips, hover/focus, overflow strategy, disclosure, and accessibility.
- Style generalization result for reusable sample work: selected controlled pattern field, `styleGeneralization` status, adaptive variables, fallback, and whether a text-only model can reproduce the style.
- Proof obligations: KPI alignment and alignment-intent classification, duplicate controls/title ownership, overflow/clipping, chart/table option evidence, ECharts resize lifecycle evidence, contract-to-DOM/CSS/renderer mapping, non-default states, and screenshot/crop or DOM assertion result when code/URL exists.
- Acceptance result: `ready`, `partial`, or `blocked`, with `DESIGN-*`, `RPT-*`, `VIS-*`, or implementation gaps when relevant.

## Quality Gate

- Do not style a component before the business purpose, data grain, key fields, filter scope, and interaction state are known.
- Do not continue through this broad component skill alone when the affected surface is specifically chart, table, filter, or implementation-ready placement; route to the specific front-door skill first.
- Do not invent component colors, font sizes, spacing, shadows, or base control styles for Haier/enterprise report components before inheriting Haier application UI tokens.
- Implementation-ready specs must include measurable placement rules, not only CSS layout or visual adjectives.
- Every component family must declare a display budget before acceptance: maximum visible items/cards/rows/columns/categories/series/annotations/steps as applicable, the budget basis, and overflow strategy such as Top N + other, pagination, internal scroll, sampling, collapse, drawer/fullscreen, or table fallback.
- Component-internal filters must be current-component or declared local-group scoped; they cannot silently change page/global scope, backend aggregation, pagination, export scope, permission scope, or other components.
- Report components must preserve decision evidence: metric口径, source/freshness, numeric display contract, baseline, exact values, drilldown/detail/export/action path, and realistic data states.
- Metric-bearing components must declare value type, raw/display unit, display scale, screen precision, tooltip/export precision, rounding mode, null/zero/denominator-zero behavior, negative-zero handling, and formatter ownership; arbitrary decimals or component-local `toFixed` assumptions are not accepted.
- KPI/metric cards must pass actual rendered value-anchor checks, not only slot allocation: the measured value+unit group is centered in the value anchor viewport, the numeral has sufficient visual scale for the card size, and auxiliary title/status/source/target content does not push the primary value off center.
- Do not turn "core content should be centered" into a blanket rule. Implementation-ready specs must classify alignment intent by component family: KPI primary value/empty/loading states center by default; charts center the plot after reserved title/legend/axis bands; tables and long text use scan-friendly top-left content with numeric cells right-aligned; rankings/lists use row-aligned comparison. A centered-content claim fails if it lacks selectors, geometry targets, or an exception for table/text/list scanning.
- KPI/metric card title ownership must be explicit. Do not visibly render both a block/card title and a body metric label when they normalize to the same or highly similar text; use `displayTitle` for the visible title and keep `metricName` for tooltip/export/口径 metadata unless `showBodyMetricLabel` is explicitly justified.
- Declared component contracts are not acceptance proof by themselves. `compositePanelContract`, `analysisInsightContract`, KPI placement metadata, local-filter metadata, or chart/table contracts must map to inspectable DOM attributes/classes, CSS/computed styles, ECharts/S2 options, browser assertions, and screenshot/crop evidence when implementation or runtime is available. Otherwise record `LAZY-CONTRACT-THEATER` and keep readiness `partial`.
- Component-local controls cannot duplicate template-owned refresh, download/export, copy/share, global filters, or topbar controls. If the template owns the shell controls, component specs must either remove the duplicate controls or cite an explicit `controlOwnership: "component"` decision with the template control disabled/hidden.
- Standard ECharts charts must be implemented with ECharts-owned options/series/runtime behavior; do not hand-draw standard charts while importing ECharts.
- Standard ECharts charts must pass the resize lifecycle gate when implementation or URL exists: the chart body has non-zero measured width/height before `echarts.init`; option changes call `setOption` or wrapper equivalent; container changes use `ResizeObserver` or a documented equivalent plus tab/drawer/fullscreen hooks; cleanup calls `dispose` and disconnects listeners; QA verifies at the design viewport and at least one different viewport/container size. Missing lifecycle proof is `VIS-CHART-NO-RESIZE-PROOF`; a blank or stale chart after resize is `VIS-CHART-RESIZE-BROKEN`.
- ECharts Cartesian charts with legends, y-axis names, axis units, target labels, or local filters sharing an edge band must declare explicit slot budgets and collision checks. `grid.containLabel` alone is not sufficient evidence for legend/axis-name safety.
- ECharts line/bar/combo charts must pass plot-viability checks, not only lifecycle checks. Standard axis charts require chart body `>=180px`; dense combo, dual-axis, target/reference, or chart + table/list cards require chart body `>=220px`; plot height must meet the owning chart floor, y-axis labels must not stack, and gridlines must not merge into a stripe. If chart and preview rows cannot both fit, split/enlarge or move the preview before styling.
- SVG/canvas/ECharts/custom geometry must preserve aspect ratio and must not stretch, squeeze, or distort business shapes.
- Do not use generic AI/SaaS polish, decorative gradients/glass/glow, oversized radius, vague copy, or ornamental motion when it competes with data reading.
- Screenshot-inspired reusable component rules must be converted into text/structured visual pattern contracts. Do not rely on raw screenshots, image paths, or image embeddings as the only durable source of truth unless the task is exact restoration, runtime asset retention, visual regression, or audit evidence.
- Screenshot-derived or sample-derived reusable styles are not ready unless each provided sample is routable to an existing controlled pattern, a composed pattern contract, or a documented `requires-pattern-extension` gap under `00a-style-generalization-goal.md`.
- Load `12-component-acceptance-gates.md` before accepting dense charts, tables, Composite Panels, Micro Dashboard Cards, state feedback components, Analysis & Insight, KPI cards, local filters, or shape-sensitive graphics for implementation.
