# KPI Card Pattern Library

Use this reference after `04-kpi-metric-cards.md` when a report prototype or component spec needs KPI cards that feel product-specific rather than generic metric shells, including portrait KPI cards, KPI overview cards, single-indicator KPI grid cards, KPI judgment cards for status/health/rating/gauge decisions, KPI goal execution cards for target attainment/gap/progress/milestones, KPI time-series analysis cards for trend/change/YoY-MoM/cycle/volatility/forecast decisions, KPI comparison analysis cards for direct/group/competitor/benchmark/variance decisions, landscape/horizontal KPI cards, horizontal axis-line diagnostic KPI cards, horizontal axis-bar diagnostic KPI cards, horizontal scatter diagnostic KPI cards, horizontal spatial-map diagnostic KPI cards, and paired comparison diagnostic KPI cards.

The pattern library does not replace the KPI data contract, numeric display contract, or placement rules. It chooses the card expression after the metric purpose, target/baseline, trend evidence, and parent viewport are known.

## Pattern Selection

Keep `visualType: "metric-card"` for all KPI cards. Add `kpiCardPattern` in component metadata or widget config to choose the internal expression. When one card summarizes a business domain with several metrics, also add `kpiOverviewCardPattern`; do not force the card into a single-indicator pattern. When the card's main job is to judge status, health, score, rating, risk, or gauge progress, also add `kpiJudgmentCardPattern` so the card has explicit status scale, threshold, and evidence semantics rather than decorative KPI polish. When the card's main job is target execution management, also add `kpiGoalExecutionCardPattern` so target attainment, gap, progress, milestone, remaining work, and deadline semantics are explicit instead of being scattered across generic gauges, timelines, or decorative progress bars. When the card's main job is time-series analysis, also add `kpiTimeSeriesCardPattern` so trend, change, YoY/MoM, cycle, volatility, and forecast semantics are explicit instead of being hidden in generic sparklines. When the card's main job is comparison analysis, also add `kpiComparisonAnalysisCardPattern` so direct comparison, group comparison, competitor comparison, benchmark position, and variance/gap semantics are explicit instead of being hidden in generic bars, radar charts, tables, or paired panes.

| `kpiCardPattern` | Use when | Required data | Avoid when |
| --- | --- | --- | --- |
| `plain-metric` | The card only needs a current value and one or two comparisons. | metric name, value, unit, period, at least one baseline/comparison or status. | A target/progress/trend is the main evidence. |
| `target-wave` | Target attainment or completion rate is the main judgment. | value, target, attainment rate, unit, period, target formula. | No bounded target exists, or progress semantics are unclear. |
| `mini-bar-trend` | The user needs quick period volatility or recent distribution evidence. | value, unit, period, trend series with ordered categories, comparison values. | The series has fewer than three points or exact trend audit is the main task. |
| `highlight-line-trend` | One KPI should become the primary visual anchor in a KPI group or first viewport. | value, unit, period, trend series, latest point, comparison values, target or threshold when available. | Many cards need equal weight, or a dark/emphasis token is not approved. |
| `horizontal-trend-compare` | A landscape KPI needs current value, prior/baseline comparison, and a small trend line. | value, unit, comparison label/value, ordered trend series, tooltip payload. | The trend needs axes, target lines, or exact audit. |
| `horizontal-axis-line-trend` | A landscape KPI needs a readable line chart with axes, grid, target/reference/threshold bands, phase annotation, or dual-series comparison under the primary value. | value, unit, comparison label/value, ordered trend dataset, x field, y field, axis unit, tooltip payload, optional target/reference/threshold/phase/comparison series fields. | The card is below `420x260`, the line is only decorative, or the chart evidence is the main block rather than supporting one KPI. |
| `horizontal-axis-bar-compare` | A landscape KPI needs a readable horizontal bar body for ranked/time/category comparison, target line, dual-series comparison, threshold warning, or per-category change-rate evidence under the primary value. | value, unit, comparison label/value, ordered bar dataset, category field, value field, axis unit, tooltip payload, optional target/reference/threshold/change-rate/comparison series fields. | The card is below `420x260`, labels or values do not fit, more than 8 bars are needed, or the bar chart is the main block rather than supporting one KPI. |
| `horizontal-axis-scatter-diagnostic` | A landscape KPI needs a readable scatter body for relationship, distribution, outlier, quadrant, threshold, target-crosshair, or correlation diagnosis under the primary value. | value, unit, comparison label/value, object-grain scatter dataset, x field, y field, x/y units, tooltip payload, optional trendline/reference/threshold/quadrant/category/size fields. | The card is below `420x300`, only one numeric metric exists, point density is unmanaged, or exact row audit is the main task. |
| `horizontal-spatial-map-diagnostic` | A landscape KPI needs geography as the evidence: choropleth, graded map, bubble map, point map, column-symbol map, or change-zone map under the primary value. | value, unit, comparison label/value, region code or lon/lat fields, map value field, map resource/projection, legend/visualMap payload, optional target gap/change/category/point fields. | Geography is only a label, the map would be decorative, the card is below `460x320`, or the map resource/projection cannot be proven. |
| `paired-comparison-diagnostic` | A KPI needs two comparable panes such as current vs prior, actual vs target, before vs after, or good/bad status with a central `VS` anchor and bottom conclusion. | left/right metric fields or comparable datasets, baseline labels, unit, comparison/gap field, optional mini charts/rings/dot matrices/breakdown rows, conclusion field. | The two sides are not comparable, baselines differ, the card is below `420x260`, or the user needs a full comparison table/chart. |
| `horizontal-ring-progress` | A landscape KPI needs a bounded status/progress reading such as OEE, utilization, SLA, or completion. | value, min/max or target range, progress rate, prior/baseline value, status direction. | The metric is unbounded or compares many categories. |
| `horizontal-target-progress` | A landscape KPI needs target attainment with a linear progress track and optional target marker. | value, target, attainment rate, target direction, target label/formula. | A circular gauge or detailed variance chart is the main task. |
| `horizontal-status-trend-compare` | A business-negative or quality metric needs before/after comparison and a compact trend. | current value, prior value, improvement/change rate, direction semantics, trend series. | Direction semantics are unknown or lower-is-better is not declared. |
| `horizontal-grain-bar-switch` | A KPI card includes a small time-grain switch and mini bars for recent distribution. | value, comparison, time-grain options, ordered bar series, selected period. | More than one local filter group is required. |
| `horizontal-period-summary-strip` | The card compares current/previous/target values in a bottom strip rather than a chart. | current value, prior value, target value, comparison label, selected period. | A trend or distribution is required to explain the judgment. |
| `horizontal-pp-assist-info` | A percent/ratio metric needs a percentage-point delta plus an auxiliary evidence panel. | value, baseline value, pp delta, evidence label/value, optional mini bars. | The delta is a percent change rather than percentage-point movement. |
| `horizontal-warning-status-band` | A KPI needs a visible warning/status badge plus a bottom alert band. | value, threshold, status, warning reason, selected status/period, action/detail path. | The status is neutral or no threshold/action path exists. |

Single-indicator KPI cards use the existing `kpiCardPattern` as the primary family and add `kpiSingleIndicatorLayoutMode` to choose the internal card layout. Use this when a page shows a peer grid of one-metric cards, each with one value, one comparison, one small evidence visual, and one target/progress footer.

KPI overview cards use the existing `kpiCardPattern` only for the lead metric evidence style and add `kpiOverviewCardPattern` to choose the multi-metric anatomy. Use this when one wide card answers a business-domain overview question, such as sales overview, user growth overview, operations overview, or finance overview.

| `kpiOverviewCardPattern` | Pair with `kpiCardPattern` | Use when |
| --- | --- | --- |
| `lead-metric-comparison-sparkline-overview` | `horizontal-trend-compare` or `horizontal-target-progress` | One lead metric is supported by two comparison cells, one target/progress cell, and one right-side sparkline. |
| `multi-metric-strip-progress-overview` | `plain-metric` or `horizontal-target-progress` | The card shows `3-5` sibling metrics as equal cells, each with value, comparison, target/attainment text, and a small progress track. |
| `domain-metric-cluster-progress-overview` | `horizontal-period-summary-strip`, `horizontal-target-progress`, or `plain-metric` | A domain card combines a lead metric with `2-3` companion metrics and one target/progress summary, often with a unit or metric switch. |

KPI judgment cards use the existing `kpiCardPattern` as the primary metric family and add `kpiJudgmentCardPattern` to choose the judgment anatomy. Use this when the card answers "是否正常 / 是否健康 / 是否达标 / 评分如何 / 风险多高" and the visible design depends on a bounded score, status dictionary, target threshold, or rating distribution.

| `kpiJudgmentCardPattern` | Pair with `kpiCardPattern` | Use when |
| --- | --- | --- |
| `semantic-status-icon-card` | `plain-metric` or `horizontal-warning-status-band` | A categorical state such as normal, processing, warning, failed, pending review, or paid/success is the main answer. |
| `progress-status-ring-card` | `horizontal-ring-progress` | A task, project, payment, or completion state needs a circular progress reading plus status copy. |
| `health-score-ring-card` | `horizontal-ring-progress` or `plain-metric` | A bounded health score needs an overall number, level label, and comparison strip. |
| `health-threshold-bullet-card` | `horizontal-target-progress` | A health, service, quality, or risk score is judged against multiple threshold bands. |
| `health-dimension-breakdown-card` | `plain-metric` | Several health dimensions or resource dimensions explain the overall score. |
| `rating-score-summary-card` | `plain-metric` or `horizontal-ring-progress` | A review/score/risk/project assessment needs a score, level, star/hex/shield motif, and comparison strip. |
| `rating-distribution-card` | `horizontal-ring-progress` or `plain-metric` | A rating metric needs visible distribution such as 5-star share bars or valid-review count. |
| `semicircle-gauge-target-card` | `horizontal-ring-progress` or `target-wave` | A bounded dashboard gauge needs arc, ticks, target marker, and pass/fail/status semantics. |

KPI goal execution cards use the existing `kpiCardPattern` as the primary metric family and add `kpiGoalExecutionCardPattern` to choose the execution anatomy. Use this when the card answers "目标达成了吗 / 还差多少 / 进度到哪了 / 关键节点到哪了 / 是否会延期" and the visible design depends on actual-vs-target, gap, planned-vs-actual progress, milestone status, or deadline/remaining-time fields.

| `kpiGoalExecutionCardPattern` | Pair with `kpiCardPattern` | Use when |
| --- | --- | --- |
| `attainment-ring-summary-card` | `horizontal-ring-progress` or `target-wave` | A target attainment rate is the hero, with actual value, target value, and remaining target visible. |
| `attainment-gauge-deadline-card` | `horizontal-ring-progress` or `target-wave` | Attainment needs a semi-gauge/ring plus due date, ahead/overdue status, or overachievement state. |
| `attainment-linear-target-card` | `horizontal-target-progress` | A linear progress track, target marker, min/max scale, and actual/target text best communicate target distance. |
| `attainment-unit-progress-card` | `horizontal-target-progress` or `plain-metric` | Count-based execution such as orders, users, projects, or people uses dot/pictogram/progress items plus actual/target. |
| `gap-gauge-deficit-card` | `horizontal-ring-progress` or `target-wave` | The main answer is deficit, shortage, overspend, lag, or target miss, with gap value and gap rate emphasized. |
| `gap-target-actual-compare-card` | `paired-comparison-diagnostic` or `horizontal-target-progress` | Target and actual must be compared side by side through bars, budget/actual rows, or a compact VS structure. |
| `progress-plan-actual-card` | `horizontal-target-progress` or `paired-comparison-diagnostic` | Actual progress is judged against planned progress, target progress, or schedule progress. |
| `milestone-timeline-card` | `plain-metric` or `horizontal-target-progress` | Milestones, phases, countdowns, or node status are the main evidence for completion state. |

KPI time-series analysis cards use the existing `kpiCardPattern` as the primary metric family and add `kpiTimeSeriesCardPattern` to choose the temporal evidence anatomy. Use this when the card answers "过去怎么变 / 和哪个周期比 / 当前处在哪个周期 / 波动大不大 / 未来可能怎么走" and the visible design depends on ordered series, comparison baseline, cycle window, volatility statistics, or forecast intervals.

| `kpiTimeSeriesCardPattern` | Pair with `kpiCardPattern` | Use when |
| --- | --- | --- |
| `trend-line-target-card` | `horizontal-axis-line-trend`, `highlight-line-trend`, or `horizontal-trend-compare` | A current KPI needs a readable trend line, target/reference line, status badge, and latest-value context. |
| `change-baseline-delta-card` | `horizontal-axis-line-trend`, `horizontal-axis-bar-compare`, or `horizontal-trend-compare` | A metric must explain how much it changed from a named baseline such as 上月, 上周, or 去年同期. |
| `yoy-mom-comparison-card` | `horizontal-axis-line-trend`, `horizontal-axis-bar-compare`, or `paired-comparison-diagnostic` | 同比 and 环比 are both visible, and their baseline values or baseline series must be inspectable. |
| `cycle-period-progress-card` | `horizontal-ring-progress`, `horizontal-period-summary-strip`, or `horizontal-axis-line-trend` | A metric is judged inside a selected day/week/month/quarter/year cycle with current period index, phase, progress, or period target. |
| `volatility-stat-card` | `horizontal-axis-line-trend` or `horizontal-trend-compare` | Stability or fluctuation is the main judgment, backed by amplitude, max/min, standard deviation, and volatility level. |
| `forecast-interval-card` | `horizontal-axis-line-trend` or `highlight-line-trend` | Forecasted future values, forecast interval, confidence band, horizon, or prediction status are visible. |

