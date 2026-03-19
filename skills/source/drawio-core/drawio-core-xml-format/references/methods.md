# Methods Reference: Draw.io Core XML Format

Complete attribute and property reference for the mxGraph XML format.

---

## 1. mxfile Attributes

The outermost container element. Optional for single-page diagrams (Draw.io auto-wraps).

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `host` | String | No | `"app.diagrams.net"` | Application that created the file |
| `modified` | ISO 8601 | No | Current time | Last modification timestamp |
| `agent` | String | No | Browser UA | User-agent of creating application |
| `etag` | String | No | Random | Change tracking identifier |
| `version` | String | No | Current | Draw.io editor version (e.g., `"24.0.0"`) |
| `type` | String | No | `"device"` | Storage backend: `"device"`, `"google"`, `"github"`, `"gitlab"`, `"dropbox"`, `"onedrive"`, `"browser"` |
| `compressed` | `"true"`/`"false"` | No | `"true"` | Whether diagram content uses DEFLATE+Base64. ALWAYS set to `"false"` for AI generation. |
| `vars` | JSON String | No | None | File-level variables as JSON: `'{"key":"value"}'` |

---

## 2. diagram Attributes

Each `<diagram>` represents one page. Contained within `<mxfile>`.

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `id` | String | Yes | Auto-generated | Unique page identifier |
| `name` | String | No | `"Page-1"` | Display name on the tab bar |

Content is EITHER an `<mxGraphModel>` child element (uncompressed) OR a Base64-encoded DEFLATE string (compressed). AI MUST ALWAYS use the uncompressed child element form.

---

## 3. mxGraphModel Attributes

Canvas and editor configuration. The only required child is `<root>`.

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `dx` | Number | `0` | Horizontal scroll offset |
| `dy` | Number | `0` | Vertical scroll offset |
| `grid` | `0`/`1` | `1` | Show grid |
| `gridSize` | Number | `10` | Grid spacing in pixels |
| `guides` | `0`/`1` | `1` | Enable snap guides |
| `tooltips` | `0`/`1` | `1` | Show tooltips on hover |
| `connect` | `0`/`1` | `1` | Enable connection handling |
| `arrows` | `0`/`1` | `1` | Show connection arrows |
| `fold` | `0`/`1` | `1` | Enable group folding/collapsing |
| `page` | `0`/`1` | `1` | Show page boundary |
| `pageScale` | Number | `1` | Page zoom scale factor |
| `pageWidth` | Number | `1169` | Page width in pixels (A4 landscape at 96 DPI) |
| `pageHeight` | Number | `827` | Page height in pixels |
| `math` | `0`/`1` | `0` | Enable LaTeX math rendering |
| `shadow` | `0`/`1` | `0` | Enable global shadow on all cells |
| `background` | Color | `none` | Canvas background color (e.g., `"#FFFFFF"`) |

---

## 4. root Element

Simple container for all `<mxCell>` elements. Has NO attributes.

MUST contain at minimum:
```xml
<mxCell id="0" />
<mxCell id="1" parent="0" />
```

---

## 5. mxCell Attributes

The universal building block. Every visual element is an mxCell.

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `id` | String | REQUIRED | Unique identifier. MUST be unique across the entire file (all pages). |
| `parent` | String | REQUIRED (except id="0") | ID of parent cell. `"1"` for default layer content, `"0"` for layers. |
| `value` | String | `""` | Display text. Supports HTML when `html=1` is in style. MUST be XML-escaped. |
| `style` | String | `""` | Semicolon-separated `key=value;` pairs. See Style Properties below. |
| `vertex` | `"1"` | Not set | Marks cell as a shape. Mutually exclusive with `edge`. |
| `edge` | `"1"` | Not set | Marks cell as a connector. Mutually exclusive with `vertex`. |
| `source` | String | Not set | ID of source vertex (edges ONLY). MUST reference an existing vertex. |
| `target` | String | Not set | ID of target vertex (edges ONLY). MUST reference an existing vertex. |
| `connectable` | `"0"`/`"1"` | `"1"` | Whether edges can connect to this cell. Set `"0"` on edge labels. |
| `visible` | `"0"`/`"1"` | `"1"` | Whether the cell renders. Hidden cells exist in the model but are not drawn. |
| `collapsed` | `"0"`/`"1"` | `"0"` | Whether a container/group shows in collapsed state. Uses `alternateBounds`. |

