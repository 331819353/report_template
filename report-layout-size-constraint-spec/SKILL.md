---
name: report-layout-size-constraint-spec
description: "用于报表页面区块尺寸、容器尺寸、高度预算、首屏层级、8*N网格、图表/表格容器高度、固定高度卡片、Composite Panel/Micro Dashboard Card多组件最小尺寸、状态反馈几何、裁切、溢出、重叠和响应式尺寸约束设计/评审。用户提到区块尺寸、容器尺寸、卡片高度、首屏放不下、图表太挤、表格太矮、多组件组合挤压、1920x1080、1280x768、高度预算、scrollHeight/clientHeight、overflow、裁切、重叠、响应式布局时触发；不负责组件内部图表细节。"
---

# Report Layout Size Constraint Spec

## Positioning

Use this as the direct front door for page/block sizing and viewport fit. It promotes the layout sizing reference that was previously nested under `$report-visual-layout-design`.

Use `$report-visual-layout-design` for full page layout decisions; use this skill for block size budgets, fixed-height risk, parent/child container fit, and responsive overflow checks.

## Reference Map

| Need | Read |
| --- | --- |
| Preflight understanding before implementation/repair/acceptance | `$quality-gate-validation` `references/preflight-understanding-gate.md` |
| Size source map | `references/01-size-reference-map.md` |
| Parent layout references | `$report-visual-layout-design` references: `block-size-constraints.md`, `grid-containers.md`, `block-composition.md`, `layout-acceptance-gates.md` |
| Component minimums for Composite Panel, Micro Dashboard Card, state feedback, dense tables/charts | `$report-visual-layout-design` `references/block-size-constraints-02-component-requirements.md` |

## Anti-Laziness Gate

For non-trivial work, apply `$quality-gate-validation` `references/anti-laziness-execution-gate.md` before final output, handoff, or readiness. Do not mark the result ready while `LAZY-*` findings remain open, when available local evidence was not inspected, when owning skills were skipped, or when proof is limited to generic statements such as "checked", "optimized", "looks good", or "implemented".

## Workflow

1. Run the Preflight understanding gate for implementation, repair, or acceptance work; name affected blocks, child component families, viewport targets, hard constraints, missing evidence, and start decision.
2. Identify viewport targets, grid system, parent blocks, child components, fixed-height surfaces, and density.
3. Calculate usable width/height for the block before deciding chart/table/KPI composition.
4. Check row count, header/filter/toolbar/legend/footer/state masks, child-component minimums, gaps, padding, line-height, and scroll areas.
5. Decide whether to enlarge, split, move to drawer/fullscreen, paginate, scroll, or reduce component density.
6. Require DOM overflow checks when code or URL exists: fixed-height cards, summary/ranking blocks, KPI tiles, nav items, Composite Panels, table bodies, and compact controls must pass `scrollHeight <= clientHeight + 2` and `scrollWidth <= clientWidth + 2`, or declare an intentional visible scroll, expand/collapse, drawer/fullscreen, pagination, or split strategy.
7. Inspect `overflow: hidden` on parent/root containers. It is allowed for decorative masks or known non-content regions, but fails acceptance when it hides decision-critical text, ranking rows, controls, legends, values, or table content without a declared disclosure path.

## Required Output

- Preflight understanding result when the work is implementation/repair/acceptance, plus target viewport and block/container size budget.
- Fit decision for each dense block: fit, enlarge, split, scroll, drawer/fullscreen, or blocked.
- Overflow/cropping risks and required DOM/runtime checks, including selectors, target viewports, `scrollHeight/clientHeight`, `scrollWidth/clientWidth`, overflow CSS, and pass/fail result when code or URL exists.
- Handoff to component/table/chart skills when internal fit rules are needed.

## Quality Gate

- Do not approve a block only because it looks acceptable at one viewport.
- Do not approve or edit a layout before identifying affected child component families and their owning chart/table/filter/placement skills.
- Fixed-height KPI/card/navigation/table areas need explicit padding, line-height, gap, and overflow checks.
- Fixed-height summary/ranking/composite cards cannot pass with hidden overflow. They must prove content budget, pass DOM overflow checks within the `+2px` tolerance, or expose usable visible scroll, expand/collapse, pagination, drawer/fullscreen, or split behavior.
- Dense charts, tables, Micro Dashboard Cards, Composite Panels, and state feedback surfaces need enough reserved area for labels, axes, legends, pagination, child minimums, and states.
