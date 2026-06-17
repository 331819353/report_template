# 06 Binding Implementation Contract

Use this reference before implementation, prototype configuration, API handoff, or any output that must be buildable.

## Unified Component Mapping Contract

Every mapped component must be expressible as an implementation contract.

```ts
type ControlSemantics =
  | 'perspective-switch'
  | 'global-filter'
  | 'local-filter'
  | 'drilldown-param';

type ActionType =
  | 'openModal'
  | 'closeModal'
  | 'setFilters'
  | 'resetFilters'
  | 'navigateUrl'
  | 'print'
  | 'fullscreen'
  | 'refresh'
  | 'custom';

type ComponentSchemaImpact =
  | 'none'
  | 'row-scope-only'
  | 'metric-name'
  | 'metric-set'
  | 'component-set'
  | 'table-schema'
  | 'dimension-set'
  | 'definition-change'
  | 'domain-vocabulary'
  | 'mixed';

type ComponentSchemaImpactDetail = {
  categories: ComponentSchemaImpact[];
  changesMetricNames: boolean;
  changesComponentSet: boolean;
  changesTableHeaders: boolean;
  changesDimensions: boolean;
  changesFormulaOrDefinition: boolean;
  changesDomainVocabulary: boolean;
  notes?: string;
};

type NavigationMetricLineage = {
  navigationId: string;
  metricKind: 'percentage' | 'ranking' | 'status-light';
  sourceDataset: string;
  field?: string;
  formula?: string;
  grain: string;
  affectedFilters: string[];
  periodBehavior:
    | 'selected-period'
    | 'current-period'
    | 'comparison-period'
    | 'rolling-window'
    | 'latest-snapshot'
    | 'static-display-copy';
  staticDisplayCopy?: boolean;
};

type DisplayTheme =
  | 'detail-table'
  | 'summary-stat'
  | 'business-dashboard'
  | 'exploratory-analysis'
  | 'management-report'
  | 'monitoring-alert';

type PatternRole =
  | 'primary-structure'
  | 'supporting-evidence'
  | 'interaction'
  | 'state'
  | 'export'
  | 'governance'
  | 'acceptance-only';

type VisualSourceRole =
  | 'temporary-evidence'
  | 'exact-restoration-source'
  | 'visual-regression-baseline'
  | 'runtime-asset'
  | 'audit-evidence'
  | 'reusable-inspiration';

type StyleGeneralizationStatus =
  | 'covered-by-existing-pattern'
  | 'covered-by-composed-patterns'
  | 'requires-pattern-extension'
  | 'out-of-scope-one-off';

type StyleGeneralizationContract = {
  sourceRole: VisualSourceRole;
  generalizationStatus: StyleGeneralizationStatus;
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

type ConclusionCardPattern =
  | 'metric-evidence-conclusion'
  | 'finding-action-conclusion'
  | 'compact-conclusion-summary';

type AnalysisInsightContract = {
  subtype:
    | 'conclusion-card'
    | 'insight-card'
    | 'anomaly-alert'
    | 'attribution-card'
    | 'impact-factor-card'
    | 'comparison-interpretation'
    | 'trend-interpretation'
    | 'target-diagnosis'
    | 'recommendation-card'
    | 'risk-card'
    | 'definition-card'
    | 'data-quality-card'
    | 'chart-annotation'
    | 'summary-bar'
    | 'change-explanation'
    | 'ranking-interpretation'
    | 'forecast-note'
    | 'review-card'
    | 'explanatory-empty-state'
    | 'task-card'
    | 'permission-no-result-delay-note';
  insightFamily: 'conclusion' | 'insight' | 'diagnosis' | 'recommendation' | 'explanation' | 'state';
  conclusionCardPattern?: ConclusionCardPattern;
  conclusion: string;
  evidence?: string[];
  affectedObjects?: string[];
  compareWith?: string;
  changeValue?: string;
  reasonFields?: string[];
  recommendedActions?: string[];
  confidence?: 'high' | 'medium' | 'low' | 'insufficient';
  definitionRefs?: string[];
  dataQualityScope?: string;
  annotationTarget?: { componentId: string; field?: string; markId?: string; range?: string };
  maxVisibleItems?: number;
  localFilters?: string[];
  tooltipPayload?: string[];
  detailRoute?: string;
  sourceDataset?: string;
  freshnessField?: string;
  validationRules: string[];
};

type NumericFormatContract = {
  metricId: string;
  field: string;
  valueType:
    | 'count'
    | 'amount'
    | 'currency'
    | 'percent'
    | 'rate'
    | 'ratio'
    | 'average'
    | 'score'
    | 'duration'
    | 'rank'
    | 'index'
    | 'geo'
    | 'scientific'
    | 'project-enum';
  rawUnit: string;
  displayUnit: string;
  displayScale: string;
  precision: number | string;
  tooltipPrecision: number | string;
  exportPrecision: number | string;
  roundingMode: 'half-up' | 'bankers' | 'floor' | 'ceil' | 'truncate' | 'project-defined';
  trimTrailingZeros?: boolean;
  thousandsSeparator?: boolean;
  nullDisplay: string;
  zeroDisplay: string;
  zeroDivisionDisplay?: string;
  negativeZeroRule: string;
  smallNonZeroRule?: string;
  formulaPrecisionPolicy?: string;
  formatterOwner: 'frontend' | 'backend-export' | 'shared-contract' | 'project-defined';
};

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

type KpiJudgmentBandBinding = {
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

type KpiOverviewMetricBinding = {
  metricId: string;
  metricName: string;
  valueField: string;
  unit: string;
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

type TargetActualCardPattern =
  | 'standard-summary-panel'
  | 'emphasis-header-summary'
  | 'soft-chip-summary';

type TargetActualTrendCardPattern =
  | 'emphasis-wave-trend'
  | 'standard-summary-trend'
  | 'soft-chip-trend';

type TargetActualRadarCardPattern =
  | 'emphasis-wave-radar'
  | 'standard-action-radar';

type TargetActualDonutCardPattern =
  | 'emphasis-filter-donut'
  | 'standard-filter-donut';

type TargetActualScatterCardPattern =
  | 'emphasis-filter-scatter'
  | 'standard-filter-scatter';

type TargetActualTablePattern =
  | 'standard-audit-table'
  | 'compact-audit-table';

type TargetActualPivotTablePattern =
  | 'standard-hierarchy-pivot'
  | 'share-matrix-pivot'
  | 'tree-expand-pivot';

type TableCardPattern =
  | 'plain-detail-ledger-table'
  | 'filtered-operational-status-table'
  | 'grouped-header-summary-table'
  | 'metric-matrix-table'
  | 's2-cross-pivot-table'
  | 'fixed-column-scroll-table'
  | 'grouped-subtotal-summary-table'
  | 'tree-hierarchy-table';

type RankingCardPattern =
  | 'basic-rank-list-card'
  | 'trend-delta-rank-list-card'
  | 'progress-bar-rank-list-card'
  | 'podium-rank-card'
  | 'yoy-microbar-rank-list-card'
  | 'radar-comparison-rank-card'
  | 'metric-summary-rank-card'
  | 'time-switch-rank-card'
  | 'share-donut-rank-card'
  | 'map-distribution-rank-card'
  | 'topn-bar-rank-card'
  | 'topn-comparison-rank-card'
  | 'topn-waterfall-strip-card'
  | 'topn-sparkline-rank-list-card'
  | 'topn-bubble-rank-card'
  | 'topn-icon-card-grid'
  | 'medal-horizontal-ranking'
  | 'bar-progress-ranking'
  | 'compact-list-ranking';

type ParetoCardPattern =
  | 'pareto-basic-card'
  | 'pareto-table-chart-card'
  | 'pareto-dual-axis-card'
  | 'pareto-cumulative-fill-card'
  | 'pareto-stacked-share-card'
  | 'pareto-bubble-card'
  | 'pareto-zone-card'
  | 'pareto-ring-list-card';

type CompositionShareCardPattern =
  | 'basic-donut-share-card'
  | 'donut-detail-share-card'
  | 'percent-bar-share-card'
  | 'multi-ring-hierarchy-share-card'
  | 'share-trend-stack-card'
  | 'share-ranking-topn-card'
  | 'treemap-composition-card'
  | 'share-metrics-summary-card'
  | 'stacked-strip-composition-card'
  | 'stacked-column-trend-composition-card'
  | 'funnel-composition-card'
  | 'bubble-composition-card'
  | 'market-share-overview-card'
  | 'market-share-concentration-card'
  | 'share-distribution-interval-card'
  | 'map-structure-card'
  | 'sunburst-structure-card';

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

type DistributionAnalysisCardPattern =
  | 'numeric-histogram-distribution-card'
  | 'interval-donut-distribution-card'
  | 'percentile-cdf-distribution-card'
  | 'geographic-distribution-card'
  | 'time-distribution-card'
  | 'distribution-comparison-card'
  | 'calendar-heatmap-distribution-card'
  | 'multidimensional-population-distribution-card'
  | 'interval-histogram-card'
  | 'interval-share-donut-card'
  | 'interval-boxplot-card'
  | 'interval-comparison-card'
  | 'interval-stacked-trend-card'
  | 'cumulative-interval-card'
  | 'interval-scatter-strip-card'
  | 'interval-detail-table-card'
  | 'univariate-density-curve-card'
  | 'interval-density-curve-card'
  | 'grouped-density-comparison-card'
  | 'density-heatmap-card'
  | 'kde-cumulative-density-card'
  | 'bivariate-density-hexbin-card'
  | 'quantile-band-density-card'
  | 'density-overview-card'
  | 'boxplot-kpi-summary-card'
  | 'time-series-boxplot-card'
  | 'grouped-boxplot-comparison-card'
  | 'boxplot-overview-card'
  | 'boxplot-side-summary-card'
  | 'weekday-boxplot-card'
  | 'anomaly-boxplot-card'
  | 'boxplot-detail-table-card';

type AnomalyAnalysisCardPattern =
  | 'anomaly-overview-card'
  | 'anomaly-trend-compare-card'
  | 'anomaly-distribution-structure-card'
  | 'anomaly-interval-threshold-card'
  | 'anomaly-timeline-card'
  | 'anomaly-ranking-top-card'
  | 'anomaly-impact-assessment-card'
  | 'anomaly-baseline-compare-card'
  | 'anomaly-summary-table-card'
  | 'anomaly-multi-metric-monitor-card'
  | 'risk-matrix-card'
  | 'risk-response-status-card'
  | 'anomaly-relation-influence-card'
  | 'anomaly-geographic-distribution-card'
  | 'outlier-scatter-card'
  | 'warning-progress-donut-card';

type RankingEvidenceBinding = {
  rankingMode: 'leaderboard' | 'top-n' | 'bottom-n' | 'rank-comparison' | 'rank-distribution' | 'spatial-rank';
  metricId: string;
  metricName: string;
  unit: string;
  topN: number;
  visibleCount: number;
  rankingOrder: 'desc' | 'asc';
  rankField: string;
  objectIdField: string;
  objectNameField: string;
  objectSecondaryField?: string;
  valueField: string;
  shareField?: string;
  denominatorField?: string;
  comparisonField?: string;
  deltaField?: string;
  deltaRateField?: string;
  targetField?: string;
  progressField?: string;
  trendSeriesField?: string;
  scoreDimensionFields?: string[];
  geographyFields?: string[];
  periodField?: string;
  tieBreakFields: string[];
  totalPolicy: 'all-filtered-rows' | 'visible-top-n' | 'api-provided-total';
  badgeRule: 'top3-medals' | 'rank-circles' | 'plain-rank' | 'brand-icons';
  overflowStrategy: 'view-all' | 'pagination' | 'drawer' | 'table-fallback' | 'scroll';
  tooltipPayload: string[];
  detailAction?: string;
};

type ParetoEvidenceBinding = {
  metricId: string;
  metricName: string;
  unit: string;
  itemIdField: string;
  itemNameField: string;
  rankField: string;
  valueField: string;
  totalField: string;
  contributionShareField: string;
  cumulativeValueField: string;
  cumulativeShareField: string;
  thresholdShare: number;
  keyFactorFlagField: string;
  boundaryItemField?: string;
  longTailField?: string;
  tieBreakFields: string[];
  otherAggregationPolicy: 'aggregate-tail' | 'show-tail-gray' | 'drawer-detail' | 'table-fallback';
  tooltipPayload: string[];
  detailAction?: string;
};

type CompositionShareEvidenceBinding = {
  compositionMode: 'share' | 'composition' | 'structure' | 'market-share' | 'concentration' | 'distribution';
  metricId: string;
  metricName: string;
  unit: string;
  categoryIdField: string;
  categoryNameField: string;
  valueField: string;
  totalField: string;
  shareField: string;
  denominatorPolicy: 'all-filtered-rows' | 'api-total' | 'visible-total' | 'declared-market-total' | 'parent-total';
  orderRule: 'value-desc' | 'business-order' | 'time-order' | 'hierarchy-order';
  otherPolicy: 'topn-plus-other' | 'small-slice-merge' | 'none' | 'blocked';
  topN?: number;
  parentIdField?: string;
  parentNameField?: string;
  levelField?: string;
  parentValueField?: string;
  parentShareField?: string;
  totalShareField?: string;
  childShareField?: string;
  timeField?: string;
  comparisonValueField?: string;
  comparisonShareField?: string;
  deltaShareField?: string;
  concentrationFields?: {
    cr1Field?: string;
    cr3Field?: string;
    cr5Field?: string;
    hhiField?: string;
    otherShareField?: string;
  };
  distributionFields?: {
    bucketField: string;
    bucketSortField: string;
    countField: string;
    bucketShareField: string;
  };
  geoField?: string;
  lonField?: string;
  latField?: string;
  tooltipPayload: string[];
  detailAction?: string;
};

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

type DistributionAnalysisEvidenceBinding = {
  distributionMode:
    | 'numeric-distribution'
    | 'interval-distribution'
    | 'density-distribution'
    | 'quantile-distribution'
    | 'boxplot-distribution'
    | 'spatial-distribution'
    | 'time-distribution'
    | 'comparison-distribution'
    | 'multidimensional-distribution';
  metricId: string;
  metricName: string;
  unit: string;
  sampleGrain: string;
  sampleCountField: string;
  valueField?: string;
  weightField?: string;
  bucketFields?: {
    bucketIdField: string;
    bucketLabelField: string;
    lowerBoundField?: string;
    upperBoundField?: string;
    countField: string;
    shareField?: string;
    cumulativeCountField?: string;
    cumulativeShareField?: string;
    sortField?: string;
  };
  densityFields?: {
    xField: string;
    densityField: string;
    bandwidthField?: string;
    estimatorField?: string;
    groupField?: string;
  };
  quantileFields?: {
    percentileField?: string;
    percentileValueField?: string;
    q1Field?: string;
    medianField?: string;
    q3Field?: string;
    p10Field?: string;
    p25Field?: string;
    p75Field?: string;
    p90Field?: string;
  };
  boxplotFields?: {
    categoryField: string;
    minField: string;
    q1Field: string;
    medianField: string;
    q3Field: string;
    maxField: string;
    outlierField?: string;
    whiskerRuleField?: string;
  };
  heatmapFields?: {
    xField: string;
    yField: string;
    valueField: string;
    missingPolicy: 'missing-as-null' | 'missing-as-zero' | 'explicit-empty-cell';
  };
  geographyFields?: {
    geoIdField?: string;
    geoNameField?: string;
    lonField?: string;
    latField?: string;
    mapResource?: string;
  };
  comparisonFields?: {
    groupField?: string;
    baselineField?: string;
    deltaField?: string;
    deltaRateField?: string;
  };
  intervalPolicy?: 'equal-width' | 'quantile' | 'business-rule' | 'api-provided' | 'custom';
  missingValuePolicy:
    | 'missing-as-null'
    | 'missing-as-zero'
    | 'explicit-empty-cell'
    | 'exclude-with-disclosure';
  zeroValuePolicy: 'true-zero' | 'empty-zero' | 'exclude-zero' | 'domain-defined';
  outOfRangePolicy:
    | 'clip-to-domain'
    | 'show-overflow-bucket'
    | 'mark-as-outlier'
    | 'exclude-with-disclosure';
  densityPolicy?: 'kde' | 'histogram-smoothed' | 'hexbin' | 'precomputed-density' | 'none';
  tooltipPayload: string[];
  detailAction?: string;
  exportFields?: string[];
};

type AnomalyAnalysisEvidenceBinding = {
  anomalyObjectType:
    | 'metric'
    | 'order'
    | 'request'
    | 'server'
    | 'region'
    | 'user'
    | 'service'
    | 'indicator'
    | 'risk-event'
    | 'warning'
    | 'outlier-point'
    | 'project-defined';
  anomalyIdField?: string;
  objectIdField?: string;
  objectNameField?: string;
  severityField: string;
  severityDictionary: string[];
  statusField?: string;
  statusDictionary?: string[];
  currentValueField?: string;
  unit?: string;
  baselineValueField?: string;
  deltaField?: string;
  deltaRateField?: string;
  directionRule?: 'higher-is-worse' | 'lower-is-worse' | 'outside-band-is-worse' | 'domain-defined';
  thresholdFields?: {
    warningThresholdField?: string;
    highThresholdField?: string;
    mediumThresholdField?: string;
    lowThresholdField?: string;
    thresholdUnit?: string;
    thresholdRule?: string;
    intervalLabelField?: string;
    lowerBoundField?: string;
    upperBoundField?: string;
  };
  timeFields?: {
    firstSeenAtField?: string;
    occurredAtField?: string;
    updatedAtField?: string;
    durationField?: string;
    timeGrain?: string;
    sortRule?: string;
  };
  impactFields?: {
    affectedUserField?: string;
    affectedOrderField?: string;
    affectedServiceField?: string;
    lossAmountField?: string;
    impactScoreField?: string;
    durationField?: string;
  };
  distributionFields?: {
    categoryField?: string;
    countField?: string;
    shareField?: string;
    totalField?: string;
    denominatorPolicy?: string;
  };
  timelineFields?: {
    eventIdField: string;
    eventTimeField: string;
    eventTitleField: string;
    eventStatusField: string;
    eventDetailField?: string;
  };
  rankingFields?: {
    rankField?: string;
    valueField: string;
    tieBreakFields?: string[];
    visibleLimit: number;
  };
  relationFields?: {
    nodeIdField?: string;
    nodeNameField?: string;
    nodeTypeField?: string;
    edgeSourceField?: string;
    edgeTargetField?: string;
    edgeWeightField?: string;
    relationDirection?: 'directed' | 'undirected' | 'mixed';
  };
  geoFields?: {
    regionIdField?: string;
    regionNameField?: string;
    geoCodeField?: string;
    lonField?: string;
    latField?: string;
    mapResource?: string;
    missingGeoPolicy?: string;
  };
  responseFields?: {
    ownerField?: string;
    actionField?: string;
    actionStatusField?: string;
    resolvedAtField?: string;
    slaField?: string;
  };
  tooltipPayload: string[];
  detailAction: string;
  exportFields?: string[];
  validationCases: string[];
};

type RelationshipAnalysisEvidenceBinding = {
  relationshipAnalysisCardPattern: RelationshipAnalysisCardPattern;
  relationTask:
    | 'correlation'
    | 'association'
    | 'influence'
    | 'dependency'
    | 'cooccurrence'
    | 'similarity'
    | 'flow'
    | 'community'
    | 'hierarchy'
    | 'pair-audit';
  entityGrain: string;
  sourceEntityFields?: string[];
  targetEntityFields?: string[];
  nodeFields?: string[];
  edgeFields?: string[];
  pairFields?: string[];
  metricFields: string[];
  strengthField?: string;
  directionField?: string;
  methodField?: string;
  timeField?: string;
  groupField?: string;
  thresholdRule?: string;
  densityLimit: string;
  labelRule: string;
  tooltipPayload: string[];
  exactValueRoute: string;
  localControls?: string[];
  rendererOwner: 'echarts' | 'antv-s2' | 'project-table' | 'data-driven-custom-diagram';
  fallback: string;
};

type BasicChartCardPattern =
  | 'single-series-bar-card'
  | 'comparison-line-trend-card'
  | 'area-trend-card'
  | 'bar-line-combo-card'
  | 'pie-composition-card'
  | 'donut-composition-card'
  | 'stacked-bar-composition-card'
  | 'multi-metric-combo-card'
  | 'filtered-bar-card'
  | 'tooltip-line-trend-card';

type SpecializedChartCardPattern =
  | 'gauge-progress-card'
  | 'choropleth-ranking-map-card'
  | 'time-heatmap-card'
  | 'candlestick-volume-card'
  | 'boxplot-distribution-card'
  | 'parallel-profile-card'
  | 'bubble-opportunity-card';

type FlowHierarchyDiagramCardPattern =
  | 'conversion-funnel-card'
  | 'multi-stage-sankey-card'
  | 'journey-stage-map-card'
  | 'hierarchy-tree-card'
  | 'hub-relation-network-card'
  | 'sunburst-composition-card'
  | 'treemap-composition-card'
  | 'path-conversion-flow-card';

type RelationshipAnalysisCardPattern =
  | 'relation-overview-hub-card'
  | 'relation-strength-matrix-card'
  | 'relation-flow-sankey-card'
  | 'relation-community-network-card'
  | 'relation-pair-compare-card'
  | 'relation-trend-card'
  | 'relation-hierarchy-tree-card'
  | 'relation-bubble-quadrant-card'
  | 'relation-factor-ranking-card'
  | 'relation-evolution-snapshot-card'
  | 'relation-bipartite-attribute-card'
  | 'relation-detail-table-card';

type ListStatusPattern =
  | 'simple-info-list'
  | 'progress-task-list'
  | 'severity-alert-list'
  | 'exception-record-list'
  | 'status-chip-set'
  | 'event-timeline'
  | 'user-object-list'
  | 'mixed-info-list';

type FilterControlPattern =
  | 'single-select-dropdown'
  | 'multi-tag-select'
  | 'date-range-selector'
  | 'searchable-select'
  | 'tree-path-selector'
  | 'advanced-filter-drawer'
  | 'combined-filter-chipbar';

type OverlayPanelPattern =
  | 'right-filter-drawer'
  | 'bottom-action-sheet'
  | 'center-confirmation-modal'
  | 'fullscreen-detail-modal'
  | 'top-notification-bar'
  | 'left-navigation-drawer'
  | 'side-detail-drawer'
  | 'large-detail-side-panel';

type MicroDashboardCardPattern =
  | 'sales-fresh-analysis-board'
  | 'user-operations-purple-board'
  | 'supply-chain-orange-monitoring-board'
  | 'finance-blue-analysis-board';

type StateFeedbackPattern =
  | 'fresh-line-state-set'
  | 'soft-illustration-state-set'
  | 'minimal-line-state-set'
  | 'dark-tech-state-set'
  | 'glass-card-state-set'
  | 'playful-healing-state-set'
  | 'business-blue-state-set'
  | 'immersive-fullscreen-state-set';

type StateFeedbackKind =
  | 'empty'
  | 'filtered-empty'
  | 'loading'
  | 'error'
  | 'no-permission'
  | 'building'
  | 'stale'
  | 'partial-data'
  | 'disabled'
  | 'success';

type StateFeedbackScope =
  | 'page'
  | 'parent-block'
  | 'sub-block'
  | 'component-body'
  | 'overlay'
  | 'card';

type AnalysisPerspective =
  | 'currentStatus'
  | 'targetProgress'
  | 'trendMovement'
  | 'comparisonDifference'
  | 'rankingContribution'
  | 'compositionShare'
  | 'decompositionDriver'
  | 'distributionSpread'
  | 'anomalyRisk'
  | 'relationshipInfluence'
  | 'flowTransfer'
  | 'processBottleneck'
  | 'conversionRetention'
  | 'spatialDistribution'
  | 'timePattern'
  | 'multiDimensionalProfile'
  | 'populationObject'
  | 'matrixDecision'
  | 'marketMovement'
  | 'definitionHelp'
  | 'conclusionInsight'
  | 'causeDiagnosis'
  | 'actionRecommendation'
  | 'reviewImpact'
  | 'dataQualityTrust'
  | 'detailEvidence'
  | 'filterExploration';

type SubBlockRole =
  | 'summary'
  | 'evidence'
  | 'primaryEvidence'
  | 'secondaryEvidence'
  | 'detail'
  | 'control'
  | 'peer'
  | 'state'
  | 'feedback'
  | 'status'
  | 'kpiStrip'
  | 'exactValuePath'
  | 'microGroup';

type ComponentMapping = {
  id: string;
  // Metadata for the layout/block title. Do not render this again inside the component body.
  title: string;
  priority: 'must-have' | 'should-have' | 'optional';
  sampleModuleRole?: 'businessRequired' | 'sampleStructure' | 'optionalEnhancement';
  displayTheme?: DisplayTheme;
  sourcePatternIds?: string[];
  patternRoles?: PatternRole[];
  styleGeneralization?: StyleGeneralizationContract;
  businessQuestion: string;
  analysisPerspective?: AnalysisPerspective;
  secondaryAnalysisPerspectives?: AnalysisPerspective[];
  answerAtom: string;
  semanticRole: string;
  block: string;
  // Top-level page-grid occupant. Uses the report page `8 * N` grid.
  parentBlockId?: string;
  // Optional local region inside the parent block body. Not a page-grid block.
  subBlockId?: string;
  subBlockRole?: SubBlockRole;
  componentType: 'card' | 'chart' | 'table' | 'text-summary' | 'drawer' | 'task' | 'action' | 'custom';
  visualType: string;
  kpiCardPattern?: KpiCardPattern;
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
  targetActualCardPattern?: TargetActualCardPattern;
  targetActualTrendCardPattern?: TargetActualTrendCardPattern;
  targetActualRadarCardPattern?: TargetActualRadarCardPattern;
  targetActualDonutCardPattern?: TargetActualDonutCardPattern;
  targetActualScatterCardPattern?: TargetActualScatterCardPattern;
  targetActualTablePattern?: TargetActualTablePattern;
  targetActualPivotTablePattern?: TargetActualPivotTablePattern;
  tableCardPattern?: TableCardPattern;
  rankingCardPattern?: RankingCardPattern;
  paretoCardPattern?: ParetoCardPattern;
  compositionShareCardPattern?: CompositionShareCardPattern;
  decompositionAttributionCardPattern?: DecompositionAttributionCardPattern;
  distributionAnalysisCardPattern?: DistributionAnalysisCardPattern;
  anomalyAnalysisCardPattern?: AnomalyAnalysisCardPattern;
  relationshipAnalysisCardPattern?: RelationshipAnalysisCardPattern;
  basicChartCardPattern?: BasicChartCardPattern;
  specializedChartCardPattern?: SpecializedChartCardPattern;
  flowHierarchyDiagramCardPattern?: FlowHierarchyDiagramCardPattern;
  listStatusPattern?: ListStatusPattern;
  overlayPanelPattern?: OverlayPanelPattern;
  microDashboardCardPattern?: MicroDashboardCardPattern;
  stateFeedbackPattern?: StateFeedbackPattern;
  chartSubtype?: string;
  tableSubtype?: string;
  dataSource: string;
  apiId?: string;
  apiEndpoint?: string;
  frontendComputePolicy?: 'component-ready' | 'format-only' | 'blocked';
  grain: string;
  primaryKey?: string;
  requiredFields: string[];
  formulas?: string[];
  rollupLogic?: string;
  numericFormatContracts?: NumericFormatContract[];
  analysisInsightContract?: AnalysisInsightContract;
  rankingEvidenceBinding?: RankingEvidenceBinding;
  paretoEvidenceBinding?: ParetoEvidenceBinding;
  compositionShareEvidenceBinding?: CompositionShareEvidenceBinding;
  decompositionAttributionEvidenceBinding?: DecompositionAttributionEvidenceBinding;
  distributionAnalysisEvidenceBinding?: DistributionAnalysisEvidenceBinding;
  anomalyAnalysisEvidenceBinding?: AnomalyAnalysisEvidenceBinding;
  relationshipAnalysisEvidenceBinding?: RelationshipAnalysisEvidenceBinding;
  compositePanelContract?: {
    topic: string;
    analysisSequence: Array<'summary' | 'trend' | 'structure' | 'contribution' | 'exception' | 'detail' | 'action'>;
    layoutPattern:
      | 'metric-main'
      | 'main-side'
      | 'main-detail'
      | 'main-two-side'
      | 'two-by-two'
      | 'metric-main-side';
    primaryChildId: string;
    children: Array<{
      id: string;
      role:
        | 'primary-metric'
        | 'main-visual'
        | 'auxiliary-visual'
        | 'top-list'
        | 'detail-preview'
        | 'insight'
        | 'legend'
        | 'state';
      visualType: string;
      priority: 'P1' | 'P2' | 'P3' | 'P4';
      minW: number;
      minH: number;
      datasetId?: string;
      requiredFields?: string[];
      unit?: string;
      localFilterScope?: 'panel' | 'child-only';
    }>;
    childCountLimit: number;
    primaryVisualWeight: '50-70%';
    contentHeightRule: 'contentH>=CH*0.60';
    sharedLocalFilters?: string[];
    childLocalFilterException?: string;
    sharedLegend?: boolean;
    sharedUnit?: string;
    linkedInteraction?: 'none' | 'hover-highlight' | 'click-select' | 'hover-and-click';
    detailPreview?: { maxRows: number; maxColumns: number; detailRoute?: string };
    responsiveFallback: string[];
    stateRules: string[];
  };
  microDashboardContract?: {
    topic: string;
    themeTone: 'fresh-green' | 'operation-purple' | 'warning-orange' | 'finance-blue' | 'neutral-blue';
    layoutPattern: 'portrait-kpi-grid' | 'portrait-kpi-grid-status' | 'wide-kpi-grid' | 'wide-kpi-grid-status';
    primarySequence: Array<'status' | 'trend' | 'structure' | 'ranking' | 'conversion' | 'progress' | 'warning' | 'detail' | 'cash' | 'action'>;
    kpiCount: number;
    parentMinW: number;
    parentMinH: number;
    childCountLimit: number;
    sections: Array<{
      id: string;
      role:
        | 'kpi-strip'
        | 'primary-trend'
        | 'composition'
        | 'ranking'
        | 'target-progress'
        | 'funnel'
        | 'heatmap'
        | 'sparkline-group'
        | 'status-strip'
        | 'warning-table'
        | 'detail-preview'
        | 'cash-status'
        | 'supplier-sla';
      componentType: 'card' | 'chart' | 'table' | 'text-summary' | 'drawer' | 'task' | 'action' | 'custom';
      visualType: string;
      patternField?: string;
      priority: 'P1' | 'P2' | 'P3' | 'P4';
      minW: number;
      minH: number;
      datasetId?: string;
      requiredFields?: string[];
      fallback: 'keep' | 'collapse-to-tab' | 'move-to-drawer' | 'move-to-fullscreen' | 'split-block' | 'hide-optional';
    }>;
    sharedFilters?: string[];
    linkedInteraction?: 'none' | 'hover-highlight' | 'click-select' | 'hover-and-click';
    detailRoute?: string;
    responsiveFallback: string[];
    stateRules: string[];
  };
  stateFeedbackContract?: {
    stateKind: StateFeedbackKind;
    scope: StateFeedbackScope;
    title: string;
    reason?: string;
    impact?: string;
    primaryAction?: { label: string; actionType: ActionType; customActionId?: string; payload?: string[] };
    secondaryAction?: { label: string; actionType: ActionType; customActionId?: string; payload?: string[] };
    statusMeta?: string[];
    minW: number;
    minH: number;
    preserveGeometry: boolean;
    permissionLeakageRule?: 'no-counts-no-silhouettes' | 'safe-scope-only' | 'not-applicable';
    retryPolicy?: 'wired-retry' | 'no-retry' | 'deferred';
    motionPolicy?: 'none' | 'reduced-motion-safe' | 'skeleton-only' | 'project-defined';
    accessibility: string[];
    responsiveFallback: string[];
    validationRules: string[];
  };
  pivotContract?: {
    rowDimensions: string[];
    columnDimensions: string[];
    measures: string[];
    aggregationFunctions: Record<string, string>;
    rateFormulas?: Record<string, { numerator: string; denominator: string; formula: string }>;
    subtotalRules?: string[];
    grandTotalRules?: string[];
    rowHierarchyDepth?: number;
    columnHierarchyDepth?: number;
    sortRules?: string[];
    densityFallback?: string[];
    renderer?: 'antv-s2' | 'project-s2-equivalent' | 'static-preview';
  };
  groupedHeaderContract?: {
    columnTree: Array<{
      id: string;
      title: string;
      field?: string;
      children?: string[];
      unit?: string;
      definition?: string;
      align?: 'left' | 'center' | 'right';
      width?: number;
      minWidth?: number;
      maxWidth?: number;
      priority?: number;
      sortable?: boolean;
      filterable?: boolean;
      fixed?: 'left' | 'right';
    }>;
    maxDepth: number;
    leafColumnCount: number;
    spanRules: 'computed-colSpan-rowSpan';
    fixedHeader: boolean;
    frozenColumns?: string[];
    componentLocalFilters?: string[];
    columnHeaderFilters?: string[];
    densityFallback?: string[];
    tooltipFields?: string[];
  };
  controlSemantics: ControlSemantics[];
  componentSchemaImpact: ComponentSchemaImpactDetail;
  navigationMetricLineage?: NavigationMetricLineage[];
  globalFilters: string[];
  filterMap: Record<string, string>;
  filterControlPatterns?: Record<string, FilterControlPattern>;
  filterExecutionStage?: 'sql-where' | 'source-query' | 'provider-query' | 'repository-query' | 'resolver-param' | 'redis-cache' | 'precompute-cache' | 'component-local' | 'bounded-local' | 'blocked';
  ignoredFilters?: string[];
  localControls?: string[];
  interactions?: string[];
  actionPayload?: string[];
  stateKeys?: string[];
  kpiEvidenceBinding?: {
    overview?: {
      overviewTopic: string;
      overviewPattern: KpiOverviewCardPattern;
      leadMetricId?: string;
      metrics: KpiOverviewMetricBinding[];
      visibleMetricLimit: number;
      localControlId?: string;
      localControlType?:
        | 'period-segmented'
        | 'period-dropdown'
        | 'metric-segmented'
        | 'unit-scale-segmented'
        | 'overflow-menu';
      localControlOptions?: string[];
      selectedControlField?: string;
      exactValuePayload: string[];
      detailRoute?: string;
    };
    singleIndicator?: {
      evidenceVisual: 'sparkline' | 'mini-bars' | 'ring' | 'area-sparkline' | 'semi-gauge';
      trendDatasetId?: string;
      trendCategoryField?: string;
      trendValueField?: string;
      latestPointField?: string;
      targetField?: string;
      attainmentRateField?: string;
      progressTrackField?: string;
      localControlId?: string;
      localControlType?: 'period-dropdown' | 'grain-segmented' | 'unit-toggle' | 'scale-toggle';
      localControlOptions?: string[];
      selectedControlField?: string;
      exactValuePayload: string[];
    };
    judgment?: {
      judgmentPattern: KpiJudgmentCardPattern;
      judgmentKind: 'status' | 'health' | 'rating' | 'score' | 'gauge' | 'risk' | 'progress';
      statusField?: string;
      scoreField?: string;
      scoreRange?: [number, number];
      levelField?: string;
      bands?: KpiJudgmentBandBinding[];
      thresholdFields?: string[];
      direction: 'higher-better' | 'lower-better' | 'range-target' | 'status-enum';
      heroVisual:
        | 'semantic-icon'
        | 'ring'
        | 'semi-gauge'
        | 'bullet-range'
        | 'dimension-bars'
        | 'rating-stars'
        | 'rating-distribution';
      dimensionDatasetId?: string;
      dimensionNameField?: string;
      dimensionScoreField?: string;
      ratingDistributionFields?: string[];
      comparisonStripFields?: string[];
      footerEvidenceFields: string[];
      exactValuePayload: string[];
    };
    goalExecution?: {
      goalPattern: KpiGoalExecutionCardPattern;
      goalExecutionKind: 'attainment' | 'gap' | 'progress' | 'milestone';
      direction: 'higher-better' | 'lower-better' | 'range-target' | 'schedule-target';
      actualField?: string;
      targetField?: string;
      attainmentRateField?: string;
      gapField?: string;
      gapRateField?: string;
      remainingField?: string;
      deadlineField?: string;
      dueStatusField?: string;
      planProgressField?: string;
      actualProgressField?: string;
      progressDeltaField?: string;
      remainingTimeField?: string;
      milestone?: KpiGoalMilestoneBinding;
      heroVisual:
        | 'ring'
        | 'semi-gauge'
        | 'linear-progress'
        | 'target-actual-bars'
        | 'dot-strip'
        | 'stepper'
        | 'timeline'
        | 'cumulative-line';
      comparisonStripFields?: string[];
      footerEvidenceFields: string[];
      exactValuePayload: string[];
    };
    timeSeries?: {
      timeSeriesPattern: KpiTimeSeriesCardPattern;
      temporalAnalysisKind: 'trend' | 'change' | 'yoy-mom' | 'cycle' | 'volatility' | 'forecast';
      direction: 'higher-better' | 'lower-better' | 'range-target' | 'neutral';
      datasetId: string;
      xField: string;
      yField: string;
      grainField?: string;
      latestPeriodField: string;
      tooltipPayload: string[];
      baselineLabelField?: string;
      baselineValueField?: string;
      deltaValueField?: string;
      deltaRateField?: string;
      yoyValueField?: string;
      yoyRateField?: string;
      momValueField?: string;
      momRateField?: string;
      priorYearComparableValueField?: string;
      priorPeriodValueField?: string;
      cycle?: {
        grainField: string;
        periodStartField: string;
        periodEndField: string;
        currentIndexField: string;
        totalCountField: string;
        progressField?: string;
        phaseStatusField?: string;
      };
      volatility?: {
        formula: string;
        volatilityRateField: string;
        levelField: string;
        maxField?: string;
        minField?: string;
        stdDevField?: string;
        thresholdBandFields?: string[];
      };
      forecast?: {
        forecastDatasetId: string;
        forecastStartField: string;
        forecastEndField?: string;
        horizonField?: string;
        forecastValueField: string;
        lowerBoundField?: string;
        upperBoundField?: string;
        forecastStatusField?: string;
      };
      footerEvidenceFields: string[];
      exactValuePayload: string[];
    };
    scatter?: {
      datasetId: string;
      objectIdField: string;
      objectNameField: string;
      xField: string;
      yField: string;
      xUnit: string;
      yUnit: string;
      sizeField?: string;
      colorField?: string;
      trendlineField?: string;
      referenceFields?: string[];
      thresholdFields?: string[];
      quadrantFields?: string[];
      pointLimit?: number;
    };
    map?: {
      datasetId: string;
      regionCodeField?: string;
      regionNameField?: string;
      valueField: string;
      visualMapField?: string;
      pointDatasetId?: string;
      lonField?: string;
      latField?: string;
      pointValueField?: string;
      categoryField?: string;
      projection: string;
      mapResource: string;
      legendFields?: string[];
      missingGeoPolicy: string;
    };
    comparison?: {
      leftPaneFields: string[];
      rightPaneFields: string[];
      baselineLabels: string[];
      valueFields: string[];
      deltaField?: string;
      gapField?: string;
      conclusionField: string;
      sharedUnit: string;
      sharedGrain: string;
    };
    comparisonAnalysis?: {
      comparisonPattern: KpiComparisonAnalysisCardPattern;
      comparisonAnalysisKind: 'direct' | 'group' | 'competitor' | 'benchmark' | 'variance';
      evidenceMode: KpiComparisonAnalysisEvidenceMode;
      direction: 'higher-better' | 'lower-better' | 'range-target' | 'neutral';
      datasetId: string;
      subjectIdField?: string;
      subjectNameField: string;
      subjectRoleField?: string;
      groupField?: string;
      competitorField?: string;
      metricField: string;
      metricNameField?: string;
      unit: string;
      grainField?: string;
      periodField?: string;
      filterScopeField?: string;
      currentValueField: string;
      comparisonValueField?: string;
      deltaValueField?: string;
      deltaRateField?: string;
      rankField?: string;
      shareField?: string;
      marketTotalField?: string;
      benchmarkSourceField?: string;
      benchmarkValueField?: string;
      benchmarkP50Field?: string;
      benchmarkP75Field?: string;
      benchmarkP90Field?: string;
      varianceFormula?: string;
      varianceValueField?: string;
      varianceRateField?: string;
      attainmentRateField?: string;
      normalizedScoreField?: string;
      seriesDatasetId?: string;
      xField?: string;
      yField?: string;
      seriesField?: string;
      radarDimensionField?: string;
      radarScoreField?: string;
      sortRule?: string;
      visibleSubjectLimit?: number;
      tooltipPayload: string[];
      footerEvidenceFields: string[];
      exactValuePayload: string[];
    };
  };
  updateTriggers: string[];
  parentLayoutSpan?: string;
  subBlockLayout?: string;
  layoutSpan: string;
  emptyState: string;
  validationCases: string[];
};
```

