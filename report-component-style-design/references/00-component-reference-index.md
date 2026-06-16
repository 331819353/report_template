# Component Style Reference Index

Use this index to load only the component rules needed for the current task.

## Loading Order

1. For screenshot-derived, sample-derived, or reusable adaptive component standards, first read `00a-style-generalization-goal.md` so every sample is routed to a controlled pattern, composed pattern, extension gap, or out-of-scope one-off.
2. Always read `01-shared-foundation.md` for viewport, typography, overflow, density, and hover disclosure rules.
3. Read the files matching the requested component types.
4. Read `12-internal-placement-algorithms.md` whenever the task asks for component design, component restoration, component-internal local filters, or an implementation-ready component spec. It is now an index; load only the split placement file that matches the component family.
5. If the component is mixed, such as a KPI card with a mini chart, read every relevant file and apply the stricter fit rule.
6. If the component cannot satisfy the relevant rules inside its current block, recommend a larger span, split component, drawer, fullscreen, internal scroll, zoom/pan, or table fallback.

## Component File Map

| Component type | Read this reference | Use when |
| --- | --- | --- |
| Style generalization target and screenshot-to-text abstraction | `00a-style-generalization-goal.md` plus `$artifact-readability-standard` `references/visual-source-abstraction-standard.md` | Any screenshot/sample-derived reusable component style, adaptive generation goal, or "沉淀为 skill" request |
| Shared containers, titles, labels, units, badges, empty states, aspect-ratio integrity | `01-shared-foundation.md` | Any component style task, especially SVG/canvas/custom graphics that may deform |
| Filters, query bars, filter chips, advanced filter popovers | `02-filter-controls.md`; for reusable selector patterns also load `$report-filter-control-design-spec` `references/02-filter-selector-patterns.md` | Page/global filters, date, organization, status, owner, metric, baseline, simple dropdown, tag multi-select, date range, searchable select, tree path selector, advanced drawer, combined chipbar |
| Analysis & Insight components, text summaries, conclusion blocks, insight cards | `03-text-summary.md` | Executive conclusion, diagnosis, risk explanation, recommendation, data-quality note, definition note, chart annotation, explanatory empty state |
| Conclusion/evidence/action cards | `03a-conclusion-evidence-action-cards.md`, `03-text-summary.md`, `04a-kpi-card-patterns.md`, `12b-placement-insight-kpi.md` | Lead conclusion card with KPI evidence, key findings, action suggestions, source/freshness, and anti-generic-copy rules |
| KPI cards, pyramid KPI cards, metric groups, comparison tiles, mini trends | `04-kpi-metric-cards.md`, plus `04a-kpi-card-patterns.md` for reusable card expressions | KPI, target attainment, YoY/MoM, target, sparkline, status, submetric tile, target-wave card, mini bar trend card, lead line trend card, landscape/horizontal KPI card, compact KPI row, wide KPI banner |
| Target/actual comparison cards | `04b-target-actual-comparison-cards.md`, `05a-echarts-foundation-bars-lines.md`, `12c1-placement-target-actual-bars.md` | KPI headline + grouped actual/comparison bars + target line + bottom summary, such as sales amount actual vs prior period vs target |
| Target/actual trend cards | `04c-target-actual-trend-cards.md`, `05a-echarts-foundation-bars-lines.md`, `12c2-placement-line-trends.md` | KPI headline + actual/comparison/target lines + bottom summary, such as sales amount actual vs prior period vs target over time |
| Target/actual radar cards | `04d-target-actual-radar-cards.md`, `05b-echarts-combo-pie-radar-gauge.md`, `12d1-placement-radar.md` | KPI headline + actual/comparison/target radar polygons + bottom summary, such as sales amount profile across products vs prior period and target |
| Target/actual donut cards | `04e-target-actual-donut-cards.md`, `05b-echarts-combo-pie-radar-gauge.md`, `12c4-placement-pie-donut.md` | KPI headline + local period switch + actual composition donut + category legend + bottom target/actual/comparison summary |
| Target/actual scatter cards | `04f-target-actual-scatter-cards.md`, `05c-echarts-specialized-and-flow.md`, `12d3-placement-scatter-bubble.md` | KPI headline + local period switch + actual/comparison scatter points + target/reference line + bottom target/actual/comparison summary |
| Target/actual detail table cards | `06a-target-actual-detail-tables.md`, `06-analytical-tables.md`, `10-in-component-controls.md`, `12f4-placement-detail-table.md` | Ranked row-evidence table with comparison, actual, target, completion rate, total row, local period switch, legend, and field definitions |
| Target/actual pivot table cards | `06b-target-actual-pivot-tables.md`, `06-analytical-tables.md`, `10-in-component-controls.md`, `12f3-placement-pivot-table.md`, `12f2-placement-grouped-table-header.md` | Pivot table card with row hierarchy, dimension/metric controls, comparison/actual/target measures, completion rate, subtotal, grand total, and footer definitions |
| Composite Panel / multi-component analysis card | `12f-placement-composite-tables.md`, then `12f1-placement-composite-panel.md`, plus each child component reference | KPI + chart + Top list/detail, main chart + auxiliary composition, target attainment mini-loop, diagnostic card with multiple coordinated child components |
| Micro Dashboard Card / themed multi-component mini board | `12f-placement-composite-tables.md`, then `12f6-placement-micro-dashboard-card.md`, plus each child component reference | Large single-topic cards with KPI strip, 4-8 bounded child sections, exact-value/status path, shared filters, and strict child minimums |
| ECharts charts, axes, legends, data labels, tooltips, proportional geometry, chart-engine fidelity | `05-echarts-charts.md`; for reusable basic chart cards also load `05d-basic-chart-card-patterns.md`; for reusable specialized chart cards also load `05e-specialized-chart-card-patterns.md` | Bar, line/area trend, Combo/mixed bar-line chart, pie/donut, stacked bar, local-filter chart card, tooltip trend card, gauge progress card, choropleth ranking map card, time heatmap card, K-line volume card, boxplot distribution card, parallel profile card, bubble opportunity card, target/actual column, radar, scatter, parallel coordinates, map, candlestick/K-line, boxplot, heatmap, Sankey, sunburst, treemap/rectangular tree map, path/user/process path, tree/hierarchical tree, relation/network graph, funnel, waterfall, gauge, custom path, or any case where ECharts may be imported but chart marks are hand-drawn |
| AntV S2 and analytical tables | `06-analytical-tables.md`; for reusable table card patterns also load `06c-table-card-patterns.md` | Plain detail ledger table, filtered operational status table, grouped header summary table, metric matrix table, S2 cross pivot table, fixed-column scroll table, grouped subtotal summary table, tree hierarchy table, Pivot table, cross table, metric matrix, detail table, financial grid |
| Cards, lists, task cards, anomaly cards, status badges | `07-cards-lists-tasks.md`; for reusable operational list/status patterns also load `07b-operational-list-status-patterns.md` | Object cards, ordinary information lists, task lists, alert lists, exception lists, status chip sets, event timelines, user/object lists, mixed work-item lists |
| Top ranking cards / leaderboard cards | `07a-top-ranking-cards.md`, `07-cards-lists-tasks.md`, `10-in-component-controls.md`, `03-text-summary.md` | TOP N cards with medals, progress bars, rank badges, local period switch, values, shares, and data-grounded conclusion strip |
| Drawers, modals, detail panels, evidence panels | `08-drawers-detail-panels.md`; for reusable overlay patterns also load `08a-overlay-drawer-modal-patterns.md` | Row detail, evidence, logs, source trace, object profile, right filter drawer, bottom action sheet, confirmation modal, fullscreen detail, notification bar, left navigation drawer, side detail drawer, large detail side panel |
| Complex diagrams, trees, decomposition, Sankey, flows, aspect-safe scaling | `09-complex-diagrams.md`; for reusable flow/hierarchy diagram cards also load `09a-flow-hierarchy-diagram-card-patterns.md` | Funnel card, Sankey card, journey stage map, hierarchy tree card, hub relation network card, sunburst composition card, treemap composition card, path conversion flow card, Tree, sunburst, treemap, path, process, DuPont, attribution, relation, flow diagrams, SVG/canvas diagrams |
| In-component capsule switches, dropdowns, and local filters | `10-in-component-controls.md` | Component-level local filter, view mode, metric switch, period switch, dimension select, ranking scope, chart/table mode |
| Empty/loading/error/no-permission/building state components | `13-state-feedback-patterns.md`, plus `01-shared-foundation.md` | Report/table/chart/card/page states with controlled stateKind, stateFeedbackPattern, reason, action, geometry preservation, no-permission leakage rules, and text-only reproduction |
| Component internal placement and coordinate algorithms | `12-internal-placement-algorithms.md` index, then the matching `12a`-`12f` split file | Any implementation-ready component design, component-local filter placement, KPI card coordinates, element x/y, alignment, size tiers, and state geometry |
| Component acceptance gates | `12-component-acceptance-gates.md` | Implementation-ready specs, dense chart/table acceptance, ECharts/S2 fidelity, local-filter scope, metric evidence, and anti-polish checks |

