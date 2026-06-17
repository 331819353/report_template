# Decomposition, Attribution, Contribution, And Hierarchy Cards

Use this reference when a card explains how a metric is built, why it changed, which factors contributed, or how a hierarchy rolls up. The design goal is text-only reuse: a downstream model that cannot see the screenshots must still be able to select, size, bind, render, and validate the card.

## Why These Samples Feel Designed

- They have an analytical grammar before they have decoration. Formula cards show operators, attribution cards show contribution direction, contribution cards reconcile to a total, and hierarchy cards show levels and parent-child responsibility.
- They keep the root metric visible while users inspect the explanation path. The title, root value, active tab, and update/freshness line anchor the card so the chart is not an isolated illustration.
- They separate "what happened" from "why it happened". Values, deltas, shares, contribution rates, and residual/other buckets are explicit instead of implied by shape alone.
- They use the right geometry for the business question: formula for multiplicative drivers, waterfall for signed additive variance, Sankey for flow allocation, tree for ownership or hierarchy, heatmap/matrix for cross attribution.
- They reserve exact-value routes. Good cards include detail tabs, side lists, bottom summaries, update time, or drilldown affordances so the visual never becomes decorative evidence.
- They avoid AI flavor by staying constrained: small palette, light borders, clear hierarchy, real numbers, local controls that affect only the card, and no generic "insight" copy without data proof.

## Controlled Pattern Field

Use `decompositionAttributionCardPattern` when the component is one self-contained card whose primary job is explaining metric structure, drivers, attribution, contribution, or hierarchy.

```ts
type DecompositionAttributionCardPattern =
  | 'formula-decomposition-card'
  | 'funnel-decomposition-card'
  | 'tree-decomposition-card'
  | 'sankey-decomposition-card'
  | 'driver-factor-decomposition-card'
  | 'variance-waterfall-decomposition-card'
  | 'combined-decomposition-card'
  | 'multilevel-metric-decomposition-card'
  | 'total-attribution-card'
  | 'funnel-attribution-card'
  | 'channel-attribution-donut-card'
  | 'touchpoint-attribution-list-card'
  | 'segment-attribution-card'
  | 'feature-attribution-bar-card'
  | 'time-attribution-waterfall-card'
  | 'multidimensional-attribution-matrix-card'
  | 'overall-contribution-card'
  | 'contribution-waterfall-card'
  | 'contribution-structure-card'
  | 'contribution-comparison-card'
  | 'contribution-trend-card'
  | 'contribution-tree-card'
  | 'key-contribution-topn-card'
  | 'contribution-heatmap-card'
  | 'progressive-hierarchy-decomposition-card'
  | 'hierarchy-tree-decomposition-card'
  | 'hierarchy-waterfall-card'
  | 'indented-hierarchy-table-card'
  | 'hierarchy-share-card'
  | 'path-contribution-card'
  | 'multilevel-comparison-hierarchy-card'
  | 'target-attainment-hierarchy-attribution-card';
```

## Pattern Selection