Rules:

- Use stable IDs such as `attritionTrend`, `riskEmployeeTable`, or `revenueGapWaterfall`.
- For sample/source restoration, set `sampleModuleRole`. Only `businessRequired` modules should become `must-have`; `sampleStructure` preserves visible sample structure, and `optionalEnhancement` must be labeled as an enhancement.
- Set `analysisPerspective` on each mapped component when the component is selected from a business intent such as 看现状, 看目标, 看趋势, 看排名, 看原因, 看行动, or equivalent. Use `secondaryAnalysisPerspectives` only when the same visible component supports additional decision questions; do not duplicate the component only to represent each perspective.
- When a display-theme pattern library is used, set `displayTheme`, `sourcePatternIds`, and `patternRoles` on every affected mapping row. Pattern IDs should be stable values such as `detail-table-01`.
- For screenshot/sample-derived reusable styles, set `styleGeneralization`. Use `covered-by-existing-pattern` when one controlled pattern field is enough, `covered-by-composed-patterns` when the design is a valid composition of several controlled pattern fields, `requires-pattern-extension` when the sample is reusable but not yet covered, and `out-of-scope-one-off` only for non-reusable, audit-only, or exact-restoration-only surfaces. Reusable style knowledge must have `textOnlyReproduction: true`.
- `visualType` must match runnable template/widget capability where a template is used.
- Conclusion/evidence/action cards should keep `componentType: 'text-summary'`, `visualType: 'text-summary'`, set `analysisInsightContract.subtype: 'conclusion-card'`, `analysisInsightContract.insightFamily: 'conclusion'`, and set `analysisInsightContract.conclusionCardPattern` to `metric-evidence-conclusion`, `finding-action-conclusion`, or `compact-conclusion-summary` from `$report-component-style-design` `references/03a-conclusion-evidence-action-cards.md`.
- Metric cards that use `visualType: 'metric-card'` should set `kpiCardPattern` when the card's expression matters. Use `plain-metric`, `target-wave`, `mini-bar-trend`, `highlight-line-trend`, `horizontal-trend-compare`, `horizontal-axis-line-trend`, `horizontal-axis-bar-compare`, `horizontal-axis-scatter-diagnostic`, `horizontal-spatial-map-diagnostic`, `paired-comparison-diagnostic`, `horizontal-ring-progress`, `horizontal-target-progress`, `horizontal-status-trend-compare`, `horizontal-grain-bar-switch`, `horizontal-period-summary-strip`, `horizontal-pp-assist-info`, or `horizontal-warning-status-band` from `$report-component-style-design` `references/04a-kpi-card-patterns.md`; do not create new enum values for visual variants. For KPI overview cards, also set `kpiOverviewCardPattern` and `kpiEvidenceBinding.overview` so the card can be reproduced without screenshot access. For single-indicator KPI grid cards, also set `kpiSingleIndicatorLayoutMode` and `kpiEvidenceBinding.singleIndicator`. For status/health/score/rating/gauge judgment cards, also set `kpiJudgmentCardPattern` and `kpiEvidenceBinding.judgment` with status or score fields, range/status dictionary, thresholds/bands when visible, direction semantics, one hero visual, comparison strip fields, footer evidence, and exact-value payload. For target attainment, gap, progress, or milestone execution cards, also set `kpiGoalExecutionCardPattern` and `kpiEvidenceBinding.goalExecution` with `goalExecutionKind`, direction semantics, actual/target fields, required attainment/gap/progress/milestone fields, formula/denominator behavior, deadline or remaining-time fields when visible, one execution hero visual, comparison strip fields, footer evidence, and exact-value payload. For trend, change, YoY/MoM, cycle, volatility, or forecast time-series cards, also set `kpiTimeSeriesCardPattern` and `kpiEvidenceBinding.timeSeries` with `temporalAnalysisKind`, ordered x/y fields, grain, latest period, direction semantics, baseline/cycle/volatility/forecast fields required by the selected pattern, tooltip payload, footer evidence, and exact-value payload. For direct comparison, group comparison, competitor comparison, benchmark position, or variance/gap diagnosis cards, also set `kpiComparisonAnalysisCardPattern`, `kpiComparisonAnalysisEvidenceMode`, and `kpiEvidenceBinding.comparisonAnalysis` with `comparisonAnalysisKind`, comparable subject grain/roles, shared metric definition, unit, period/grain, filter scope, direction semantics, benchmark or variance fields when required, sort/visible-limit rules, tooltip payload, footer evidence, and exact-value payload. When `horizontal-axis-line-trend` is used, set `kpiAxisLineEvidenceMode`, ordered x/y fields, axis unit, tooltip payload, and any target/reference/threshold/phase/comparison-series fields. When `horizontal-axis-bar-compare` is used, set `kpiAxisBarEvidenceMode`, category/value fields, axis unit, sort rule, visible limit, tooltip payload, and any target/reference/threshold/change-rate/comparison-series fields. When `horizontal-axis-scatter-diagnostic` is used, set `kpiScatterEvidenceMode`, `kpiEvidenceBinding.scatter`, object grain, x/y fields and units, point limit/density strategy, tooltip payload, and any trendline/reference/threshold/quadrant/category/size fields. When `horizontal-spatial-map-diagnostic` is used, set `kpiMapEvidenceMode`, `kpiEvidenceBinding.map`, geography fields, projection/map resource, missing-geo policy, visualMap/legend fields, tooltip payload, and any target-gap/change/category/point fields. When `paired-comparison-diagnostic` is used, set `kpiComparisonEvidenceMode`, `kpiEvidenceBinding.comparison`, left/right pane fields, baseline labels, shared unit/grain, delta/gap/conclusion fields, and optional mini evidence fields.
- Target/actual comparison cards should keep `visualType: 'bar'`, set `chartSubtype: 'target-actual-comparison'`, and set `targetActualCardPattern` to `standard-summary-panel`, `emphasis-header-summary`, or `soft-chip-summary` from `$report-component-style-design` `references/04b-target-actual-comparison-cards.md`.
- Target/actual trend cards should keep `visualType: 'line'`, set `chartSubtype: 'target-actual-trend'`, and set `targetActualTrendCardPattern` to `emphasis-wave-trend`, `standard-summary-trend`, or `soft-chip-trend` from `$report-component-style-design` `references/04c-target-actual-trend-cards.md`.
- Target/actual radar cards should keep `visualType: 'radar'`, set `chartSubtype: 'target-actual-radar'`, and set `targetActualRadarCardPattern` to `emphasis-wave-radar` or `standard-action-radar` from `$report-component-style-design` `references/04d-target-actual-radar-cards.md`.
- Target/actual donut cards should keep `visualType: 'pie'`, set `chartSubtype: 'target-actual-donut'`, and set `targetActualDonutCardPattern` to `emphasis-filter-donut` or `standard-filter-donut` from `$report-component-style-design` `references/04e-target-actual-donut-cards.md`.
- Target/actual scatter cards should keep `visualType: 'scatter'`, set `chartSubtype: 'target-actual-scatter'`, and set `targetActualScatterCardPattern` to `emphasis-filter-scatter` or `standard-filter-scatter` from `$report-component-style-design` `references/04f-target-actual-scatter-cards.md`.
- Target/actual detail table cards should keep `componentType: 'table'`, `visualType: 'table'`, set `tableSubtype: 'target-actual-detail'`, and set `targetActualTablePattern` to `standard-audit-table` or `compact-audit-table` from `$report-component-style-design` `references/06a-target-actual-detail-tables.md`.
- Target/actual pivot table cards should keep `componentType: 'table'`, `visualType: 'pivot'`, set `tableSubtype: 'target-actual-pivot'`, and set `targetActualPivotTablePattern` to `standard-hierarchy-pivot`, `share-matrix-pivot`, or `tree-expand-pivot` from `$report-component-style-design` `references/06b-target-actual-pivot-tables.md`.
- Reusable table card patterns should keep `componentType: 'table'`, keep `visualType` as `table` or `pivot`, and set `tableCardPattern` to `plain-detail-ledger-table`, `filtered-operational-status-table`, `grouped-header-summary-table`, `metric-matrix-table`, `s2-cross-pivot-table`, `fixed-column-scroll-table`, `grouped-subtotal-summary-table`, or `tree-hierarchy-table` from `$report-component-style-design` `references/06c-table-card-patterns.md`.
- Ranking, leaderboard, and Top N cards should keep `componentType: 'card'`, `visualType: 'ranking-list'`, set `rankingCardPattern` from `$report-component-style-design` `references/07a-top-ranking-cards.md`, and declare `rankingEvidenceBinding` with source-side Top N, object id/name, value/share/denominator, rank/tie-break fields, visible-count budget, overflow strategy, tooltip payload, and detail action. Use `paretoCardPattern` plus `paretoEvidenceBinding` when the card answers key-factor contribution, 80/20, cumulative share, or Pareto threshold questions.
- Composition, share, structure, and market-share cards should keep `componentType: 'card'`, `visualType: 'composition-card'`, set `compositionShareCardPattern` from `$report-component-style-design` `references/07c-composition-share-cards.md`, and declare `compositionShareEvidenceBinding` with metric/unit, category id/name, value, total, share, denominator policy, order rule, `Top N + 其他` or small-slice merge behavior, tooltip payload, and detail action. Use chart `visualType` values only for standalone chart blocks; use `composition-card` when donut, bars, treemap, funnel, bubble, map, or sunburst are wrapped with denominator, exact values, local controls, update time, and fallback inside one card.
- Decomposition, attribution, contribution, and hierarchy decomposition cards should keep `componentType: 'card'`, `visualType: 'decomposition-card'`, set `decompositionAttributionCardPattern` from `$report-component-style-design` `references/07d-decomposition-attribution-contribution-cards.md`, and declare `decompositionAttributionEvidenceBinding` with root metric, value fields, formula/node/link/stage/matrix fields as required by the pattern, sign rule, attribution method when causal attribution is claimed, reconciliation policy, residual/other policy, tooltip payload, and detail action. Use chart `visualType` values only for standalone chart blocks; use `decomposition-card` when formula, funnel, tree, Sankey, waterfall, matrix, heatmap, Top N, or hierarchy evidence is wrapped with root metric, exact values, local controls, and reconciliation inside one card.
- Distribution, interval, density, quantile, and boxplot cards should keep `componentType: 'card'`, `visualType: 'distribution-card'`, set `distributionAnalysisCardPattern` from `$report-component-style-design` `references/07e-distribution-interval-density-cards.md`, and declare `distributionAnalysisEvidenceBinding` with sample grain/count, metric/unit, selected bucket/density/quantile/boxplot/heatmap/geography/comparison fields, interval policy, density policy, explicit `missingValuePolicy`, `zeroValuePolicy`, `outOfRangePolicy`, tooltip payload, detail action, and export fields when exact audit is needed. Use chart `visualType` values only for standalone chart blocks; use `distribution-card` when histogram, interval donut, CDF, KDE, density heatmap, boxplot, distribution map, population pyramid, statistic strip, local controls, and exact-value evidence are packaged in one card.
- Anomaly, risk, warning, and outlier analysis cards should keep `componentType: 'card'`, `visualType: 'anomaly-card'`, `analysisPerspective: 'anomalyRisk'`, set `anomalyAnalysisCardPattern` from `$report-component-style-design` `references/07f-anomaly-risk-warning-outlier-cards.md`, and declare `anomalyAnalysisEvidenceBinding` with severity/status, current/baseline or threshold fields, occurrence/update/freshness time, impact or affected-object fields when visible, tooltip payload, detail action, export fields when exact audit is needed, and validation cases. Use chart/list/table `visualType` values only for standalone evidence blocks; use `anomaly-card` when trend, donut, interval, timeline, ranking, matrix, relation, map, scatter, gauge, list, or table evidence is wrapped with abnormality context and action path inside one card.
- Relationship, correlation, association, and influence cards should keep the real `visualType` such as `scatter`, `heatmap`, `graph`, `sankey`, `tree`, `line`, `bar`, or `table`, set `relationshipAnalysisCardPattern` from `$report-component-style-design` `references/09b-relationship-analysis-card-patterns.md`, and declare `relationshipAnalysisEvidenceBinding` with relation task, entity grain, source/target or pair/node/edge fields, metric/strength/direction/method fields, threshold rule when visible, density and label rules, tooltip payload, exact-value route, renderer ownership, and fallback. Use influence wording only when a method/model/business rule supports it; otherwise use correlation, association, co-occurrence, similarity, or dependency wording.
- Basic chart cards should keep `componentType: 'chart'`, keep `visualType` as the real chart family (`bar`, `line`, `combo`, or `pie`), and set `basicChartCardPattern` to `single-series-bar-card`, `comparison-line-trend-card`, `area-trend-card`, `bar-line-combo-card`, `pie-composition-card`, `donut-composition-card`, `stacked-bar-composition-card`, `multi-metric-combo-card`, `filtered-bar-card`, or `tooltip-line-trend-card` from `$report-component-style-design` `references/05d-basic-chart-card-patterns.md`.
- Specialized chart cards should keep `componentType: 'chart'`, keep `visualType` as the real chart family (`gauge`, `map`, `heatmap`, `candlestick`, `boxplot`, `parallel`, or `scatter`), and set `specializedChartCardPattern` to `gauge-progress-card`, `choropleth-ranking-map-card`, `time-heatmap-card`, `candlestick-volume-card`, `boxplot-distribution-card`, `parallel-profile-card`, or `bubble-opportunity-card` from `$report-component-style-design` `references/05e-specialized-chart-card-patterns.md`.
- Flow/hierarchy diagram cards should keep `componentType: 'chart'`, keep `visualType` as the real diagram family (`funnel`, `sankey`, `path`, `tree`, `graph`, `sunburst`, or `treemap`), and set `flowHierarchyDiagramCardPattern` to `conversion-funnel-card`, `multi-stage-sankey-card`, `journey-stage-map-card`, `hierarchy-tree-card`, `hub-relation-network-card`, `sunburst-composition-card`, `treemap-composition-card`, or `path-conversion-flow-card` from `$report-component-style-design` `references/09a-flow-hierarchy-diagram-card-patterns.md`.
- Reusable operational information lists, task lists, alert lists, exception lists, status chip groups, timelines, user/object lists, or mixed work-item lists should use `visualType: 'operational-list'` and set `listStatusPattern` to `simple-info-list`, `progress-task-list`, `severity-alert-list`, `exception-record-list`, `status-chip-set`, `event-timeline`, `user-object-list`, or `mixed-info-list` from `$report-component-style-design` `references/07b-operational-list-status-patterns.md`.
- Reusable overlay, drawer, modal, notification, action sheet, or detail panel components should use `visualType: 'overlay-panel'` and set `overlayPanelPattern` to `right-filter-drawer`, `bottom-action-sheet`, `center-confirmation-modal`, `fullscreen-detail-modal`, `top-notification-bar`, `left-navigation-drawer`, `side-detail-drawer`, or `large-detail-side-panel` from `$report-component-style-design` `references/08a-overlay-drawer-modal-patterns.md`.
- Micro Dashboard Cards should use `componentType: 'custom'`, `visualType: 'micro-dashboard'`, set `microDashboardCardPattern` to `sales-fresh-analysis-board`, `user-operations-purple-board`, `supply-chain-orange-monitoring-board`, or `finance-blue-analysis-board`, and declare `microDashboardContract` from `$report-component-style-design` `references/12f6-placement-micro-dashboard-card.md`. Use this only for one large single-topic card that passes child minimum sizes; otherwise use `compositePanelContract`, tabs, split blocks, drawer, or fullscreen.
- Reusable empty/loading/error/no-permission/building states should use `componentType: 'custom'`, `visualType: 'state-feedback'`, set `stateFeedbackPattern`, and declare `stateFeedbackContract` from `$report-component-style-design` `references/13-state-feedback-patterns.md`. State contracts must preserve geometry and must not leak restricted data in no-permission states.
- `parentBlockId` groups components that live in the same top-level `8 * N` parent block. `subBlockId` identifies the internal sub-block viewport that owns the component. Leave `subBlockId` empty only for single-component parent blocks.
- `parentLayoutSpan` is the top-level `columns * rows` span. `subBlockLayout` describes local grid/flex placement such as `area:evidence`, `local:2x1`, `track:minmax(240px,1fr)`, or `tab:trend`, and must preserve `subBlockInset:5px` plus `subBlockGap:5px` when sub-blocks exist.
- `filterMap` must map UI filter IDs to dataset fields or query params.
- `filterControlPatterns` should map visible filter IDs to `single-select-dropdown`, `multi-tag-select`, `date-range-selector`, `searchable-select`, `tree-path-selector`, `advanced-filter-drawer`, or `combined-filter-chipbar` when filter visual design is part of the handoff.
- `controlSemantics` must classify controls that affect the component as `perspective-switch`, `global-filter`, `local-filter`, or `drilldown-param`.
- `componentSchemaImpact` must explicitly state whether a control changes metric names, component collection, table headers, dimensions, metric formulas/口径, domain vocabulary, or only narrows rows.
- `navigationMetricLineage` is required when perspective navigation displays percentages, rankings, or status lights. Each item must declare `sourceDataset`, `field/formula`, `grain`, `affectedFilters`, and `periodBehavior`.
- `filterExecutionStage` must show where filters, sorting, pagination, ranking, grouping, and aggregation execute when implementation or handoff is in scope. Use `sql-where` for global/page-level database filters, `component-local` for filters over the already fetched component dataset, and `blocked` when the current design depends on page/API-level full-materialize-then-filter behavior.
- `apiId`/`apiEndpoint` should identify the API that serves this component when the output feeds API planning or frontend integration. Default to one component or coherent component group per API.
- `frontendComputePolicy` must be `component-ready` or `format-only` for implementation handoff. Use `blocked` when required business formulas, aggregations, rankings, filters, or series shaping are still expected to happen in the frontend.
- `grain` must state row level: employee-month, org-month, order, contract, project, alert, task, or reconciliation-pair.
- `numericFormatContracts` are required for visible metric-bearing fields. Each contract must define value type, raw/display unit, display scale, screen precision, tooltip/export precision, rounding mode, null/zero/denominator-zero behavior, negative-zero handling, formula precision policy when derived, and formatter ownership. Use `$metric-number-display-contract` as the default baseline.
- `analysisInsightContract` is required when a text-summary/card/task/custom component is used as a conclusion card, insight card, anomaly/risk explanation, attribution summary, recommendation/action card, definition/data-quality/forecast note, chart annotation, explanatory empty state, permission/no-result/delay note, or any analysis copy that influences a decision. It must declare subtype, family, conclusion, evidence or explicit insufficiency, affected object, comparison/change value when relevant, action/detail path when relevant, confidence/source/freshness/definition when relevant, local-filter scope, tooltip payload, and state rules.
- `compositePanelContract` is required when multiple child components live inside one report component container as one analysis unit. It must declare the shared topic, sequence, layout pattern, primary child, child roles/priorities/minimum sizes, default child-count limit, primary visual weight, content-height rule, panel-level local filters, any child-only filter exception, shared legend/unit behavior, linked interaction, detail-preview limit, responsive fallback, and parent/child state rules. Use it only when child components answer one question; split unrelated children into separate parent blocks.
- `groupedHeaderContract` is required when a table has `>8` visible columns or natural field groups such as metric families, actual/target/variance, current/YoY/MoM, amount/count/rate, time periods, finance sections, or pivot columns. It must declare the grouped column tree, leaf-field metadata, computed `colSpan`/`rowSpan`, max depth, fixed header, frozen row/primary columns, component-local filters vs per-column header filters, tooltip fields, and density fallback.
- `validationCases` must include default state, filtered state, empty/no-permission state, and interaction state when clickable.
- Use the controlled vocabularies and naming rules in `08-generation-stability.md`; do not invent enum values for `priority`, `componentType`, `visualType`, action type, data policy, or filter value type.

