# Component Spec Source Map

Use this map to load only the source references needed for the component families in scope.

| Component family | Primary source references |
| --- | --- |
| Sample-derived style generalization goal | `$report-component-style-design` `references/00a-style-generalization-goal.md` and `$artifact-readability-standard` `references/visual-source-abstraction-standard.md` |
| Shared foundation, state, overflow, typography | `$report-component-style-design` `references/01-shared-foundation.md` |
| Page/global and component-local filters | `$report-filter-control-design-spec`, especially `references/02-filter-selector-patterns.md` when reusable filter selector patterns are needed |
| Analysis & Insight / text summaries | `$report-component-style-design` `references/03-text-summary.md`, `references/12b-placement-insight-kpi.md` |
| Conclusion/evidence/action cards | `$report-component-style-design` `references/03a-conclusion-evidence-action-cards.md`, `$report-component-style-design` `references/03-text-summary.md`, `$report-component-style-design` `references/12b-placement-insight-kpi.md` |
| KPI and metric cards | `$report-component-style-design` `references/04-kpi-metric-cards.md`, `references/04a-kpi-card-patterns.md`, `references/12b-placement-insight-kpi.md` |
| Target/actual comparison cards | `$report-component-style-design` `references/04b-target-actual-comparison-cards.md`, `$report-chart-design-spec`, `$report-component-style-design` `references/12c1-placement-target-actual-bars.md` |
| Target/actual trend cards | `$report-component-style-design` `references/04c-target-actual-trend-cards.md`, `$report-chart-design-spec`, `$report-component-style-design` `references/12c2-placement-line-trends.md` |
| Target/actual radar cards | `$report-component-style-design` `references/04d-target-actual-radar-cards.md`, `$report-chart-design-spec`, `$report-component-style-design` `references/12d1-placement-radar.md` |
| Target/actual donut cards | `$report-component-style-design` `references/04e-target-actual-donut-cards.md`, `$report-chart-design-spec`, `$report-component-style-design` `references/12c4-placement-pie-donut.md` |
| Target/actual scatter cards | `$report-component-style-design` `references/04f-target-actual-scatter-cards.md`, `$report-chart-design-spec`, `$report-component-style-design` `references/12d3-placement-scatter-bubble.md` |
| Basic chart cards | `$report-component-style-design` `references/05d-basic-chart-card-patterns.md`, `$report-chart-design-spec`, and matching `$report-component-style-design` `references/05a-echarts-foundation-bars-lines.md` or `references/05b-echarts-combo-pie-radar-gauge.md` |
| Specialized chart cards | `$report-component-style-design` `references/05e-specialized-chart-card-patterns.md`, `$report-chart-design-spec`, and matching `$report-component-style-design` `references/05b-echarts-combo-pie-radar-gauge.md` or `references/05c-echarts-specialized-and-flow.md` |
| Flow/hierarchy diagram cards | `$report-component-style-design` `references/09a-flow-hierarchy-diagram-card-patterns.md`, `$report-component-style-design` `references/09-complex-diagrams.md`, `$report-chart-design-spec`, and matching `$report-component-style-design` `references/05c-echarts-specialized-and-flow.md` |
| Target/actual detail table cards | `$report-component-style-design` `references/06a-target-actual-detail-tables.md`, `$report-table-design-spec`, `$report-component-style-design` `references/12f4-placement-detail-table.md` |
| Target/actual pivot table cards | `$report-component-style-design` `references/06b-target-actual-pivot-tables.md`, `$report-table-design-spec`, `$report-component-style-design` `references/12f3-placement-pivot-table.md`, `$report-component-style-design` `references/12f2-placement-grouped-table-header.md` |
| Table card patterns | `$report-component-style-design` `references/06c-table-card-patterns.md`, `$report-component-style-design` `references/06-analytical-tables.md`, `$report-table-design-spec`, and matching `$report-component-style-design` `references/12f2-placement-grouped-table-header.md`, `references/12f3-placement-pivot-table.md`, `references/12f4-placement-detail-table.md`, or `references/12f5-placement-table-acceptance-checks.md` |
| ECharts charts | `$report-chart-design-spec` |
| Detail tables, Pivot/S2, complex headers | `$report-table-design-spec` |
| Cards, lists, tasks, status blocks | `$report-component-style-design` `references/07-cards-lists-tasks.md`, `$report-component-style-design` `references/07b-operational-list-status-patterns.md` |
| Top ranking cards / leaderboard cards | `$report-component-style-design` `references/07a-top-ranking-cards.md`, `$report-component-style-design` `references/07-cards-lists-tasks.md`, `$report-component-style-design` `references/10-in-component-controls.md` |
| Drawers, modals, detail panels | `$report-component-style-design` `references/08-drawers-detail-panels.md`, `$report-component-style-design` `references/08a-overlay-drawer-modal-patterns.md` |
| Flow/hierarchy/complex diagrams | `$report-chart-design-spec` |
| Composite Panels / multi-component analysis cards | `$report-component-placement-spec` plus child component references |
| Micro Dashboard Cards / themed multi-component mini boards | `$report-component-style-design` `references/12f6-placement-micro-dashboard-card.md`, `$report-layout-size-constraint-spec`, and child component references |
| Empty/loading/error/no-permission/building state components | `$report-component-style-design` `references/13-state-feedback-patterns.md`, `$report-component-style-design` `references/01-shared-foundation.md` |
| Implementation-ready placement | `$report-component-placement-spec` |
| Acceptance gates | `$report-component-style-design` `references/12-component-acceptance-gates.md` |

For report-wide rules such as metric口径, chart/table format, filters, states, and acceptance, also load `$report-design-system-governance` guideline references.
