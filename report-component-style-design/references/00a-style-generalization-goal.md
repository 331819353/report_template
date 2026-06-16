# Component Style Generalization Goal

Use this reference whenever screenshot samples, visual examples, or component-style requests are meant to become reusable design knowledge.

The goal is not to archive screenshots. The goal is to make every provided component style become a text-only, pattern-driven contract that a non-multimodal model can use to generate an adaptive design for a new business requirement.

## Generalization Target

For the user-provided sample universe, the standard aims for `100% routable coverage`:

- Every reusable sample maps to one existing pattern field, one composition of pattern fields, or a documented `requires-pattern-extension` gap.
- Every mapped pattern has a business trigger, data shape, component family, container size rule, internal slots, visual hierarchy, interaction/state contract, renderer owner, fallback path, and acceptance checklist.
- Every selected pattern can be generated from text contracts without retaining raw screenshot paths, image embeddings, or hidden visual memory.
- Every future requirement follows the same route: business question -> answer atom -> component family -> pattern field -> adaptive variables -> placement/fallback -> proof obligations.

`100% routable coverage` does not mean pixel-identical replication for unknown future designs. It means no provided style remains an opaque image-only reference, and no generator may silently invent a decorative one-off when an existing pattern or extension path is required.

## Canonical Workflow

1. Classify the business decision: state, target gap, trend, structure, ranking, process, cause, anomaly, detail, action, evidence, or data trust.
2. Choose the component family: KPI, target/actual card, chart card, table card, filter, ranking, list/status, overlay, conclusion card, or flow/hierarchy diagram.
3. Select a controlled pattern field from the binding contract, such as `kpiCardPattern`, `basicChartCardPattern`, `tableCardPattern`, `filterControlPattern`, or `overlayPanelPattern`.
4. Fill the adaptive variables: container size tier, title zone, value zone, plot/table/body zone, legend/control positions, item counts, density limits, tokens, and responsive fallback.
5. Bind data and interaction: grain, primary key, required fields, formulas, numeric format, controls, filters, tooltip/detail/export path, and loading/empty/error/no-permission states.
6. Validate with gates: text-only reproducibility, renderer ownership, layout fit, overflow strategy, exact-value access, anti-AI risks, and fallback behavior.

## Required Pattern Contract

Every reusable visual pattern must define:

```ts
type StyleGeneralizationContract = {
  sourceRole:
    | 'temporary-evidence'
    | 'exact-restoration-source'
    | 'visual-regression-baseline'
    | 'runtime-asset'
    | 'audit-evidence'
    | 'reusable-inspiration';
  generalizationStatus:
    | 'covered-by-existing-pattern'
    | 'covered-by-composed-patterns'
    | 'requires-pattern-extension'
    | 'out-of-scope-one-off';
  canonicalPatternRef: string;
  patternFields: string[];
  componentFamily: string;
  businessTrigger: string;
  dataShapeTrigger: string;
  adaptiveVariables: string[];
  minContainer: string;
  responsiveFallback: string[];
  rendererOwner: string;
  textOnlyReproduction: true;
};
```

For implementation-ready mapping rows, put this information in `styleGeneralization`.

## Current Pattern Universe

These pattern fields are the current reusable vocabulary. Prefer controlled values before creating a new family.