## Required Controlled Values

Use these values unless an existing project explicitly defines a different local vocabulary.

- `priority`: `must-have`, `should-have`, `optional`.
- `componentType`: `card`, `chart`, `table`, `text-summary`, `drawer`, `task`, `action`, `custom`.
- `visualType`: `line`, `bar`, `combo`, `candlestick`, `heatmap`, `pie`, `radar`, `path`, `sunburst`, `gauge`, `scatter`, `boxplot`, `parallel`, `map`, `graph`, `tree`, `treemap`, `sankey`, `funnel`, `metric-card`, `text-summary`, `table`, `pivot`, `ranking-list`, `composition-card`, `decomposition-card`, `distribution-card`, `anomaly-card`, `operational-list`, `overlay-panel`, `composite-panel`, `micro-dashboard`, `state-feedback`, `other`.
- `analysisPerspective`: `currentStatus`, `targetProgress`, `trendMovement`, `comparisonDifference`, `rankingContribution`, `compositionShare`, `decompositionDriver`, `distributionSpread`, `anomalyRisk`, `relationshipInfluence`, `flowTransfer`, `processBottleneck`, `conversionRetention`, `spatialDistribution`, `timePattern`, `multiDimensionalProfile`, `populationObject`, `matrixDecision`, `marketMovement`, `definitionHelp`, `conclusionInsight`, `causeDiagnosis`, `actionRecommendation`, `reviewImpact`, `dataQualityTrust`, `detailEvidence`, `filterExploration`.
- `conclusionCardPattern`: `metric-evidence-conclusion`, `finding-action-conclusion`, `compact-conclusion-summary`.
- `kpiCardPattern`: `plain-metric`, `target-wave`, `mini-bar-trend`, `highlight-line-trend`, `horizontal-trend-compare`, `horizontal-axis-line-trend`, `horizontal-axis-bar-compare`, `horizontal-axis-scatter-diagnostic`, `horizontal-spatial-map-diagnostic`, `paired-comparison-diagnostic`, `horizontal-ring-progress`, `horizontal-target-progress`, `horizontal-status-trend-compare`, `horizontal-grain-bar-switch`, `horizontal-period-summary-strip`, `horizontal-pp-assist-info`, `horizontal-warning-status-band`.
- `kpiAxisLineEvidenceMode`: `basic-compare-line`, `filled-baseline-line`, `target-reference-line`, `phase-annotated-line`, `unit-axis-line`, `grain-switch-line`, `dual-comparison-line`, `threshold-band-line`. Use only with `kpiCardPattern: horizontal-axis-line-trend`.
- `kpiAxisBarEvidenceMode`: `basic-horizontal-bar`, `period-comparison-bar`, `target-reference-bar`, `category-change-sidebar-bar`, `time-series-horizontal-bar`, `grain-switch-horizontal-bar`, `dual-series-horizontal-bar`, `threshold-warning-bar`. Use only with `kpiCardPattern: horizontal-axis-bar-compare`.
- `kpiScatterEvidenceMode`: `correlation-trendline-scatter`, `mean-reference-scatter`, `target-crosshair-scatter`, `distribution-change-band-scatter`, `threshold-quadrant-scatter`, `dual-series-trendline-scatter`, `change-callout-scatter`, `category-quadrant-scatter`. Use only with `kpiCardPattern: horizontal-axis-scatter-diagnostic`.
- `kpiMapEvidenceMode`: `choropleth-heat-map`, `graded-choropleth-map`, `bubble-target-gap-map`, `distribution-change-marker-map`, `column-symbol-map`, `annotated-interval-map`, `yoy-change-zone-map`, `point-category-summary-map`. Use only with `kpiCardPattern: horizontal-spatial-map-diagnostic`.
- `kpiComparisonEvidenceMode`: `metric-yoy-vs`, `progress-mom-vs`, `target-gap-progress-vs`, `improvement-dot-matrix-vs`, `trend-yoy-vs`, `structure-breakdown-vs`, `percentage-ring-vs`, `trend-mom-vs`. Use only with `kpiCardPattern: paired-comparison-diagnostic`.
- `kpiOverviewCardPattern`: `lead-metric-comparison-sparkline-overview`, `multi-metric-strip-progress-overview`, `domain-metric-cluster-progress-overview`. Use with `visualType: metric-card` when one wide card summarizes one business domain/topic with `2-5` visible metrics.
- `kpiSingleIndicatorLayoutMode`: `dropdown-sparkline-progress`, `unit-toggle-ring-progress`, `dropdown-minibar-progress`, `grain-switch-minibar-progress`, `dropdown-area-sparkline-progress`, `scale-toggle-area-progress`, `dropdown-gauge-progress`. Use with `visualType: metric-card` when a peer grid of single-indicator cards needs one metric, one comparison, one mini evidence visual, and one target/progress footer.
- `kpiJudgmentCardPattern`: `semantic-status-icon-card`, `progress-status-ring-card`, `health-score-ring-card`, `health-threshold-bullet-card`, `health-dimension-breakdown-card`, `rating-score-summary-card`, `rating-distribution-card`, `semicircle-gauge-target-card`. Use with `visualType: metric-card` when one card judges status, health, score, rating, risk, progress, or gauge state; bind status/score/range/threshold semantics, comparison strip fields, and footer evidence.
- `kpiGoalExecutionCardPattern`: `attainment-ring-summary-card`, `attainment-gauge-deadline-card`, `attainment-linear-target-card`, `attainment-unit-progress-card`, `gap-gauge-deficit-card`, `gap-target-actual-compare-card`, `progress-plan-actual-card`, `milestone-timeline-card`. Use with `visualType: metric-card` when one card manages target attainment, target gap, plan-vs-actual progress, remaining work, deadlines, or milestones; bind actual/target/gap/progress/milestone fields, direction semantics, formula/denominator behavior, comparison strip, footer evidence, and exact values.
- `kpiTimeSeriesCardPattern`: `trend-line-target-card`, `change-baseline-delta-card`, `yoy-mom-comparison-card`, `cycle-period-progress-card`, `volatility-stat-card`, `forecast-interval-card`. Use with `visualType: metric-card` when one card answers trend movement, named-baseline change, YoY/MoM comparison, cycle/period state, volatility/stability, or forecast uncertainty; bind ordered series, grain, latest period, baseline/cycle/volatility/forecast fields, direction semantics, footer evidence, and exact values.
- `kpiComparisonAnalysisCardPattern`: `direct-value-compare-card`, `group-segment-compare-card`, `competitor-position-card`, `benchmark-position-card`, `variance-gap-card`. Use with `visualType: metric-card` when one card answers direct value comparison, group/segment comparison, competitor position, benchmark distance, or variance/gap diagnosis; bind comparable subject roles, shared metric/unit/grain, benchmark or variance fields, sort/visible-limit rules, footer evidence, and exact values.
- `kpiComparisonAnalysisEvidenceMode`: `side-by-side-values`, `grouped-bars`, `stacked-distribution`, `multi-series-trend`, `market-share-donut`, `radar-profile`, `benchmark-ruler`, `variance-gauge`, `nps-score-scale`, `comparison-table`, `map-table-compare`. Use only with `kpiComparisonAnalysisCardPattern` and `kpiEvidenceBinding.comparisonAnalysis`.
- `targetActualCardPattern`: `standard-summary-panel`, `emphasis-header-summary`, `soft-chip-summary`.
- `targetActualTrendCardPattern`: `emphasis-wave-trend`, `standard-summary-trend`, `soft-chip-trend`.
- `targetActualRadarCardPattern`: `emphasis-wave-radar`, `standard-action-radar`.
- `targetActualDonutCardPattern`: `emphasis-filter-donut`, `standard-filter-donut`.
- `targetActualScatterCardPattern`: `emphasis-filter-scatter`, `standard-filter-scatter`.
- `tableSubtype`: `target-actual-detail` for target/actual detail table cards; `target-actual-pivot` for target/actual pivot table cards.
- `targetActualTablePattern`: `standard-audit-table`, `compact-audit-table`.
- `targetActualPivotTablePattern`: `standard-hierarchy-pivot`, `share-matrix-pivot`, `tree-expand-pivot`.
- `tableCardPattern`: `plain-detail-ledger-table`, `filtered-operational-status-table`, `grouped-header-summary-table`, `metric-matrix-table`, `s2-cross-pivot-table`, `fixed-column-scroll-table`, `grouped-subtotal-summary-table`, `tree-hierarchy-table`.
- `rankingCardPattern`: `basic-rank-list-card`, `trend-delta-rank-list-card`, `progress-bar-rank-list-card`, `podium-rank-card`, `yoy-microbar-rank-list-card`, `radar-comparison-rank-card`, `metric-summary-rank-card`, `time-switch-rank-card`, `share-donut-rank-card`, `map-distribution-rank-card`, `topn-bar-rank-card`, `topn-comparison-rank-card`, `topn-waterfall-strip-card`, `topn-sparkline-rank-list-card`, `topn-bubble-rank-card`, `topn-icon-card-grid`, `medal-horizontal-ranking`, `bar-progress-ranking`, `compact-list-ranking`.
- `paretoCardPattern`: `pareto-basic-card`, `pareto-table-chart-card`, `pareto-dual-axis-card`, `pareto-cumulative-fill-card`, `pareto-stacked-share-card`, `pareto-bubble-card`, `pareto-zone-card`, `pareto-ring-list-card`.
- `compositionShareCardPattern`: `basic-donut-share-card`, `donut-detail-share-card`, `percent-bar-share-card`, `multi-ring-hierarchy-share-card`, `share-trend-stack-card`, `share-ranking-topn-card`, `treemap-composition-card`, `share-metrics-summary-card`, `stacked-strip-composition-card`, `stacked-column-trend-composition-card`, `funnel-composition-card`, `bubble-composition-card`, `market-share-overview-card`, `market-share-concentration-card`, `share-distribution-interval-card`, `map-structure-card`, `sunburst-structure-card`. Use with `componentType: card`, `visualType: composition-card`, and `compositionShareEvidenceBinding`.
- `decompositionAttributionCardPattern`: `formula-decomposition-card`, `funnel-decomposition-card`, `tree-decomposition-card`, `sankey-decomposition-card`, `driver-factor-decomposition-card`, `variance-waterfall-decomposition-card`, `combined-decomposition-card`, `multilevel-metric-decomposition-card`, `total-attribution-card`, `funnel-attribution-card`, `channel-attribution-donut-card`, `touchpoint-attribution-list-card`, `segment-attribution-card`, `feature-attribution-bar-card`, `time-attribution-waterfall-card`, `multidimensional-attribution-matrix-card`, `overall-contribution-card`, `contribution-waterfall-card`, `contribution-structure-card`, `contribution-comparison-card`, `contribution-trend-card`, `contribution-tree-card`, `key-contribution-topn-card`, `contribution-heatmap-card`, `progressive-hierarchy-decomposition-card`, `hierarchy-tree-decomposition-card`, `hierarchy-waterfall-card`, `indented-hierarchy-table-card`, `hierarchy-share-card`, `path-contribution-card`, `multilevel-comparison-hierarchy-card`, `target-attainment-hierarchy-attribution-card`. Use with `componentType: card`, `visualType: decomposition-card`, and `decompositionAttributionEvidenceBinding`.
- `distributionAnalysisCardPattern`: `numeric-histogram-distribution-card`, `interval-donut-distribution-card`, `percentile-cdf-distribution-card`, `geographic-distribution-card`, `time-distribution-card`, `distribution-comparison-card`, `calendar-heatmap-distribution-card`, `multidimensional-population-distribution-card`, `interval-histogram-card`, `interval-share-donut-card`, `interval-boxplot-card`, `interval-comparison-card`, `interval-stacked-trend-card`, `cumulative-interval-card`, `interval-scatter-strip-card`, `interval-detail-table-card`, `univariate-density-curve-card`, `interval-density-curve-card`, `grouped-density-comparison-card`, `density-heatmap-card`, `kde-cumulative-density-card`, `bivariate-density-hexbin-card`, `quantile-band-density-card`, `density-overview-card`, `boxplot-kpi-summary-card`, `time-series-boxplot-card`, `grouped-boxplot-comparison-card`, `boxplot-overview-card`, `boxplot-side-summary-card`, `weekday-boxplot-card`, `anomaly-boxplot-card`, `boxplot-detail-table-card`. Use with `componentType: card`, `visualType: distribution-card`, and `distributionAnalysisEvidenceBinding`.
- `anomalyAnalysisCardPattern`: `anomaly-overview-card`, `anomaly-trend-compare-card`, `anomaly-distribution-structure-card`, `anomaly-interval-threshold-card`, `anomaly-timeline-card`, `anomaly-ranking-top-card`, `anomaly-impact-assessment-card`, `anomaly-baseline-compare-card`, `anomaly-summary-table-card`, `anomaly-multi-metric-monitor-card`, `risk-matrix-card`, `risk-response-status-card`, `anomaly-relation-influence-card`, `anomaly-geographic-distribution-card`, `outlier-scatter-card`, `warning-progress-donut-card`. Use with `componentType: card`, `visualType: anomaly-card`, `analysisPerspective: anomalyRisk`, and `anomalyAnalysisEvidenceBinding`.
- `basicChartCardPattern`: `single-series-bar-card`, `comparison-line-trend-card`, `area-trend-card`, `bar-line-combo-card`, `pie-composition-card`, `donut-composition-card`, `stacked-bar-composition-card`, `multi-metric-combo-card`, `filtered-bar-card`, `tooltip-line-trend-card`.
- `specializedChartCardPattern`: `gauge-progress-card`, `choropleth-ranking-map-card`, `time-heatmap-card`, `candlestick-volume-card`, `boxplot-distribution-card`, `parallel-profile-card`, `bubble-opportunity-card`.
- `flowHierarchyDiagramCardPattern`: `conversion-funnel-card`, `multi-stage-sankey-card`, `journey-stage-map-card`, `hierarchy-tree-card`, `hub-relation-network-card`, `sunburst-composition-card`, `treemap-composition-card`, `path-conversion-flow-card`.
- `relationshipAnalysisCardPattern`: `relation-overview-hub-card`, `relation-strength-matrix-card`, `relation-flow-sankey-card`, `relation-community-network-card`, `relation-pair-compare-card`, `relation-trend-card`, `relation-hierarchy-tree-card`, `relation-bubble-quadrant-card`, `relation-factor-ranking-card`, `relation-evolution-snapshot-card`, `relation-bipartite-attribute-card`, `relation-detail-table-card`. Use with `analysisPerspective: relationshipInfluence` and the real renderer `visualType`.
- `listStatusPattern`: `simple-info-list`, `progress-task-list`, `severity-alert-list`, `exception-record-list`, `status-chip-set`, `event-timeline`, `user-object-list`, `mixed-info-list`.
- `overlayPanelPattern`: `right-filter-drawer`, `bottom-action-sheet`, `center-confirmation-modal`, `fullscreen-detail-modal`, `top-notification-bar`, `left-navigation-drawer`, `side-detail-drawer`, `large-detail-side-panel`.
- `microDashboardCardPattern`: `sales-fresh-analysis-board`, `user-operations-purple-board`, `supply-chain-orange-monitoring-board`, `finance-blue-analysis-board`.
- `stateFeedbackPattern`: `fresh-line-state-set`, `soft-illustration-state-set`, `minimal-line-state-set`, `dark-tech-state-set`, `glass-card-state-set`, `playful-healing-state-set`, `business-blue-state-set`, `immersive-fullscreen-state-set`.
- `stateFeedbackKind`: `empty`, `filtered-empty`, `loading`, `error`, `no-permission`, `building`, `stale`, `partial-data`, `disabled`, `success`.
- `subBlockRole`: `summary`, `evidence`, `primaryEvidence`, `secondaryEvidence`, `detail`, `control`, `peer`, `state`, `feedback`, `status`, `kpiStrip`, `exactValuePath`, `microGroup`. Use the specific role instead of overloading `state` or `microGroup` when the sub-block is a feedback state, status strip, KPI strip, primary evidence chart, secondary evidence chart, or exact-value path.
- Built-in action type: `openModal`, `closeModal`, `setFilters`, `resetFilters`, `navigateUrl`, `print`, `fullscreen`, `refresh`. Use `custom` only with `customActionId`, event owner, and payload contract. Avoid `switchNav` for new components unless maintaining legacy config.
- `controlSemantics`: `perspective-switch`, `global-filter`, `local-filter`, `drilldown-param`.
- `componentSchemaImpact`: `none`, `row-scope-only`, `metric-name`, `metric-set`, `component-set`, `table-schema`, `dimension-set`, `definition-change`, `domain-vocabulary`, `mixed`.
- `navigationMetricKind`: `percentage`, `ranking`, `status-light`.
- `periodBehavior`: `selected-period`, `current-period`, `comparison-period`, `rolling-window`, `latest-snapshot`, `static-display-copy`.
- `filterExecutionStage`: `sql-where`, `source-query`, `provider-query`, `repository-query`, `resolver-param`, `redis-cache`, `precompute-cache`, `component-local`, `bounded-local`, or `blocked`.
- `filterValueType`: `single`, `multiple`, `range`, `keyword`, `date`, `treePath`, `enum`, `toggle`, `mixed`.
- `filterControlPattern`: `single-select-dropdown`, `multi-tag-select`, `date-range-selector`, `searchable-select`, `tree-path-selector`, `advanced-filter-drawer`, `combined-filter-chipbar`.
- `dataPolicy`: `static` only for explicit narrative/static content, `external` only when the component manages runtime data outside normal datasets.
- `visualSourceRole`: `temporary-evidence`, `exact-restoration-source`, `visual-regression-baseline`, `runtime-asset`, `audit-evidence`, `reusable-inspiration`.
- `styleGeneralizationStatus`: `covered-by-existing-pattern`, `covered-by-composed-patterns`, `requires-pattern-extension`, `out-of-scope-one-off`.