KPI comparison analysis cards use the existing `kpiCardPattern` as the primary metric family and add `kpiComparisonAnalysisCardPattern` to choose the comparison evidence anatomy. Use this when the card answers "谁更高 / 哪组更强 / 我与竞品差在哪 / 与标杆差多少 / 差异是否显著" and the visible design depends on comparable subjects, groups, competitors, benchmark percentiles, or variance formulas.

| `kpiComparisonAnalysisCardPattern` | Pair with `kpiCardPattern` | Use when |
| --- | --- | --- |
| `direct-value-compare-card` | `paired-comparison-diagnostic`, `horizontal-axis-line-trend`, or `horizontal-axis-bar-compare` | Two or more comparable values, periods, regions, products, or channels are judged on the same metric definition and unit. |
| `group-segment-compare-card` | `horizontal-axis-bar-compare`, `horizontal-axis-line-trend`, or `horizontal-trend-compare` | Several business groups or segments must be compared across the same metric, often through grouped/stacked bars, multi-line trends, or group summary tiles. |
| `competitor-position-card` | `horizontal-axis-bar-compare`, `horizontal-axis-line-trend`, `paired-comparison-diagnostic`, or `plain-metric` | One primary product/company is compared with named competitors, peer products, or industry average across share, ranking, dimensions, satisfaction, channel, or KPI matrix evidence. |
| `benchmark-position-card` | `horizontal-axis-bar-compare`, `horizontal-ring-progress`, `horizontal-target-progress`, or `plain-metric` | The current object is positioned against industry average, peer rank, P50/P75/P90, standard value, best practice, or a selected benchmark. |
| `variance-gap-card` | `paired-comparison-diagnostic`, `horizontal-axis-bar-compare`, `horizontal-target-progress`, or `plain-metric` | The main answer is the difference value/rate versus baseline, target, peer, region, group, or rank, including positive/negative gap semantics. |

| `kpiSingleIndicatorLayoutMode` | Pair with `kpiCardPattern` | Use when |
| --- | --- | --- |
| `dropdown-sparkline-progress` | `horizontal-trend-compare` | The card has a compact period dropdown, a right-side sparkline, and a bottom target/progress footer. |
| `unit-toggle-ring-progress` | `horizontal-ring-progress` | The card switches display unit or rate basis, and a ring communicates bounded progress/completion. |
| `dropdown-minibar-progress` | `mini-bar-trend` or `horizontal-trend-compare` | The card has a period dropdown, mini bars, and a bottom target/progress footer without needing bar axes. |
| `grain-switch-minibar-progress` | `horizontal-grain-bar-switch` | The card has a `日/周/月` or similar local grain switch plus mini bars. |
| `dropdown-area-sparkline-progress` | `horizontal-trend-compare` | The card has a period dropdown and a small filled/soft sparkline for rate, retention, or revenue movement. |
| `scale-toggle-area-progress` | `horizontal-trend-compare` | The card switches value scale such as `元/万/亿` and keeps the evidence as a small area/sparkline. |
| `dropdown-gauge-progress` | `horizontal-ring-progress` | The card has a period dropdown and a semi-gauge for bounded status, threshold, or attainment. |

Selection order:

1. If the parent container is landscape, wide, or row-based and the line evidence needs visible axes, gridlines, target/reference lines, threshold bands, phase annotations, or dual-series comparison, choose `horizontal-axis-line-trend` only when `W >= 420px` and `H >= 260px`.
2. If the parent container is landscape, wide, or row-based and the evidence is ranked/time/category bar comparison with readable category labels, value labels, target lines, dual-series comparison, threshold warning, or category change-rate evidence, choose `horizontal-axis-bar-compare` only when `W >= 420px`, `H >= 260px`, and visible bars are `3-8`.
3. If the parent container is landscape, wide, or row-based and the evidence is relationship, distribution, outlier, threshold, or quadrant diagnosis with two numeric fields, choose `horizontal-axis-scatter-diagnostic` only when `W >= 420px`, `H >= 300px`, and the point-density strategy is declared.
4. If the parent container is landscape, wide, or row-based and the evidence is spatial distribution, regional target gap, point coverage, or geographic change, choose `horizontal-spatial-map-diagnostic` only when `W >= 460px`, `H >= 320px`, geography is the decision dimension, and the map resource/projection is declared.
5. If the card's main job is a side-by-side baseline judgment, choose `paired-comparison-diagnostic` only when both panes share metric definition, unit, period/grain, and comparable baselines, and when each pane can keep its minimum content box.
6. If the parent container is landscape, wide, or row-based and `W >= 360px`, choose a horizontal pattern when the supporting evidence can fit without becoming a full chart.
7. For horizontal cards, choose by evidence type: compact trend comparison -> `horizontal-trend-compare`; readable axis line -> `horizontal-axis-line-trend`; readable horizontal bars -> `horizontal-axis-bar-compare`; readable scatter diagnosis -> `horizontal-axis-scatter-diagnostic`; spatial evidence -> `horizontal-spatial-map-diagnostic`; paired baseline judgment -> `paired-comparison-diagnostic`; bounded ring or semi-gauge status -> `horizontal-ring-progress`; target bar -> `horizontal-target-progress`; lower-is-better status trend -> `horizontal-status-trend-compare`; local time-grain bars -> `horizontal-grain-bar-switch`; current/prior/target strip -> `horizontal-period-summary-strip`; percentage-point delta -> `horizontal-pp-assist-info`; threshold warning -> `horizontal-warning-status-band`.
8. If the card's main job is status, health, score, rating, risk, or bounded gauge judgment, select `kpiJudgmentCardPattern` before treating it as an ordinary KPI. Choose icon cards for categorical states, ring/gauge cards for bounded progress or score, threshold bullet cards for multi-band health, dimension breakdown for multi-factor health, and rating distribution for satisfaction/review evidence.
9. If the card's main job is target execution management, select `kpiGoalExecutionCardPattern` before treating it as an ordinary KPI, gauge, timeline, or target/actual chart. Choose attainment patterns for "达成率/超额达成", gap patterns for "差距/缺口/落后/超支", progress patterns for "计划进度 vs 实际进度", and milestone patterns for "阶段/节点/倒计时/里程碑".
10. If the card's main job is time-series analysis, select `kpiTimeSeriesCardPattern` before treating the line, bar, area, or forecast mark as an ordinary mini chart. Choose trend for overall movement, change for current-vs-baseline delta, YoY/MoM for dual baselines, cycle for period window/stage, volatility for fluctuation/stability, and forecast for future interval or predicted value.
11. If the card's main job is comparison analysis, select `kpiComparisonAnalysisCardPattern` before treating bars, radar, donut, table, map, or `VS` panes as ordinary chart variety. Choose direct comparison for same-metric values, group comparison for segment/group cohorts, competitor for named market players, benchmark for P50/P75/P90 or industry standards, and variance for signed gap value/rate.
12. If one wide card summarizes a business domain with `2-5` visible metrics, select `kpiOverviewCardPattern` before choosing a single-indicator layout. Use `lead-metric-comparison-sparkline-overview` for one dominant metric plus comparison/target/sparkline, `multi-metric-strip-progress-overview` for equal sibling metric cells, and `domain-metric-cluster-progress-overview` for a lead metric plus companion metrics without a full chart.
13. If the design is a peer grid of single-indicator cards, select `kpiSingleIndicatorLayoutMode` after the primary `kpiCardPattern`. Each card must keep one metric, one comparison, one evidence visual, and one target/progress footer.
14. If target/achievement is the main question and `target` plus `attainmentRate` exist but the card is portrait/narrow, choose `target-wave`.
15. If one card is the lead KPI and trend movement is business-critical, choose `highlight-line-trend`.
16. If recent period evidence matters but the card is not the lead KPI, choose `mini-bar-trend`.
17. Otherwise choose `plain-metric`.

## Shared Anatomy

Every pattern keeps the same decision structure:

```text
metric label -> primary value -> comparison context -> target/status/trend evidence -> exact-value disclosure
```

Required slots:

| Slot | Rule |
| --- | --- |
| Metric label | Short business noun, normally top-left. Do not use generic labels such as "Revenue" unless the domain uses that exact term. |
| Primary value | Strongest visual anchor. It must remain readable before any decorative or evidence layer is tuned. |
| Unit | Close to the value; use display unit scaling for long currency values. |
| Period/scope | Visible or discoverable through tooltip/header context. |
| Comparison | YoY/MoM/baseline/status with signed value and semantic icon/color. |
| Target/status | Use progress, attainment, gap, or threshold wording; do not force target into up/down semantics. |
| Evidence visual | Wave, mini bars, or mini line only when it proves the KPI judgment. |
| Disclosure | Tooltip, focus, drawer, or detail route for formula, exact trend points, target, source, and freshness. |

## Pattern: `plain-metric`

Purpose: lightweight KPI or peer cards in a KPI strip.

Minimum viewport:

- Small: `W >= 220px`, `H >= 120px`.
- Standard: `W >= 260px`, `H >= 140px`.

Permanent content:

- Metric label.
- Primary value + unit.
- One priority comparison, or two compact comparison chips when width permits.
- Target/status only when it does not push the value anchor off center.

Fallback:

- If two comparisons do not fit, keep the comparison most relevant to the current decision and move the other to tooltip.
- If the target text is long, show `达成 87.6%` or `差 124万` and expose full target in tooltip.

## Pattern: `target-wave`

Purpose: target completion, budget consumption, quota attainment, inventory usage, SLA attainment, or another bounded progress/status metric.

Required contract:

```text
value
target
attainmentRate = value / target
targetLabel
targetFormula or definition reference
targetDirection: good-when-higher | good-when-lower | bounded-range
```

Layout:

- Keep the primary value in the upper or central value zone.
- Put target and attainment rate in the lower evidence zone.
- The wave/progress backdrop sits behind the lower evidence zone or bottom third; it cannot reduce text contrast.
- Wave height, progress fill, or area level must be derived from `attainmentRate`, clamped to the declared min/max.

Visual rules:

- Use soft brand tint or semantic progress color. Do not use a random decorative wave.
- The progress shape is evidence, not a hero illustration.
- If `attainmentRate` is over target, show overflow through status text, marker, or capped fill plus tooltip; do not let the wave fill obscure the value.
- If `target` is zero/null/missing, do not render the wave. Use `plain-metric` with an insufficient-target state.

## Pattern: `mini-bar-trend`

Purpose: show recent period volatility under a KPI without turning the card into a full chart.

Required contract:

```text
trendSeries: ordered category/time rows
valueField
categoryField
seriesGrain
latestPoint
tooltipPayload
```

Layout:

- Reserve the bottom `28-40%` of the card for the mini bar band.
- Hide axes and permanent data labels by default.
- Keep bars within the evidence band and away from comparison/target text.
- Use one bar series unless a target/actual mini comparison is explicitly needed and still fits.

Data and interaction:

- `trendSeries.length >= 3` by default.
- For `3-16` points, bars may render directly.
- For `17-30` points, sample labels away and use tooltip for exact values.
- For more than `30` points, use a full chart, drawer, or aggregation instead of a mini bar card.

Fallback:

- If the mini bars crowd the value or comparisons, remove the chart first and keep the KPI evidence in tooltip/detail.
- If exact period comparison is the user's task, use a full bar chart block instead of this card.

## Pattern: `highlight-line-trend`

Purpose: one lead KPI card that needs stronger visual memory while still reading as a business report component.

Required contract:

```text
trendSeries
valueField
timeField
latestPoint
comparison values
target or threshold when the line is judged against a goal
```

Layout:

- Use a stronger card surface token only for one lead card or a small number of primary cards.
- Keep the line in the lower half or lower third. It must not pass through the primary value or comparison text.
- Reserve a clear latest/attainment/status value in a stable lower-right or footer zone when used.
- The line is a sparkline: hide axes by default, keep exact points in tooltip.

Visual rules:

- Use approved dark/brand-emphasis tokens. Do not introduce unrelated neon, glass, glow, or oversized radius.
- Line stroke should be thin enough to remain evidence, not decoration.
- Avoid smooth all-up fake data. Mock data should include realistic bends, flat segments, or dips when the domain allows it.
- Use this pattern sparingly. A page full of lead cards destroys hierarchy and becomes template polish.

Fallback:

- If the dark/emphasis surface harms readability or conflicts with the page baseline, use `mini-bar-trend` or `plain-metric`.
- If the line needs axes, labels, target bands, or anomaly markers, move it to a full line chart block.