### ID Generation Rules

- `id="0"` is ALWAYS the root container cell.
- `id="1"` is ALWAYS the default layer cell.
- Content cells: use sequential integers `"2"`, `"3"`, `"4"`, ... for simplicity.
- NEVER reuse an ID, even across different pages in the same file.
- Draw.io natively generates random alphanumeric IDs (e.g., `"aB3x-Kz9q"`), but any unique string works.

---

## 6. mxGeometry Attributes

ALWAYS a child of `<mxCell>`. ALWAYS includes `as="geometry"`.

### Vertex Geometry (Absolute)

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `x` | Number | `0` | Horizontal position of top-left corner. Relative to parent group if inside a container. |
| `y` | Number | `0` | Vertical position of top-left corner. 0,0 = top-left, y increases downward. |
| `width` | Number | `0` | Shape width in pixels |
| `height` | Number | `0` | Shape height in pixels |
| `as` | String | REQUIRED | ALWAYS `"geometry"` |

### Edge Geometry (Relative)

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `relative` | `"1"` | REQUIRED for edges | Enables relative coordinate mode |
| `x` | Number | `0` | Position along edge path: `-1` (source) to `1` (target), `0` = center |
| `y` | Number | `0` | Perpendicular offset in pixels. Positive = below/right, Negative = above/left |
| `as` | String | REQUIRED | ALWAYS `"geometry"` |

### Child Elements of mxGeometry

| Element | `as` Value | Purpose |
|---------|-----------|---------|
| `<mxPoint>` | `"sourcePoint"` | Start coordinate for unconnected edge endpoints |
| `<mxPoint>` | `"targetPoint"` | End coordinate for unconnected edge endpoints |
| `<mxPoint>` | `"offset"` | Additional pixel offset for label positioning |
| `<Array>` | `"points"` | Container for intermediate waypoints (`<mxPoint>` children) |
| `<mxRectangle>` | `"alternateBounds"` | Collapsed size for collapsible containers |

---

## 7. mxPoint Attributes

Used inside `<mxGeometry>` for waypoints, source/target points, and offsets.

| Attribute | Type | Description |
|-----------|------|-------------|
| `x` | Number | Horizontal coordinate |
| `y` | Number | Vertical coordinate |
| `as` | String | Binding: `"sourcePoint"`, `"targetPoint"`, `"offset"`, or omitted when inside `<Array>` |

---

## 8. Array Element

Container for waypoints inside edge geometry.

| Attribute | Type | Description |
|-----------|------|-------------|
| `as` | String | ALWAYS `"points"` |

Children: one or more `<mxPoint x="..." y="..." />` elements representing intermediate routing points in absolute canvas coordinates.

---

## 9. object / UserObject Attributes

Wrapper for attaching custom metadata to cells. `<object>` and `<UserObject>` are identical.

### Reserved Attributes