## Binding Matrix

Every mapping must produce a binding matrix before implementation or final specification.

Minimum columns:

- Component ID, parent block ID, optional sub-block ID, and layout/block title metadata.
- Display theme, source pattern IDs, and pattern roles when the workflow selected reusable pattern cards.
- Style generalization status, canonical pattern reference, pattern fields, adaptive variables, renderer owner, and text-only reproduction flag when the component style is sample-derived or reusable.
- Priority.
- Component type, `visualType`, planned parent `columns * rows` span, and sub-block layout when present.
- Sub-block spacing: `subBlockInset:5px` and `subBlockGap:5px` when the component lives inside a composed parent block.
- Business question, answer atom, and semantic role.
- Data source or dataset.
- API ID/path and frontend compute policy when an API/backend handoff is in scope.
- Row grain, primary key, and required fields.
- Metric formulas and rollup logic.
- Numeric display contracts for every visible metric-bearing field, including percent/rate scale and denominator-zero behavior.
- `analysisInsightContract` when the component is an analysis/explanation/decision-support text summary, card, annotation, task, or state note.
- `anomalyAnalysisEvidenceBinding` when `visualType` is `anomaly-card`, including severity/status, baseline or threshold, time/freshness, impact/object, exact-value/detail/action path, and validation cases.
- `compositePanelContract` when `visualType` is `composite-panel` or multiple child components are intentionally combined into one component container.
- Control semantics for each control that affects the component.
- Component schema impact: whether the control changes metric names, component set, table headers, dimensions, formulas/口径, domain vocabulary, or only row scope.
- Navigation metric lineage when perspective navigation shows percentages, rankings, or status lights: `sourceDataset`, `field/formula`, `grain`, `affectedFilters`, `periodBehavior`.
- Global filters that affect it.
- Ignored filters and visible scope label.
- Local filters or internal tabs.
- Filter-to-field or filter-to-query mapping.
- Filter control pattern for every visible filter when visual filter design is in scope.
- Filter/sort/page execution stage.
- Interaction state: selected row, chart mark, drill path, drawer, modal, or jump context.
- Action payload or emitted event.
- Update trigger: filter change, refresh, drilldown, permission change, data reload, resize, fullscreen.
- Reset/stale behavior when selected object leaves scope.
- Export/download behavior.
- Validation cases.