## Landscape KPI Card Patterns

Use these patterns when a KPI card is intentionally horizontal, such as a first-row management indicator, an operations console summary card, a table/detail header card, or a wide dashboard peer card.

These designs feel strong and not AI-generated because each card follows a clear decision chain:

```text
metric name -> primary value -> comparison/status -> one evidence visual -> detail/action path
```

The visual evidence is not decoration. The line, ring, progress track, mini bars, comparison strip, percentage-point badge, or warning band must be derived from the KPI contract.

Axis-line diagnostic KPI cards add one more reason they feel designed: they spend enough height on a real chart body, so the y-axis scale, x-axis period, target/reference line, threshold zone, phase mark, or comparison series can be read without competing with the headline value. This makes the card look like a deliberate analytical module instead of a decorative KPI tile with a random sparkline.

Axis-bar diagnostic KPI cards feel designed for a similar but more scan-oriented reason: the card uses horizontal bars for ordered comparison, so labels stay left, bar lengths stay middle, and exact values or change rates stay right. The visual rhythm supports reading and ranking rather than decoration, and target/threshold marks sit on the same quantitative axis as the bars.

Scatter diagnostic KPI cards feel designed because the dots are not random garnish: x/y axes name two business measures, the point cloud shows distribution, reference lines or quadrants turn the cloud into a decision, and sparse labels/tooltip keep exact object evidence available.

Spatial map diagnostic KPI cards feel designed because geography is the evidence layer. A muted basemap, bounded projection, visualMap/legend, and selective labels make spatial differences readable without turning the card into a decorative map.

Paired comparison diagnostic KPI cards feel designed because the two panes are intentionally comparable. The central `VS` rail, mirrored pane geometry, and bottom conclusion strip create a clear judgment path instead of two unrelated numbers placed side by side.

KPI overview cards feel designed because they compress a business-domain answer into one disciplined horizontal scan: domain title/control -> lead or sibling metrics -> comparison context -> target/progress -> one small evidence visual or explicit disclosure path. The card does not become a chart collage; every cell has a declared role and shared baseline.

Single-indicator KPI grid cards feel designed because the repetition is disciplined: every card uses the same metric grammar, but the evidence visual changes only when the metric needs it. Index number, title/help, local control, value, comparison, evidence visual, target text, and progress footer form a predictable scan path, so a page can contain many KPIs without becoming a random chart collage.

Common landscape anatomy:

| Zone | Rule |
| --- | --- |
| Header row | Title top-left, one local control top-right. The control is a segmented capsule or compact dropdown, never a second toolbar. |
| Primary value zone | Left or center-left. It owns the largest text and keeps value + unit together. |
| Comparison/status zone | Sits directly under or beside the value. It names the baseline, direction, and semantic meaning. |
| Auxiliary visual zone | Right side or bottom band. It must explain the judgment: trend, ring, target track, status icon, or bar strip. |
| Evidence/footer band | Optional. Use for prior/current/target cells, warning text, previous-period value, or auxiliary mini bars. |
| Exact-value path | Tooltip, focus, detail drawer, or linked full chart/table. |

Minimum useful landscape sizes:

| Tier | Width | Height | Use |
| --- | ---: | ---: | --- |
| Compact row | `360-420px` | `128-160px` | Value, one comparison, one compact icon/progress/status; chart-like evidence usually hidden. |
| Standard landscape | `420-560px` | `180-240px` | Full horizontal KPI card with local control and one auxiliary evidence visual. |
| KPI overview card | `720-960px` | `220-320px` | One business-domain card with `2-5` metrics, local control, comparison/target cells, and optional sparkline. |
| KPI judgment card | `360-460px` | `240-360px` | One status/health/rating/gauge judgment, one semantic hero visual, comparison strip, and footer evidence. |
| KPI goal execution card | `360-520px` | `240-360px` | One target attainment, gap, progress, or milestone execution judgment with actual/target/gap/progress fields, comparison strip, and deadline/footer evidence. |
| Single-indicator grid card | `360-460px` | `220-320px` | One metric, one comparison, right/bottom mini evidence, and bottom target/progress footer in a peer KPI grid. |
| Axis-line diagnostic | `420-560px` | `260-340px` | KPI headline plus a readable ECharts line body with axes, target/reference/threshold/dual-series evidence. |
| Axis-bar diagnostic | `420-560px` | `260-340px` | KPI headline plus readable horizontal bars with labels, value column, target/reference/threshold/dual-series evidence. |
| Axis-scatter diagnostic | `420-560px` | `300-360px` | KPI headline plus readable scatter body with axes, reference/trend/threshold/quadrant evidence. |
| Spatial-map diagnostic | `460-640px` | `320-380px` | KPI headline plus map body with preserved geography, visualMap/legend, and selective labels. |
| Paired comparison diagnostic | `420-560px` | `260-340px` | Two comparable panes, central `VS` rail, optional mini evidence, and bottom conclusion strip. |
| Wide banner | `560-760px` | `160-240px` | Split value/evidence zones; can show a larger trend, ring, strip, or warning band. |

Landscape slot minimums:

- Title/control row: `28-40px`.
- Primary value column: `140-220px` wide.
- Auxiliary visual zone: at least `96x72px`; ring/progress/gauge-like visuals need `108x96px`.
- Bottom evidence band: `44-68px` when present.
- Mini line/bar evidence: plot or glyph band `48-72px`; do not render axis labels inside a landscape KPI card.
- Axis-line evidence: chart body `>=180px`, plot height `>=130px`, y-axis label band `36-56px`, x-axis label band `28-40px`; if any axis or threshold label is visible, do not classify it as a sparkline.
- Axis-bar evidence: chart body `>=180px`, plot height `>=140px`, category label column `44-88px`, value/change-rate column `48-96px`, x-axis band `28-40px`, and per-bar row height `>=22px`; if value labels or target lines are visible, do not classify it as a mini bar strip.
- Axis-scatter evidence: chart body `>=200px`, inner plot height `>=160px`, y-axis label band `40-60px`, x-axis label band `32-48px`, point radius `3-6px`, permanent labels `<=6`, and point count/density strategy declared.
- Spatial-map evidence: map body `>=220px`, map viewport `>=180px` on the shorter side, legend or side summary budget `72-140px`, and projection/aspect ratio preserved through a measured fit box.
- Paired comparison evidence: each pane `>=140px` wide, central `VS` rail `32-44px`, optional mini evidence `>=72px` high, and bottom conclusion band `36-52px`.
- Linear target progress track: at least `200x24px` for track + marker + min/max labels.

### KPI Overview Card Patterns

Use this mode set when a single wide card answers a business-domain overview question. It differs from a single-indicator KPI card in two ways: the card may carry `2-5` metrics, and the title names the domain/topic rather than only the metric.

```text
index/section marker -> domain title -> one local control group -> lead/sibling metrics -> comparison/target evidence -> compact visual or detail path
```

These cards feel strong and not AI-generated because the repetition is purposeful. Icon tiles, dividers, progress tracks, and sparklines are subordinate to the metric hierarchy; they do not create random decoration. Each metric has a named baseline, unit, and target/status path, so the user can read a domain summary without guessing what the visuals mean.

Layout modes:

| `kpiOverviewCardPattern` | Anatomy | Required data |
| --- | --- | --- |
| `lead-metric-comparison-sparkline-overview` | icon tile, lead metric, `1-2` comparison cells, target/attainment cell, right sparkline | lead value, unit, `1-2` comparisons, target, attainment rate, ordered trend series |
| `multi-metric-strip-progress-overview` | `3-5` equal metric cells with vertical dividers, each with comparison and progress | metric list, value/unit/comparison per metric, target/attainment per metric when progress is visible |
| `domain-metric-cluster-progress-overview` | icon tile, lead metric, `2-3` companion metrics, one target/progress summary | lead value, companion metric values, comparison fields, target/attainment or summary status |

Minimum and slot budget:

- Minimum outer size: `720x220`; standard size: `760-960px` wide and `240-320px` high.
- Header row: `36-48px`, with index/section marker optional, domain title left, one local control group plus optional overflow menu right.
- Icon tile: `64-92px` square when used; hide before shrinking metric cells.
- Lead metric zone: `180-260px` wide; primary value remains the strongest glyph.
- Metric cell zone: each metric cell `>=128px` wide and `>=112px` high; equal sibling cells share value, comparison, target, and progress baselines.
- Comparison cell: `112-160px` wide, with label, signed value, baseline helper, and tooltip payload.
- Target/progress cell: `150-200px` wide; progress track `>=120px`; target and attainment values remain visible or discoverable.
- Sparkline/evidence fit box: `120x56px` minimum, `160x72px` preferred; no axes inside this overview card.

Rules:

- One overview card answers one domain or management topic, such as sales, users, operations, finance, production, quality, inventory, or delivery.
- Keep visible metrics to `2-5`. More than `5` metrics require a metric switch, tabs, split cards, or a Micro Dashboard Card.
- The visible local control is scoped to this card only. Period switches change the metric and evidence dataset; unit/scale switches change display units; metric switches change which bounded metric set is visible.
- The card has at most one compact evidence visual. A sparkline, small bars, icon tile, or progress track may appear, but not a combination that competes with the metrics.
- Vertical dividers separate sibling metric cells only when the cells share height and baselines. Do not draw divider lines through values, badges, or progress tracks.
- Theme color follows domain semantics or project tokens: blue for sales/target, green for growth/quality/improvement, purple for finance/efficiency only when approved. Color never substitutes for labels, units, or target definitions.
- Icon tiles are meaningful only when they identify the domain. They are soft anchors, not illustrations; remove them first when the card is tight.
- Mock data must include at least one non-perfect comparison, target gap, or weaker companion metric when business reality allows it. An all-up, all-green overview card is suspect unless source evidence proves it.

Fallback:

1. Collapse segmented local control to a selected-value dropdown.
2. Hide overflow menu or definition icon if actions are secondary.
3. Hide icon tile or decorative domain mark.
4. Move secondary baseline helper text to tooltip while keeping comparison values.
5. Reduce visible metrics to Top `3` by priority and move the rest to drawer/detail.
6. Hide sparkline evidence before shrinking metric values.
7. Split into separate KPI cards, a full chart/table block, or a Micro Dashboard Card when the overview needs more than `5` metrics or more than one evidence visual.

### KPI Judgment Card Patterns

Use this mode set when one card answers a bounded judgment question: "是否正常", "是否健康", "是否优秀", "是否达标", "风险多高", "评分如何", or "处在哪个状态". These cards are still KPI cards, not generic icon tiles or chart blocks. The hero visual is accepted only when it is backed by a status dictionary, score range, threshold bands, target, or rating distribution.

```text
index/title/control -> semantic hero visual -> value/status label -> comparison strip -> footer evidence/disclosure
```

These cards feel designed and not AI-generated because the visual grammar follows the metric semantics. A check icon means categorical normality, a ring means bounded completion or score, a bullet bar means threshold judgment, dimension bars explain a composite health score, rating bars explain a satisfaction score, and a gauge makes target/range status visible. The repeated comparison strip and footer keep the cards auditable instead of merely polished.

Pattern modes:

| `kpiJudgmentCardPattern` | Hero visual | Required data |
| --- | --- | --- |
| `semantic-status-icon-card` | domain icon inside soft semantic disk/tile | status field, status dictionary, latest state, reason/detail path, optional status duration |
| `progress-status-ring-card` | circular progress/ring with center value or percent | value/progress, min/max or denominator, target, status label, due date or completion denominator |
| `health-score-ring-card` | circular score ring with health level | score field, score range, level dictionary, comparison fields, update/freshness |
| `health-threshold-bullet-card` | horizontal threshold/bullet bar with pointer | value/score, threshold band fields, target/min/max, direction, level labels |
| `health-dimension-breakdown-card` | overall score plus `3-5` dimension chips/bars | dimension dataset, dimension name, score/value, status/level per dimension |
| `rating-score-summary-card` | star, badge, hex, shield, or score tile plus label | score/rating, score range, level dictionary, comparison/gap, sample/evidence count |
| `rating-distribution-card` | rating distribution bars or share rows | distribution fields, total sample count, score/rating value, denominator-zero policy |
| `semicircle-gauge-target-card` | semi-gauge arc with ticks and target marker | value, min/max, target or threshold, direction, status color rule, overflow/clamp behavior |

Minimum and slot budget:

- Minimum outer size: `360x240`; standard size: `400-460px` wide and `300-360px` high.
- Header row: `32-44px`, including optional index, title/help, and one local control. Collapse the control before shrinking the hero visual.
- Hero zone: `96-160px` high. Semantic icons need `72-96px` square; rings need `136-180px` square; semi-gauges need `180x112px` minimum; threshold bars need `220x28px` minimum; dimension/rating rows need `4-6` visible rows at `20-28px` each.
- Judgment label/value zone: status/level copy sits beside or below the hero and must stay close enough to read as one judgment. The label is not decorative copy; it names the business state.
- Comparison strip: `54-72px`, usually `3` cells (`同比`, `环比`, `目标` or equivalent). Use vertical dividers only when cells share baselines.
- Footer evidence band: `32-52px`, for last check time, source/freshness, target definition, due date, sample count, risk count, progress text, or a compact sparkline. It cannot introduce a second full chart.