| Attribute | Type | Description |
|-----------|------|-------------|
| `id` | String | Unique identifier (moves FROM mxCell TO wrapper) |
| `label` | String | Display text (replaces mxCell's `value`) |
| `tooltip` | String | Hover text in the editor |
| `link` | String | URL or internal link (`data:page/id,<pageId>`) |
| `placeholders` | `"1"` | Enable `%variable%` substitution in label and tooltip |
| `tags` | String | Comma-separated tags for search/filter |

### Custom Attributes

Any additional attribute on `<object>` becomes a custom property visible in Draw.io's "Edit Data" dialog (Ctrl+M). Arbitrary key-value pairs are supported.

---

## 10. Core Style Properties

These are the most important style properties for vertex and edge cells. Style strings use the format `key=value;key=value;` with NO spaces.

### Vertex Style Properties

| Property | Values | Description |
|----------|--------|-------------|
| `html` | `1` | ALWAYS include. Enables rich text rendering. |
| `whiteSpace` | `wrap` | ALWAYS include. Enables text wrapping. |
| `rounded` | `0`/`1` | Rounded corners on rectangles |
| `shape` | String | Shape type: `ellipse`, `rhombus`, `triangle`, `hexagon`, `cylinder`, `parallelogram`, etc. |
| `perimeter` | String | Connection point calculation. MUST match shape. See SKILL.md Shape-Perimeter table. |
| `fillColor` | Hex color | Shape fill color (e.g., `#DAE8FC`) |
| `strokeColor` | Hex color | Border color (e.g., `#6C8EBF`) |
| `fontColor` | Hex color | Text color |
| `fontSize` | Number | Font size in points |
| `fontStyle` | Bitmask | `1`=bold, `2`=italic, `4`=underline. Combine by adding: `3`=bold+italic |
| `align` | `left`/`center`/`right` | Horizontal text alignment |
| `verticalAlign` | `top`/`middle`/`bottom` | Vertical text alignment |
| `opacity` | 0-100 | Cell opacity percentage |
| `shadow` | `0`/`1` | Drop shadow |
| `glass` | `0`/`1` | Glass effect overlay |
| `swimlane` | (no value) | Marks cell as a swimlane container |
| `group` | (no value) | Marks cell as a group container |
| `container` | `0`/`1` | Explicitly enable/disable container behavior |
| `collapsible` | `0`/`1` | Enable collapse/expand on containers |
| `childLayout` | `stackLayout` | Automatic child layout inside container |

### Edge Style Properties

| Property | Values | Description |
|----------|--------|-------------|
| `edgeStyle` | String | Routing algorithm: `orthogonalEdgeStyle`, `elbowEdgeStyle`, `entityRelationEdgeStyle`, `isometricEdgeStyle` |
| `curved` | `0`/`1` | Smooth curved routing |
| `endArrow` | String | Arrow at target: `classic`, `block`, `open`, `oval`, `diamond`, `none` |
| `startArrow` | String | Arrow at source (same values as endArrow) |
| `endFill` | `0`/`1` | Fill the end arrow |
| `startFill` | `0`/`1` | Fill the start arrow |
| `strokeWidth` | Number | Line thickness in pixels |
| `dashed` | `0`/`1` | Dashed line |
| `dashPattern` | String | Custom dash pattern (e.g., `"8 4"`) |
| `exitX`/`exitY` | 0-1 | Fixed exit point on source (0,0=top-left, 1,1=bottom-right) |
| `entryX`/`entryY` | 0-1 | Fixed entry point on target |
| `exitDx`/`exitDy` | Number | Pixel offset from exit point |
| `entryDx`/`entryDy` | Number | Pixel offset from entry point |
| `jettySize` | `auto`/Number | Length of orthogonal segments leaving shapes |

---

## 11. Placeholder System

### File-Level Variables

Defined in `vars` attribute of `<mxfile>` as a JSON string:

```xml
<mxfile vars='{"project":"Atlas","version":"2.1"}'>
```

### Resolution Order (First Match Wins)

1. Cell-level custom properties (attributes on `<object>`)
2. Parent container properties
3. Ancestor containers (walking up the tree)
4. Layer-level properties
5. Root cell (id="0") properties
6. File-level `vars` on `<mxfile>`

### Predefined Placeholders

| Placeholder | Value |
|-------------|-------|
| `%id%` | Cell ID |
| `%width%` | Cell width in pixels |
| `%height%` | Cell height in pixels |
| `%date%` | Current date |
| `%time%` | Current time |
| `%timestamp%` | Full timestamp |
| `%pagenumber%` | Current page number |
| `%pagecount%` | Total number of pages |
| `%page%` | Current page name |
| `%filename%` | File name |

Unit variants: `%width:mm%`, `%height:in%`, `%width:m%`.

Escape literal `%` with `%%` (e.g., `80%%` renders as `80%`).

---

## 12. Compression Algorithm

**AI MUST NEVER use this.** Documented for reference only.

### Compression (XML to stored string)

1. Start with raw `<mxGraphModel>...</mxGraphModel>` XML string
2. URL-encode (JavaScript `encodeURIComponent`)
3. Raw DEFLATE (RFC 1951 — NO zlib headers, NO gzip wrapper)
4. Base64-encode the compressed bytes
5. Store as text content of `<diagram>` element

### Decompression (stored string to XML)

1. Base64-decode to compressed bytes
2. Raw INFLATE (no zlib/gzip headers)
3. URL-decode (JavaScript `decodeURIComponent`)
4. Parse as `<mxGraphModel>` XML