## Data Accuracy Rules

- A component without a data source is decorative unless explicitly static narrative.
- A selected pattern card without a component/control/data/API/interaction/export/operations/validation impact is decorative. Mark it as backlog or remove it from completed scope.
- A data-bearing component should have a matching API or provider contract when implementation or handoff is in scope. Do not make a complex page-level API the hidden source for multiple unrelated components.
- KPI cards, conclusion cards, status cards, warning cards, and text-summary cards must have a source dataset or explicit static policy.
- Visible sample/source modules are not automatically `must-have`. A module becomes `businessRequired` only when it directly answers the stated report question; otherwise it remains `sampleStructure` or `optionalEnhancement`.
- Empty states must name the reason: no matching filter result, no permission, loading failed, source not configured, or static placeholder.
- Additive KPI/chart totals must reconcile with detail rows under the same filters.
- Non-additive metrics such as rates, scores, and completion rates must recalculate from raw numerator/denominator fields.
- A primary/global filter that should affect a component must map to a dataset field, query param, resolver param, or required filter. It cannot be hidden in `ignoredFilters`.
- Business domain, report theme, management object, subject area, and first-level perspective switching must not be represented as ordinary filters when they change metric names, component semantics, table headers, metric口径, or domain vocabulary.
- Perspective navigation percentages, rankings, and status lights are data-bearing metrics. They must be backed by business facts, aggregate datasets, or resolvers with lineage; they must not be hidden in `filterData.meta`.
- Filter option `meta` may contain only dimensional/static descriptors such as name aliases, sort order, permission, description, icon, disabled reason, stable category tags, or UI hints. Dynamic KPI values belong in business facts or resolvers.
- Mock/offline data must include enough dimension grain or resolver logic for each affected primary filter to return different values when business reality differs. A single static snapshot is allowed only for explicitly invariant/static content.
- For backend/API handoff, business formulas, aggregations, ranking, grouping, Top/Bottom, filtering, pagination, and chart-series/table shaping should be returned as component-ready response fields. The frontend may do display formatting, enum label display, null handling, local UI sorting of tiny already-returned option lists, and interaction state only.
- Do not design page/API-level full-materialize-then-filter data paths. Components, stores, adapters, and static helpers must not build/fetch all candidate rows and then apply global filters, permission filters, pagination, ranking, grouping, aggregation, or counts locally. Use `component-local` only for filters over the already fetched component dataset; use `bounded-local` for tiny static enums or confirmed bounded lookups; otherwise use `blocked`.
- Selected mock objects used by drawers, drilldowns, or jumps must exist in filtered data or produce a stale-selection state.