| Pattern field | Covered surface |
| --- | --- |
| `conclusionCardPattern` | Conclusion, evidence, action, and executive summary cards |
| `kpiCardPattern` | Plain KPI, target wave, mini bar trend, and lead line trend cards |
| `targetActualCardPattern` | KPI headline plus target/actual comparison bars |
| `targetActualTrendCardPattern` | KPI headline plus actual/comparison/target trends |
| `targetActualRadarCardPattern` | KPI headline plus product/object radar profiles |
| `targetActualDonutCardPattern` | KPI headline plus composition donut and bottom summary |
| `targetActualScatterCardPattern` | KPI headline plus relationship/scatter target evidence |
| `targetActualTablePattern` | Target/actual detail audit tables |
| `targetActualPivotTablePattern` | Target/actual hierarchy/pivot tables |
| `tableCardPattern` | Detail ledgers, operational tables, grouped headers, metric matrices, S2 cross tables, fixed wide tables, grouped subtotals, and tree tables |
| `rankingCardPattern` | Medal, bar-progress, and compact TOP ranking cards |
| `basicChartCardPattern` | Bar, line, area, combo, pie/donut, stacked bar, filtered bar, and tooltip trend cards |
| `specializedChartCardPattern` | Gauge, map, heatmap, K-line, boxplot, parallel, and bubble cards |
| `flowHierarchyDiagramCardPattern` | Funnel, Sankey, journey, tree, relation graph, sunburst, treemap, and path flow cards |
| `listStatusPattern` | Info lists, task lists, alerts, exceptions, chips, timelines, user/object lists, and mixed work items |
| `filterControlPattern` | Single select, multi-tag, date range, searchable select, tree path, advanced drawer, and combined chipbar |
| `overlayPanelPattern` | Filter drawers, action sheets, confirmation modals, fullscreen detail, notifications, navigation drawers, side details, and large panels |
| `microDashboardCardPattern` | Large single-topic mini dashboard cards that combine KPI strip, multiple small charts, status/detail evidence, and shared filters |
| `stateFeedbackPattern` | Empty, loading, error, no-permission, stale, partial, disabled, success, and building states |

## Adaptive Design Rules

- Match the pattern to the business job first, then adapt the visual density. Do not choose a pattern because it looks impressive.
- Preserve the underlying component renderer: ECharts for standard charts, AntV S2 for analytical pivot/cross tables, Element Plus or project controls for selectors, drawers, modals, lists, and simple tables.
- Treat color, radius, shadow, and gradients as semantic variables, not the source of the pattern. The pattern survives theme changes.
- Use composition before invention: a new card can combine a KPI headline, a chart pattern, local controls, and a bottom evidence strip if each child contract remains valid.
- When the container is too small, degrade predictably: reduce labels, collapse legends, move exact values to tooltip/drawer, paginate/scroll tables, or switch to fullscreen/detail.
- When data shape does not satisfy the pattern trigger, reject the pattern and pick a simpler chart, table, list, or KPI fallback.

## Extension Rules

Create a new pattern only when all of these are true:

- No existing pattern field or safe composition can represent the business task and data shape.
- The new pattern has at least one reusable trigger beyond a single screenshot.
- The pattern has a controlled enum value, selection rule, size/placement contract, data/interaction contract, fallback, and acceptance checklist.
- The binding contract, generation stability rules, mapping gates, component source map, and relevant chart/table/filter/design-system indexes are updated in the same change.

## Anti-AI Gate

Reject the design or keep readiness `partial` when:

- The source screenshot remains the only way to understand the style.
- A raw image path, embedding, or OCR text is treated as the durable standard.
- A sample is copied as decorative markup without business trigger, data contract, or fallback.
- A pattern is selected because it feels modern, high-end, blue, glassy, or polished, rather than because the data shape needs it.
- The generator invents a near-synonym enum instead of using the controlled vocabulary.
- The component has no exact-value path, state geometry, overflow strategy, or renderer ownership.

## Acceptance Checklist

- Every reusable sample is mapped to a pattern field, a composed pattern contract, or `requires-pattern-extension`.
- The chosen pattern answers a named business question and has required data fields.
- `styleGeneralization.textOnlyReproduction` is `true` for reusable knowledge.
- Raw screenshot paths are absent from long-lived skill references unless retained for runtime asset, exact restoration, visual baseline, or audit evidence.
- Pattern selection is deterministic under `report-info-component-mapping/references/08-generation-stability.md`.
- Mapping gates can validate the component without multimodal access to the original image.
