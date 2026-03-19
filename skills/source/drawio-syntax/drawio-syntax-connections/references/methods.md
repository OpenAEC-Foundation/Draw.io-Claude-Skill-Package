# Methods Reference: Draw.io Syntax Connections

Complete property reference for edges, connections, and routing in mxGraph XML.

---

## 1. Edge Cell Attributes

Attributes set directly on the `<mxCell>` element for edge cells.

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `id` | String | ALWAYS | — | Unique identifier. MUST be unique across the entire file. |
| `value` | String | No | `""` | Label text. XML-escape HTML content. |
| `style` | String | ALWAYS | — | Semicolon-separated `key=value;` pairs. |
| `edge` | `"1"` | ALWAYS | — | Marks this cell as an edge. NEVER omit. |
| `source` | String | ALWAYS | — | ID of the source vertex cell. |
| `target` | String | ALWAYS | — | ID of the target vertex cell. |
| `parent` | String | ALWAYS | `"1"` | Parent cell ID. Use `"1"` for default layer. |
| `connectable` | `"0"` / `"1"` | No | `"1"` | Set to `"0"` on edge label children. |

---

## 2. Edge Style Properties

Properties set inside the `style` attribute string of an edge cell.

### 2.1 Routing Algorithm

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `edgeStyle` | `orthogonalEdgeStyle`, `elbowEdgeStyle`, `entityRelationEdgeStyle`, `segmentEdgeStyle`, `sideToSideEdgeStyle`, `topToBottomEdgeStyle`, `loopEdgeStyle`, `isometricEdgeStyle` | *(none — straight line)* | Routing algorithm for the edge path. |
| `noEdgeStyle` | `0`, `1` | `0` | When `1`, disables all edge style routing. Edge draws as straight line. |

### 2.2 Path Shape Modifiers

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `curved` | `0`, `1` | `0` | Smooth Bezier-like curves instead of sharp corners. |
| `rounded` | `0`, `1` | `1` | Round the corners of orthogonal edge bends. |
| `elbow` | `horizontal`, `vertical` | — | Preferred bend direction for `elbowEdgeStyle`. |
| `orthogonalLoop` | `0`, `1` | `1` | Routing mode for self-referencing loop edges. |

### 2.3 Connection Point Properties (Exit — Source Side)

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `exitX` | `0.0` to `1.0` | — | Relative X coordinate on source shape. `0` = left, `1` = right. |
| `exitY` | `0.0` to `1.0` | — | Relative Y coordinate on source shape. `0` = top, `1` = bottom. |
| `exitDx` | number | — | Absolute X pixel offset from exit point. ALWAYS set to `0` when using exitX/Y. |
| `exitDy` | number | — | Absolute Y pixel offset from exit point. ALWAYS set to `0` when using exitX/Y. |
| `exitPerimeter` | `0`, `1` | `1` | When `1`, project exit point onto shape perimeter. |

### 2.4 Connection Point Properties (Entry — Target Side)

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `entryX` | `0.0` to `1.0` | — | Relative X coordinate on target shape. `0` = left, `1` = right. |
| `entryY` | `0.0` to `1.0` | — | Relative Y coordinate on target shape. `0` = top, `1` = bottom. |
| `entryDx` | number | — | Absolute X pixel offset from entry point. ALWAYS set to `0` when using entryX/Y. |
| `entryDy` | number | — | Absolute Y pixel offset from entry point. ALWAYS set to `0` when using entryX/Y. |
| `entryPerimeter` | `0`, `1` | `1` | When `1`, project entry point onto shape perimeter. |