Rules:

- One card answers one judgment. Do not combine status icon, ring, gauge, dimension bars, and sparkline in the same card.
- Declare `judgmentKind`, `judgmentDirection`, `judgmentScoreRange`, `judgmentBands` or status dictionary, and the main `judgmentStatusField` or `judgmentScoreField`.
- Colors follow business meaning: green healthy/success/improved, blue progress/neutral information, orange pending/warning, red high risk/failure, purple only for approved domain semantics such as user/payment/product theme. Color never replaces label text.
- The visible comparison strip is capped at `3` cells. Additional comparisons move to tooltip, detail drawer, or a linked full analysis block.
- Ring and gauge cards must declare min/max, clamp/overflow behavior, target/threshold, and center value formatting. Unbounded metrics use a plain KPI or trend card instead.
- Health and rating cards must declare score ranges and level names, such as `优秀/良好/中等/较差`, not rely on raw color.
- Dimension breakdown cards show `3-5` dimensions by default. More dimensions require Top N, drawer, or a full table/radar chart.
- Rating distribution cards show at most `5` rating buckets permanently. Distribution percentages must reconcile to the visible sample count.
- Footer evidence is mandatory unless the surrounding block provides source/freshness and exact-value path.

Fallback:

1. Collapse segmented local control to a dropdown or inherited page filter.
2. Hide optional index/help/overflow menu.
3. Move secondary helper copy to tooltip while keeping status/level text.
4. Reduce comparison strip to the one most decision-relevant baseline.
5. Reduce dimension rows to Top `4` or rating rows to the defined rating scale only.
6. Replace ring/gauge with status chip + value when the hero fit box fails.
7. Split to a full gauge, radar, table, or detail drawer before accepting a squeezed judgment card.

### KPI Goal Execution Card Patterns

Use this mode set when one card answers a target execution question rather than a generic KPI question. The card must prove one of four execution jobs:

```text
target attainment -> gap/variance -> progress against plan -> milestone/deadline evidence
```

These cards feel designed and not AI-generated because the visual grammar follows the management contract. The ring, semi-gauge, target bar, dot strip, red deficit panel, paired bars, stage stepper, or milestone timeline is not decorative variety; it is the shortest visual form for actual value, target value, gap, planned progress, actual progress, remaining work, due date, and status.

Pattern modes:

| `kpiGoalExecutionCardPattern` | Hero visual | Required data |
| --- | --- | --- |
| `attainment-ring-summary-card` | ring/donut with center attainment rate | actual value, target value, attainment rate, remaining target, target formula |
| `attainment-gauge-deadline-card` | semi-gauge/ring plus due-status label | actual value, target value, attainment rate, deadline, due status, over/under target handling |
| `attainment-linear-target-card` | linear progress track with marker and min/max labels | actual value, target value, attainment rate, target marker, direction, optional scale min/max |
| `attainment-unit-progress-card` | dot/person/order strip or bounded count progress | actual count, target count, completion count, remaining count, item denominator |
| `gap-gauge-deficit-card` | deficit gauge/ring or red deficit callout | actual value, target value, gap value, gap rate, target miss status, direction |
| `gap-target-actual-compare-card` | target-vs-actual bars, budget/actual rows, or compact VS | actual value, target value, gap value, gap rate, baseline labels, shared unit/grain |
| `progress-plan-actual-card` | plan vs actual progress bars or progress delta strip | actual progress, planned progress, target progress, progress delta, remaining time, forecast status |
| `milestone-timeline-card` | stepper, phase cards, timeline, or cumulative milestone line | milestone dataset, milestone name, status, date, current milestone, total milestones, due date |

Minimum and slot budget:

- Minimum outer size: `360x240`; standard size: `400-520px` wide and `280-360px` high.
- Header row: `32-44px`, including optional index, title/help, local period/target control, and overflow menu. Collapse the control before shrinking the execution visual.
- Execution hero zone: `96-160px` high. Rings need `136x136px`; semi-gauges need `180x112px`; linear target bars need `220x24px` including marker and labels; paired bars/VS panes need each pane `>=120px` wide; milestone steppers need `3-7` visible nodes with node gap `>=52px`; timeline bodies need `>=240x80px`.
- Target/actual/gap summary zone: `40-72px`, with actual, target, gap, remaining target, or progress delta. Values must use the same unit/scale and remain inspectable.
- Comparison strip: `54-72px`, usually `2-4` cells such as `同比`, `环比`, `剩余目标`, `预计达成`, `剩余时间`, or `风险等级`.
- Footer evidence band: `32-52px`, for target completion date, remaining days, schedule status, source/freshness, next milestone, or exact-value/detail route.

Rules:

- One card answers one execution question. Do not combine ring, gauge, bar chart, dot strip, timeline, and detailed table in the same card.
- Declare `goalExecutionKind`, `goalDirection`, actual field, target field, and either attainment/gap/progress/milestone fields according to the selected pattern.
- `attainmentRate = actual / target` unless the business formula declares a different denominator. If lower-is-better or bounded-range applies, declare the direction and formatter.
- `gapValue = actual - target` or `target - actual` according to `goalDirection`; do not infer red/green from raw sign without business semantics.
- Deadline and remaining-time fields are mandatory when the visible copy mentions `提前`, `剩余`, `逾期`, `预计完成`, or `目标完成时间`.
- Planned-vs-actual progress cards must declare both planned progress and actual progress. A single progress value belongs to attainment, not plan-vs-actual progress.
- Milestone cards show `3-7` visible milestones by default. More milestones require horizontal scroll, phase grouping, condensed current-window display, drawer/detail, or a full timeline/Gantt.
- Red is reserved for target miss, deficit, lag, overspend, risk, or overdue. Orange is attention/overachievement/warning. Green is achieved/on-track/improved. Blue is neutral execution/progress. Purple only appears when the domain theme is approved.
- Overachievement must be labeled explicitly, such as `超额达成`, `已超前`, or `超过目标`. Do not silently cap all visuals at 100% without tooltip/detail explaining the overflow.
- Mock data should include non-perfect cases: remaining target, lagging progress, overachievement, upcoming deadline, or one pending milestone when business reality allows it.

Fallback:

1. Collapse segmented local control to dropdown or inherit the page period.
2. Hide optional index, help icon, domain illustration, or overflow action.
3. Reduce comparison strip to the two most decision-relevant cells.
4. Replace ring/semi-gauge/dot strip with a linear target progress track when the hero fit box fails.
5. Collapse milestone nodes to current + previous + next, with full list in drawer/detail.
6. Move secondary deadline/source copy to tooltip while keeping due status or remaining time visible.
7. Split to a full target/actual chart, progress table, timeline, Gantt, or detail drawer before accepting a squeezed execution card.

### KPI Time-Series Analysis Card Patterns

Use this mode set when one card answers a time-series analysis question rather than a generic KPI question. The card must prove one of six temporal jobs:

```text
trend movement -> change from baseline -> YoY/MoM comparison -> cycle/period state -> volatility/stability -> forecast/uncertainty
```

These cards feel designed and not AI-generated because every visual element has a statistical or temporal job. The line, area fill, grouped bars, period ring, volatility badge, comparison cells, dashed forecast, or confidence band is not decorative variety; it encodes ordered time, baseline choice, cycle window, volatility formula, or forecast uncertainty.

Pattern modes:

| `kpiTimeSeriesCardPattern` | Main evidence visual | Required data |
| --- | --- | --- |
| `trend-line-target-card` | line/area trend with latest point, optional target/reference | ordered time series, x field, y field, period grain, latest value, trend direction, optional target/reference/threshold |
| `change-baseline-delta-card` | current series vs baseline series, delta badge, or recent bars | current value, baseline value, baseline label, delta value, delta rate, comparison period, current series, optional baseline series |
| `yoy-mom-comparison-card` | trend or bars plus visible YoY/MoM chips and baseline cells | current value, YoY value/rate, MoM value/rate, prior-year comparable value, prior-period value, baseline semantics |
| `cycle-period-progress-card` | cycle progress ring, period phase badge, line/bars inside selected period | cycle grain, period start/end, current period index, total periods, period progress, phase/status, period target or attainment when visible |
| `volatility-stat-card` | jagged line/area with volatility level badge and stat footer | ordered series, volatility formula, volatility amplitude/rate, volatility level, max value, min value, standard deviation, threshold bands |
| `forecast-interval-card` | actual solid line plus forecast dashed line/bars and confidence band | actual series, forecast series, forecast start/end, forecast horizon, predicted value, confidence interval lower/upper, model/status field |

Minimum and slot budget:

- Minimum outer size: `360x240`; standard size: `400-520px` wide and `280-360px` high.
- Header row: `32-44px`, including optional index, title/help, local grain/period control, and overflow menu. Collapse the control before shrinking the chart evidence.
- Value and comparison zone: `56-88px`, with primary value, unit, period/baseline label, and `1-2` comparison chips. If the value line wraps, move the secondary baseline to tooltip/detail before shrinking the number.
- Time-series evidence zone: `112-176px`. Axis-visible line/bar evidence needs chart body `>=120px` and plot height `>=86px`; compact sparkline evidence needs fit box `>=160x64`. Forecast bands need at least `40px` future-region width after the forecast start.
- Footer evidence band: `44-72px`, usually `2-4` cells for max/min/stddev, prior-year/prior-period values, period target, forecast range, confidence interval, peak date, or exact-value route.
- Local legend/chip row: `18-28px` when actual/baseline/forecast series are visible. Hide series legend only when line styles and tooltip labels remain unambiguous.

Rules:

- One card answers one temporal question. Do not combine volatility, forecast, cycle phase, YoY/MoM, and target attainment in the same small card unless lower-priority details move to tooltip/detail.
- Every time-series card declares ordered time grain, x field, y field, latest period, period scope, and tooltip payload for exact points.
- Trend and change cards must name the baseline: previous period, prior-year comparable period, selected baseline, target, or forecast. A percentage without a named denominator fails.
- YoY/MoM cards must keep YoY and MoM as separate fields and labels; do not merge both into one generic "growth" value.
- Cycle cards must declare `cycleGrain`, period start/end, current period index, total periods or phase count, and period progress. A cycle badge without a cycle window is decorative.
- Volatility cards must declare the formula, such as `standardDeviation / average * 100%`, and threshold bands for low/medium/high volatility. Max/min/stddev values in the footer must come from the same filtered series.
- Forecast cards must distinguish actual from forecast through line style, fill, or bar style, and must expose forecast start/end, horizon, predicted value, and confidence interval or uncertainty status.
- Direction semantics are metric-specific. For costs, defects, response time, inventory days, and bad rates, lower can be better; do not infer green/red from positive or negative signs without `temporalDirection`.
- Use stable but non-perfect mock data: slight noise, plateaus, drops, spikes, baseline differences, forecast uncertainty, and at least one non-good state when realistic. Smooth monotone lines across every card look synthetic.
- Dense daily series should sample or aggregate to the visible grain when the plot would exceed `60` points; keep exact values in tooltip/detail.

Fallback:

1. Collapse segmented grain/period controls to a dropdown or inherit the page period.
2. Hide optional index, help icon, domain icon, or overflow action.
3. Reduce footer evidence to the two most decision-relevant cells.
4. Move secondary baseline, phase copy, or forecast method text to tooltip/detail.
5. Hide ordinary point markers and keep only latest/peak/forecast-start markers.
6. Downgrade axis-visible line/bar evidence to a compact sparkline only when exact values remain available.
7. Split to a full line/bar/forecast chart, volatility detail table, cycle timeline, or drawer before accepting a squeezed temporal card.

### KPI Comparison Analysis Card Patterns

Use this mode set when one card answers a comparison analysis question rather than a generic KPI or chart question. The card must prove one of five comparison jobs:

```text
direct value comparison -> group/segment comparison -> competitor position -> benchmark position -> variance/gap diagnosis
```

These cards feel designed and not AI-generated because every visual element is anchored to a declared comparison contract. The donut, grouped bars, multi-line trend, radar, NPS scale, benchmark ruler, variance gauge, comparison table, or map is not decorative variety; it encodes comparable subjects, group membership, competitor role, benchmark source, percentile/rank, or signed gap formula.

Pattern modes:

| `kpiComparisonAnalysisCardPattern` | Main evidence visual | Required data |
| --- | --- | --- |
| `direct-value-compare-card` | side-by-side values, dual line/bar series, map/table compare, or small comparison matrix | primary subject, comparison subject, shared metric definition, unit, grain, value fields, baseline label, delta value/rate |
| `group-segment-compare-card` | grouped bars, stacked bars, multi-line group trend, ranked segment bars, or segment summary tiles | group/segment field, comparable metric fields, shared period/filter scope, group sort rule, group count, per-group value and delta |
| `competitor-position-card` | market share donut, competitor ranking bars, multi-series trend, radar profile, NPS/score scale, channel table, or KPI matrix | primary product/company role, competitor roles, industry average or market total when used, metric list, competitor values, rank/share/delta fields |
| `benchmark-position-card` | benchmark ruler, peer ranking bars, P50/P75/P90 markers, standard-value bars, gauge-to-benchmark, or benchmark trend | benchmark source, benchmark value(s), percentile/rank fields, current value, gap to benchmark, benchmark label and validity period |
| `variance-gap-card` | signed gap summary, actual-vs-comparison bar, variance table, gap gauge, ranked variance rows, or difference trend | actual/current field, comparison/target/baseline field, gap value, gap rate, direction semantics, signed color rule, reconciliation total when tabular |

Minimum and slot budget:

- Minimum outer size: `360x240`; standard size: `400-560px` wide and `280-380px` high.
- Header row: `32-44px`, including optional index, title/help, local comparison scope control, period switch, or overflow menu. Collapse the control before shrinking comparison evidence.
- Value/comparison summary zone: `56-92px`, with primary value, comparison label, role labels, rank/share/gap or delta chip. If subject labels wrap, shorten labels and expose full names in tooltip/detail.
- Comparison evidence zone: `112-180px`. Axis-visible bars/lines need chart body `>=140px` and plot height `>=92px`; radar needs a `150x150px` circular fit box; donut/share evidence needs a `128x128px` circular fit box; benchmark ruler needs `220x40px`; NPS/score scale needs `220x32px`; comparison table preview needs at least `3` rows and `3-6` columns.
- Footer evidence band: `44-72px`, usually `2-4` cells for rank, benchmark, gap, market total, competitor count, sample count, or exact-value route.
- Legend/role row: `18-28px` when multiple subjects, groups, competitors, or benchmark roles are visible. Hide legend only when role labels remain directly visible.

Rules:

- One card answers one comparison question. Do not combine competitor ranking, group trend, benchmark P90, and target gap in the same small card unless one is primary and the rest move to tooltip/detail.
- Every comparison card declares comparable subject grain, metric definition, unit, period/grain, filter scope, comparison role labels, and exact-value tooltip/detail payload.
- Direct comparison requires the compared sides to share metric definition, unit, denominator, and period. If definitions differ, use a metric matrix or explanation card rather than a visual `VS`.
- Group comparison requires a deterministic group sort: chronological, descending value, ascending risk, business order, or selected-priority order. Mock array order is not a valid sort.
- Competitor comparison must distinguish `primary`, `competitor`, `peer`, `industry-average`, and `market-total` roles. The primary product/company may be highlighted, but competitor geometry must remain comparable.
- Benchmark cards must name the benchmark source, such as industry average, P50, P75, P90, peer Top N, standard value, best practice, or selected baseline. A benchmark marker without source and period is decorative.
- Variance cards must declare `gapValue` and `gapRate` formulas plus direction semantics. Red/green follows business meaning, not raw sign; cost overrun and defect reduction invert ordinary positive/negative coloring.
- Radar and multi-dimensional competitor cards require a shared normalized scale. Raw mixed units cannot be plotted directly as comparable dimensions.
- Tables used inside these cards are evidence previews, not full audit tables. If exact comparison across many rows/metrics is the main task, split to a full table or matrix block.
- Use realistic comparison data: uneven gaps, one weak group, one competitor lead, one benchmark miss, or one negative variance when the domain allows it. Perfectly balanced groups and all-green comparisons look synthetic.

Fallback:

1. Collapse comparison scope, period, or metric segmented controls to a dropdown or inherit page filters.
2. Hide optional index, help icon, domain icon, or decorative rank badge.
3. Reduce visible subjects/groups to Top `4-5` plus `其他`, or show primary + Top competitors.
4. Move secondary metric dimensions, long competitor names, or benchmark definitions to tooltip/detail.
5. Convert radar/donut/gauge-like evidence to bars or table rows when circular geometry cannot pass its fit box.
6. Reduce footer evidence to the two most decision-relevant facts.
7. Split to a full comparison chart, benchmark table, metric matrix, detail table, or drawer before accepting a squeezed comparison card.

### Pattern: `lead-metric-comparison-sparkline-overview`

Use for sales, user growth, order, production, or finance overview cards where one lead metric anchors the decision and the remaining content explains how it compares, whether it reaches target, and how it moves.

Rules:

- Lead metric sits after the domain icon or at the first metric position. It owns the largest number.
- Comparison cells (`同比`, `环比`, `较上期`, `较目标`) share label and value baselines.
- Target completion cell includes target value and attainment/progress. Do not show a progress bar without target and denominator.
- The right sparkline is secondary. It shows direction and latest point; exact period points live in tooltip/detail.

### Pattern: `multi-metric-strip-progress-overview`

Use when the card needs equal sibling metrics, such as visits, conversion, average order value, and order count in one operations overview.

Rules:

- Use `3-5` equal columns. Each column has metric label/help, value+unit, comparison, target/attainment text, and optional progress.
- Values align by baseline across columns; progress tracks align by footer baseline.
- Keep column titles short. If a title needs more than two lines, abbreviate and disclose the full definition.
- If one metric needs a chart while siblings do not, either make it the lead overview pattern or split to a chart card.

### Pattern: `domain-metric-cluster-progress-overview`

Use when the domain card has one lead metric and several companion metrics, such as finance overview with revenue, gross margin, net profit, and target completion.

Rules:

- Lead metric and icon tile form the left anchor. Companion metrics read left-to-right by business priority.
- Use one unit/scale switch when financial or count values share a scale; do not create per-metric controls.
- Companion metrics may omit progress tracks when the target summary already owns the progress evidence.
- Keep one target/progress summary visible when the card is used for management review; otherwise provide a detail route.

### Single-Indicator KPI Grid Layout Modes

Use this mode set for pages like a KPI overview grid where every card carries exactly one metric. The card can vary its evidence visual, but the reading grammar stays fixed:

```text
index -> metric title/help -> local period/unit control -> primary value -> semantic comparison -> one evidence visual -> target + attainment footer
```

These cards feel strong because the style is not decorative variety. The small chart changes by metric semantics: sparkline for trend, mini bars for period distribution, ring for bounded completion, area sparkline for rate movement, and semi-gauge for threshold/status. The bottom target/progress footer anchors the card in a measurable goal, so the reader does not stop at a pretty number.

Layout modes:

| `kpiSingleIndicatorLayoutMode` | Evidence visual | Local control | Required data |
| --- | --- | --- | --- |
| `dropdown-sparkline-progress` | right-side sparkline with latest point | compact period dropdown | value, comparison, trend series, target, attainment rate |
| `unit-toggle-ring-progress` | right-side ring/donut progress | 2-option unit/rate toggle | bounded value or rate, min/max or target, attainment rate |
| `dropdown-minibar-progress` | right-side or lower-right mini bars | compact period dropdown | ordered bar series, selected/latest period, target, attainment rate |
| `grain-switch-minibar-progress` | right-side mini bars | `2-4` option grain segmented control | grain options, ordered series per grain, selected grain |
| `dropdown-area-sparkline-progress` | soft filled sparkline/area | compact period dropdown | ordered trend series, comparison, target, attainment rate |
| `scale-toggle-area-progress` | soft filled sparkline/area | value scale segmented control such as `元/万/亿` | value, scale options, trend series in raw unit, formatter contract |
| `dropdown-gauge-progress` | right-side semi-gauge | compact period dropdown | min/max, value, target/threshold, attainment or status rate |

Minimum and slot budget:

- Minimum outer size: `360x220`; standard grid size: `400-460px` wide and `260-320px` high.
- Header row: `32-44px`, including optional light index number `20-28px`, title/help, and one local control.
- Value band: `64-92px`; primary numeral should be the strongest glyph and normally occupies `22-30%` of card height.
- Comparison row: `20-28px`, directly below the value, with signed color semantics based on metric direction.
- Evidence visual fit box: at least `112x72px`; ring or semi-gauge needs `116x96px`; mini bars/sparkline need `120x56px`.
- Footer target/progress band: `44-60px`, with target text left, attainment text right, and progress track `>=200px` when rendered.

Rules:

- One card, one metric, one evidence visual. Do not combine sparkline + bars + ring in the same single-indicator card.
- Use a light index number only for sample grids, design review, or ordered pattern libraries. Production dashboards should use it only when the order itself matters.
- Top-right controls are local to this card or declared peer KPI group. Unit/scale switches change formatting; period/grain switches change the evidence dataset and comparison baseline.
- The footer target/progress band is not optional when the card claims completion or target achievement. If there is no target, remove the footer and select a simpler trend/metric card.
- Mini evidence uses real data and keeps exact points in tooltip/detail. Smooth fake lines, equal-height decorative bars, and arbitrary gauge arcs fail the anti-AI gate.
- Cards in the same grid share outer height, padding, title baseline, value baseline, comparison baseline, and footer height. Evidence visuals may differ, but their fit boxes align.

Fallback:

1. Collapse segmented controls to compact dropdown.
2. Hide the light index number and definition icon.
3. Move secondary comparison wording to tooltip.
4. Hide the mini evidence visual and keep target/progress.
5. Remove footer progress track but keep target/attainment text.
6. Split to a full chart/table/detail block if the evidence visual is the decision task.

### Pattern: `horizontal-trend-compare`

Use for KPI cards like production volume, energy, orders, visits, or other current values that need a compact trend and a named baseline such as `同比`, `环比`, or `较去年同期`.

Rules:

- Primary value stays left. Trend evidence sits in the lower or right band.
- Trend line hides axes and permanent point labels; exact points live in tooltip.
- A faint domain icon may sit in the right background only when it supports the metric meaning and does not reduce contrast.
- If the trend needs target bands, annotations, or axis reading, use a full line chart block instead.

### Pattern: `horizontal-axis-line-trend`

Use for KPI cards like production volume, OEE, order completion, defect rate, energy, production cost, on-time delivery, or inventory turnover when the value needs a compact but readable line chart below it.

This pattern covers these controlled evidence modes:

| `kpiAxisLineEvidenceMode` | Use when | Required evidence |
| --- | --- | --- |
| `basic-compare-line` | One KPI needs current value plus YoY/MoM/baseline trend. | ordered time rows, value field, comparison label/value, unit. |
| `filled-baseline-line` | The line should emphasize magnitude or period area without becoming a full area chart. | ordered time rows, value field, fill semantics, baseline meaning. |
| `target-reference-line` | A target, SLA, budget, or goal line is part of the judgment. | target value, target label, target formula, value series. |
| `phase-annotated-line` | A business phase or improvement period explains a visible change. | phase start/end, phase label, affected points, before/after semantics. |
| `unit-axis-line` | Unit reading matters and the chart has no fill or extra comparison. | y-axis unit, ordered time rows, value series. |
| `grain-switch-line` | A compact `日/周/月`, `月/季/年`, or similar switch changes the time grain. | local control options, selected grain, grain-specific dataset. |
| `dual-comparison-line` | Current and prior/baseline series must be compared on the same axis. | two comparable series, shared time grain, legend labels, tooltip payload. |
| `threshold-band-line` | The KPI is judged against good/normal/warning ranges. | threshold bands, band labels, status direction, action/detail path when warning. |

Rules:

- The KPI headline remains the first-read object. The chart proves or qualifies it; it does not replace it.
- Use ECharts for the line body when axes, gridlines, target/reference lines, threshold bands, axisPointer, tooltip, or local grain switching are visible.
- Put title and the one local control in the top row. Put the primary value and comparison immediately below. Put the axis line chart in the bottom body.
- Keep one visible local control group only. If both comparison mode and time grain are needed, show the higher-priority group and collapse the other into tooltip/detail or a dropdown.
- Y-axis labels, x-axis labels, unit, legend, target label, and threshold labels must reserve chart-body space. They cannot overlay the value zone.
- Use point symbols only when `N <= 12`. For denser lines, keep hover/emphasis points and tooltip.
- Filled area is allowed only when the fill means magnitude, baseline, improvement zone, or status band. Do not add a soft fill because it looks polished.
- Target/reference labels should sit near the line with reserved right or top gap. If the label collides, keep the line and move label text into tooltip.
- Threshold bands are weak background evidence. They must not reduce line contrast or make the card read as an alert unless the KPI state is actually abnormal.
- Mock data must include plausible bends, plateaus, dips, or phase changes when the domain is operational. A perfectly smooth upward line fails the anti-AI gate unless it comes from real data.

Minimum and fallback:

- Minimum outer size: `420x260`; standard size: `460-560px` wide and `280-340px` high.
- Chart body after title/value/comparison/control bands must be `>=180px`; inner plot height must be `>=130px`.
- If the card cannot satisfy the chart body floor, downgrade to `horizontal-trend-compare` by hiding axes/grid/target labels, or split the chart into a full `comparison-line-trend-card`.
- If exact audit, dense annotations, many series, dataZoom, or table comparison is the task, use a full chart/table block instead of this KPI card.

### Pattern: `horizontal-axis-bar-compare`