| Business trigger | Pattern | Primary geometry | Required proof |
| --- | --- | --- | --- |
| A metric equals a formula such as revenue = price * orders * conversion | `formula-decomposition-card` | metric tokens linked by operators | formula, factor values, operator order, root reconciliation |
| A root metric is explained by ordered funnel stages | `funnel-decomposition-card` | funnel or horizontal stages | ordered stages, stage value, stage share, drop/conversion if used |
| A root metric splits into parent-child metric nodes | `tree-decomposition-card` | compact tree | node id, parent id, value, level, rollup policy |
| A root value flows into categories, regions, or outcomes | `sankey-decomposition-card` | Sankey | source, target, value, unit, aggregation policy |
| Drivers explain a growth/change result | `driver-factor-decomposition-card` | driver tree/list | baseline, current, driver value, contribution, confidence |
| Signed changes bridge baseline to current | `variance-waterfall-decomposition-card` | waterfall | start, signed deltas, end, residual, sign rule |
| Multiple small explanations are needed in one card | `combined-decomposition-card` | KPI + mini charts/table | primary explanation, secondary evidence limit, exact path |
| Three or more metric levels must remain visible | `multilevel-metric-decomposition-card` | hierarchy tree/table | level fields, visible depth, expand/collapse, rollup |
| Overall change needs attribution by quantity and price/quality/effect | `total-attribution-card` | formula strip + bars | attribution method, baseline, contribution value/rate |
| Ordered conversion attribution is primary | `funnel-attribution-card` | funnel + attribution columns | stage attribution, conversion/drop, same cohort rule |
| Channel contribution should show share and value | `channel-attribution-donut-card` | donut + attribution list | channel id/name, contribution, share, total, method |
| Touchpoints or steps drive a result | `touchpoint-attribution-list-card` | stepped list/timeline | touchpoint order, contribution, share, attribution method |
| User/customer/product segments explain change | `segment-attribution-card` | segmented table/list | segment id, contribution, share, delta, total |
| Product features explain a target metric | `feature-attribution-bar-card` | horizontal bars | feature id, contribution, rank, share, direction |
| Attribution changes over time | `time-attribution-waterfall-card` | time waterfall | time grain, signed deltas, cumulative/period rule |
| Two dimensions cross to explain contribution | `multidimensional-attribution-matrix-card` | matrix/heatmap table | row dimension, column dimension, contribution, total |
| Contribution is a compact summary | `overall-contribution-card` | KPI + ranked bars | root total, contributor value/share, top contributor |
| Contributions bridge from baseline to target/current | `contribution-waterfall-card` | waterfall | additive positive/negative values, subtotal/end value |
| Contribution structure matters more than ranking | `contribution-structure-card` | donut/treemap | total, category contribution, share, other policy |
| Contributors must be compared side by side | `contribution-comparison-card` | bars/table | comparable dimension, metric, delta/share/rank |
| Contribution movement across time matters | `contribution-trend-card` | multi-series trend | time grain, contributor series, total reconciliation |
| Parent-child contribution is primary | `contribution-tree-card` | tree or tree list | hierarchy, contribution values, parent share |
| The top contributors answer the question | `key-contribution-topn-card` | Top N list/bars | rank, contribution, share, cumulative or total |
| Contribution by time and dimension is dense | `contribution-heatmap-card` | heatmap/matrix | time/dimension cells, value, color scale, detail |
| A hierarchy should read as step-by-step rollup | `progressive-hierarchy-decomposition-card` | vertical levels | level order, value/share per level, comparison with parent |
| A formal hierarchy is the answer | `hierarchy-tree-decomposition-card` | tree chart | root, parent-child, visible depth, collapse behavior |
| Level-by-level loss/gain should be compared | `hierarchy-waterfall-card` | waterfall by level | signed level deltas, baseline/current, residual |
| Dense hierarchy needs rows, not shapes | `indented-hierarchy-table-card` | tree table | row hierarchy, expand state, visible columns |
| Parent/child shares across levels matter | `hierarchy-share-card` | stacked bars or share rows | parent total, child share, level share, total share |
| Contribution flows through named paths | `path-contribution-card` | path/tree flow | path id, source, target, contribution, path share |
| Same hierarchy needs current vs baseline comparison | `multilevel-comparison-hierarchy-card` | hierarchy table | current, baseline, change, level, rollup |
| Target attainment must be attributed by hierarchy | `target-attainment-hierarchy-attribution-card` | target card + hierarchy | actual, target, attainment, node contribution/gap |

## Evidence Binding

Every selected card must carry `decompositionAttributionEvidenceBinding` or an equivalent project contract.

```ts
type DecompositionAttributionEvidenceBinding = {
  decompositionMode:
    | 'formula'
    | 'driver'
    | 'attribution'
    | 'contribution'
    | 'variance'
    | 'hierarchy'
    | 'path'
    | 'matrix';
  metricId: string;
  metricName: string;
  unit: string;
  rootMetricId?: string;
  rootValueField: string;
  baselineValueField?: string;
  currentValueField?: string;
  targetValueField?: string;
  attainmentRateField?: string;
  formulaText?: string;
  formulaOperatorField?: string;
  nodeDatasetId?: string;
  nodeIdField?: string;
  nodeNameField?: string;
  parentIdField?: string;
  levelField?: string;
  pathField?: string;
  orderField?: string;
  valueField: string;
  comparisonValueField?: string;
  deltaValueField?: string;
  deltaRateField?: string;
  contributionValueField?: string;
  contributionRateField?: string;
  shareField?: string;
  parentShareField?: string;
  totalShareField?: string;
  directionField?: string;
  signRule: 'positive-is-good' | 'negative-is-good' | 'signed-neutral' | 'domain-defined';
  attributionMethod?: 'first-touch' | 'last-touch' | 'linear' | 'position-based' | 'shapley' | 'rule-based' | 'model-based' | 'domain-defined';
  reconciliationPolicy: 'must-equal-root' | 'allow-residual' | 'non-additive-explained' | 'model-estimate';
  residualField?: string;
  otherPolicy?: 'topn-plus-other' | 'small-item-merge' | 'show-residual' | 'none';
  stageField?: string;
  sourceField?: string;
  targetField?: string;
  linkValueField?: string;
  timeField?: string;
  rowDimensionField?: string;
  columnDimensionField?: string;
  confidenceField?: string;
  tooltipPayload: string[];
  detailAction?: string;
};
```

## Anatomy

Standard cards use the following regions:

1. Header: index/title, optional info icon, local tab or selector, and optional "more" action. The title names the explanatory job, such as "利润归因拆解", not only the chart type.
2. Root metric band: root value, baseline/target/current context, comparison or status chip. This band may collapse in table-heavy cards but must remain available through a summary strip or tooltip.
3. Explanation body: formula, funnel, tree, Sankey, waterfall, matrix, list, or bars. The body must own at least `52%` of card height in visual-heavy cards.
4. Evidence/detail band: exact rows, top contributors, summary cells, update time, detail tab, or drilldown entry.
5. State band: loading/empty/error/no-permission states preserve the same root/body/detail geometry.

