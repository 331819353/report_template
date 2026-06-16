# KPI Card Pattern Library

Use this reference after `04-kpi-metric-cards.md` when a report prototype or component spec needs KPI cards that feel product-specific rather than generic metric shells.

The pattern library does not replace the KPI data contract, numeric display contract, or placement rules. It chooses the card expression after the metric purpose, target/baseline, trend evidence, and parent viewport are known.

## Pattern Selection

Keep `visualType: "metric-card"` for all KPI cards. Add `kpiCardPattern` in component metadata or widget config to choose the internal expression.

| `kpiCardPattern` | Use when | Required data | Avoid when |
| --- | --- | --- | --- |
| `plain-metric` | The card only needs a current value and one or two comparisons. | metric name, value, unit, period, at least one baseline/comparison or status. | A target/progress/trend is the main evidence. |
| `target-wave` | Target attainment or completion rate is the main judgment. | value, target, attainment rate, unit, period, target formula. | No bounded target exists, or progress semantics are unclear. |
| `mini-bar-trend` | The user needs quick period volatility or recent distribution evidence. | value, unit, period, trend series with ordered categories, comparison values. | The series has fewer than three points or exact trend audit is the main task. |
| `highlight-line-trend` | One KPI should become the primary visual anchor in a KPI group or first viewport. | value, unit, period, trend series, latest point, comparison values, target or threshold when available. | Many cards need equal weight, or a dark/emphasis token is not approved. |

Selection order:

1. If target/achievement is the main question and `target` plus `attainmentRate` exist, choose `target-wave`.
2. If one card is the lead KPI and trend movement is business-critical, choose `highlight-line-trend`.
3. If recent period evidence matters but the card is not the lead KPI, choose `mini-bar-trend`.
4. Otherwise choose `plain-metric`.

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

## Data Contract

Implementation-ready KPI cards require these fields unless explicitly scoped out:

```ts
type KpiCardPattern =
  | 'plain-metric'
  | 'target-wave'
  | 'mini-bar-trend'
  | 'highlight-line-trend';

type KpiCardContract = {
  kpiCardPattern: KpiCardPattern;
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
- Decorative-looking layers are data-driven or removed.
- Long value, zero/null, denominator-zero, filtered-empty, no-permission, stale-data, loading, and error states are defined.
- Click, hover, or focus reveals formula/source/freshness and exact hidden trend values.
