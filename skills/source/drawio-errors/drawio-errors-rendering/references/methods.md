# Draw.io Rendering Errors — Diagnostic Methods Reference

> Systematic methods for diagnosing and fixing Draw.io rendering issues.
> Each method targets a specific category of visual defect.

---

## 1. Visibility Audit Method

Use this method when shapes exist in XML but are not visible on the canvas.

### Steps

1. Locate the `mxCell` by its `id` in the XML
2. Read the `style` attribute and extract these properties:
   - `fillColor` — MUST NOT be `none` unless `strokeColor` is visible
   - `strokeColor` — MUST NOT be `none` unless `fillColor` is visible
   - `opacity` — MUST be between 1 and 100 (default: 100)
   - `fillOpacity` — MUST be > 0 if `strokeOpacity` is also 0
   - `strokeOpacity` — MUST be > 0 if `fillOpacity` is also 0
3. Read the `<mxGeometry>` element:
   - `width` MUST be > 0
   - `height` MUST be > 0
   - `x` and `y` MUST be within the visible canvas range (typically 0–5000)
4. Check the `parent` attribute:
   - If parent points to a container, verify that container is expanded
   - If parent is `1` (root layer), the shape is at the top level

### Properties That Cause Invisibility

| Property | Invisible When | Default |
|----------|---------------|---------|
| `fillColor` | `none` (combined with `strokeColor=none`) | `default` (theme white) |
| `strokeColor` | `none` (combined with `fillColor=none`) | `default` (theme black) |
| `opacity` | `0` | `100` |
| `fillOpacity` | `0` (combined with `strokeOpacity=0`) | `100` |
| `strokeOpacity` | `0` (combined with `fillOpacity=0`) | `100` |
| `noLabel` | `1` on a text-only shape | `0` |
| `textOpacity` | `0` (for text-only shapes) | `100` |

---

## 2. Perimeter Verification Method

Use this method when edges connect at wrong positions on shapes.

### Steps

1. Identify the target shape's base type from its style string (leading identifier or `shape=`)
2. Look up the REQUIRED perimeter from the mapping table
3. Compare with the actual `perimeter=` value in the style
4. If missing or wrong, set the correct perimeter value

### Perimeter Mapping Table

| Shape Identifier | Required Perimeter |
|-----------------|-------------------|
| (default/rectangle) | `rectanglePerimeter` (can omit — it is the default) |
| `rounded=1` | `rectanglePerimeter` |
| `ellipse` | `ellipsePerimeter` |
| `doubleEllipse` | `ellipsePerimeter` |
| `rhombus` | `rhombusPerimeter` |
| `triangle` | `trianglePerimeter` |
| `hexagon` | `hexagonPerimeter` |
| `shape=cloud` | `ellipsePerimeter` |
| `shape=cylinder` / `shape=cylinder3` | `rectanglePerimeter` |
| `swimlane` | `rectanglePerimeter` |
| `shape=parallelogram` | `rectanglePerimeter` |
| `shape=trapezoid` | `rectanglePerimeter` |
| `shape=step` | `rectanglePerimeter` |

### What Happens With Wrong Perimeters

- **Ellipse + rectanglePerimeter**: Edge endpoints land on the bounding box boundary instead of the curved ellipse boundary. Visible gaps appear between edge endpoints and the ellipse outline.
- **Rectangle + ellipsePerimeter**: Edge endpoints are calculated for a curved boundary, landing inside or outside the rectangle corners.
- **Rhombus + rectanglePerimeter**: Edge endpoints target the bounding box instead of the diamond's angled sides.

---

## 3. Label Rendering Audit Method

Use this method when labels are truncated, missing, or overlapping.

### Steps

1. Check for mandatory properties:
   - `html=1` MUST be present — without it, HTML formatting is lost
   - `whiteSpace=wrap` MUST be present — without it, text does not wrap
2. Check overflow behavior:
   - `overflow=hidden` — text is clipped at shape boundary
   - `overflow=visible` — text extends beyond shape (default for edges)
   - `overflow=fill` — label fills entire shape
   - `overflow=width` — fixed width, variable height
3. Check label dimensions:
   - Calculate available width: `shape_width - (spacing + spacingLeft) - (spacing + spacingRight)`
   - Calculate available height: `shape_height - (spacing + spacingTop) - (spacing + spacingBottom)`
   - If text exceeds available space, either resize shape or reduce fontSize
