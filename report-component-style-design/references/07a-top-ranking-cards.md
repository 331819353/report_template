# Top Ranking Card Patterns

Use this reference for TOP N ranking cards, leaderboard cards, and compact ranking summaries where the business question is "who leads, by how much, and what action follows".

Pair with:

- `07-cards-lists-tasks.md` for generic list/card overflow and interaction rules.
- `10-in-component-controls.md` when the card owns a local period, scope, metric, or dimension switch.
- `03-text-summary.md` when the ranking card contains a conclusion strip or recommendation.
- `06-binding-implementation-contract.md` for `rankingCardPattern`, field binding, and source-side Top N rules.

## Pattern Identity

Use:

```ts
componentType: card
visualType: ranking-list
rankingCardPattern:
  | medal-horizontal-ranking
  | bar-progress-ranking
  | compact-list-ranking
```

Do not map these cards as ordinary `bar` charts unless the primary visual is a full analytical chart with axes, legend, and chart interaction. A TOP N ranking card is a list component with metric-bearing rows, not just a decorative chart.

## Why These Cards Feel Designed

- They have a clear business sentence: "TOP5 by sales amount/order count", not a generic dashboard decoration.
- Ranking semantics are visible before reading numbers: rank badges, medals, crowns, row order, or bar length encode position.
- The top three are emphasized with different affordances, while ranks 4 and 5 stay quieter. This creates editorial hierarchy instead of uniformly loud AI polish.
- Values and shares are both present. The card answers absolute scale and contribution in one glance.
- The period switch is local to the ranking card and sits in the header, so the user knows exactly what will change.
- The conclusion strip converts the ranking into a decision: keep advantage, expand a weak region, or watch concentration.
- Decorations are semantic: trophy means ranking champion; target means goal/order performance. They are not random gradients, blobs, or glass effects.
- The geometry is constrained: fixed row count, consistent number columns, stable badges, and predictable bottom summary.

## Business Use

Use this component when:

- The task is locating leading or lagging objects: region, product, channel, salesperson, store, customer, project, supplier, or campaign.
- The ranking is part of a management report where exact values, contribution share, and a short conclusion are enough.
- The default visible set is Top 5 or Top 10, with a deterministic sort and a detail path for the full set.
- The user needs a first-screen "who is strongest/weakest" answer rather than full row audit.

Avoid this component when:

- The user needs exact row reconciliation, many columns, export, or audit. Use a detail table.
- The task is trend over time. Use a trend card.
- The task is composition with category share only. Use donut/bar composition.
- The object count is unstable or very large and the source cannot return a deterministic Top N.
- The ranking formula, denominator, or tie rule is missing.

## Pattern Selection

| Pattern | Use when | Visual signature |
| --- | --- | --- |
| `medal-horizontal-ranking` | One TOP5 card is a lead module and the user needs to see winners as a stage. | Wide card, top-left semantic icon, title/unit, top-right local period switch, five horizontal ranking slots, crowns/medals for top 3, value + share, bottom conclusion strip. |
| `bar-progress-ranking` | Relative magnitude and gap are more important than ceremony. | Header band or simple title row, rank badges down the left, horizontal bars scaled to the max row, right-aligned value and share, bottom conclusion strip. |
| `compact-list-ranking` | The card is narrow, secondary, embedded, or mobile. | Vertical rows, simple rank circles, value/share stacked or right-aligned, reduced decoration, optional short conclusion. |

Default to `bar-progress-ranking` for operational dashboards because it shows magnitude gaps most directly. Use `medal-horizontal-ranking` only when award-style emphasis is appropriate and enough width exists.

## Data Contract

Each ranking card must declare:

```ts
type TopRankingCardContract = {
  rankingCardPattern: RankingCardPattern;
  metricId: string;
  metricName: string;
  unit: string;
  topN: 5 | 10 | number;
  rankingOrder: 'desc' | 'asc';
  rankField: string;
  objectIdField: string;
  objectNameField: string;
  valueField: string;
  shareField?: string;
  denominatorField?: string;
  comparisonField?: string;
  targetField?: string;
  periodField?: string;
  localPeriodOptions?: string[];
  defaultPeriodOption?: string;
  tieBreakFields: string[];
  totalPolicy: 'all-filtered-rows' | 'visible-top-n' | 'api-provided-total';
  sourceDataset: string;
  numericFormatContractIds: string[];
  badgeRule: 'top3-medals' | 'rank-circles' | 'plain-rank';
  barEncoding?: {
    baseField: string;
    scaleMaxPolicy: 'max-visible-row' | 'target' | 'absolute-domain';
    minBarPx: number;
  };
  conclusionRule?: string;
  tooltipPayload: string[];
  detailAction?: string;
  stateRules: string[];
};
```

Required fields:

- Rank: `rank`, stable sort key, tie-breaker fields.
- Object: object id and display name.
- Metric: value field, unit, numeric format contract, null/zero behavior.
- Share: share numerator/denominator or API-provided share; do not hard-code percentages in labels.
- Period: selected period when a local period switch exists.
- Total policy: whether shares are against all filtered rows, visible Top N rows, or an API total.

Backend/API should return component-ready ranked rows. The frontend may format values and apply tiny already-returned local period switches only when the dataset is explicitly bounded.

## Shared Anatomy