## Placement Split Map

| Need | Read |
| --- | --- |
| Coordinate variables and component-local filters | `12a-placement-foundation-controls.md` |
| Analysis & Insight and KPI cards | `12b-placement-insight-kpi.md` |
| Basic charts: target/actual bars, line trends, combo, pie/donut | `12c-placement-basic-charts.md`, then exact `12c1`-`12c4` file |
| Specialized charts: radar, gauge, scatter, parallel coordinates, map, K-line, boxplot, heatmap | `12d-placement-specialized-charts.md`, then exact `12d1`-`12d8` file |
| Flow/hierarchy charts: path, sunburst, treemap, tree, relation graph, Sankey, funnel | `12e-placement-flow-hierarchy-charts.md`, then exact `12e1`-`12e7` file |
| Composite Panel, Micro Dashboard Card, grouped headers, Pivot Table, Detail Table | `12f-placement-composite-tables.md`, then exact `12f1`-`12f6` file |

## Mandatory Decision Record

For every component style output, state:

- Which reference files were applied.
- The component viewport size assumption or minimum viable size.
- The internal coordinate system, main visual center, slot rectangles, and alignment rules for implementation-ready components.
- The visible labels or values that remain permanent.
- The hidden labels or values and how users inspect them, such as hover tooltip, focus tooltip, click drawer, fullscreen, table fallback, or internal scroll.
- The overflow strategy for long text, long labels, many marks, wide tables, or dense diagrams.
- The aspect-ratio strategy for SVG/canvas/ECharts custom graphics, maps, gauges, radar, pies, paths, and complex diagrams.
- The in-component controls used, their placement, selected state, dropdown behavior, and what content each control changes.
- When component-local filters exist, the `组件内筛选区 / 局部筛选区` rules used: affected component only, suitable/unsuitable filters, `2-4` capsule vs `>4` dropdown decision, placement, title/unit/legend relationship, and responsive collapse.
- For reusable screenshot/sample-derived work, the selected controlled pattern field, `styleGeneralization.generalizationStatus`, adaptive variables, fallback, and proof that the pattern is usable without raw image access.