## Template Implementation Rules

For bundled templates:

- One template widget normally represents one top-level parent block. When the parent block contains multiple sub-blocks, implement them inside that widget with local CSS grid/flex or a typed `subBlocks[]` view model; do not create fake page-grid blocks for internal sub-blocks.
- Global/page filters must be declared in `filters[]` and invoked through the selected template's native filter trigger/panel/popover/drawer. Do not generate a standalone filter toolbar, persistent filter bar, or extra filter drawer unless the user explicitly requests template-level redesign.
- Template `filters[]` is for horizontal row-scope constraints. First-level business domain, report theme, management object, subject area, or analysis perspective must be represented through nav/page/route/tab/segment/perspective state when it changes component schema, metric names, table headers, or domain wording.
- Offline/mock filter options and business rows must live in `src/data/dashboard.dataset.json` and be loaded through `src/data/dashboard.loader.ts` plus the data-source registry. Do not create generated TS files for fixture rows, arrays, or payloads.
- `widget.data.params.key` must point to a real dataset in `dashboardData`.
- Use `filters[].source` for data-derived filter options and `filters[].options` for static enums.
- Do not put dynamic perspective-navigation KPIs in `filterData.meta`. Use `businessData`, aggregate rows, or a custom resolver and bind the navigation display to that data chain.
- Use `widget.data.filterFields` when filter ID differs from dataset field.
- Use `widget.data.requiredFilters` for filters that must affect the dataset.
- Use `widget.data.requiredParams` for fixed params that must filter `staticData`.
- Use SQL `WHERE`, source/provider/repository/resolver params, Redis/precompute cache keys, or equivalent source-side scope for high-volume or business-defined global filtering before component data is constructed. `staticData` or component-local filtering is acceptable only for already fetched component datasets, explicitly bounded demo datasets, tiny enums, or lookup options.
- Use `widget.data.ignoredFilters` only for intentionally ignored global filters whose component scope is invariant. Do not use it to bypass missing mock grain, mismatched field names, or unimplemented resolver behavior; fix the data with `filterFields`, `requiredFilters`, `requiredParams`, API params, or a custom resolver.
- Use `widget.filterScope` plus `filters[].scope` for local filter behavior.
- Business widgets should emit `dashboard-action` and central action config should handle the event.
- `navigateUrl` should include active filters by default.

