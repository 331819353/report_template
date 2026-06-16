# KPI Card Pattern Library

Use this reference after `04-kpi-metric-cards.md` when a report prototype or component spec needs KPI cards that feel product-specific rather than generic metric shells, including portrait KPI cards and landscape/horizontal KPI cards.

The pattern library does not replace the KPI data contract, numeric display contract, or placement rules. It chooses the card expression after the metric purpose, target/baseline, trend evidence, and parent viewport are known.

## Pattern Selection

Keep `visualType: "metric-card"` for all KPI cards. Add `kpiCardPattern` in component metadata or widget config to choose the internal expression.

| `kpiCardPattern` | Use when | Required data | Avoid when |
| --- | --- | --- | --- |
| `plain-metric` | The card only needs a current value and one or two comparisons. | metric name, value, unit, period, at least one baseline/comparison or status. | A target/progress/trend is the main evidence. |
| `target-wave` | Target attainment or completion rate is the main judgment. | value, target, attainment rate, unit, period, target formula. | No bounded target exists, or progress semantics are unclear. |
| `mini-bar-trend` | The user needs quick period volatility or recent distribution evidence. | value, unit, period, trend series with ordered categories, comparison values. | The series has fewer than three points or exact trend audit is the main task. |
| `highlight-line-trend` | One KPI should become the primary visual anchor in a KPI group or first viewport. | value, unit, period, trend series, latest point, comparison values, target or threshold when available. | Many cards need equal weight, or a dark/emphasis token is not approved. |
| `horizontal-trend-compare` | A landscape KPI needs current value, prior/baseline comparison, and a small trend line. | value, unit, comparison label/value, ordered trend series, tooltip payload. | The trend needs axes, target lines, or exact audit. |
| `horizontal-ring-progress` | A landscape KPI needs a bounded status/progress reading such as OEE, utilization, SLA, or completion. | value, min/max or target range, progress rate, prior/baseline value, status direction. | The metric is unbounded or compares many categories. |
| `horizontal-target-progress` | A landscape KPI needs target attainment with a linear progress track and optional target marker. | value, target, attainment rate, target direction, target label/formula. | A circular gauge or detailed variance chart is the main task. |
| `horizontal-status-trend-compare` | A business-negative or quality metric needs before/after comparison and a compact trend. | current value, prior value, improvement/change rate, direction semantics, trend series. | Direction semantics are unknown or lower-is-better is not declared. |
| `horizontal-grain-bar-switch` | A KPI card includes a small time-grain switch and mini bars for recent distribution. | value, comparison, time-grain options, ordered bar series, selected period. | More than one local filter group is required. |
| `horizontal-period-summary-strip` | The card compares current/previous/target values in a bottom strip rather than a chart. | current value, prior value, target value, comparison label, selected period. | A trend or distribution is required to explain the judgment. |
| `horizontal-pp-assist-info` | A percent/ratio metric needs a percentage-point delta plus an auxiliary evidence panel. | value, baseline value, pp delta, evidence label/value, optional mini bars. | The delta is a percent change rather than percentage-point movement. |
| `horizontal-warning-status-band` | A KPI needs a visible warning/status badge plus a bottom alert band. | value, threshold, status, warning reason, selected status/period, action/detail path. | The status is neutral or no threshold/action path exists. |

Selection order:

1. If the parent container is landscape, wide, or row-based and `W >= 360px`, choose a horizontal pattern when the supporting evidence can fit without becoming a full chart.
2. For horizontal cards, choose by evidence type: trend comparison -> `horizontal-trend-compare`; bounded ring status -> `horizontal-ring-progress`; target bar -> `horizontal-target-progress`; lower-is-better status trend -> `horizontal-status-trend-compare`; local time-grain bars -> `horizontal-grain-bar-switch`; current/prior/target strip -> `horizontal-period-summary-strip`; percentage-point delta -> `horizontal-pp-assist-info`; threshold warning -> `horizontal-warning-status-band`.
3. If target/achievement is the main question and `target` plus `attainmentRate` exist but the card is portrait/narrow, choose `target-wave`.
4. If one card is the lead KPI and trend movement is business-critical, choose `highlight-line-trend`.
5. If recent period evidence matters but the card is not the lead KPI, choose `mini-bar-trend`.
6. Otherwise choose `plain-metric`.

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
| Wide banner | `560-760px` | `160-240px` | Split value/evidence zones; can show a larger trend, ring, strip, or warning band. |

Landscape slot minimums:

- Title/control row: `28-40px`.
- Primary value column: `140-220px` wide.
- Auxiliary visual zone: at least `96x72px`; ring/progress/gauge-like visuals need `108x96px`.
- Bottom evidence band: `44-68px` when present.
- Mini line/bar evidence: plot or glyph band `48-72px`; do not render axis labels inside a landscape KPI card.
- Linear target progress track: at least `200x24px` for track + marker + min/max labels.

### Pattern: `horizontal-trend-compare`

Use for KPI cards like production volume, energy, orders, visits, or other current values that need a compact trend and a named baseline such as `同比`, `环比`, or `较去年同期`.

Rules:

- Primary value stays left. Trend evidence sits in the lower or right band.
- Trend line hides axes and permanent point labels; exact points live in tooltip.
- A faint domain icon may sit in the right background only when it supports the metric meaning and does not reduce contrast.
- If the trend needs target bands, annotations, or axis reading, use a full line chart block instead.

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

type KpiCardContract = {
  kpiCardPattern: KpiCardPattern;
  kpiCardOrientation?: KpiCardOrientation;
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
- Decorative-looking layers are data-driven or removed.
- Long value, zero/null, denominator-zero, filtered-empty, no-permission, stale-data, loading, and error states are defined.
- Click, hover, or focus reveals formula/source/freshness and exact hidden trend values.