Use for KPI cards like production volume, OEE, order completion, defect rate, energy, production cost, on-time delivery, inventory turnover, or category quality comparison when the value needs a compact but readable horizontal bar chart below it.

This pattern covers these controlled evidence modes:

| `kpiAxisBarEvidenceMode` | Use when | Required evidence |
| --- | --- | --- |
| `basic-horizontal-bar` | One KPI needs recent period or ranked category comparison plus a named baseline. | ordered category rows, value field, comparison label/value, unit. |
| `period-comparison-bar` | Period-to-period comparison such as 本期/上期/上上期 is the main evidence. | ordered period rows, value field, period labels, baseline semantics. |
| `target-reference-bar` | A target, SLA, budget, or goal line is part of the judgment. | target value, target label, target formula, value rows. |
| `category-change-sidebar-bar` | Each category needs a value plus change-rate, such as product line defect rate changes. | category rows, value field, change-rate field, direction semantics. |
| `time-series-horizontal-bar` | Recent dates/months should be compared as horizontal bars rather than a line. | ordered time rows, value field, time grain, unit. |
| `grain-switch-horizontal-bar` | A compact `日/周/月`, `月/季/年`, or similar switch changes the bar grain. | local control options, selected grain, grain-specific dataset. |
| `dual-series-horizontal-bar` | Current and prior/baseline bars must be compared on the same row. | two comparable value fields or series rows, shared category/time grain, legend labels. |
| `threshold-warning-bar` | The KPI is judged against good/normal/warning ranges or an inventory/quality threshold. | threshold value or bands, warning label, status direction, action/detail path when warning. |

Rules:

- The KPI headline remains the first-read object. The horizontal bar body explains rank, period comparison, target gap, category variation, or warning state.
- Use ECharts for the horizontal bar body when axes, gridlines, target/reference lines, threshold bands, legend, tooltip, or local grain switching are visible.
- Put title and the one local control in the top row. Put the primary value and comparison immediately below. Put the horizontal bar body in the bottom body.
- Keep category labels on the left and exact value or change-rate labels on the right. Do not center labels inside bars unless labels still pass contrast and fit checks.
- Visible bars default to `3-6`, maximum `8` inside a KPI card. More bars require Top N, scrolling/detail, or a full bar chart block.
- Sort order must be explicit: chronological for time, descending/ascending value for ranking, or declared business order for categories. Do not let mock array order decide silently.
- Bar color follows the semantic role: primary blue/green for the main series, muted gray for comparison, orange/red only for warning or negative status. Do not assign random colors per row.
- Target/reference lines and threshold bands are data-driven and share the x-axis scale with the bars. They cannot float as decorative vertical lines.
- Dual-series bars must keep the primary series visually stronger. The comparison series is muted, outline, lighter, or slightly thinner.
- Change-rate sidebars must follow business direction, not raw sign. Lower defect rate or lower inventory days can be good.
- Mock data should include realistic uneven gaps, one or two weak categories, and at least one non-perfect target/comparison case when the domain allows it.

Minimum and fallback:

- Minimum outer size: `420x260`; standard size: `460-560px` wide and `280-340px` high.
- Chart body after title/value/comparison/control bands must be `>=180px`; inner plot height must be `>=140px`; row height must be `>=22px`.
- If the card cannot satisfy the chart body floor, downgrade to `horizontal-grain-bar-switch` only when axes/labels can be hidden, or split the chart into a full `single-series-bar-card`, `filtered-bar-card`, or target/actual bar card.
- If exact audit, many categories, sorting/filtering, dataZoom, or table comparison is the task, use a full chart/table block instead of this KPI card.

### Pattern: `horizontal-axis-scatter-diagnostic`

Use for KPI cards like energy vs output, OEE vs runtime, order completion vs delivery cycle, defect rate distribution, cost vs production, age vs failure count, or supplier delivery quality when the value needs a compact relationship/distribution diagnosis below it.

This pattern covers these controlled evidence modes:

| `kpiScatterEvidenceMode` | Use when | Required evidence |
| --- | --- | --- |
| `correlation-trendline-scatter` | A relationship or correlation supports the KPI judgment. | x/y metrics, object grain, trendline or fit result, optional correlation field. |
| `mean-reference-scatter` | The cloud should be judged against average or reference lines. | x/y metrics, x/y average or reference values, comparison semantics. |
| `target-crosshair-scatter` | Two target thresholds define desired placement. | x/y target values, target labels, gap fields, target direction. |
| `distribution-change-band-scatter` | Distribution is judged by change-rate bands or side legend. | point values, change-rate field, band thresholds, direction semantics. |
| `threshold-quadrant-scatter` | Operating zones such as normal/warning/alarm are the main reading. | x/y threshold fields, quadrant or band labels, action/detail path for bad zones. |
| `dual-series-trendline-scatter` | Current and prior/baseline points need comparison. | current and baseline point series or comparable fields, legend labels, shared axis scale. |
| `change-callout-scatter` | A selected point or cluster needs a small change callout. | selected object/cluster id, change field, callout text/value, tooltip payload. |
| `category-quadrant-scatter` | Points need category color plus quadrant or strategy labels. | category field, category legend, x/y thresholds or quadrant labels. |

Rules:

- The scatter is the evidence for relationship, spread, outlier, target fit, or quadrant decision. Do not use it for a single metric or simple category comparison.
- Use ECharts `scatter` or `effectScatter` only for highlighted points; axes, grid, reference lines, trendlines, quadrants, legends, tooltips, and resize behavior remain renderer-owned.
- Keep the KPI headline first. The scatter body proves why the current value is good, bad, improving, or uncertain.
- Point labels are key-only: selected, outlier, Top, or abnormal labels. Ordinary labels stay in tooltip.
- Reference lines, trendlines, target crosshairs, threshold bands, and quadrant backgrounds are data-driven and named. They cannot float as decorative diagonals or translucent zones.
- If color encodes category, keep visible categories `<=5`; otherwise use Top categories, filter, or tooltip-only category.
- Mock point clouds should include realistic spread, clusters, outliers, or mixed zones when the business allows it. A perfectly regular cloud fails the anti-AI gate.

Minimum and fallback:

- Minimum outer size: `420x300`; standard size: `460-560px` wide and `320-360px` high.
- Chart body after title/value/comparison/control bands must be `>=200px`; inner plot height must be `>=160px`.
- Recommended point count is `12-80`; `81-200` needs lower opacity and no permanent labels; `>200` needs aggregation, sampling, zoom/brush, density, or a full chart/detail path.
- If the card cannot satisfy the plot floor, downgrade to `horizontal-trend-compare`, a small anomaly note, or a full scatter chart block. Do not shrink the scatter into a decorative dot field.

### Pattern: `horizontal-spatial-map-diagnostic`

Use for KPI cards like national output distribution, online rate by region, order completion by province, defect-rate distribution, energy intensity by location, cost interval map, on-time delivery by supplier location, or regional change diagnosis when geography itself answers the question.

This pattern covers these controlled evidence modes:

| `kpiMapEvidenceMode` | Use when | Required evidence |
| --- | --- | --- |
| `choropleth-heat-map` | Administrative regions show metric intensity. | region code/name, value field, color bins, map resource. |
| `graded-choropleth-map` | Business thresholds classify regions. | region field, value field, threshold bins, status direction. |
| `bubble-target-gap-map` | Regional points or provinces need magnitude plus target gap. | lon/lat or region centroid, value/size field, target/gap field. |
| `distribution-change-marker-map` | Location markers need change-rate status. | point/region location, value, change-rate, status legend. |
| `column-symbol-map` | Regions need small vertical columns on a basemap. | region/coordinate, value field, unit, column scale. |
| `annotated-interval-map` | Selected locations carry interval labels or numeric annotations. | selected locations, value labels, interval bins. |
| `yoy-change-zone-map` | Increase/decrease zones are the primary reading. | region field, YoY/MoM change field, divergent bins. |
| `point-category-summary-map` | Many locations need category status plus side summary. | lon/lat, category/status, value, category counts. |

Rules:

- Use a map only when spatial position, adjacency, coverage, or regional clustering changes the decision. Region names alone do not justify a map.
- The basemap is muted evidence scaffolding; the data layer, legend, and selected labels carry the meaning.
- Administrative maps require `regionCode` whenever possible. Point maps require longitude/latitude. Missing geography is reported in tooltip/detail/QA evidence.
- Preserve map projection and aspect ratio with a measured fit box. Letterboxing is acceptable; stretching geography is not.
- Visible labels are key-only: Top, selected, abnormal, or hovered regions/points. The legend/visualMap must not cover important geography.
- If the map needs exact ranking or audit, pair it with a side ranking/table or route to detail, instead of printing all values on the map.

Minimum and fallback:

- Minimum outer size: `460x320`; standard size: `500-640px` wide and `340-380px` high.
- Map body after title/value/comparison/control bands must be `>=220px`; map viewport shorter side must be `>=180px`.
- Reserve `72-140px` for legend, visualMap, or side summary when it is outside the map; otherwise use compact in-map legend with safe overlap checks.
- If the card cannot preserve geography and legend, switch to a bar/ranking/table card or a full map block. Do not render a tiny decorative map.

### Pattern: `paired-comparison-diagnostic`

Use for KPI cards like this period vs prior period, actual vs target, before vs after, improvement vs previous, percentage vs benchmark, inventory days current vs last month, or cost structure current vs baseline when the main judgment is the difference between two comparable states.

This pattern covers these controlled evidence modes:

| `kpiComparisonEvidenceMode` | Use when | Required evidence |
| --- | --- | --- |
| `metric-yoy-vs` | Current value is compared with prior-year or prior-period value. | current value, baseline value, comparison label, delta. |
| `progress-mom-vs` | Two progress strips or bounded statuses compare current and previous. | current/baseline rates, min/max or target, delta direction. |
| `target-gap-progress-vs` | Actual and target panes compare target distance. | actual value, target value, gap, attainment rate. |
| `improvement-dot-matrix-vs` | Status counts or quality improvement is shown through dot matrices. | current/baseline counts or rate buckets, improvement field. |
| `trend-yoy-vs` | Two mini trends compare the shape of current and baseline movement. | current and baseline trend series, shared grain, comparable scale. |
| `structure-breakdown-vs` | Two structures compare cost/category composition. | current and baseline category rows, shared categories, delta. |
| `percentage-ring-vs` | Two bounded percentages compare completion/fulfillment. | current and baseline rates, denominator/target, delta. |
| `trend-mom-vs` | Month-over-month trend change is judged by two mini line panes. | current and prior period trend series, shared grain, delta. |

Rules:

- The two panes must compare the same metric definition, unit, grain, and filter scope. If definitions differ, use a table or explanation card instead.
- Central `VS` rail is structural, not decorative: it keeps left/right panes comparable and separates baselines.
- Left and right panes share typography scale, value baseline, mini-chart scale when comparable, and equal padding. The winning/primary side may use stronger color, but geometry stays mirrored.
- Bottom conclusion strip names the result, such as `本月能耗降低 818 kWh` or `未达目标，差距 2.7 个百分点`.
- Mini bars, rings, dot matrices, or small trends are evidence for the pane, not second full charts.

Minimum and fallback:

- Minimum outer size: `420x260`; standard size: `460-560px` wide and `280-340px` high.
- Each pane must be `>=140px` wide after padding, the `VS` rail must be `32-44px`, and bottom conclusion band must be `36-52px`.
- If pane evidence cannot fit, keep values plus delta and move mini evidence to tooltip/detail.
- If multiple categories, many baselines, or exact audit are needed, use a full comparison chart/table instead of this KPI card.

### Pattern: `horizontal-ring-progress`

Use for bounded progress/status metrics such as OEE, utilization, SLA, yield, completion, or availability.

Rules:

- Ring sits right of the value or centered in the right half.
- Center text equals the same display value or a declared progress rate; it cannot contradict the primary value.
- Footer may show prior period or baseline as weak evidence.
- If the ring would shrink below `96px` diameter, switch to `horizontal-target-progress` or `plain-metric`.

### Pattern: `horizontal-target-progress`

Use for target attainment where a linear progress track communicates distance to target better than a circle.

Rules:

- Show target label and value near the primary value or track, such as `目标 95.0%`.
- Progress track has min/max or start/end labels only when they fit.
- Target marker/tick is data-driven and must not float as decoration.
- If target is missing, degrade to `horizontal-trend-compare` or `plain-metric`.

### Pattern: `horizontal-status-trend-compare`

Use for lower-is-better quality, risk, defect, complaint, overdue, or cost metrics where improvement is the business point.

Rules:

- Status color follows business meaning, not raw sign. A lower value may be good.
- Show prior/current labels or an equivalent before/after comparison.
- The trend line should move in the same semantic direction as the stated improvement or explain exceptions in tooltip.
- If direction semantics are not declared, mark the mapping incomplete instead of guessing color.

### Pattern: `horizontal-grain-bar-switch`

Use when a KPI card needs a local `日/周/月`, `月/年`, or similar compact grain switch plus a mini bar distribution.

Rules:

- One local control group only; it affects this card or declared local KPI group.
- Mini bars show recent distribution or selected-period pattern. They do not replace a full bar chart.
- Highlight the selected/current bar only when its relationship to the primary value is declared.
- If the mini bars need axes or category labels to be useful, move them to a chart card.

### Pattern: `horizontal-period-summary-strip`

Use when current, previous, and target values are the evidence, and a chart would be unnecessary.

Rules:

- Bottom strip uses `2-3` equal cells, usually `本月 / 上月 / 目标` or `本期 / 上期 / 目标`.
- Cell labels and values align on a shared baseline.
- Do not add decorative icons or charts when the strip already answers the comparison.
- If more than `3` values are required, use a small table or detail drawer.

### Pattern: `horizontal-pp-assist-info`

Use for percentage or rate metrics where the change should be expressed as percentage points, such as on-time rate, conversion rate, yield, or fulfillment rate.

Rules:

- Use `pp` only when the delta is `currentRate - baselineRate`. Do not use `pp` for percent growth such as `(current - prior) / prior`.
- Show the pp delta as a compact badge near the primary value.
- Auxiliary info panel may show prior period value, calendar/period, or mini bars.
- If the audience expects percent change rather than percentage points, rename the metric or change the pattern.

### Pattern: `horizontal-warning-status-band`

Use when the KPI value has a threshold state and the next action is to notice or resolve the condition, such as inventory turnover days, overdue rate, stockout risk, abnormal cost, or safety warning.

Rules:

- Warning badge is adjacent to the value, not hidden in the footer.
- Bottom band carries the warning reason and threshold, such as `高于目标值（<=25天）`.
- The band color is semantic and restrained; do not turn the entire card into a full warning surface unless it is a blocking alert.
- The warning must have a detail/action path when operational follow-up is expected.

Landscape fallback order:

1. Remove decorative icon or background illustration.
2. Collapse local control from segmented options to compact dropdown.
3. Move secondary comparison or prior-period value to tooltip.
4. Hide mini chart evidence before shrinking the primary value.
5. Switch to `plain-metric` or a full chart/table block when the evidence cannot fit.

## Data Contract

Implementation-ready KPI cards require these fields unless explicitly scoped out:

```ts
type KpiCardPattern =
  | 'plain-metric'
  | 'target-wave'
  | 'mini-bar-trend'
  | 'highlight-line-trend'
  | 'horizontal-trend-compare'
  | 'horizontal-axis-line-trend'
  | 'horizontal-axis-bar-compare'
  | 'horizontal-axis-scatter-diagnostic'
  | 'horizontal-spatial-map-diagnostic'
  | 'paired-comparison-diagnostic'
  | 'horizontal-ring-progress'
  | 'horizontal-target-progress'
  | 'horizontal-status-trend-compare'
  | 'horizontal-grain-bar-switch'
  | 'horizontal-period-summary-strip'
  | 'horizontal-pp-assist-info'
  | 'horizontal-warning-status-band';

type KpiCardOrientation =
  | 'portrait'
  | 'landscape'
  | 'compact-row'
  | 'wide-banner';

type KpiAxisLineEvidenceMode =
  | 'basic-compare-line'
  | 'filled-baseline-line'
  | 'target-reference-line'
  | 'phase-annotated-line'
  | 'unit-axis-line'
  | 'grain-switch-line'
  | 'dual-comparison-line'
  | 'threshold-band-line';

type KpiAxisBarEvidenceMode =
  | 'basic-horizontal-bar'
  | 'period-comparison-bar'
  | 'target-reference-bar'
  | 'category-change-sidebar-bar'
  | 'time-series-horizontal-bar'
  | 'grain-switch-horizontal-bar'
  | 'dual-series-horizontal-bar'
  | 'threshold-warning-bar';

type KpiScatterEvidenceMode =
  | 'correlation-trendline-scatter'
  | 'mean-reference-scatter'
  | 'target-crosshair-scatter'
  | 'distribution-change-band-scatter'
  | 'threshold-quadrant-scatter'
  | 'dual-series-trendline-scatter'
  | 'change-callout-scatter'
  | 'category-quadrant-scatter';

type KpiMapEvidenceMode =
  | 'choropleth-heat-map'
  | 'graded-choropleth-map'
  | 'bubble-target-gap-map'
  | 'distribution-change-marker-map'
  | 'column-symbol-map'
  | 'annotated-interval-map'
  | 'yoy-change-zone-map'
  | 'point-category-summary-map';

type KpiComparisonEvidenceMode =
  | 'metric-yoy-vs'
  | 'progress-mom-vs'
  | 'target-gap-progress-vs'
  | 'improvement-dot-matrix-vs'
  | 'trend-yoy-vs'
  | 'structure-breakdown-vs'
  | 'percentage-ring-vs'
  | 'trend-mom-vs';

type KpiSingleIndicatorLayoutMode =
  | 'dropdown-sparkline-progress'
  | 'unit-toggle-ring-progress'
  | 'dropdown-minibar-progress'
  | 'grain-switch-minibar-progress'
  | 'dropdown-area-sparkline-progress'
  | 'scale-toggle-area-progress'
  | 'dropdown-gauge-progress';

type KpiOverviewCardPattern =
  | 'lead-metric-comparison-sparkline-overview'
  | 'multi-metric-strip-progress-overview'
  | 'domain-metric-cluster-progress-overview';

type KpiJudgmentCardPattern =
  | 'semantic-status-icon-card'
  | 'progress-status-ring-card'
  | 'health-score-ring-card'
  | 'health-threshold-bullet-card'
  | 'health-dimension-breakdown-card'
  | 'rating-score-summary-card'
  | 'rating-distribution-card'
  | 'semicircle-gauge-target-card';

type KpiGoalExecutionCardPattern =
  | 'attainment-ring-summary-card'
  | 'attainment-gauge-deadline-card'
  | 'attainment-linear-target-card'
  | 'attainment-unit-progress-card'
  | 'gap-gauge-deficit-card'
  | 'gap-target-actual-compare-card'
  | 'progress-plan-actual-card'
  | 'milestone-timeline-card';

type KpiTimeSeriesCardPattern =
  | 'trend-line-target-card'
  | 'change-baseline-delta-card'
  | 'yoy-mom-comparison-card'
  | 'cycle-period-progress-card'
  | 'volatility-stat-card'
  | 'forecast-interval-card';

type KpiComparisonAnalysisCardPattern =
  | 'direct-value-compare-card'
  | 'group-segment-compare-card'
  | 'competitor-position-card'
  | 'benchmark-position-card'
  | 'variance-gap-card';

type KpiComparisonAnalysisEvidenceMode =
  | 'side-by-side-values'
  | 'grouped-bars'
  | 'stacked-distribution'
  | 'multi-series-trend'
  | 'market-share-donut'
  | 'radar-profile'
  | 'benchmark-ruler'
  | 'variance-gauge'
  | 'nps-score-scale'
  | 'comparison-table'
  | 'map-table-compare';

type KpiJudgmentBand = {
  label: string;
  minField?: string;
  maxField?: string;
  colorRole: 'success' | 'info' | 'warning' | 'danger' | 'neutral' | 'domain';
  statusKind: 'healthy' | 'normal' | 'progress' | 'warning' | 'risk' | 'failed' | 'unknown';
};

type KpiGoalMilestoneBinding = {
  milestoneDatasetId: string;
  nameField: string;
  statusField: string;
  dateField?: string;
  orderField?: string;
  currentMilestoneField?: string;
  dueDateField?: string;
};

type KpiOverviewMetricItem = {
  metricId: string;
  metricName: string;
  valueField: string;
  unit: string;
  valueType: string;
  numericFormatContractId: string;
  comparisonFields?: Array<'yoy' | 'mom' | 'baseline' | 'targetGap' | 'status'>;
  targetField?: string;
  attainmentRateField?: string;
  progressTrackField?: string;
  evidenceVisual?: 'none' | 'sparkline' | 'mini-bars' | 'progress-track' | 'semantic-icon';
  trendDatasetId?: string;
  trendCategoryField?: string;
  trendValueField?: string;
  tooltipPayload: string[];
};

type KpiCardContract = {
  kpiCardPattern: KpiCardPattern;
  kpiCardOrientation?: KpiCardOrientation;
  kpiAxisLineEvidenceMode?: KpiAxisLineEvidenceMode;
  kpiAxisBarEvidenceMode?: KpiAxisBarEvidenceMode;
  kpiScatterEvidenceMode?: KpiScatterEvidenceMode;
  kpiMapEvidenceMode?: KpiMapEvidenceMode;
  kpiComparisonEvidenceMode?: KpiComparisonEvidenceMode;
  kpiSingleIndicatorLayoutMode?: KpiSingleIndicatorLayoutMode;
  kpiOverviewCardPattern?: KpiOverviewCardPattern;
  kpiJudgmentCardPattern?: KpiJudgmentCardPattern;
  kpiGoalExecutionCardPattern?: KpiGoalExecutionCardPattern;
  kpiTimeSeriesCardPattern?: KpiTimeSeriesCardPattern;
  kpiComparisonAnalysisCardPattern?: KpiComparisonAnalysisCardPattern;
  kpiComparisonAnalysisEvidenceMode?: KpiComparisonAnalysisEvidenceMode;
  metricId: string;
  metricName: string;
  valueField: string;
  unit: string;
  periodField?: string;
  valueType: string;
  numericFormatContractId: string;
  comparisonFields?: Array<'yoy' | 'mom' | 'baseline' | 'targetGap' | 'status'>;
  targetField?: string;
  attainmentRateField?: string;
  thresholdField?: string;
  warningReasonField?: string;
  previousValueField?: string;
  currentValueField?: string;
  ppDeltaField?: string;
  localControlFields?: string[];
  trendDatasetId?: string;
  trendCategoryField?: string;
  trendValueField?: string;
  trendXAxisField?: string;
  trendYAxisUnit?: string;
  trendComparisonSeriesFields?: string[];
  trendTargetValueField?: string;
  trendReferenceFields?: string[];
  trendThresholdBandFields?: string[];
  trendPhaseAnnotationFields?: string[];
  temporalAnalysisKind?: 'trend' | 'change' | 'yoy-mom' | 'cycle' | 'volatility' | 'forecast';
  temporalDirection?: 'higher-better' | 'lower-better' | 'range-target' | 'neutral';
  temporalGrainField?: string;
  temporalLatestPeriodField?: string;
  temporalBaselineLabelField?: string;
  temporalBaselineValueField?: string;
  temporalDeltaValueField?: string;
  temporalDeltaRateField?: string;
  temporalYoyValueField?: string;
  temporalYoyRateField?: string;
  temporalMomValueField?: string;
  temporalMomRateField?: string;
  temporalPriorYearComparableValueField?: string;
  temporalPriorPeriodValueField?: string;
  cycleGrainField?: string;
  cyclePeriodStartField?: string;
  cyclePeriodEndField?: string;
  cycleCurrentIndexField?: string;
  cycleTotalCountField?: string;
  cycleProgressField?: string;
  cyclePhaseStatusField?: string;
  volatilityFormula?: string;
  volatilityRateField?: string;
  volatilityLevelField?: string;
  volatilityMaxField?: string;
  volatilityMinField?: string;
  volatilityStdDevField?: string;
  volatilityThresholdBandFields?: string[];
  forecastDatasetId?: string;
  forecastStartField?: string;
  forecastEndField?: string;
  forecastHorizonField?: string;
  forecastValueField?: string;
  forecastLowerBoundField?: string;
  forecastUpperBoundField?: string;
  forecastStatusField?: string;
  temporalFooterEvidenceFields?: string[];
  comparisonAnalysisKind?: 'direct' | 'group' | 'competitor' | 'benchmark' | 'variance';
  comparisonDirection?: 'higher-better' | 'lower-better' | 'range-target' | 'neutral';
  comparisonSubjectDatasetId?: string;
  comparisonSubjectIdField?: string;
  comparisonSubjectNameField?: string;
  comparisonSubjectRoleField?: string;
  comparisonPrimarySubjectIdField?: string;
  comparisonBaselineSubjectIdField?: string;
  comparisonGroupField?: string;
  comparisonSegmentField?: string;
  comparisonCompetitorRoleField?: string;
  comparisonMetricFields?: string[];
  comparisonValueFields?: string[];
  comparisonBaselineValueField?: string;
  comparisonDeltaValueField?: string;
  comparisonDeltaRateField?: string;
  comparisonRankField?: string;
  comparisonShareField?: string;
  comparisonMarketTotalField?: string;
  comparisonBenchmarkSourceField?: string;
  comparisonBenchmarkValueField?: string;
  comparisonBenchmarkLabelField?: string;
  comparisonP50Field?: string;
  comparisonP75Field?: string;
  comparisonP90Field?: string;
  comparisonPercentileField?: string;
  comparisonIndustryAverageField?: string;
  comparisonVarianceValueField?: string;
  comparisonVarianceRateField?: string;
  comparisonSortRule?: string;
  comparisonVisibleSubjectLimit?: number;
  comparisonFooterEvidenceFields?: string[];
  barDatasetId?: string;
  barCategoryField?: string;
  barValueField?: string;
  barXAxisUnit?: string;
  barComparisonSeriesFields?: string[];
  barTargetValueField?: string;
  barReferenceFields?: string[];
  barThresholdFields?: string[];
  barChangeRateField?: string;
  barSortRule?: string;
  barVisibleLimit?: number;
  scatterDatasetId?: string;
  scatterObjectIdField?: string;
  scatterObjectNameField?: string;
  scatterXField?: string;
  scatterYField?: string;
  scatterXUnit?: string;
  scatterYUnit?: string;
  scatterSizeField?: string;
  scatterColorField?: string;
  scatterTrendlineField?: string;
  scatterReferenceFields?: string[];
  scatterThresholdFields?: string[];
  scatterQuadrantFields?: string[];
  scatterPointLimit?: number;
  mapDatasetId?: string;
  mapRegionCodeField?: string;
  mapRegionNameField?: string;
  mapValueField?: string;
  mapVisualMapField?: string;
  mapPointDatasetId?: string;
  mapPointLonField?: string;
  mapPointLatField?: string;
  mapPointValueField?: string;
  mapCategoryField?: string;
  mapProjection?: string;
  mapResource?: string;
  mapLegendFields?: string[];
  comparisonBaselineField?: string;
  comparisonValueFields?: string[];
  comparisonPaneFields?: string[];
  comparisonConclusionField?: string;
  singleIndicatorEvidenceVisual?: 'sparkline' | 'mini-bars' | 'ring' | 'area-sparkline' | 'semi-gauge';
  singleIndicatorControlType?: 'period-dropdown' | 'grain-segmented' | 'unit-toggle' | 'scale-toggle';
  singleIndicatorControlOptions?: string[];
  singleIndicatorSelectedControlField?: string;
  singleIndicatorProgressTrack?: boolean;
  overviewTopic?: string;
  overviewLeadMetricId?: string;
  overviewMetrics?: KpiOverviewMetricItem[];
  overviewLocalControlType?:
    | 'period-segmented'
    | 'period-dropdown'
    | 'metric-segmented'
    | 'unit-scale-segmented'
    | 'overflow-menu';
  overviewLocalControlFields?: string[];
  overviewVisibleMetricLimit?: number;
  overviewExactValueRoute?: string;
  judgmentKind?: 'status' | 'health' | 'rating' | 'score' | 'gauge' | 'risk' | 'progress';
  judgmentStatusField?: string;
  judgmentScoreField?: string;
  judgmentScoreRange?: [number, number];
  judgmentLevelField?: string;
  judgmentBands?: KpiJudgmentBand[];
  judgmentThresholdFields?: string[];
  judgmentDirection?: 'higher-better' | 'lower-better' | 'range-target' | 'status-enum';
  judgmentHeroVisual?:
    | 'semantic-icon'
    | 'ring'
    | 'semi-gauge'
    | 'bullet-range'
    | 'dimension-bars'
    | 'rating-stars'
    | 'rating-distribution';
  judgmentDimensionDatasetId?: string;
  judgmentDimensionNameField?: string;
  judgmentDimensionScoreField?: string;
  judgmentRatingDistributionFields?: string[];
  judgmentFooterEvidenceFields?: string[];
  goalExecutionKind?: 'attainment' | 'gap' | 'progress' | 'milestone';
  goalDirection?: 'higher-better' | 'lower-better' | 'range-target' | 'schedule-target';
  goalActualField?: string;
  goalTargetField?: string;
  goalAttainmentRateField?: string;
  goalGapField?: string;
  goalGapRateField?: string;
  goalRemainingField?: string;
  goalDeadlineField?: string;
  goalDueStatusField?: string;
  goalPlanProgressField?: string;
  goalActualProgressField?: string;
  goalProgressDeltaField?: string;
  goalRemainingTimeField?: string;
  goalMilestoneBinding?: KpiGoalMilestoneBinding;
  goalHeroVisual?:
    | 'ring'
    | 'semi-gauge'
    | 'linear-progress'
    | 'target-actual-bars'
    | 'dot-strip'
    | 'stepper'
    | 'timeline'
    | 'cumulative-line';
  goalFooterEvidenceFields?: string[];
  sourceField?: string;
  freshnessField?: string;
  drilldownAction?: string;
  tooltipPayload: string[];
  stateRules: string[];
};
```