## Custom Implementation Rules

For custom Vue or non-template pages:

- Keep `activeFilters` as a single runtime object.
- Keep a `filterMap` table from filter IDs to data fields, API query params, permission scopes, and affected components.
- Keep exports, jumps, fullscreen views, drawers, and modals reading from the same filtered context as visible components.
- Use a shared action dispatcher for drilldowns, drawers, modals, jumps, exports, refresh, and fullscreen actions.
- Store selection and drill path in one place so filter changes can invalidate them consistently.
- Keep raw mock rows outside visual components so KPI cards, charts, tables, drawers, and exports can use the same source.

## Prototype Technology Mapping

- Use TypeScript + Vue 3 single-file components with Composition API unless the existing project uses another stack.
- Use Element Plus for standard UI controls in Vue report prototypes: filter forms, selects, tree selects, cascaders, date pickers, inputs, buttons, tabs, tags, popovers, tooltips, dialogs, drawers, pagination, and simple operation/detail tables.
- Detail Table mappings with `componentType: 'table'` and `visualType: 'table'` must carry row grain, primary key, default sort, column metadata, visible-column priority, search/sort/pagination/export scope, row detail/action payload, local-filter behavior, and state handling. Use Element Plus/project table for ordinary row-level details; use S2 only when the table is a pivot, cross table, wide metric matrix, frozen-header analytical table, or dense comparison grid.
- Use ECharts for standard visual charts: KPI trend cards, line, bar, area, Combo through data-driven `bar` + `line`/`markLine` series on one shared x-axis, scatter, Gauge through `series.type: 'gauge'`, parallel coordinates through `parallelAxis` plus `series.type: 'parallel'`, heatmap, map, Sankey through `series.type: 'sankey'` with node/link `source`/`target`/`value`, path/user/process path when implemented through ECharts sankey/graph/custom series, treemap/rectangular tree map through `series.type: 'treemap'`, sunburst through `series.type: 'sunburst'`, tree/hierarchical tree through `series.type: 'tree'` or a declared data-driven hierarchy component, relation/network graph, waterfall, funnel, mixed chart.
- Gauge implementation must use ECharts `series.type: 'gauge'` with declared `min`, `max`, `startAngle`, `endAngle`, `radius`, `center`, `progress`/`axisLine`, `detail`, `data`, target/threshold encoding when present, and tooltip evidence. Do not map a standard Gauge to hand-authored SVG/CSS arcs, needles, ticks, or labels while merely importing ECharts.
- Combo implementation must use ECharts `xAxis`, one or two `yAxis` definitions, data-driven `bar` and `line`/`markLine`/reference series, `legend`, `tooltip`, and `axisPointer`. The mapping must carry the paired relationship, axis units, series limits, category-density fallback, and exact tooltip evidence; do not map unrelated metrics into a dual-axis Combo.
- Funnel implementation may be ECharts `series.type: 'funnel'` for traditional trapezoids or ECharts horizontal `bar` series for the report-default bar funnel. In both cases the mapping must carry ordered stage rows, value/unit, conversion/drop formulas, tooltip evidence, and target/comparison semantics instead of hand-drawn decorative bars or trapezoids.
- When the binding matrix maps a component to ECharts, implementation must use an actual ECharts instance or approved project wrapper with data-driven `option`/`series`. Do not mark a standard chart as ECharts if the intended implementation is hand-authored SVG/HTML/CSS/canvas. Use `customDiagram`, `svgIcon`, or another explicit non-standard component type only when the visual is genuinely not an ECharts chart.
- Use AntV S2 through `@antv/s2` and `@antv/s2-vue` for analytical tables: pivot tables, cross tables, wide metric matrices, frozen-header tables, drillable comparison grids, and dense financial/operation tables. Treat those packages as on-demand dependencies; do not add or install them when the mapped components only use charts, KPI cards, simple Element Plus tables, lists, or text summaries.
- Use regular Vue/HTML tables only when Element Plus and S2 are both unavailable or the existing project stack explicitly forbids them.
- Keep chart/table widgets typed, data-driven, and isolated from shell actions.
- Keep mock/static data in JSON data files or data-source resolvers, not embedded in ECharts/S2 setup code or generated TS fixture modules. In bundled templates, use `src/data/dashboard.dataset.json`.
- Visible Chinese UI uses `%` for rate, completion, variance-rate, YoY, MoM, and change labels. Avoid `pt`, `p.p.`, and `percentage point` labels unless explicitly requested.
- Change-rate and variance-rate indicators use positive-red-up and negative-green-down semantics: positive value = red text plus upward SVG/icon; negative value = green text plus downward SVG/icon; zero = neutral.