### 2.5 Spacing and Jetty

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jettySize` | `auto`, number | `auto` | Minimum length of first/last segment for orthogonal edges. |
| `sourceJettySize` | number | — | Override jetty size at source end only. |
| `targetJettySize` | number | — | Override jetty size at target end only. |
| `perimeterSpacing` | number | `0` | Gap between edge endpoint and shape perimeter (both ends). |
| `sourcePerimeterSpacing` | number | — | Gap at source end only. |
| `targetPerimeterSpacing` | number | — | Gap at target end only. |

### 2.6 Arrow Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `endArrow` | `none`, `classic`, `classicThin`, `block`, `blockThin`, `open`, `openThin`, `oval`, `diamond`, `diamondThin`, `box`, `halfCircle`, `circle`, `circlePlus`, `cross`, `baseDash`, `doubleBlock`, `dash`, `async`, `openAsync`, `manyOptional` | `classic` | Arrow marker at target end. |
| `startArrow` | *(same values as endArrow)* | `none` | Arrow marker at source end. |
| `endFill` | `0`, `1` | `1` | `1` = solid/filled, `0` = hollow/outline end arrow. |
| `startFill` | `0`, `1` | `1` | `1` = solid/filled, `0` = hollow/outline start arrow. |
| `endSize` | number | — | Size of end arrow marker in pixels. |
| `startSize` | number | — | Size of start arrow marker in pixels. |

### 2.7 Line Style Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `strokeColor` | `#RRGGBB`, `none` | `#000000` | Line color. |
| `strokeWidth` | number | `1` | Line thickness in pixels. |
| `dashed` | `0`, `1` | `0` | `1` = dashed line. |
| `dashPattern` | pattern string | — | Custom dash pattern (e.g., `"8 4"` for 8px dash, 4px gap). |
| `opacity` | `0` to `100` | `100` | Line opacity percentage. |

### 2.8 Line Crossing Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jumpStyle` | `arc`, `gap`, `sharp` | — | Visual style at line crossings. |
| `jumpSize` | number | `6` | Size of crossing marker in pixels. |

---

## 3. Edge Geometry

The `<mxGeometry>` child element of an edge cell. ALWAYS uses `relative="1"`.

### 3.1 Geometry Attributes

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `relative` | `"1"` | ALWAYS | — | MUST be `"1"` for edges. Enables relative label positioning. |
| `x` | `-1` to `1` | No | `0` | Label position along edge path. `-1` = source, `0` = center, `1` = target. |
| `y` | number (pixels) | No | `0` | Label perpendicular offset. Positive = below/right, negative = above/left. |
| `as` | `"geometry"` | ALWAYS | — | Binding attribute. ALWAYS `"geometry"`. |

### 3.2 Child Elements

| Element | `as` Attribute | Description |
|---------|---------------|-------------|
| `<Array as="points">` | `"points"` | Contains `<mxPoint>` waypoints. Absolute canvas coordinates. |
| `<mxPoint as="sourcePoint">` | `"sourcePoint"` | Start coordinate for unconnected edges (no `source` attribute). |
| `<mxPoint as="targetPoint">` | `"targetPoint"` | End coordinate for unconnected edges (no `target` attribute). |
| `<mxPoint as="offset">` | `"offset"` | Additional pixel offset for label positioning. |

---

## 4. Custom Connection Points (Shape Style)

Properties set on the SHAPE (vertex) style to control where edges can attach.

| Property | Values | Description |
|----------|--------|-------------|
| `points` | `[[x,y],...]` | Array of relative connection points. Each `[x,y]` is 0-1 range. |
| `portConstraint` | `eastwest`, `northsouth`, `perimeter`, `fixed` | Restrict allowed connection directions. |
| `sourcePortConstraint` | direction | Constraint on source connections only. |
| `targetPortConstraint` | direction | Constraint on target connections only. |

---

## 5. Edge Label Children

Edge labels created as separate vertex cells that are children of the edge.

| Attribute | Value | Description |
|-----------|-------|-------------|
| `vertex` | `"1"` | ALWAYS set to `"1"` — labels are vertex cells. |
| `connectable` | `"0"` | ALWAYS set to `"0"` — prevents edges connecting to the label. |
| `parent` | edge ID | Set to the ID of the parent edge cell. |
| `style` | `edgeLabel;html=1;...` | Use `edgeLabel` as the base style. |

The label's `<mxGeometry>` uses the same `relative="1"`, `x` (-1 to 1), and `y` (pixels) as the main edge label.
