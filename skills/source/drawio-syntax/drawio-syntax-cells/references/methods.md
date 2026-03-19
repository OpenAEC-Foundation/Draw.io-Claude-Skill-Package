# Methods Reference: Draw.io Syntax Cells

Complete attribute reference for mxCell vertices, edges, object wrappers, HTML labels, groups, containers, and placeholders.

---

## 1. mxCell Attributes (All Types)

These attributes apply to every `<mxCell>` element regardless of type.

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `id` | String | ALWAYS | — | Unique identifier. MUST be unique across the entire file (all pages). Use sequential integers: `"2"`, `"3"`, `"4"`. |
| `parent` | String | ALWAYS (except id="0") | — | ID of the parent cell. `"1"` = default layer. `"0"` = root (for layers only). Container ID for nested cells. |
| `value` | String | No | `null` | Display text. Supports plain text or XML-escaped HTML (when `html=1` is in style). |
| `style` | String | No | `null` | Semicolon-separated `key=value;` pairs. NO spaces around `=` or `;`. |
| `vertex` | `"1"` | Shapes only | Not set | Marks cell as a shape. NEVER combine with `edge="1"`. |
| `edge` | `"1"` | Connectors only | Not set | Marks cell as a connector. NEVER combine with `vertex="1"`. |
| `source` | String | Edges only | `null` | ID of the source vertex. MUST reference an existing vertex cell. |
| `target` | String | Edges only | `null` | ID of the target vertex. MUST reference an existing vertex cell. |
| `connectable` | `"0"` / `"1"` | No | `"1"` | Set to `"0"` to prevent other edges from connecting to this cell. Used on edge labels. |
| `visible` | `"0"` / `"1"` | No | `"1"` | Set to `"0"` to hide the cell. Hidden cells remain in the model. |
| `collapsed` | `"0"` / `"1"` | No | `"0"` | Set to `"1"` to collapse a container/group. Uses `alternateBounds` for collapsed size. |

---

## 2. Vertex-Specific Configuration

### Mandatory Style Properties for Vertices

| Property | Value | Rule |
|----------|-------|------|
| `html` | `1` | ALWAYS include. Enables rich text rendering. |
| `whiteSpace` | `wrap` | ALWAYS include. Enables text wrapping within bounds. |

### Common Vertex Style Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `rounded` | `0` / `1` | `0` | Rounded corners on rectangles |
| `fillColor` | Hex color | `#FFFFFF` | Shape fill color |
| `strokeColor` | Hex color | `#000000` | Shape border color |
| `fontColor` | Hex color | `#000000` | Text color |
| `fontSize` | Number | `12` | Font size in points |
| `fontStyle` | Bitmask | `0` | `1`=bold, `2`=italic, `4`=underline (combine by addition) |
| `opacity` | `0`-`100` | `100` | Cell opacity percentage |
| `container` | `0` / `1` | `0` | Set to `1` to make the vertex a container |
| `collapsible` | `0` / `1` | `1` | Set to `0` to disable collapse toggle on containers |
| `resizable` | `0` / `1` | `1` | Set to `0` to prevent resizing |
| `movable` | `0` / `1` | `1` | Set to `0` to prevent dragging |
| `editable` | `0` / `1` | `1` | Set to `0` to prevent label editing |
| `deletable` | `0` / `1` | `1` | Set to `0` to prevent deletion |

### Shape Types

| Style Value | Shape | Notes |
|-------------|-------|-------|
| (default) | Rectangle | No shape property needed |
| `rounded=1` | Rounded rectangle | Combine with default rectangle |
| `shape=ellipse` | Ellipse/circle | ALWAYS add `perimeter=ellipsePerimeter` |
| `shape=rhombus` | Diamond | ALWAYS add `perimeter=rhombusPerimeter` |
| `shape=triangle` | Triangle | ALWAYS add `perimeter=trianglePerimeter` |
| `shape=hexagon` | Hexagon | ALWAYS add `perimeter=hexagonPerimeter2` |
| `shape=parallelogram` | Parallelogram | ALWAYS add `perimeter=parallelogramPerimeter` |
| `shape=cylinder3` | Cylinder (database) | Default perimeter works |
| `shape=document` | Document | Default perimeter works |
| `shape=cloud` | Cloud | Default perimeter works |
| `shape=image` | Image placeholder | Use with `image=<url>` |

---

## 3. Edge-Specific Configuration

### Edge Style Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `edgeStyle` | See below | Straight | Edge routing algorithm |
| `curved` | `0` / `1` | `0` | Smooth curved routing |
| `orthogonalLoop` | `0` / `1` | `1` | Allow self-referencing orthogonal edges |
| `jettySize` | `"auto"` / Number | `"auto"` | Length of orthogonal stub segments |
| `entryX` | `0`-`1` | Auto | X position on target boundary (0=left, 1=right) |
| `entryY` | `0`-`1` | Auto | Y position on target boundary (0=top, 1=bottom) |
| `exitX` | `0`-`1` | Auto | X position on source boundary |
| `exitY` | `0`-`1` | Auto | Y position on source boundary |
| `entryDx` | Pixels | `0` | Horizontal offset from entry point |
| `entryDy` | Pixels | `0` | Vertical offset from entry point |
| `exitDx` | Pixels | `0` | Horizontal offset from exit point |
| `exitDy` | Pixels | `0` | Vertical offset from exit point |
| `endArrow` | Arrow type | `"classic"` | Arrow at target end |
| `startArrow` | Arrow type | `"none"` | Arrow at source end |
| `endFill` | `0` / `1` | `1` | Fill the end arrow |
| `startFill` | `0` / `1` | `1` | Fill the start arrow |
| `strokeWidth` | Number | `1` | Line thickness in pixels |
| `dashed` | `0` / `1` | `0` | Dashed line |
| `dashPattern` | Pattern | `"3 3"` | Dash-space pattern |