## Size Rules

Use these as component minimums before adapting to page grid spans.

| Size family | Min outer size | Use for | Body minimum |
| --- | ---: | --- | --- |
| `decomposition_card` | `480x320` | formula, driver, overall contribution, compact attribution | body `>=160px`, detail band `>=44px` |
| `decomposition_flow_card` | `560x340` | funnel, Sankey, path contribution | flow body `>=190px`, label columns reserved |
| `decomposition_hierarchy_card` | `560x360` | tree, multilevel metric, hierarchy share | hierarchy body `>=200px`, node min `76x34` |
| `decomposition_matrix_card` | `640x360` | attribution matrix, heatmap, hierarchy table | matrix/table body `>=220px`, at least `4` useful rows |
| `contribution_heatmap_card` | `560x340` | contribution heatmap or dense contribution table | heatmap body `>=200px`, legend `>=72px` |

Compact embedded cards may shrink to `360x260` only when there is one root metric, one simple visual, `<=4` visible factors, and a detail route. Do not shrink tree/Sankey/matrix cards below their body floors.

## Data And Interaction Rules

- Formula cards require formula order and operator semantics. Do not show a multiplication or equality chain unless the fields actually reconcile.
- Additive contribution and waterfall cards require signed values, baseline, end value, and residual policy. Positive and negative colors follow business direction, not generic red/green assumptions.
- Attribution cards require an attribution method. If the method is unknown, label the card as contribution or driver evidence rather than causal attribution.
- Hierarchy cards require stable node IDs, parent IDs, levels, and a default expanded depth. Orphan nodes fail acceptance.
- Flow cards require directed `source`, `target`, and `value` fields. Negative values in Sankey/funnel/path flows are invalid.
- Matrix and heatmap cards require bounded row/column counts. Default visible cells should stay within `8 x 6`; larger matrices need scroll, paging, drawer, or fullscreen.
- Every card has an exact-value route through tooltip, side list, table tab, drawer, or fullscreen. Shapes alone are not evidence.
- Local tabs such as "指标拆解/明细数据" or "贡献值/贡献率" are component-local. They must not silently change page-level filters or export scope.
- Update time/source freshness is recommended for any card used to explain business decisions.

## Style Rules

- Keep the root metric and decomposition body in one visual rhythm: same numeric formatter, same unit, same filter period.
- Use color families by semantic role: root/current, positive contribution, negative contribution, neutral/residual, hierarchy group, and selected node. Avoid assigning new colors to every minor node.
- Use light node backgrounds, thin connectors, and reserved gutters. Connectors must terminate at node edges and never cross labels.
- Use permanent labels only for root, key nodes, top factors, and selected state. Secondary labels move to tooltip/detail.
- Prefer tables when exact comparison is the main task; prefer diagram geometry only when structure, flow, or explanatory path is the task.

## Fallback Rules

- Missing formula or rollup proof: use `overall-contribution-card`, ranked bars, or a detail table, not formula/tree decomposition.
- Missing attribution method: downgrade attribution wording to contribution/driver evidence.
- Missing additive signed values: do not use waterfall; use bars/table/tree.
- Too many nodes: show Top N + other, default collapse to `2-3` levels, or move to fullscreen/detail.
- Too little card space: keep root metric, one primary explanation, and detail route; remove decorative icons, reduce secondary cells, collapse tabs to dropdown, then split the card.
- Dense matrix/table cannot fit: keep summary card plus "view detail" action; do not compress rows or columns below readability.

## Anti-AI Pitfalls

- Do not present a causal claim when the data only supports correlation or descriptive contribution.
- Do not use Sankey, tree, or funnel because the shape looks sophisticated. Require the matching nodes, links, stages, or formula.
- Do not hide residual, "other", rounding differences, or unmatched children. Reconciliation is part of the design.
- Do not use generic copy such as "核心因素表现良好" without naming the factor, value, direction, and evidence path.
- Do not keep screenshot images as the durable standard. Store this controlled pattern, binding fields, size family, and fallback instead.

## Acceptance Checklist

- `decompositionAttributionCardPattern` is selected from the controlled values.
- `decompositionAttributionEvidenceBinding` declares root metric, value fields, sign rule, reconciliation policy, tooltip payload, and detail action.
- The selected pattern has the required data shape: formula, stages, nodes, links, matrix dimensions, or signed deltas.
- Root value and child values reconcile according to the declared policy, or residual/other is visible.
- Minimum size family is satisfied, or a documented fallback is selected before implementation.
- Exact values, update/source, state geometry, and overflow behavior are defined.
- The design can be reproduced from text by a non-multimodal model without raw screenshots or image embeddings.