## Validation Requirements

For each primary filter, include at least one scenario proving:

- KPI cards, charts, tables, lists, drawers, and exports change consistently.
- Filtered detail rows reconcile to filtered KPI totals when additive.
- Non-additive metrics recalculate from raw numerator/denominator fields.
- Selected objects remain in scope or show a stale-selection state.

For each `perspective-switch`, include at least one default and one non-default scenario proving:

- Metric names and title/summary wording match the selected domain.
- Component collection and table dimensions/headers change when `componentSchemaImpact` says they should.
- Domain-specific specialty metrics and risk focus appear for the selected domain.
- Formula/口径 differences are visible in labels, field mapping, or validation notes instead of only changing numeric values.
- Navigation percentages, rankings, and status lights reconcile to the same `sourceDataset`/field/formula chain used by overview KPIs, journey cards, and chart summaries.

A runnable prototype should fail validation when:

- A primary filter has no explicit component binding.
- A schema-changing control is modeled only as a normal filter or lacks `componentSchemaImpact`.
- A navigation percentage, ranking, or status light lacks `sourceDataset`, `field/formula`, `grain`, `affectedFilters`, or `periodBehavior`.
- A dynamic navigation KPI is stored in filter option `meta` or `filterData.meta` without being explicitly static display copy.
- A non-default perspective only changes numeric values while metric names, titles, table dimensions, component set, specialty metrics, and口径 stay incorrectly default.
- A primary filter only narrows data after full dataset/component construction.
- A primary filter changes only UI selected state while affected component data stays identical. Treat `ignoredFilters` or missing `filterFields` as binding gaps after data completeness is proven; treat single-snapshot mock data, missing non-default rows, or missing resolver/API branches as data-completeness gaps first.
- A clickable element has no emitted event or configured action.
- A multi-period filter is backed by single-period data.
- A first-screen component has no dataset, static policy, or external runtime contract.
- A component mapped as an ECharts standard chart only imports `echarts` but renders chart marks through hand-authored SVG/HTML/CSS/canvas.