4. Check label positioning:
   - If `labelPosition` is `left` or `right`, verify `align` is the OPPOSITE value
   - If `verticalLabelPosition` is `top` or `bottom`, verify `verticalAlign` is the OPPOSITE value

### Available Label Space Formula

```
available_width  = shape_width  - 2 * spacing - spacingLeft - spacingRight
available_height = shape_height - 2 * spacing - spacingTop  - spacingBottom
```

Default `spacing` is `2`. Default individual spacing values are `0`.

---

## 4. Container Layout Audit Method

Use this method when container children are misplaced or clipped.

### Steps

1. Verify the parent has `container=1` in its style
2. Verify every child `mxCell` has `parent="<container_id>"`
3. Check child coordinates are RELATIVE to the container:
   - Child x MUST be >= 0
   - Child y MUST be >= `startSize` (for swimlanes, default 23)
   - Child x + child width MUST be <= container width
   - Child y + child height MUST be <= container height
4. If using `childLayout=stackLayout`:
   - Check `horizontalStack` (0=vertical, 1=horizontal)
   - Check `spacing` between stacked children
   - Check `resizeLast` for filling remaining space

### Container Bounds Validation

```
For each child in container:
  ASSERT child.x >= 0
  ASSERT child.y >= container.startSize (or 0 if no header)
  ASSERT child.x + child.width <= container.width
  ASSERT child.y + child.height <= container.height
```

If any assertion fails, either reposition the child or resize the container.

---

## 5. Edge Routing Audit Method

Use this method when edges take unexpected paths.

### Steps

1. Check `edgeStyle` property:
   - `orthogonalEdgeStyle` — right-angle routing (default for most diagrams)
   - `elbowEdgeStyle` — single elbow connector
   - `entityRelationEdgeStyle` — ER diagram routing
   - `isometricEdgeStyle` — isometric projection routing
   - Empty or absent — straight line connection
2. Check for stale waypoints:
   - Look for `<Array as="points">` inside the edge's `<mxGeometry>`
   - Waypoints are absolute coordinates that may be outdated after shapes moved
   - Remove the `<Array>` element to let the router recalculate
3. Check connection points:
   - `exitX`, `exitY` — departure point on source (0–1 range)
   - `entryX`, `entryY` — arrival point on target (0–1 range)
   - `exitDx`, `exitDy` — pixel offset from exit point
   - `entryDx`, `entryDy` — pixel offset from entry point
4. Check `relative="1"` on edge geometry — MUST be present

---

## 6. Export Rendering Audit Method

Use this method when diagrams look correct in the editor but wrong in exports.

### Steps

1. Check font compatibility:
   - SVG/PNG exports may not embed custom fonts
   - Use web-safe fonts: `Helvetica`, `Arial`, `Verdana`, `Times New Roman`, `Courier New`
2. Check shadow configuration:
   - `shadow="1"` MUST be on the `<mxGraphModel>` element
   - Individual cells with `shadow=1` are ignored without the model-level attribute
3. Check sketch mode:
   - Shapes with `sketch=1` use rough.js, which introduces randomness
   - Each export renders slightly different line paths — this is expected behavior
4. Check diagram bounds:
   - Shapes extending beyond the canvas bounds will be clipped in exports
   - Add margin/padding in export settings
5. For PNG exports:
   - Default resolution may be 1x — increase to 2x or 3x for high-DPI displays
   - Transparent background is the default — set a background color if needed

---

## 7. Boolean Property Verification Method

Use this method when style properties appear to have no effect.

### Steps

1. Search the style string for `true` or `false` values
2. Replace ALL `true` with `1` and ALL `false` with `0`
3. Draw.io ALWAYS uses `0`/`1` for booleans — NEVER `true`/`false`
4. Properties using `true`/`false` are silently ignored

### Common Boolean Properties

| Property | Off | On |
|----------|-----|-----|
| `rounded` | `0` | `1` |
| `dashed` | `0` | `1` |
| `shadow` | `0` | `1` |
| `html` | `0` | `1` |
| `container` | `0` | `1` |
| `collapsible` | `0` | `1` |
| `sketch` | `0` | `1` |
| `noLabel` | `0` | `1` |
| `fixDash` | `0` | `1` |