### Edge Style Values

| Value | Description |
|-------|-------------|
| `orthogonalEdgeStyle` | Right-angle routing (most common) |
| `elbowEdgeStyle` | Single-elbow routing |
| `entityRelationEdgeStyle` | ER diagram-style routing |
| `isometricEdgeStyle` | Isometric projection routing |
| (none) | Straight line segments |

### Arrow Types

| Value | Shape |
|-------|-------|
| `classic` | Standard filled arrow |
| `classicThin` | Thin filled arrow |
| `block` | Block arrow |
| `blockThin` | Thin block arrow |
| `open` | Open arrow (unfilled) |
| `openThin` | Thin open arrow |
| `oval` | Circle |
| `diamond` | Diamond |
| `diamondThin` | Thin diamond |
| `dash` | Dash |
| `cross` | Cross |
| `none` | No arrow |
| `ERone` | ER "one" notation |
| `ERmany` | ER "many" notation |
| `ERmandOne` | ER "mandatory one" |
| `ERoneToMany` | ER "one to many" |
| `ERzeroToMany` | ER "zero to many" |
| `ERzeroToOne` | ER "zero to one" |

---

## 4. object / UserObject Attributes

The `<object>` (or `<UserObject>`) wrapper element supports these reserved attributes:

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | String | ALWAYS | Unique identifier (moves from inner mxCell to wrapper) |
| `label` | String | ALWAYS | Display text (replaces mxCell `value` attribute) |
| `tooltip` | String | No | Hover text shown in the Draw.io editor |
| `link` | String | No | URL or internal link (`data:page/id,<pageId>` for page links) |
| `placeholders` | `"1"` | No | Set to `"1"` to enable `%variable%` substitution |
| `tags` | String | No | Comma-separated tags for search and filter |

Any additional attribute becomes a custom property visible in Edit Data (Ctrl+M).

### Inner mxCell Rules When Wrapped

| Attribute | On `<object>` | On inner `<mxCell>` |
|-----------|---------------|---------------------|
| `id` | ALWAYS | NEVER |
| `label` / `value` | `label` on object | NEVER `value` on mxCell |
| `vertex` / `edge` | NEVER | ALWAYS |
| `parent` | NEVER | ALWAYS |
| `source` / `target` | NEVER | ALWAYS (edges) |
| `style` | NEVER | ALWAYS |

---

## 5. Placeholder Syntax

### Predefined Placeholders (No Custom Properties Needed)

| Placeholder | Value |
|-------------|-------|
| `%id%` | Cell ID |
| `%width%` | Cell width (pixels) |
| `%height%` | Cell height (pixels) |
| `%length%` | Edge length (edges only) |
| `%date%` | Current date |
| `%time%` | Current time |
| `%timestamp%` | Full timestamp |
| `%date{format}%` | Formatted date (Java SimpleDateFormat) |
| `%pagenumber%` | Current page number |
| `%pagecount%` | Total page count |
| `%page%` | Current page name |
| `%filename%` | File name |

Unit conversion: `%width:mm%`, `%height:in%`, `%width:m%` convert pixels to physical units.

### Custom Placeholders

Custom placeholders resolve from attributes on the `<object>` wrapper or ancestor elements:

```xml
<object id="2" label="%name% (%role%)" placeholders="1"
        name="Alice" role="Developer">
```

### Escape Sequence

`%%` produces a literal `%` character.

---

## 6. Container and Group Style Properties

| Property | Value | Description |
|----------|-------|-------------|
| `container` | `1` | Makes a vertex act as a container for child cells |
| `collapsible` | `0` / `1` | Whether the container shows a collapse toggle (default: `1`) |
| `swimlane` | (as shape) | Collapsible container with a title bar |
| `group` | (as full style) | Invisible bounding box — `style="group"` |
| `childLayout` | `stackLayout` | Automatic vertical stacking of children |
| `horizontalStack` | `0` / `1` | Stack direction: `0` = vertical, `1` = horizontal |
| `stackFill` | `0` / `1` | Whether children fill the container width/height |
| `stackSpacing` | Number | Spacing between stacked children (pixels) |
| `resizeParent` | `0` / `1` | Whether the container resizes to fit children |

---

## 7. mxGeometry Child Elements

Elements that can appear inside `<mxGeometry>`:

| Element | `as` Value | Used In | Purpose |
|---------|-----------|---------|---------|
| `<mxPoint>` | `"sourcePoint"` | Edges | Starting point for floating edges |
| `<mxPoint>` | `"targetPoint"` | Edges | Ending point for floating edges |
| `<mxPoint>` | `"offset"` | Both | Additional pixel offset for label positioning |
| `<Array>` | `"points"` | Edges | Intermediate waypoints (`<mxPoint>` children) |
| `<mxRectangle>` | `"alternateBounds"` | Vertices | Collapsed size for collapsible containers |
