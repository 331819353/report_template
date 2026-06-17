# Insight And KPI Placement Algorithms

This file was split from `12-internal-placement-algorithms.md`. Load it only when the matching component family is present.

## Analysis & Insight Component Placement Algorithm

Use this for conclusion cards, insight cards, anomaly/risk explanations, attribution summaries, recommendation cards, data-quality notes, definition cards, forecast notes, explanatory empty states, task cards, and chart annotations. These components are analysis surfaces, not decorative text blocks. They should turn data into judgment, reason, action, or trust context.

### Anatomy

| Slot | Required | Default behavior |
| --- | ---: | --- |
| Type marker/status label | Yes | Top-left, weak label or slim status bar |
| Semantic icon | Optional | `14-18px`, aligned to title, never dominant |
| Title | Yes except summary bar | Top-left, names the subtype or question |
| Component-local filter | Optional | Header-right capsule/dropdown; current component only |
| Main conclusion | Yes | First readable body line, strongest text |
| Evidence | Required when data-backed | Metric, baseline, comparison, affected object, source, or reason |
| Recommended action/detail route | Required for recommendation/risk/task; optional elsewhere | Bottom-right or final line |
| Definition/confidence/freshness | Required for definition/data-quality/prediction; optional elsewhere | Bottom-left, tooltip, or drawer |
| Tooltip/detail payload | Required when anything is clamped | Hover/focus/click disclosure |

Implementation-ready components declare `analysisInsightContract` or equivalent metadata: subtype, insight family, conclusion, evidence, affected object, comparison/change value, reasons, recommended actions, confidence/definition/source/freshness, local filters, tooltip payload, detail route, and state rules.

### Size Tiers

| Tier | Width | Height | Permanent content | Move or hide |
| --- | ---: | ---: | --- | --- |
| Summary bar | `280-960px` | `36-56px` | one sentence, optional status | title, icon, secondary evidence |
| Small card | `220-360px` | `88-128px` | title, conclusion, one evidence line | action label, freshness, secondary reason |
| Standard card | `320-560px` | `120-180px` | title, conclusion, evidence, optional action | extra insights, long definition |
| Enhanced card | `480-720px` | `160-240px` | Top reasons/actions, confidence, detail route | long explanation to drawer |
| Side insight panel | `220-320px` | `240-480px` | `2-4` insight items | secondary action/source |
| Annotation bubble | `120-240px` | `40-96px` | short conclusion, optional value | title, long explanation |

### Padding And Line Budgets

```text
P = clamp(12px, W * 0.04, 24px)
headerH = 20-28px
conclusionLineH = 20-24px
bodyLineH = 18-20px
footerH = 0-32px
gapTitleBody = 8-12px
gapConclusionEvidence = 6-8px
gapBodyAction = 8-12px
```

Padding tiers:

| Container width | Padding |
| ---: | ---: |
| `W < 280px` | `12px` |
| `280px <= W < 480px` | `16px` |
| `480px <= W < 720px` | `20px` |
| `W >= 720px` | `24px` |

Height check:

```text
requiredContentHeight =
  P * 2
  + headerH
  + visibleConclusionLines * conclusionLineH
  + visibleEvidenceLines * bodyLineH
  + visibleActionOrFooterH
  + sum(visibleGaps)

requiredContentHeight <= H
```

If the budget fails, remove optional content in this order: decorative icon, secondary evidence, freshness/source line, long action label, extra insight items. Do not hide the main conclusion or status meaning without tooltip/drawer access.

### Slot Position Rules

Header:

```text
headerX = P
headerY = P
iconSize = 14-18px
typeMarkerW = measuredText + 12px
filterMaxW = min(CW * 0.45, 280px)

titleX = P + visibleIconW + iconGap
titleMaxW = CW - visibleIconW - iconGap - visibleFilterW - 12px
filterX = W - P - filterW
filterY = P + (headerH - filterH) / 2
```

Body:

```text
conclusionX = P
conclusionY = P + headerH + gapTitleBody
conclusionW = CW

evidenceY = conclusionY + conclusionH + gapConclusionEvidence
evidenceW = CW
```

Footer/action:

```text
footerY = H - P - footerH
actionX = W - P - actionW
actionY = footerY + (footerH - actionH) / 2
metaX = P
metaW = max(0, CW - actionW - 12px)
```

Rules:

- The conclusion owns the first body line. Evidence never appears above it.
- Values inside evidence can right-align only when the evidence is rendered as a compact list.
- Actions and detail links cannot overlap evidence text; they move to a final row or icon button before shrinking the conclusion.
- Source/freshness/confidence should be weak, but discoverable.

### Local Filter Rules

Analysis & Insight local filters are optional and usually inherit page/global, Composite Panel, or chart filters first. Add a component-local filter only for explanation mode switches such as:

- `全部 / 异常 / 建议`
- `本月 / 本季 / 本年`
- `实际 / 预测`
- `高 / 中 / 低风险`
- `原因 / 影响 / 建议`

```text
filterH = 24-28px
optionW = clamp(44px, textWidth + 24px, 96px)
filterMaxW = min(CW * 0.45, 280px)
```

When the capsule does not fit, collapse to a compact dropdown. The filter must not change global/page scope, metric口径, table schema, permission, pagination, export, or another component.

### Chart And Composite Placement

Chart-side insight:

```text
insightW = clamp(200px, W * 0.28, 320px)
mainChartW = W - insightW - gap
insightArea <= W * H * 0.25
```

Rules:

- Above-chart summary uses `36-56px` height and one sentence.
- Right-side insight panels use `2-4` items and do not exceed `25%` of a Composite Panel area unless the panel's declared purpose is explanation.
- Chart annotations use a bounded bubble and leader line:

```text
bubbleW = clamp(120px, textWidth + 32px, 240px)
bubbleH = clamp(40px, lineCount * 18px + 20px, 96px)
leaderLine = 12-48px
annotationCount <= 3
```

Annotations cannot cover axis labels, legends, selected marks, or the main anomaly point they explain.

### Responsive Degradation

| Condition | Behavior |
| --- | --- |
| `W < 280px` or `H < 96px` | Hide subtitle/evidence, hide or shrink icon, collapse action/filter, keep conclusion `1-2` lines |
| `280px <= W < 560px` and `H >= 120px` | Title, conclusion, one evidence line, weak status |
| `W >= 560px` and `H >= 160px` | Multi-insight list, Top3 reasons, action suggestions, confidence/source |
| `H < 120px` | No under-title filter row; use inline/collapsed control |
| Long explanation | Clamp to visible budget and disclose through tooltip/drawer |

### Subtype Fit Rules

- Conclusion card: `320-560px` wide, `96-144px` high, one conclusion plus one evidence line.
- Insight card: `2-4` insights by default, max `5`, item height `22-28px`.
- Anomaly/risk card: reserve object, metric, magnitude, and action; use weak warning tint or `3-4px` left bar, not full-card red.
- Attribution/impact card: Top `3` reasons by default, max `5`; contribution values align right.
- Target diagnosis card: current, target, and gap are mandatory; forecast text must be marked `预计`.
- Recommendation/task card: `1-3` actions; owner/deadline/status fit in footer or drawer.
- Definition/data-quality card: definition/source/freshness/confidence are mandatory; complex text opens popover/drawer.
- State explanation card: reason, impact, and next step are mandatory; not only `暂无数据`.

### State Geometry

- Loading: skeleton header plus `1-3` text rows in the same slots.
- Generating: stable message row `分析生成中`.
- Insufficient data: preserve conclusion slot with `当前数据不足以生成结论`, then show missing reason/action.
- Empty/filter no-result: state message occupies conclusion slot and names the condition.
- Data delay: use data-quality tone, freshness field, and retry/detail action.
- Error/no-permission: show reason and next step without masking unrelated sibling components.

## Metric Card Placement Algorithm

Use this for KPI cards, metric cards, target cards, comparison tiles, and mini-trend cards.

### Anatomy

