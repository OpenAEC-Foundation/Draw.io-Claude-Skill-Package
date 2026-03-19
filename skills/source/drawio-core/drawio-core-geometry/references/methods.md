# Geometry Methods and Attributes Reference

## mxGeometry Element

The `<mxGeometry>` element is ALWAYS a child of `<mxCell>` and MUST have `as="geometry"`.

### Vertex Geometry Attributes

| Attribute | Type | Default | Required | Description |
|-----------|------|---------|----------|-------------|
| `x` | number | `0` | NO (defaults to 0) | Horizontal position of top-left corner in pixels. Absolute if parent is layer; relative if parent is container. |
| `y` | number | `0` | NO (defaults to 0) | Vertical position of top-left corner in pixels. Positive = downward. |
| `width` | number | `0` | YES | Shape width in pixels. MUST be > 0 for visible shapes. |
| `height` | number | `0` | YES | Shape height in pixels. MUST be > 0 for visible shapes. |
| `as` | string | — | YES | ALWAYS set to `"geometry"`. Binds the element to its parent mxCell. |

### Edge Geometry Attributes

| Attribute | Type | Default | Required | Description |
|-----------|------|---------|----------|-------------|
| `relative` | `"1"` | — | YES | MUST be `"1"` for edges. Switches x/y to label positioning mode. |
| `x` | number | `0` | NO | Label position along edge path: `-1` (source) to `1` (target), `0` = midpoint. |
| `y` | number | `0` | NO | Label perpendicular offset in pixels. Positive = below/right of edge. |
| `as` | string | — | YES | ALWAYS set to `"geometry"`. |

### Shared Child Elements

| Element | `as` Attribute | Parent Context | Description |
|---------|---------------|----------------|-------------|
| `<mxPoint>` | `"offset"` | Vertex or Edge | Additional pixel offset. For edges: shifts label after relative positioning. For vertices: shifts label from default position. |
| `<mxPoint>` | `"sourcePoint"` | Edge only | Start coordinate for unconnected edge (no `source` attribute). Absolute canvas coordinates. |
| `<mxPoint>` | `"targetPoint"` | Edge only | End coordinate for unconnected edge (no `target` attribute). Absolute canvas coordinates. |
| `<Array>` | `"points"` | Edge only | Ordered list of waypoint `<mxPoint>` elements. Absolute canvas coordinates. |
| `<mxRectangle>` | `"alternateBounds"` | Collapsible vertex | Dimensions used when `collapsed="1"`. Swaps with main geometry on collapse/expand. |

## mxPoint Element

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| `x` | number | YES | Horizontal coordinate in pixels |
| `y` | number | YES | Vertical coordinate in pixels |
| `as` | string | Context-dependent | Binding identifier: `"offset"`, `"sourcePoint"`, `"targetPoint"`, or omitted inside `<Array>` |

## mxRectangle Element (alternateBounds)

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| `x` | number | YES | Horizontal position (MUST match parent geometry x) |
| `y` | number | YES | Vertical position (MUST match parent geometry y) |
| `width` | number | YES | Collapsed width in pixels |
| `height` | number | YES | Collapsed height in pixels |
| `as` | string | YES | ALWAYS `"alternateBounds"` |

## Connection Point Style Properties

These are set on the **edge's style string**, NOT on mxGeometry.

### Exit Point (Source Side)

| Property | Type | Range | Description |
|----------|------|-------|-------------|
| `exitX` | float | 0.0 - 1.0 | Relative X on source shape. 0 = left edge, 0.5 = center, 1 = right edge. |
| `exitY` | float | 0.0 - 1.0 | Relative Y on source shape. 0 = top edge, 0.5 = center, 1 = bottom edge. |
| `exitDx` | number | any | Absolute X pixel offset from exit point. |
| `exitDy` | number | any | Absolute Y pixel offset from exit point. |
| `exitPerimeter` | `0` or `1` | — | `1` (default): project point onto shape perimeter. `0`: use exact relative position. |

### Entry Point (Target Side)

| Property | Type | Range | Description |
|----------|------|-------|-------------|
| `entryX` | float | 0.0 - 1.0 | Relative X on target shape. 0 = left edge, 0.5 = center, 1 = right edge. |
| `entryY` | float | 0.0 - 1.0 | Relative Y on target shape. 0 = top edge, 0.5 = center, 1 = bottom edge. |
| `entryDx` | number | any | Absolute X pixel offset from entry point. |
| `entryDy` | number | any | Absolute Y pixel offset from entry point. |
| `entryPerimeter` | `0` or `1` | — | `1` (default): project point onto shape perimeter. `0`: use exact relative position. |

### Connection Point Reference Grid

```
Position        exitX/entryX    exitY/entryY
──────────────  ────────────    ────────────
Top-left        0               0
Top-center      0.5             0
Top-right       1               0
Middle-left     0               0.5
Center          0.5             0.5
Middle-right    1               0.5
Bottom-left     0               1
Bottom-center   0.5             1
Bottom-right    1               1
```

Values between grid points are valid (e.g., `exitX=0.25` = quarter from left).

## Label Positioning Style Properties

### Vertex Labels

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelPosition` | `left`, `center`, `right` | `center` | Horizontal label position relative to shape bounds |
| `verticalLabelPosition` | `top`, `middle`, `bottom` | `middle` | Vertical label position relative to shape bounds |
| `align` | `left`, `center`, `right` | `center` | Text alignment within the label bounding box |
| `verticalAlign` | `top`, `middle`, `bottom` | `middle` | Vertical text alignment within the label bounding box |
| `spacing` | number | `2` | Global label padding in pixels (all sides) |
| `spacingTop` | number | `0` | Additional top padding |
| `spacingBottom` | number | `0` | Additional bottom padding |
| `spacingLeft` | number | `0` | Additional left padding |
| `spacingRight` | number | `0` | Additional right padding |
| `labelWidth` | number | — | Fixed label width. When set, label wraps at this width instead of shape width. |

### Coordination Rule

When `labelPosition` is NOT `center`:

| labelPosition | Required align |
|---------------|---------------|
| `left` | `right` |
| `right` | `left` |

When `verticalLabelPosition` is NOT `middle`:

| verticalLabelPosition | Required verticalAlign |
|-----------------------|-----------------------|
| `top` | `bottom` |
| `bottom` | `top` |

## Perimeter Style Properties

| Shape Style | Required Perimeter Style |
|-------------|------------------------|
| `shape=ellipse` | `perimeter=ellipsePerimeter` |
| `shape=rhombus` | `perimeter=rhombusPerimeter` |
| `shape=triangle` | `perimeter=trianglePerimeter` |
| `shape=hexagon` | `perimeter=hexagonPerimeter2` |
| `shape=parallelogram` | `perimeter=parallelogramPerimeter` |
| `shape=trapezoid` | `perimeter=trapezoidPerimeter` |
| Rectangle / rounded rectangle | Default perimeter (no explicit value needed) |

## mxGraphModel Canvas Attributes (Geometry-Related)

| Attribute | Default | Description |
|-----------|---------|-------------|
| `dx` | `0` | Horizontal scroll offset |
| `dy` | `0` | Vertical scroll offset |
| `grid` | `1` | Show grid (`1`) or hide (`0`) |
| `gridSize` | `10` | Grid spacing in pixels |
| `guides` | `1` | Enable snap guides |
| `pageWidth` | `1169` | Canvas page width (A4 landscape at 96 DPI) |
| `pageHeight` | `827` | Canvas page height |
| `pageScale` | `1` | Page zoom scale factor |