Do not store dynamic KPI values, rankings, status lights, or percentages in filter option `meta`. KPI values must come from business fact datasets, aggregate datasets, or resolvers with declared grain and filters.

## Anti-AI Gate For KPI Cards

A KPI card fails the anti-AI gate when any of these are true:

- It has a polished gradient, wave, line, or bar background but no target, baseline, trend series, or formula.
- It shows axes, gridlines, target labels, threshold bands, or phase marks without matching trend fields, reference fields, threshold definitions, or annotation data.
- It shows horizontal bars, target lines, comparison bars, change-rate sidebars, or warning thresholds without matching bar category/value fields, target/threshold definitions, change-rate fields, or sort rules.
- It shows scatter points, trendlines, quadrant bands, or threshold crosshairs without two numeric fields, object grain, point-density strategy, and data-driven reference/threshold fields.
- It shows a map without region codes or lon/lat fields, map resource/projection, legend/visualMap, missing-geo handling, and a genuine spatial decision.
- It shows a `VS` comparison card without comparable metric definitions, units, periods, pane fields, and a declared conclusion/delta.
- It shows a single-indicator KPI grid card with multiple mini visuals in one card, a local control that does not map to period/unit/grain/scale data, or a target/progress footer without target and attainment fields.
- It shows a KPI overview card with several polished numbers but no `kpiOverviewCardPattern`, no ordered metric list, no lead metric, no local-control scope, no target/attainment binding for visible progress, or more than one compact evidence visual.
- It shows a status, health, score, rating, or gauge card without `kpiJudgmentCardPattern`, status dictionary or score range, threshold/band definitions, business direction, comparison strip binding, and footer evidence/source path.
- It shows a target attainment, gap, progress, or milestone card without `kpiGoalExecutionCardPattern`, actual/target/gap/progress/milestone fields, direction semantics, formula, deadline or remaining-time fields when visible, and footer evidence/source path.
- It shows a trend, change, YoY/MoM, cycle, volatility, or forecast card without `kpiTimeSeriesCardPattern`, ordered time series, baseline/cycle/volatility/forecast fields required by the selected pattern, direction semantics, tooltip payload, footer evidence, and source/freshness path.
- It shows a direct comparison, group comparison, competitor comparison, benchmark position, or variance/gap card without `kpiComparisonAnalysisCardPattern`, comparable subject roles, shared metric definition/unit/grain, selected comparison/benchmark/variance fields, direction semantics, sort rule, tooltip payload, footer evidence, and source/freshness path.
- The visible text could belong to any industry or product, such as generic "增长", "效率", "智能洞察", or "核心指标" without a business object.
- The chart-like mark is random decoration rather than data-driven evidence.
- Every KPI is all-good, smooth, and perfectly balanced in mock data without source evidence.
- All cards have equal visual weight even though one metric should lead the decision.
- The value is small, off-center, or visually weaker than the decorative chart.
- The card hides formula, period, source/freshness, or target definition when those details affect trust.

Countermeasure:

```text
one metric -> one judgment -> one comparison or target -> one evidence mark -> one disclosure path
```

## Implementation Notes

- Use project or template tokens for color, radius, shadow, typography, and status semantics.
- Use ECharts or the approved project wrapper for mini bars and mini lines when runtime tooltip, resize, or theme behavior matters.
- A compact data-driven SVG sparkline is acceptable only when it is documented as a sparkline glyph, not a standard chart, and exact values remain available through tooltip/detail.
- Do not copy sample images as assets. Rebuild the card from data, tokens, and slots.
- Provide stable selectors or project equivalents for `kpi-card`, `kpi-value-anchor`, `kpi-value`, `kpi-unit`, `kpi-comparison`, `kpi-target`, and `kpi-evidence`.

## Acceptance Checklist

Before marking the card ready:

- The business question for the card is named.
- `visualType` is `metric-card` and `kpiCardPattern` is one of the controlled values.
- Primary value + unit is the strongest readable element and passes the value-anchor checks in `04-kpi-metric-cards.md`.
- Numeric display contract exists for the main value and visible comparison values.
- Target/progress cards declare target formula, denominator behavior, and missing-target fallback.
- Mini trend cards declare series grain, ordered category field, value field, latest point, and tooltip payload.
- Landscape KPI cards declare `kpiCardOrientation`, chosen horizontal pattern, primary value zone, auxiliary evidence zone, local control scope, and fallback when `W < 360px` or `H < 128px`.
- KPI overview cards declare `kpiOverviewCardPattern`, one overview topic, `2-5` ordered metrics, `overviewLeadMetricId` when the pattern has a lead metric, local control type/scope, target and attainment fields for every visible progress track, outer size `>=720x220`, each metric cell `>=128px` wide, progress track `>=120px`, one compact evidence visual maximum, exact-value route, and fallback when metrics or controls do not fit.
- KPI judgment cards declare `kpiJudgmentCardPattern`, `judgmentKind`, status or score field, score range or status dictionary, threshold/band fields when visible, `judgmentDirection`, exactly one hero visual, comparison strip fields, footer evidence/source path, outer size `>=360x240`, hero fit box that matches the selected visual, and fallback when icon/ring/gauge/bars cannot fit.
- KPI goal execution cards declare `kpiGoalExecutionCardPattern`, `goalExecutionKind`, actual/target fields, attainment/gap/progress/milestone fields required by the selected pattern, `goalDirection`, formula/denominator behavior, deadline/remaining-time fields when visible, exactly one execution hero visual, comparison strip fields, footer evidence/source path, outer size `>=360x240`, hero fit box that matches the selected visual, and fallback before target/gap/progress/milestone evidence is squeezed.
- KPI time-series analysis cards declare `kpiTimeSeriesCardPattern`, `temporalAnalysisKind`, ordered time series, x/y fields, grain, latest period, direction semantics, tooltip payload, and required baseline/cycle/volatility/forecast fields for the selected pattern; they fail when outer size `<360x240`, time-series evidence zone `<112px`, footer evidence is missing, or forecast/volatility/baseline semantics are decorative.
- KPI comparison analysis cards declare `kpiComparisonAnalysisCardPattern`, `comparisonAnalysisKind`, comparable subject grain, subject role fields, shared metric definition/unit/grain, selected comparison/competitor/benchmark/variance fields, direction semantics, sort rule, tooltip payload, footer evidence/source path, and exact-value route; they fail when outer size `<360x240`, comparison evidence zone `<112px`, circular evidence fit boxes fail, footer evidence is missing, or competitor/benchmark/gap semantics are decorative.
- Single-indicator KPI grid cards declare `kpiSingleIndicatorLayoutMode`, exactly one evidence visual, local control type/scope, target and attainment fields when the footer exists, card outer size `>=360x220`, evidence fit box `>=112x72`, ring/gauge fit box `>=116x96`, footer band `44-60px`, and peer-grid baseline alignment.
- Axis-line diagnostic KPI cards declare `kpiAxisLineEvidenceMode`, ECharts renderer ownership, ordered x field, y field/unit, chart body height, tooltip payload, and any target/reference/threshold/phase/comparison-series fields; they fail when `W < 420px`, `H < 260px`, chart body `<180px`, or plot height `<130px`.
- Axis-bar diagnostic KPI cards declare `kpiAxisBarEvidenceMode`, ECharts renderer ownership, category field, value field/unit, sort rule, visible bar limit, chart body height, tooltip payload, and any target/reference/threshold/change-rate/comparison-series fields; they fail when `W < 420px`, `H < 260px`, chart body `<180px`, plot height `<140px`, row height `<22px`, or visible bars exceed `8`.
- Axis-scatter diagnostic KPI cards declare `kpiScatterEvidenceMode`, ECharts renderer ownership, object grain, x/y fields, units, point-count strategy, chart body height, tooltip payload, and any trendline/reference/threshold/quadrant/category/size fields; they fail when `W < 420px`, `H < 300px`, chart body `<200px`, plot height `<160px`, or point density is unmanaged.
- Spatial-map diagnostic KPI cards declare `kpiMapEvidenceMode`, map renderer ownership, region code or lon/lat fields, map resource/projection, map body height, visualMap/legend payload, missing-geo handling, and any target-gap/change/category/point fields; they fail when `W < 460px`, `H < 320px`, map body `<220px`, or map viewport shorter side `<180px`.
- Paired comparison diagnostic KPI cards declare `kpiComparisonEvidenceMode`, left/right pane fields, baseline labels, matched unit/period/grain, central `VS` rail, bottom conclusion field, and optional mini evidence fields; they fail when `W < 420px`, `H < 260px`, pane width `<140px`, or the two panes are not definition-compatible.
- Decorative-looking layers are data-driven or removed.
- Long value, zero/null, denominator-zero, filtered-empty, no-permission, stale-data, loading, and error states are defined.
- Click, hover, or focus reveals formula/source/freshness and exact hidden trend values.