1. Header: semantic icon, title, unit, and optional local period switch.
2. Ranking body: fixed Top N row/slot budget, rank signal, object name, value, and share.
3. Evidence encoding: medals/crowns, bars, subdued non-winners, or right-aligned numeric columns.
4. Conclusion strip: one sentence based on top object, concentration, weak tail, or target risk.
5. Tooltip/detail: full object name, rank, value, share denominator, comparison, target, and update time.

## Medal Horizontal Ranking

Minimum viable size:

- `W >= 720px`, preferred `880-1200px`.
- `H >= 260px`, preferred `300-360px`.
- Header band: `56-72px`.
- Ranking body: `120-160px`.
- Conclusion strip: `44-56px`.
- Horizontal visible count: default Top 5.

Slot rules:

- Top 3 use larger slots or framed cards. Ranks 4 and 5 may be columns without full cards.
- Rank 1 owns the strongest value color and largest value size.
- Rank 2 and 3 keep distinct medal colors but less emphasis than rank 1.
- Rank 4 and 5 use plain circular badges and quieter separators.
- Card bodies align object name, value, and share on the same vertical rhythm.
- Keep the crown/medal close to the rank badge; do not let it float as unrelated decoration.

Use this style for executive cards, leaderboard moments, and first-screen "winner" communication.

## Bar Progress Ranking

Minimum viable size:

- `W >= 640px`, preferred `760-1100px`.
- `H >= 300px`, preferred `320-420px`.
- Header/control band: `72-96px` when a colored wave header is used, otherwise `52-64px`.
- Row height: `34-44px`.
- Conclusion strip: `48-60px`.
- Visible count: Top 5 by default; Top 10 requires internal scroll or a taller block.

Row rules:

- Left rank badge width is fixed, usually `32-44px`.
- Object label column width is fixed or minmax so bar starts align.
- Bar track width is consistent for every row.
- Bar length maps to `valueField / maxVisibleValue` unless target or absolute-domain scaling is explicitly declared.
- Values and shares are right-aligned in separate stable columns.
- Shares use the same denominator as the card total policy.
- Top 3 may use medal colors; all bars should still belong to one accent family unless status coloring is meaningful.

Use this style when the gap between ranks matters, such as order count concentration, sales region distribution, or channel contribution.

## Compact List Ranking

Minimum viable size:

- `W >= 280px`, preferred `320-480px`.
- `H >= 220px`, preferred `260-360px`.
- Row height: `32-40px`.
- Visible count: Top 5; use a detail action for more rows.

Rules:

- Use simple rank circles or numeric text; avoid crowns in cramped cards.
- Keep object name left and value/share right.
- Hide long conclusion text; use one short line or tooltip.
- If values collide with object names, stack value above share on the right.
- If the card becomes record-like, switch to table.

## Visual Rules

- One dominant accent color per card family. Blue for sales/amount is acceptable; green for order/healthy growth is acceptable when project tokens allow.
- Decorative gradients must support the header or conclusion band, not compete with rank/value reading.
- Use tabular numerals for values, shares, and ranks.
- Values should be visually stronger than shares; object names should be stronger than units.
- Top 3 badges may use gold, silver, bronze. Do not color every row with unrelated colors.
- Bottom conclusion strip should be soft tint, not a second KPI card.
- Do not center the whole list. Ranking cards use row/slot alignment for scanning.

## Interaction And States

- Local period switch affects this component or declared local group only.
- Hover row/slot shows tooltip with exact value, share denominator, rank formula, comparison, target, and freshness.
- Click row/slot may emit `rankingItemClick` with object id, rank, metric id, period, active filters, and source dataset.
- Loading state preserves header, control, row skeleton count, and conclusion strip skeleton.
- Empty state says whether no data, no permission, no selected period, or no ranked objects.
- Tie state shows equal rank or stable secondary sort rule in tooltip.
- Stale state clears selected object if filters remove it.

## Conclusion Strip Rules

The conclusion must be generated from the ranking data, not generic praise.

Good conclusion patterns:

- `TOP1 object + leading position + recommended keep/expand action`.
- `Top3 concentration share + risk/opportunity statement`.
- `Bottom visible object or weak tail + improvement action`.
- `Target gap for ranked objects + follow-up direction`.

Avoid:

- "数据表现良好，请持续关注" with no object, value, or action.
- Conclusions that contradict rank/order.
- Repeating the title or only restating the top value.

## Anti-AI Gate

Reject or revise the card when:

- Medals/crowns appear but the sort order or rank field is missing.
- The bars are not data-driven or all bars are visually similar despite different values.
- Percent shares do not declare a denominator.
- The period switch changes only active style but not the ranking data.
- The conclusion is generic, ungrounded, or unrelated to the visible top/bottom objects.
- Every row is equally emphasized, making rank hierarchy unclear.
- The card uses random glow, glass, oversized radius, or decorative waves that reduce numeric legibility.
- More than Top 10 rows are crammed into one fixed card without scroll/detail/table fallback.

## Acceptance Checklist

- `componentType` is `card`, `visualType` is `ranking-list`, and `rankingCardPattern` is one of the controlled values.
- The card declares Top N, rank order, tie-break fields, total/share policy, and source dataset.
- Each visible metric-bearing value has a numeric display contract.
- Local period/scope controls declare `controlSemantics: local-filter` unless they change component schema.
- Source/API returns ranked component-ready rows or the bounded-local exception is explicitly justified.
- The visual hierarchy distinguishes top ranks without hiding lower ranks.
- The conclusion strip is data-grounded and has a stated rule.
- Tooltip/detail exposes exact value, share denominator, formula, and freshness.
- Loading, empty, no-permission, tie, and stale-selection states are defined.
