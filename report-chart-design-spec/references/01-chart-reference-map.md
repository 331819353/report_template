# Chart Reference Map

Load the smallest matching set. Do not load every chart reference for a single chart task.

| Chart task | Visual/content reference | Placement reference |
| --- | --- | --- |
| Screenshot/sample-derived chart style generalization | `$report-component-style-design` `references/00a-style-generalization-goal.md` plus `$artifact-readability-standard` `references/visual-source-abstraction-standard.md` | Then route to the exact chart/card placement reference below |
| Reusable basic chart card patterns: bar card, line trend, area trend, Combo card, pie/donut composition, stacked bar, local-filter bar, tooltip trend | `$report-component-style-design` `references/05d-basic-chart-card-patterns.md`, plus matching `05a` or `05b` reference | `$report-component-style-design` `references/12c-placement-basic-charts.md`, then exact `12c1`-`12c4` file |
| Reusable specialized chart card patterns: gauge progress, choropleth ranking map, time heatmap, K-line volume, boxplot distribution, parallel profile, bubble opportunity | `$report-component-style-design` `references/05e-specialized-chart-card-patterns.md`, plus matching `05b` or `05c` reference | `$report-component-style-design` `references/12d-placement-specialized-charts.md`, then exact `12d1`-`12d8` file |
| Reusable flow/hierarchy diagram card patterns: funnel, Sankey, journey map, tree, relation network, sunburst, treemap, path conversion flow | `$report-component-style-design` `references/09a-flow-hierarchy-diagram-card-patterns.md`, plus `references/09-complex-diagrams.md` and matching `05c` reference | `$report-component-style-design` `references/12e-placement-flow-hierarchy-charts.md`, then exact `12e1`-`12e7` file |
| Target/actual bar, attainment, gap, YoY/MoM comparison | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12c1-placement-target-actual-bars.md` |
| Line/area trend, sparse trend, reference line | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12c2-placement-line-trends.md` |
| Combo / mixed bar-line chart | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12c3-placement-combo-charts.md` |
| Pie / donut / small-card donut | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12c4-placement-pie-donut.md` |
| Radar | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d1-placement-radar.md` |
| Gauge | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d2-placement-gauge.md` |
| Scatter / bubble | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d3-placement-scatter-bubble.md` |
| Parallel coordinates | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d4-placement-parallel-coordinates.md` |
| Map / geographic / geo flow | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d5-placement-map-geographic.md` |
| Candlestick / K-line | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d6-placement-candlestick-kline.md` |
| Boxplot / box-and-whisker | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d7-placement-boxplot.md` |
| Heatmap / calendar heatmap / matrix / correlation | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12d8-placement-heatmap-matrix.md` |
| Path / journey / process path | `$report-component-style-design` `references/09-complex-diagrams.md` and `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e1-placement-path-journey.md` |
| Sunburst | `$report-component-style-design` `references/09-complex-diagrams.md` and `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e2-placement-sunburst.md` |
| Treemap | `$report-component-style-design` `references/09-complex-diagrams.md` and `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e3-placement-treemap.md` |
| Tree / hierarchy tree | `$report-component-style-design` `references/09-complex-diagrams.md` and `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e4-placement-tree.md` |
| Relation / network graph | `$report-component-style-design` `references/09-complex-diagrams.md` and `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e5-placement-relation-network.md` |
| Sankey | `$report-component-style-design` `references/09-complex-diagrams.md` and `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e6-placement-sankey.md` |
| Funnel | `$report-component-style-design` `references/05-echarts-charts.md` | `$report-component-style-design` `references/12e7-placement-funnel.md` |

Always add `$report-component-style-design` `references/12a-placement-foundation-controls.md` when the chart has component-local filters, title-right controls, or shared coordinate variables.