| Slot | Required | Default behavior |
| --- | ---: | --- |
| Metric title | Conditional | Top-left only for standalone KPI cards or when the surrounding block title does not already identify the metric |
| Definition/help entry | Optional | Top-right icon, opens tooltip/drawer |
| Component-local filter | Optional | Header-right capsule/dropdown, affects only this card |
| Value group | Yes | Metric value plus unit, centered as one group |
| Comparison group | Yes | YoY/MoM or one priority comparison, centered below value |
| Target group | Yes when target exists | Target value, attainment, target gap, or progress |
| Sparkline | Optional | Secondary trend, full content width or centered reduced width |
| Summary | Optional | Short judgment, centered or left-aligned by card type |
| Description/metadata | Optional | Bottom weak text, source, freshness, or data delay |

### Size Tiers

| Tier | Condition | Permanent content | Move or hide |
| --- | --- | --- | --- |
| Small | `W < 200px` or `H < 110px` | title, value group, one priority comparison | target, sparkline, summary, description |
| Standard | `200px <= W < 360px` and `120px <= H < 180px` | title, value group, YoY/MoM, target text | sparkline only when height allows; description in tooltip |
| Enhanced | `W >= 360px` and `H >= 180px` | title, value group, YoY/MoM, target, optional sparkline, short summary | long definition in tooltip/drawer |
| Wide | `W >= 480px` | left primary value zone plus right auxiliary zone | keep value centered within the left zone, not the full card |

Recommended card ranges:

| Type | Width | Height | Use |
| --- | ---: | ---: | --- |
| Small card | `160-220px` | `96-120px` | value plus one comparison |
| Standard card | `220-320px` | `120-160px` | value, comparison, target |
| Enhanced card | `320-480px` | `160-220px` | value, comparison, target, sparkline or summary |
| Wide card | `480px+` | `160-240px` | split primary and auxiliary information |
| Landscape KPI card | `420-560px` | `180-240px` | value, comparison/status, one auxiliary evidence visual |
| KPI overview card | `720-960px` | `220-320px` | one domain/topic, `2-5` metrics, comparison/target cells, and optional compact evidence |
| Single-indicator KPI grid card | `360-460px` | `220-320px` | one metric, one comparison, one mini evidence visual, target/progress footer |
| KPI judgment card | `360-460px` | `240-360px` | one status/health/rating/gauge judgment, one semantic hero visual, comparison strip, and footer evidence |
| KPI goal execution card | `360-520px` | `240-360px` | one target attainment/gap/progress/milestone execution judgment, one execution hero visual, comparison strip, and deadline/footer evidence |
| KPI time-series analysis card | `360-520px` | `240-360px` | one trend/change/YoY-MoM/cycle/volatility/forecast judgment, one time-series evidence zone, and footer baseline/stat/forecast evidence |
| KPI comparison analysis card | `360-560px` | `240-380px` | one direct/group/competitor/benchmark/variance comparison judgment, one comparison evidence zone, and footer rank/gap/benchmark evidence |
| Axis-scatter diagnostic KPI card | `420-560px` | `300-360px` | value, comparison/status, readable scatter evidence with axes/reference/quadrant body |
| Spatial-map diagnostic KPI card | `460-640px` | `320-380px` | value, comparison/status, geography evidence with projection-safe map body |
| Paired comparison diagnostic KPI card | `420-560px` | `260-340px` | two comparable panes, central VS rail, bottom conclusion |
| Compact KPI row | `360-420px` | `128-160px` | value, one comparison/status, compact icon/progress |
| Wide KPI banner | `560-760px` | `160-240px` | split primary value zone plus right/bottom evidence zone |

### Title Ownership

Metric title is a visible layout slot only when the KPI card is standalone, when the block/container has no visible title, or when multiple body metrics need distinct sub-labels.

```text
displayTitle = visible block/card title
metricName = semantic metric name for tooltip/export/definition
bodyMetricLabel = visible KPI body label/title
showBodyMetricLabel = explicit boolean override
```

Rules:

- If a surrounding block/container already renders `displayTitle`, and `normalized(displayTitle)` equals or is highly similar to `normalized(bodyMetricLabel)` or `normalized(metricName)`, set `showBodyMetricLabel = false` by default.
- `metricName` remains available in tooltip, export, drilldown payload, definition/help, or口径说明 even when the body label is hidden.
- Body labels in embedded KPI blocks are allowed only when they disambiguate multiple metrics in the same block, for example `满意度得分` vs `有效样本`, or when an explicit standalone-card mode is declared.
- A visible duplicate block title + KPI body label is `VIS-DUPLICATE-TITLE`, not a harmless style choice.

### Padding And Slot Heights

```text
P = clamp(12px, W * 0.05, 24px)
titleHeight = clamp(20px, H * 0.16, 28px)
valueHeight = clamp(36px, H * 0.35, 64px)
compareHeight = clamp(20px, H * 0.18, 32px)
targetHeight = clamp(22px, H * 0.18, 36px)
sparkHeight = clamp(28px, H * 0.22, 56px)
descriptionHeight = clamp(18px, H * 0.18, 40px)
valueAnchorViewportY = P + titleHeight
valueAnchorViewportH = H - P * 2 - titleHeight - visibleFooterOrMetadataH
```

Padding tiers:

| Container width | Padding |
| ---: | ---: |
| `W < 200px` | `12px` |
| `200px <= W < 320px` | `16px` |
| `320px <= W < 480px` | `20px` |
| `W >= 480px` | `24px` |

### Default Vertical Flow

```text
currentY = P

titleY = currentY
currentY += titleHeight

currentY += 8-12px
valueY = currentY
currentY += valueHeight

currentY += 8-10px
compareY = currentY
currentY += compareHeight

if sparkline is visible:
  currentY += 8-12px
  sparkY = currentY
  currentY += sparkHeight

currentY += 8-12px
targetY = currentY
currentY += targetHeight

if summary is visible:
  currentY += 6-8px
  summaryY = currentY
```

Before accepting the layout, compute:

```text
requiredContentHeight =
  P * 2
  + titleHeight
  + valueHeight
  + compareHeight
  + visibleSparkHeight
  + targetHeight
  + visibleSummaryOrDescriptionHeight
  + sum(verticalGaps)

requiredContentHeight <= H
```

If the budget fails, remove or move optional content in this order: description, summary, sparkline, second comparison, target progress bar. Do not shrink primary value text below readable size.

The fit proof must measure the actual rendered value group, not only the row allocation. A grid row such as `minmax(42px, 1fr)` is not sufficient if the numeral sits at the row's top edge.

### Landscape Metric Card Split

Use this algorithm when `kpiCardOrientation` is `landscape`, `compact-row`, or `wide-banner`, or when `kpiCardPattern` starts with `horizontal-`.

```text
headerH = clamp(28px, H * 0.18, 40px)
footerBandH =
  0 when no bottom evidence band exists
  clamp(44px, H * 0.26, 68px) when comparison strip, mini bars, or warning band exists

bodyY = P + headerH
bodyH = H - P - bodyY - footerBandH
primaryW = clamp(140px, CW * 0.46, 220px)
auxW = CW - primaryW - 16px
primaryX = P
auxX = P + primaryW + 16px
primaryCenterX = primaryX + primaryW / 2
```

Slot rules:

- Header owns title and one local control. It must not create a second filter row.
- Primary value, unit, and main comparison/status center inside the primary zone or left-align only when `alignmentIntent: scan-left` is declared.
- Auxiliary zone owns exactly one evidence visual: sparkline, ring, progress track, semantic icon, or mini bar group.
- Bottom evidence band owns previous/current/target cells, warning reason, prior-period value, or auxiliary mini bars. It cannot contain a second chart.
- If the auxiliary visual is a ring/progress/gauge-like shape, reserve a fit box of at least `108x96px` and preserve aspect ratio.
- If the auxiliary visual is a linear progress track, reserve at least `200x24px` for track plus marker and labels.
- If the auxiliary visual is a mini line/bar band, reserve `48-72px` height and use tooltip for exact values.
- If the pattern is `horizontal-axis-line-trend`, do not use this split auxiliary layout. Use the Axis-Line Diagnostic KPI algorithm below because the line body needs axes, grid, labels, and threshold/reference space.
- If the pattern is `horizontal-axis-bar-compare`, do not use this split auxiliary layout. Use the Axis-Bar Diagnostic KPI algorithm below because the bar body needs category labels, value labels, axes, target/threshold/reference space, and row-height budget.
- If the pattern is `horizontal-axis-scatter-diagnostic`, do not use this split auxiliary layout. Use the Axis-Scatter Diagnostic KPI algorithm below because the scatter body needs x/y axes, point-density, reference/trend/threshold/quadrant space, and tooltip targets.
- If the pattern is `horizontal-spatial-map-diagnostic`, do not use this split auxiliary layout. Use the Spatial-Map Diagnostic KPI algorithm below because the map body needs projection-safe fit, legend/visualMap, and key-label budget.
- If the pattern is `paired-comparison-diagnostic`, do not use this split auxiliary layout. Use the Paired Comparison Diagnostic KPI algorithm below because the two panes, `VS` rail, and conclusion band need mirrored geometry.

Landscape fit check:

```text
primaryW >= 140px
auxW >= 96px when auxiliary visual exists
bodyH >= 72px
footerBandH == 0 or footerBandH >= 44px
requiredHeaderW = titleTextW + localControlW + 12px
requiredHeaderW <= CW
```

When the fit check fails, degrade in this order:

1. Collapse segmented local control to compact dropdown.
2. Remove decorative icon or background illustration.
3. Move secondary comparison or prior-period value to tooltip.
4. Hide mini chart evidence before shrinking the primary value.
5. Switch to portrait `plain-metric`, a full chart block, or a detail drawer.

### KPI Overview Card

Use this algorithm when a wide metric card sets `kpiOverviewCardPattern`. This component is still a KPI/metric card, not a Micro Dashboard Card: it summarizes one domain or management topic with a bounded set of metrics and at most one compact evidence visual.

Minimum outer size:

```text
W >= 720px
H >= 220px
standard W = 760-960px
standard H = 240-320px
visibleMetricCount = 2-5
```

Shared slot budget:

```text
P = clamp(20px, W * 0.03, 28px)
CW = W - 2P
CH = H - 2P

headerH = 36-48px
bodyY = P + headerH
bodyH = CH - headerH
controlH = 28-36px
controlW = min(actualControlWidth, CW * 0.34, 320px)
overflowMenuW = 0 or 36px
titleMaxW = CW - controlW - overflowMenuW - 16px
```

Header geometry:

```text
indexW = 0 or 40-48px
titleX = P + indexW
titleY = P
titleH = headerH
controlX = W - P - overflowMenuW - controlW - (overflowMenuW > 0 ? 12px : 0)
controlY = P + (headerH - controlH) / 2
overflowMenuX = W - P - overflowMenuW
```

Variant geometry:

`lead-metric-comparison-sparkline-overview`:

```text
iconTileW = 0 or clamp(64px, H * 0.34, 92px)
iconTileX = P
iconTileY = bodyY + (bodyH - iconTileW) / 2

leadW = clamp(180px, CW * 0.28, 260px)
comparisonW = clamp(112px, CW * 0.16, 160px)
targetW = clamp(150px, CW * 0.20, 200px)
sparkW = clamp(120px, CW - iconTileW - leadW - comparisonW * 2 - targetW - 64px, 180px)
gap = 16-24px

leadX = P + iconTileW + (iconTileW > 0 ? gap : 0)
comparison1X = leadX + leadW + gap
comparison2X = comparison1X + comparisonW
targetX = comparison2X + comparisonW
sparkX = W - P - sparkW

metricCellY = bodyY + 20-28px
metricCellH = bodyH - 32px
sparkH = clamp(56px, bodyH * 0.42, 72px)
sparkY = bodyY + (bodyH - sparkH) / 2
```

`multi-metric-strip-progress-overview`:

```text
cellCount = visibleMetricCount
cellGap = 0
dividerW = 1px
cellW = (CW - dividerW * (cellCount - 1)) / cellCount
cellW >= 128px
cellY = bodyY + 12-20px
cellH = bodyH - 20px
progressTrackW = min(cellW - 24px, 180px)
progressTrackW >= 120px when progress is visible
```

`domain-metric-cluster-progress-overview`:

```text
iconTileW = 0 or clamp(64px, H * 0.34, 92px)
leadW = clamp(190px, CW * 0.28, 280px)
companionCount = 2-3
companionW = clamp(120px, (CW - iconTileW - leadW - 40px) / (companionCount + 1), 180px)
targetW = clamp(150px, companionW, 220px)
progressTrackW >= 120px when progress is visible
```

Slot rules:

- The header owns the domain title and one visible local control group. Overflow menu is allowed only for secondary actions.
- `overviewTopic` names the domain/topic; body metric labels name cells and may be visible because they disambiguate metrics.
- Lead overview cards use a stronger lead metric. Strip overview cards align all values equally and avoid one oversized value.
- Every metric cell declares a value+unit group, comparison/status row, and optional target/progress footer. Value baselines align across sibling cells.
- Sparkline, mini bars, or semantic icon is compact evidence. Do not render axes, legends, or permanent dense labels inside a KPI overview card.
- Progress tracks require target and attainment fields. If the target is missing, hide the track and show a target-missing state or detail route.
- Vertical dividers are decorative only after fit passes; remove them before reducing label readability.

Fit check:

```text
requiredHeaderW = indexW + titleTextW + controlW + overflowMenuW + 16px
requiredHeaderW <= CW
visibleMetricCount >= 2
visibleMetricCount <= 5
eachMetricCellW >= 128px
leadW >= 180px when a lead metric exists
comparisonW >= 112px when comparison cells exist
targetW >= 150px when a target/progress cell exists
sparkW == 0 or (sparkW >= 120px and sparkH >= 56px)
progressTrackW >= 120px when visible
evidenceVisualCount <= 1
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to compact dropdown.
2. Hide optional overflow menu, definition icon, or decorative index.
3. Hide the domain icon tile.
4. Move secondary baseline helper text to tooltip while keeping comparison values.
5. Reduce visible metric cells to Top `3` by business priority and move the rest to drawer/detail.
6. Hide sparkline/mini evidence before shrinking values.
7. Split into separate KPI cards, a full chart/table block, or a Micro Dashboard Card before accepting a crowded overview.

### KPI Judgment Card

Use this algorithm when a metric card sets `kpiJudgmentCardPattern`. The card's primary job is a bounded judgment: status, health, rating, score, risk, project state, payment state, service state, or gauge progress.

Minimum outer size:

```text
W >= 360px
H >= 240px
standard W = 400-460px
standard H = 300-360px
```

Slot budget:

```text
P = clamp(16px, W * 0.045, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
heroH = clamp(96px, H * 0.38, 160px)
comparisonStripH = 54-72px
footerH = 32-52px
bodyGap = 8-12px
```

Hero visual minimums:

```text
semanticIconBox >= 72x72px
ringBox >= 136x136px
semiGaugeBox >= 180x112px
thresholdBulletBox >= 220x28px
dimensionRowH >= 20px
dimensionRows = 3-5 preferred
ratingDistributionRows <= 5
```

Geometry:

```text
headerX = P
headerY = P
headerW = CW
controlW = min(actualControlWidth, CW * 0.34, 148px)

heroX = P
heroY = P + headerH + bodyGap
heroW = CW
heroH = min(heroH, CH - headerH - comparisonStripH - footerH - bodyGap * 3)

comparisonY = heroY + heroH + bodyGap
comparisonH = comparisonStripH
comparisonCellCount = min(3, visibleComparisonCount)
comparisonCellW = CW / comparisonCellCount

footerY = comparisonY + comparisonH + bodyGap
footerH = CH - headerH - heroH - comparisonH - bodyGap * 3
```

Rules:

- The hero zone owns exactly one judgment visual: semantic icon, ring, semi-gauge, threshold bullet, dimension bars, rating stars, or rating distribution. Do not add a second chart-like visual.
- Status/level text sits inside or immediately beside the hero zone. The user should read the visual and label as one sentence, such as `正常运行`, `健康 92`, `良好 78`, or `告警中`.
- Comparison strip cells share height and baseline. Use `2-3` cells; more comparisons move to tooltip/detail.
- Footer evidence is not optional unless inherited by a parent block. It names source/freshness, last check time, target, due date, sample count, risk count, or exact-value route.
- `health-dimension-breakdown-card` and `rating-distribution-card` may use the hero zone for rows instead of a centered icon/ring. Keep row labels readable; never render tiny unreadable bars to preserve the card shape.
- `semicircle-gauge-target-card` uses uniform scaling and keeps arc/ticks/target marker inside `semiGaugeBox`. If target labels collide with ticks, move labels to tooltip or footer.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 16px
requiredHeaderW <= CW
heroH >= 96px
comparisonStripH >= 54px when comparisons are visible
footerH >= 32px when footer evidence is visible
visibleComparisonCount <= 3
heroVisualCount == 1
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to dropdown or inherit the page filter.
2. Hide optional index, help icon, or overflow menu.
3. Move secondary helper copy to tooltip while keeping status/level text.
4. Reduce comparison strip to one priority comparison.
5. Reduce dimension rows to Top `4` or move distribution rows to detail.
6. Replace ring/gauge with status chip + value when the hero fit box is too small.
7. Split to a full gauge/chart/table/detail block before shrinking the card below `360x240`.

### KPI Goal Execution Card

Use this algorithm when a metric card sets `kpiGoalExecutionCardPattern`. The card's primary job is execution management: target attainment, gap/variance, progress against plan, milestone state, deadline, or remaining work.

Minimum outer size:

```text
W >= 360px
H >= 240px
standard W = 400-520px
standard H = 280-360px
```

Slot budget:

```text
P = clamp(16px, W * 0.045, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
heroH = clamp(96px, H * 0.38, 160px)
summaryH = 40-72px
comparisonStripH = 54-72px
footerH = 32-52px
bodyGap = 8-12px
```

Hero visual minimums:

```text
ringBox >= 136x136px
semiGaugeBox >= 180x112px
linearProgressBox >= 220x24px
targetActualPaneW >= 120px
dotStripItemCount <= 12 before grouping
milestoneNodes = 3-7 preferred
milestoneNodeGap >= 52px
timelineBox >= 240x80px
```

Geometry:

```text
headerX = P
headerY = P
headerW = CW
controlW = min(actualControlWidth, CW * 0.34, 148px)

heroX = P
heroY = P + headerH + bodyGap
heroW = CW
heroH = min(heroH, CH - headerH - summaryH - comparisonStripH - footerH - bodyGap * 4)

summaryY = heroY + heroH + bodyGap
summaryH = clamp(40px, summaryH, 72px)

comparisonY = summaryY + summaryH + bodyGap
comparisonCellCount = min(4, visibleComparisonCount)
comparisonCellW = CW / comparisonCellCount

footerY = H - P - footerH
```

Rules:

- The hero zone owns exactly one execution visual: ring, semi-gauge, linear target progress, target/actual bars, dot strip, stepper, timeline, or cumulative milestone line.
- Actual value, target value, gap, progress delta, or current milestone must be adjacent to the hero visual or summary zone. The user should not need to infer the number from the shape alone.
- Comparison strip cells share height and baseline. Use `2-4` cells; more evidence moves to tooltip/detail.
- Footer evidence names target completion date, remaining days, due status, source/freshness, next milestone, or exact-value route. It is mandatory when the card mentions deadline, remaining time, or forecast status.
- `gap-gauge-deficit-card` and `gap-target-actual-compare-card` reserve red/negative emphasis for the gap, not the whole card surface. The primary deficit value must include unit and direction semantics.
- `progress-plan-actual-card` reserves space for both planned progress and actual progress. If one is missing, use an attainment card instead.
- `milestone-timeline-card` uses the hero zone for nodes/timeline. Keep node labels short; full milestone names and dates go to tooltip/detail when labels collide.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 16px
requiredHeaderW <= CW
heroH >= 96px
summaryH >= 40px when target/actual/gap/progress text is visible
comparisonStripH >= 54px when comparisons are visible
footerH >= 32px when deadline/source/evidence is visible
visibleComparisonCount <= 4
heroVisualCount == 1
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to dropdown or inherit the page period.
2. Hide optional index, help icon, or decorative illustration.
3. Reduce comparison strip to the two most decision-relevant cells.
4. Replace ring/semi-gauge/dot strip with a linear target progress track when the hero fit box fails.
5. Collapse milestone nodes to previous/current/next and move the full list to detail.
6. Move secondary deadline/source copy to tooltip while keeping due status or remaining time visible.
7. Split to a full target/actual chart, progress table, timeline, Gantt, or detail drawer before shrinking the card below `360x240`.

### KPI Time-Series Analysis Card

Use this algorithm when a metric card sets `kpiTimeSeriesCardPattern`. The card's primary job is temporal analysis: trend movement, named-baseline change, YoY/MoM comparison, cycle or period state, volatility/stability, or forecast uncertainty.

Minimum outer size:

```text
W >= 360px
H >= 240px
standard W = 400-520px
standard H = 280-360px
```

Slot budget:

```text
P = clamp(16px, W * 0.045, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
valueH = 56-88px
legendOrChipH = 0px or 18-28px
timeSeriesEvidenceH = max(112px, CH - headerH - valueH - legendOrChipH - footerH - bodyGap * 4)
footerH = 44-72px
bodyGap = 8-12px
```

Evidence visual minimums:

```text
axisChartBodyW >= 120px
axisChartBodyH >= 112px
axisPlotH >= 86px
sparklineBox >= 160x64px
forecastFutureRegionW >= 40px after forecastStart
footerCellCount <= 4
footerCellW >= 88px
```

Geometry:

```text
headerX = P
headerY = P
headerW = CW
controlW = min(actualControlWidth, CW * 0.34, 148px)

valueX = P
valueY = P + headerH
valueW = CW
valueH = clamp(56px, valueH, 88px)

chipY = valueY + valueH + bodyGap
chipH = legendOrChipH

evidenceX = P
evidenceY = chipY + chipH + bodyGap
evidenceW = CW
evidenceH = timeSeriesEvidenceH

footerY = H - P - footerH
footerH = clamp(44px, footerH, 72px)
```

Pattern-specific requirements:

- `trend-line-target-card` reserves line or area evidence plus optional target/reference label. If the target label collides with the value band or y-axis, move it to tooltip or the footer.
- `change-baseline-delta-card` must show the named baseline, current value, and delta value/rate. Baseline and current marks share one scale; do not use separate scales to exaggerate change.
- `yoy-mom-comparison-card` keeps YoY and MoM as separate baselines. Do not merge them into a single "growth" chip; prior-year and prior-period values remain inspectable in tooltip/footer.
- `cycle-period-progress-card` may use a ring, stepper, period strip, or cycle line, but it must declare cycle grain, period start/end, current index, total count, and phase/status.
- `volatility-stat-card` must show volatility level plus at least max, min, and standard deviation or a named volatility formula. Threshold bands or level chips use business direction semantics.
- `forecast-interval-card` draws actual history as solid marks and forecast as dashed/weak marks. The forecast band or confidence interval owns a future-region width of at least `40px`; otherwise downgrade to a forecast note.

Rules:

- The card answers exactly one temporal question. Do not combine trend, target gap, forecast, and volatility unless one is the primary question and the others are footer evidence.
- Ordered time fields, time grain, latest period, direction semantics, tooltip payload, source/freshness, and exact-value route are mandatory.
- Use realistic temporal variation. Perfectly smooth lines, identical bars, and generic upward curves make the card feel synthetic unless the data source proves that shape.
- Comparison badges inherit business direction: higher-is-better, lower-is-better, range-target, or neutral. Color alone is not the rule.
- Footer evidence is mandatory and should contain the baseline value, prior period, volatility stats, forecast interval, sample count, or target/reference value.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 16px
requiredHeaderW <= CW
timeSeriesEvidenceH >= 112px
axisPlotH >= 86px when axes/grid are visible
sparklineBox >= 160x64px when no axes are visible
forecastFutureRegionW >= 40px when forecast is visible
footerH >= 44px and footerCellCount <= 4
temporalQuestionCount == 1
```

When the fit check fails, degrade in this order:

1. Collapse segmented controls to dropdown or inherit the page period.
2. Hide optional index, help icon, or decorative domain icon.
3. Move secondary chips such as extra baseline, confidence, or level to tooltip.
4. Reduce footer cells to the two most decision-relevant facts.
5. Downgrade axis chart evidence to a sparkline only when axes, thresholds, and forecast intervals are not required.
6. Split to a full line/bar/forecast chart or detail table before shrinking the card below `360x240`.

### KPI Comparison Analysis Card

Use this algorithm when a metric card sets `kpiComparisonAnalysisCardPattern`. The card's primary job is comparison analysis: direct same-metric comparison, group/segment comparison, competitor position, benchmark position, or signed variance/gap diagnosis.

Minimum outer size:

```text
W >= 360px
H >= 240px
standard W = 400-560px
standard H = 280-380px
```

Slot budget:

```text
P = clamp(16px, W * 0.045, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
summaryH = 56-92px
legendOrRoleH = 0px or 18-28px
comparisonEvidenceH = max(112px, CH - headerH - summaryH - legendOrRoleH - footerH - bodyGap * 4)
footerH = 44-72px
bodyGap = 8-12px
```

Evidence visual minimums:

```text
axisChartBodyW >= 140px
axisChartBodyH >= 112px
axisPlotH >= 92px
radarFitBox >= 150x150px
donutFitBox >= 128x128px
benchmarkRuler >= 220x40px
npsOrScoreScale >= 220x32px
comparisonTableVisibleRows >= 3
comparisonTableVisibleColumns between 3 and 6
footerCellCount <= 4
footerCellW >= 88px
visibleSubjects <= 5 by default
```

Geometry:

```text
headerX = P
headerY = P
headerW = CW
controlW = min(actualControlWidth, CW * 0.34, 148px)

summaryX = P
summaryY = P + headerH
summaryW = CW
summaryH = clamp(56px, summaryH, 92px)

roleY = summaryY + summaryH + bodyGap
roleH = legendOrRoleH

evidenceX = P
evidenceY = roleY + roleH + bodyGap
evidenceW = CW
evidenceH = comparisonEvidenceH

footerY = H - P - footerH
footerH = clamp(44px, footerH, 72px)
```

Pattern-specific requirements:

- `direct-value-compare-card` keeps compared values on the same unit, denominator, period, and axis scale. If definitions differ, switch to a metric matrix or explanation card.
- `group-segment-compare-card` reserves enough category/legend space for group labels and uses deterministic sort. If `visibleSubjects > 5`, show Top N plus `其他` or split.
- `competitor-position-card` reserves role labels for primary product, competitors, peers, industry average, and market total. The primary subject may be highlighted, but competitor geometry stays comparable.
- `benchmark-position-card` reserves space for benchmark markers such as P50/P75/P90, industry average, or standard value. The benchmark source and validity period stay visible or in tooltip/footer.
- `variance-gap-card` reserves signed gap value/rate and direction semantics. A variance table preview needs subtotal/reconciliation row when the card claims total gap.

Rules:

- The card answers exactly one comparison question. Avoid mixing competitor share, benchmark P90, group trend, and target gap as equal evidence in one small card.
- Comparable subject grain, role fields, shared metric definition/unit/grain, comparison direction, sort rule, tooltip payload, source/freshness, and exact-value route are mandatory.
- Circular evidence such as donut, radar, ring, or gauge must keep aspect ratio. If the fit box fails, switch to bars/table rows before stretching the graphic.
- Multi-series comparison uses direct labels or a visible legend; group/competitor colors cannot be random and must preserve role consistency across cards.
- Long competitor, region, product, or group names truncate only with tooltip/detail disclosure.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 16px
requiredHeaderW <= CW
comparisonEvidenceH >= 112px
axisPlotH >= 92px when axes/grid are visible
radar/donut fit boxes preserve aspect ratio
footerH >= 44px and footerCellCount <= 4
comparisonQuestionCount == 1
subject roles and shared metric definitions declared
```

When the fit check fails, degrade in this order:

1. Collapse segmented controls to dropdown or inherit the page period/comparison scope.
2. Hide optional index, help icon, rank badge, or decorative domain icon.
3. Reduce visible groups/competitors to Top `4-5` plus `其他`.
4. Move long subject labels, secondary metric dimensions, and benchmark definitions to tooltip/detail.
5. Convert circular evidence to bars or table rows when the fit box fails.
6. Reduce footer cells to the two most decision-relevant facts.
7. Split to a full comparison chart, benchmark table, metric matrix, detail table, or drawer before shrinking the card below `360x240`.

### Single-Indicator KPI Grid Card

Use this algorithm when a peer KPI grid uses `kpiSingleIndicatorLayoutMode`. This card is still a KPI card, not a chart card: the large number answers current status, the right/bottom mini visual provides one piece of evidence, and the footer states target plus attainment.

Minimum outer size:

```text
W >= 360px
H >= 220px
standard W = 400-460px
standard H = 260-320px
```

Slot budget:

```text
P = clamp(16px, W * 0.045, 24px)
CW = W - 2P
CH = H - 2P

headerH = 34-44px
valueBandH = clamp(64px, H * 0.30, 92px)
compareH = 22-28px
footerH = 44-60px when target/progress footer exists
bodyGap = 8-12px

bodyH = CH - headerH - footerH - bodyGap
evidenceBoxH = bodyH - valueBandH - compareH
evidenceBoxH >= 56px
```

Header geometry:

```text
indexW = 0 or 28-36px
titleX = P + indexW
titleY = P + 4px
titleW = CW - indexW - controlW - 12px
controlX = W - P - controlW
controlY = P
controlH = 32-36px
```

Body split:

```text
primaryX = P
primaryY = P + headerH
primaryW = clamp(150px, CW * 0.52, 230px)
auxX = P + primaryW + 12px
auxW = CW - primaryW - 12px

valueY = primaryY + 6-12px
comparisonY = valueY + valueGlyphH + 12px
evidenceFitBox = (auxX, primaryY + 8px, auxW, bodyH - 8px)
```

Footer geometry:

```text
footerY = H - P - footerH
targetTextX = P
attainmentTextX = W - P - attainmentTextW
targetTextY = footerY + 6-10px
progressTrackX = P
progressTrackW = CW
progressTrackY = footerY + footerH - 10-14px
progressTrackH = 4-6px
```

Evidence fit boxes:

- `dropdown-sparkline-progress`: sparkline uses `>=120x56px`, no axes, latest point may be highlighted.
- `unit-toggle-ring-progress`: ring uses `>=116x96px`, center value optional only if it does not duplicate the primary value.
- `dropdown-minibar-progress` and `grain-switch-minibar-progress`: bars use `>=120x56px`, normally `6-12` bars, one highlighted current bar.
- `dropdown-area-sparkline-progress` and `scale-toggle-area-progress`: area sparkline uses `>=120x56px`, fill opacity low enough to keep value hierarchy.
- `dropdown-gauge-progress`: semi-gauge uses `>=116x96px`, preserves semicircle ratio, and includes target/threshold semantics in tooltip or footer.

Fit check:

```text
requiredHeaderW = indexW + titleTextW + helpIconW + controlW + 16px
requiredHeaderW <= CW
primaryW >= 150px
auxW >= 112px when evidence visual exists
footerH == 0 or footerH >= 44px
progressTrackW >= 200px when progress track is visible
evidence visual count == 1
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to compact dropdown.
2. Hide sample index and definition icon.
3. Move secondary comparison wording to tooltip.
4. Hide the mini evidence visual while keeping target/attainment text.
5. Hide progress track and keep target/attainment text only.
6. Use `plain-metric`, a full chart card, or a detail drawer before shrinking the primary value.

### Axis-Line Diagnostic KPI Card

Use this algorithm when `kpiCardPattern` is `horizontal-axis-line-trend`.

This is a KPI card, not a generic chart block: the top value answers the current judgment, while the ECharts line body proves the trend, target, threshold, phase, or comparison evidence.

Minimum outer size:

```text
W >= 420px
H >= 260px
standard W = 460-560px
standard H = 280-340px
```

Slot budget:

```text
P = clamp(16px, W * 0.04, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
valueBandH = 56-78px
compareInlineH = 20-24px when comparison is not inline with value
chartTopGap = 8-12px
xAxisH = 28-40px
legendH = 0-24px
footerH = 0-20px

chartBodyH = CH - headerH - valueBandH - compareInlineH - chartTopGap - footerH
chartBodyH >= 180px
plotH >= 130px
```

Header geometry:

```text
titleX = P
titleY = P
controlH = 28px
controlW = min(actualControlWidth, CW * 0.42, 168px)
controlX = W - P - controlW
titleMaxW = CW - controlW - 12px
```

Value geometry:

```text
valueX = P
valueY = P + headerH
valueMaxW = CW * 0.52
compareX = valueX + valueTextW + 16px when inline comparison fits
compareY = valueY + valueBaselineOffset
```

The main value may be left-aligned in this pattern because the card is a scan-friendly analytical surface. It still must be the strongest text, and the comparison/status must sit close enough to be read as part of the value judgment.

Line body geometry:

```text
chartX = P
chartY = P + headerH + valueBandH + compareInlineH + chartTopGap
chartW = CW
chartH = chartBodyH

yAxisW = clamp(36px, maxYAxisLabelWidth + 8px, 56px)
rightGap = 8-16px
rightGap = 44-64px when target/reference/threshold labels sit on the right
gridTop = legendH + 4px
gridBottom = xAxisH
gridLeft = yAxisW
gridRight = rightGap
```

Evidence-mode placement:

- `basic-compare-line`: one primary line, weak grid, all x labels only when `N <= 8`.
- `filled-baseline-line`: area fill opacity `8-14%`; fill starts at the baseline and must not cover grid/labels.
- `target-reference-line`: reserve right/top label gap; target label may collapse to tooltip if it collides.
- `phase-annotated-line`: phase band starts and ends on x-axis positions; label sits inside the band top-right or outside the plot with a leader.
- `unit-axis-line`: unit appears in title or y-axis metadata, not as a large floating label inside the plot.
- `grain-switch-line`: segmented control lives in the header right; `2-4` short options only, otherwise use dropdown.
- `dual-comparison-line`: legend consumes `20-24px`; primary series is stronger, comparison series is muted or dashed.
- `threshold-band-line`: bands are weak background rectangles with right-side labels; line and point contrast remain dominant.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 12px
requiredHeaderW <= CW
valueBandH >= valueGlyphH + comparisonH + 4px
chartBodyH >= 180px
plotH >= 130px
yAxisW + rightGap + 160px <= chartW
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to a selected-value dropdown.
2. Hide ordinary point symbols and all non-key labels.
3. Move target/reference/threshold text labels into tooltip while keeping the line/band.
4. Remove area fill before removing axes.
5. Downgrade to `horizontal-trend-compare` by hiding axes/grid and treating the chart as a sparkline.
6. Split into a full line chart card or detail drawer before shrinking the value or rendering a thin unreadable plot.

### Axis-Bar Diagnostic KPI Card

Use this algorithm when `kpiCardPattern` is `horizontal-axis-bar-compare`.

This is a KPI card, not a generic bar chart block: the top value answers the current judgment, while the ECharts horizontal bar body proves rank, period comparison, target gap, threshold state, category variation, or per-category change-rate evidence.

Minimum outer size:

```text
W >= 420px
H >= 260px
standard W = 460-560px
standard H = 280-340px
visibleBars = 3-6 recommended, 8 maximum
```

Slot budget:

```text
P = clamp(16px, W * 0.04, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
valueBandH = 56-78px
compareInlineH = 20-24px when comparison is not inline with value
chartTopGap = 8-12px
xAxisH = 28-40px
legendH = 0-24px
footerH = 0-20px

chartBodyH = CH - headerH - valueBandH - compareInlineH - chartTopGap - footerH
chartBodyH >= 180px
plotH >= 140px
barRowH = plotH / visibleBars
barRowH >= 22px
```

Header and value geometry follow the Axis-Line Diagnostic KPI Card algorithm.

Horizontal bar body geometry:

```text
chartX = P
chartY = P + headerH + valueBandH + compareInlineH + chartTopGap
chartW = CW
chartH = chartBodyH

categoryLabelW = clamp(44px, maxCategoryLabelWidth + 8px, 88px)
valueLabelW = clamp(48px, maxValueOrChangeLabelWidth + 8px, 96px)
rightGap = valueLabelW
rightGap = valueLabelW + 36px when target/reference labels sit on the right
gridTop = legendH + 4px
gridBottom = xAxisH
gridLeft = categoryLabelW
gridRight = rightGap
plotW = chartW - categoryLabelW - rightGap
plotH = chartH - gridTop - gridBottom
```

Evidence-mode placement:

- `basic-horizontal-bar`: one primary bar series; labels left, values right; all value labels visible only when `N <= 6`.
- `period-comparison-bar`: periods are ordered chronologically or by declared recency; do not sort by value unless requested.
- `target-reference-bar`: target line/tick shares the x-axis scale; target label uses the reserved right gap or tooltip.
- `category-change-sidebar-bar`: value label and change-rate label occupy a right-side evidence column; semantic color follows business direction.
- `time-series-horizontal-bar`: dates/months remain ordered; category labels may abbreviate but tooltip keeps full period.
- `grain-switch-horizontal-bar`: segmented control lives in the header right; `2-4` short options only, otherwise use dropdown.
- `dual-series-horizontal-bar`: legend consumes `20-24px`; comparison bars are muted, thinner, or outlined; primary value label stays closest to the row.
- `threshold-warning-bar`: threshold line and warning label stay weak but visible; warning color appears on labels/bands, not every bar.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 12px
requiredHeaderW <= CW
valueBandH >= valueGlyphH + comparisonH + 4px
chartBodyH >= 180px
plotH >= 140px
barRowH >= 22px
categoryLabelW + rightGap + 180px <= chartW
visibleBars <= 8
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to a selected-value dropdown.
2. Abbreviate category labels and preserve full labels in tooltip.
3. Hide ordinary value labels, keeping only current/top/target-related labels.
4. Move target/reference/threshold labels into tooltip while keeping the line/band.
5. Reduce visible rows to Top 5 plus detail route.
6. Downgrade to `horizontal-grain-bar-switch` or a mini bar strip only if axes/value columns are intentionally hidden.
7. Split into a full bar chart card, target/actual bar card, table, or detail drawer before shrinking the primary value or rendering unreadable row bars.

### Axis-Scatter Diagnostic KPI Card

Use this algorithm when `kpiCardPattern` is `horizontal-axis-scatter-diagnostic`.

This is a KPI card, not a generic scatter block: the top value answers the current status or comparison, while the scatter body proves relationship, distribution, outlier, target fit, threshold, or quadrant evidence.

Minimum outer size:

```text
W >= 420px
H >= 300px
standard W = 460-560px
standard H = 320-360px
recommended pointCount = 12-80
```

Slot budget:

```text
P = clamp(16px, W * 0.04, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
valueBandH = 56-78px
compareInlineH = 20-24px when comparison is not inline with value
chartTopGap = 8-12px
legendH = 0-24px
xAxisH = 32-48px
footerH = 0-20px

chartBodyH = CH - headerH - valueBandH - compareInlineH - chartTopGap - footerH
chartBodyH >= 200px
plotH >= 160px
```

Scatter body geometry:

```text
chartX = P
chartY = P + headerH + valueBandH + compareInlineH + chartTopGap
chartW = CW
chartH = chartBodyH

yAxisW = clamp(40px, maxYAxisLabelWidth + 8px, 60px)
rightGap = 12-20px
rightGap = 48-72px when change-rate zone labels, quadrant labels, or target labels sit on the right
gridTop = legendH + 4px
gridBottom = xAxisH
gridLeft = yAxisW
gridRight = rightGap
plotW = chartW - gridLeft - gridRight
plotH = chartH - gridTop - gridBottom
```

Evidence-mode placement:

- `correlation-trendline-scatter`: trendline is weak/dashed, behind selected points, and named in tooltip or annotation.
- `mean-reference-scatter`: average/reference lines use weak dashed strokes and labels with reserved top/right gaps.
- `target-crosshair-scatter`: x/y target lines share axis scales; the target label can move to tooltip if it collides.
- `distribution-change-band-scatter`: side legend or background bands reserve `56-96px`; bands stay low opacity.
- `threshold-quadrant-scatter`: quadrant backgrounds are subtle, labels sit in corners, and points stay dominant.
- `dual-series-trendline-scatter`: legend consumes `20-24px`; baseline points are muted and primary points are stronger.
- `change-callout-scatter`: callout bubble is `120-180px` wide, max `2` lines, and must not cover the selected point.
- `category-quadrant-scatter`: visible categories `<=5`; selected/abnormal labels only.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 12px
requiredHeaderW <= CW
valueBandH >= valueGlyphH + comparisonH + 4px
chartBodyH >= 200px
plotH >= 160px
yAxisW + rightGap + 180px <= chartW
pointCount <= 80 for normal permanent display
permanentPointLabels <= 6
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to a selected-value dropdown.
2. Hide ordinary point symbols' labels and keep only selected/outlier labels.
3. Move trendline/reference/target/quadrant labels into tooltip while keeping the line/band.
4. Remove optional metric strip, footer, and callout.
5. Reduce point count through Top/outlier selection, sampling, or aggregation.
6. Split into a full scatter chart block, table, or detail drawer before shrinking the scatter into a decorative dot field.

### Spatial-Map Diagnostic KPI Card

Use this algorithm when `kpiCardPattern` is `horizontal-spatial-map-diagnostic`.

This is a KPI card, not a generic map block: the top value answers the current geographic judgment, while the map body proves where the value, status, target gap, or change is concentrated.

Minimum outer size:

```text
W >= 460px
H >= 320px
standard W = 500-640px
standard H = 340-380px
```

Slot budget:

```text
P = clamp(16px, W * 0.04, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
valueBandH = 56-78px
compareInlineH = 20-24px when comparison is not inline with value
mapTopGap = 8-12px
footerH = 0-20px

mapBodyAvailableH = CH - headerH - valueBandH - compareInlineH - mapTopGap - footerH
mapBodyAvailableH >= 220px
```

Map body geometry:

```text
mapBodyX = P
mapBodyY = P + headerH + valueBandH + compareInlineH + mapTopGap
mapBodyW = CW
mapBodyH = mapBodyAvailableH

legendW = 0 or clamp(72px, CW * 0.22, 140px)
legendGap = 12-16px
mapAreaW = CW - legendW - legendGap
mapViewportInset = clamp(8px, min(mapAreaW, mapBodyH) * 0.04, 20px)
mapViewportW = mapAreaW - 2 * mapViewportInset
mapViewportH = mapBodyH - 2 * mapViewportInset
min(mapViewportW, mapViewportH) >= 180px
```

Projection fit:

```text
scale = min(mapViewportW / geoBoundsWidth, mapViewportH / geoBoundsHeight)
offsetX = (mapViewportW - geoBoundsWidth * scale) / 2
offsetY = (mapViewportH - geoBoundsHeight * scale) / 2
```

Use a single `scale`. Do not stretch geography independently on X/Y.

Evidence-mode placement:

- `choropleth-heat-map` and `graded-choropleth-map`: visualMap uses `5-6` bins; no-data fill is neutral.
- `bubble-target-gap-map`: bubble radius uses sqrt mapping; side legend or tooltip explains size and target gap.
- `distribution-change-marker-map`: marker color follows change-rate semantics and side legend reserves status definitions.
- `column-symbol-map`: small columns anchor to region centroids; column height scale is capped and tooltip holds exact values.
- `annotated-interval-map`: permanent labels are only selected/key regions; interval bins sit in legend.
- `yoy-change-zone-map`: divergent scale names rise/fall/no-change bands and zero/neutral state.
- `point-category-summary-map`: side summary uses category counts; ordinary point labels hide.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 12px
requiredHeaderW <= CW
mapBodyH >= 220px
min(mapViewportW, mapViewportH) >= 180px
legendW == 0 or legendW >= 72px
map resource/projection declared
```

When the fit check fails, degrade in this order:

1. Collapse segmented control to compact dropdown.
2. Move footer/source metadata into tooltip or detail.
3. Collapse side legend into compact in-map legend if it does not cover key geography.
4. Hide ordinary labels and keep Top/selected/abnormal labels.
5. Switch to ranked bar/table or a full map block before rendering a tiny decorative basemap.

### Paired Comparison Diagnostic KPI Card

Use this algorithm when `kpiCardPattern` is `paired-comparison-diagnostic`.

This card compares two states with the same metric definition. The central `VS` rail establishes comparison, while the bottom conclusion band states the decision.

Minimum outer size:

```text
W >= 420px
H >= 260px
standard W = 460-560px
standard H = 280-340px
```

Slot budget:

```text
P = clamp(16px, W * 0.04, 24px)
CW = W - 2P
CH = H - 2P

headerH = 32-44px
paneTopGap = 8-12px
conclusionBandH = clamp(36px, H * 0.16, 52px)
paneAreaH = CH - headerH - paneTopGap - conclusionBandH - 12px

vsRailW = clamp(32px, W * 0.08, 44px)
paneGap = 12-16px
paneW = (CW - vsRailW - paneGap * 2) / 2
paneW >= 140px
paneAreaH >= 140px
```

Pane geometry:

```text
leftPaneX = P
rightPaneX = P + paneW + paneGap * 2 + vsRailW
paneY = P + headerH + paneTopGap
vsCenterX = P + paneW + paneGap + vsRailW / 2
conclusionY = H - P - conclusionBandH
```

Pane content:

- Pane label: `本月`, `去年同期`, `实际完成`, `目标值`, `本期`, `上期`, or equivalent.
- Primary pane value plus unit: same font scale and baseline on both sides.
- Optional mini evidence: bar strip, ring, progress, dot matrix, mini trend, or small breakdown rows.
- Delta/gap text sits in the winning/primary pane or bottom conclusion, not both unless one is detailed and one is summary.

Evidence-mode placement:

- `metric-yoy-vs`: values dominate; mini bars are optional and weak.
- `progress-mom-vs` and `target-gap-progress-vs`: progress tracks align on the same min/max scale.
- `improvement-dot-matrix-vs`: dot grids have the same row/column count and semantic color mapping.
- `trend-yoy-vs` and `trend-mom-vs`: mini lines share y-axis scale or explicitly state independent normalization in tooltip.
- `structure-breakdown-vs`: shared categories align row-by-row; do not compare different category sets as if equivalent.
- `percentage-ring-vs`: ring diameters, stroke widths, and center-value sizes match.

Fit check:

```text
requiredHeaderW = titleTextW + controlW + 12px
requiredHeaderW <= CW
paneW >= 140px
paneAreaH >= 140px
vsRailW >= 32px
conclusionBandH >= 36px
left/right units and metric definitions match
```

When the fit check fails, degrade in this order:

1. Collapse local control to compact dropdown.
2. Remove pane mini evidence and keep value + delta.
3. Move secondary baseline text to tooltip.
4. Stack panes vertically only when the parent allows `H >= 420px`.
5. Split into a full comparison chart/table before changing value definitions or squeezing panes.

### Slot Position Rules

Title:

```text
titleX = P
titleY = P
titleWidth = CW - helpIconWidth - helpGap
titleHeight = 20-28px
horizontalAlign = left
verticalAlign = center
```

Definition/help icon:

```text
iconSize = 14-16px
helpX = W - P - iconSize
helpY = P + (titleHeight - iconSize) / 2
```

Component-local filter:

```text
filterH = 24-28px
filterW = min(actualFilterWidth, CW * 0.45)
filterX = W - P - filterW
filterY = P
titleMaxW = CW - filterW - 8px
```

Rules:

- Metric cards allow at most one visible local filter group by default, and the group should normally have no more than three short options.
- Suitable filters include `今日 / 本周 / 本月`, `同比 / 环比`, `实际 / 目标 / 完成率`, or `金额 / 数量`.
- On small cards, collapse to a single capsule dropdown such as `本月 ▾`.
- The local filter must not change the visual center of the primary value: keep `centerX = P + CW / 2` for value, comparison, and target groups unless the card intentionally uses the wide split layout.
- If the title, help icon, and filter do not fit, keep title plus selected filter value; move help/definition to tooltip, drawer entry, or card metadata.

Value group:

```text
valueGroupWidth = valueTextWidth + unitGap + unitTextWidth
valueGroupX = centerX - valueGroupWidth / 2
valueSlotY = valueY
valueSlotH = valueHeight
valueGroupY = valueSlotY + (valueSlotH - valueGroupHeight) / 2
valueAnchorViewportCenterY = valueAnchorViewportY + valueAnchorViewportH / 2
centerDeltaY = abs(valueGroupCenterY - valueAnchorViewportCenterY)
unitGap = 4-6px
```

The value and unit are centered as one group. Do not center the number and then attach the unit far away.

Hard value-anchor rules:

- Default metric cards center the actual `value + unit` group in the declared value anchor viewport. `centerDeltaY <= 8px`; otherwise record `VIS-KPI-VALUE-OFFCENTER`.
- `valueSlotH >= valueAnchorViewportH * 0.40` for standard centered cards. Wide/split or pyramid cards may use a declared primary value zone, but the same center and glyph checks apply inside that zone.
- The primary numeral glyph height should normally be `22-28%` of the value anchor viewport for primary standard/enhanced cards. If `W >= 360px` and `H >= 180px`, allow `40-44px` main value text after width and height fit proof.
- Do not use value-row `align-items: baseline` as the vertical placement strategy. The value slot should use `place-items: center`, flex `align-items: center`, or equivalent. Apply baseline alignment only to the unit inside the centered value group.
- Title, help, status, target, source/freshness, and summary are auxiliary. If they push the value group off center or force a weak numeral, collapse/move those auxiliary items before shrinking or offsetting the primary value.

Unit:

```text
unitX = valueTextX + valueTextWidth + 4-6px
unitY = baseline-aligned with value, or 2-4px lower
unitFontSize = valueFontSize * 0.4-0.5
```

Comparison group:

```text
compareGroupWidth = yoyWidth + comparisonGap + momWidth
compareGroupX = centerX - compareGroupWidth / 2
compareGroupY = valueY + valueHeight + 8-10px
comparisonGap = 8-16px
```

Each comparison item uses:

```text
[label] [directionIcon] [signedValue]
labelIconGap = 4px
iconValueGap = 2-4px
```

Target group:

```text
targetGroupWidth = targetTextWidth + targetGap + attainmentTextWidth
targetGroupX = centerX - targetGroupWidth / 2
targetGroupY = compareY + compareHeight + 8-12px
targetGap = 8-16px
```

Progress bar:

```text
progressWidth = CW * 0.8-1.0
progressX = centerX - progressWidth / 2
progressY = targetTextBottom + 6-8px
progressHeight = 4-6px
progressFillWidth = min(attainmentRate, 100%) * progressWidth
```

Sparkline:

```text
sparkWidth = CW for standard/enhanced cards
sparkWidth = CW * 0.85 for narrow cards when needed
sparkX = centerX - sparkWidth / 2
sparkY = compareY + compareHeight + 8-12px
sparkHeight = clamp(28px, H * 0.22, 56px)
```

Summary:

```text
summaryX = P
summaryY = targetY + targetHeight + 6-8px
summaryWidth = CW
```

Alignment:

- Small cards hide summary.
- Standard cards may center a short summary.
- Enhanced cards may center or left-align summary based on business tone.
- Wide business-analysis cards prefer left-aligned summary.

Description and freshness:

```text
descX = P
descY = H - P - descriptionHeight
descWidth = CW
```

Description is left-aligned by default. Freshness metadata may align bottom-right when it is short and noncritical.

### Wide Metric Card Split

For `W >= 480px`, use a two-zone layout only when the right side has meaningful auxiliary information.

```text
leftWidth = CW * 0.45-0.55
columnGap = 16-24px
rightWidth = CW - leftWidth - columnGap
leftX = P
rightX = P + leftWidth + columnGap
leftCenterX = leftX + leftWidth / 2
```

Rules:

- Value group, comparison group, and primary target status center around `leftCenterX`.
- Sparkline, detailed target, and summary may sit in the right zone.
- Right-zone content can be left-aligned for readability.
- Do not center the primary value against the full card when the card is split; center it inside the left primary zone.

### Typography Fit

```text
valueFontSize = clamp(24px, W * 0.11, 36px) by default
valueFontSize may reach 40px only for wide or top-priority primary metric cards after fit proof
unitFontSize = valueFontSize * 0.4-0.5
```

Recommended values:

| Container width | Value font |
| ---: | ---: |
| `W < 200px` | `24px` |
| `200px <= W < 280px` | `28px` |
| `280px <= W < 360px` | `32px` |
| `360px <= W < 480px` | `36px` |
| `W >= 480px` | `36px`, or `40px` only for wide/top-priority primary metric cards |

Text rules:

- Metric title: `13-14px`, `18-22px` line-height.
- Value: `24-36px` by default, up to `40px` only for wide/top-priority primary metric cards, `1.1-1.2` line-height, tabular numerals.
- Unit: `12-16px`, `16-20px` line-height.
- Comparison label/value: `12-13px`, `16-18px` line-height.
- Target and attainment: `12-13px`, `16-18px` line-height.
- Summary: `12-13px`, `18-20px` line-height, usually one line.
- Description/freshness: `11-12px`, `16-18px` line-height.

Long value fallback:

1. Use approved display units such as `万`, `亿`, `K`, or `M`.
2. Reduce decimals based on metric precision rules.
3. Widen the card or move secondary content.
4. Use tooltip for exact raw value.

### Comparison And Target Semantics

- Show at least one of YoY or MoM when comparison data exists. If space is tight, keep the comparison most relevant to the business cadence, often MoM for short-term monitoring.
- Chinese report change-rate and variance-rate indicators use `%`.
- For Chinese report change-rate indicators, default to positive-red-up and negative-green-down unless the metric dictionary or company standard defines another convention.
- For cost, complaint, failure, return, overdue, risk, and other business-negative metrics, the value direction must follow the metric dictionary. Do not color by raw sign alone.
- Target describes attainment, target gap, or progress. Do not force it into up/down semantics unless the business defines target movement that way.

### State Geometry

| State | Metric card behavior |
| --- | --- |
| Loading | Skeleton preserves title, value, comparison, and target slots |
| Empty | Value shows `--`; hide invalid comparison and target calculations; keep the card height |
| Error | Show concise affected metric and retry path when available |
| No permission | Keep title and explain permission condition without leaking value |
| Target missing | Show `暂无目标` or hide target slot with a documented height fallback |
| YoY/MoM missing | Hide the missing comparison and recenter remaining comparison |
| Previous period is zero | Show comparison as `--` with tooltip explaining denominator is zero |
| Value is zero | Display `0` normally; do not treat zero as empty data |
| Stale data | Show freshness or delay metadata in the description/freshness slot |
