# Vooronderzoek: mxGraph XML Format — Complete Technical Reference

> Onderzocht op 2026-03-19. Bronnen: drawio.com/doc/faq/ai-drawio-generation, drawio.com/doc/faq/drawio-style-reference, jgraph.github.io/mxgraph/docs/js-api/ (mxCell, mxGeometry), drawio.com/doc/faq/predefined-placeholders, drawio.com/blog/placeholder-scope, github.com/jgraph/drawio (issues and discussions).
>
> **Verwerkt:** Nee

---

## 1. Complete XML Hierarchy

A Draw.io file uses a strict four-level XML hierarchy. Every valid `.drawio` file follows this nesting structure:

```xml
<mxfile host="app.diagrams.net" modified="2026-03-19T12:00:00.000Z"
        agent="Mozilla/5.0" etag="abc123" version="24.0.0" type="device"
        compressed="false" vars='{"project":"Atlas","version":"2.1"}'>
  <diagram id="page-1" name="Page-1">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- All diagram content here -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 1.1 mxfile Element

The outermost container. Attributes:

| Attribute | Purpose | Example Values |
|-----------|---------|----------------|
| `host` | Application that created the file | `"app.diagrams.net"`, `"Electron"`, `"embed.diagrams.net"` |
| `modified` | ISO 8601 timestamp of last modification | `"2026-03-19T12:00:00.000Z"` |
| `agent` | User-agent string of the creating application | Browser UA string |
| `etag` | Change tracking identifier | Random string |
| `version` | Draw.io editor version | `"24.0.0"` |
| `type` | Storage backend | `"device"`, `"google"`, `"github"`, `"gitlab"`, `"dropbox"`, `"onedrive"`, `"browser"` |
| `compressed` | Whether diagram content is deflated | `"true"`, `"false"` |
| `vars` | File-level variables as JSON string | `'{"project":"Atlas"}'` |

### 1.2 diagram Element

Each `<diagram>` represents one page in the file. Attributes:

| Attribute | Purpose | Default |
|-----------|---------|---------|
| `id` | Unique identifier for the page | Auto-generated |
| `name` | Display name shown on the tab | `"Page-1"` |

The content of a `<diagram>` element is either an `<mxGraphModel>` child (uncompressed) or a Base64-encoded deflated string (compressed).

### 1.3 mxGraphModel Element

Controls the canvas/editor behavior. Attributes:

| Attribute | Purpose | Default |
|-----------|---------|---------|
| `dx` | Horizontal scroll offset | `0` |
| `dy` | Vertical scroll offset | `0` |
| `grid` | Show grid (`1`) or hide (`0`) | `1` |
| `gridSize` | Grid spacing in pixels | `10` |
| `guides` | Enable snap guides | `1` |
| `tooltips` | Show tooltips on hover | `1` |
| `connect` | Enable connection handling | `1` |
| `arrows` | Show connection arrows | `1` |
| `fold` | Enable group folding/collapsing | `1` |
| `page` | Show page boundary | `1` |
| `pageScale` | Page zoom scale factor | `1` |
| `pageWidth` | Page width in pixels | `1169` (A4 landscape at 96 DPI) |
| `pageHeight` | Page height in pixels | `827` |
| `math` | Enable LaTeX math rendering | `0` |
| `shadow` | Enable global shadow | `0` |
| `background` | Canvas background color | `none` |

### 1.4 root Element

The `<root>` element is a simple container that holds all `<mxCell>` elements. It has no attributes of its own. Every `<root>` MUST contain at least two structural cells:

- `<mxCell id="0" />` — The invisible root container. All layers are children of this cell.
- `<mxCell id="1" parent="0" />` — The default layer. All visible diagram content is a child of this cell (or a child of another layer).

These two cells are mandatory. Without them, Draw.io will fail to render the diagram.

---

## 2. mxCell Deep Dive

Every visual element in a Draw.io diagram is an `<mxCell>`. Cells represent three types of objects: groups (containers), vertices (shapes), and edges (connectors).

### 2.1 All Attributes

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `id` | String | `null` | Unique identifier. MUST be unique within the entire diagram (across all pages). |
| `parent` | String | `null` | ID of the parent cell. Vertices/edges use `"1"` (default layer). Layers use `"0"` (root). |
| `value` | String | `null` | Display text. Supports HTML when `html=1` is in the style. |
| `style` | String | `null` | Semicolon-separated key=value pairs defining appearance. |
| `vertex` | `"1"` | `false` | Set to `"1"` to mark as a shape. Mutually exclusive with `edge`. |
| `edge` | `"1"` | `false` | Set to `"1"` to mark as a connector. Mutually exclusive with `vertex`. |
| `source` | String | `null` | ID of the source vertex (edges only). |
| `target` | String | `null` | ID of the target vertex (edges only). |
| `connectable` | `"0"` or `"1"` | `"1"` | Whether other edges can connect to this cell. Set to `"0"` on edge labels. |
| `visible` | `"0"` or `"1"` | `"1"` | Whether the cell is rendered. Hidden cells still exist in the model. |
| `collapsed` | `"0"` or `"1"` | `"0"` | Whether a container/group is collapsed. Uses `alternateBounds` for collapsed size. |

### 2.2 ID Generation Rules

- IDs MUST be unique across the entire diagram file (all pages).
- The root cell ALWAYS has `id="0"` and the default layer ALWAYS has `id="1"`.
- Draw.io generates IDs using a random alphanumeric pattern (e.g., `"aB3x-Kz9q"`), but any unique string or integer works.
- For programmatic generation, sequential integers (`"2"`, `"3"`, `"4"`, ...) are the safest approach.
- NEVER reuse an ID, even across different pages.

### 2.3 Parent-Child Relationships

The `parent` attribute creates a strict tree hierarchy:

```
id="0" (root container)
├── id="1" parent="0" (default layer)
│   ├── id="2" parent="1" (shape on default layer)
│   ├── id="3" parent="1" (shape on default layer)
│   └── id="4" parent="1" (edge connecting 2→3)
├── id="5" parent="0" (second layer)
│   └── id="6" parent="5" (shape on second layer)
```

Groups/containers work the same way — child shapes set their `parent` to the group's ID:

```xml
<!-- Group container -->
<mxCell id="10" value="Server Group" style="group" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="300" height="200" as="geometry" />
</mxCell>
<!-- Child of the group -->
<mxCell id="11" value="Web Server" style="rounded=1;" vertex="1" parent="10">
  <mxGeometry x="20" y="20" width="120" height="60" as="geometry" />
</mxCell>
```

When a cell is a child of a group, its `mxGeometry` coordinates are relative to the parent group's top-left corner, NOT the canvas origin.

---

## 3. mxGeometry

The `<mxGeometry>` element is always a child of `<mxCell>` and uses `as="geometry"` to bind it. It controls position, size, and (for edges) label placement and routing points.

### 3.1 Vertex Geometry (Absolute Positioning)

For shapes (vertex="1"), geometry uses absolute canvas coordinates:

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="200" y="150" width="120" height="60" as="geometry" />
</mxCell>
```

| Attribute | Meaning |
|-----------|---------|
| `x` | Horizontal position of top-left corner (pixels from canvas origin, or from parent's top-left if inside a group) |
| `y` | Vertical position of top-left corner (0,0 is top-left; y increases downward) |
| `width` | Shape width in pixels |
| `height` | Shape height in pixels |

Exception: When the vertex is a child of a group/container, x and y are relative to the parent's top-left corner.

### 3.2 Edge Geometry (Relative Positioning)

For edges (edge="1"), geometry has `relative="1"` and describes the label position, NOT the edge path:

```xml
<mxCell id="4" value="Yes" style="edgeStyle=orthogonalEdgeStyle;" edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

When `relative="1"`:

| Attribute | Meaning | Range |
|-----------|---------|-------|
| `x` | Position along the edge path | `-1` (source) to `1` (target), `0` = center |
| `y` | Perpendicular offset from the edge path | Absolute pixel value. Positive = below/right, Negative = above/left |

Example — Label offset to the right of the midpoint:

```xml
<mxGeometry x="0" y="15" relative="1" as="geometry" />
```

This places the label at the center of the edge (x=0), offset 15 pixels perpendicular to the edge path.

### 3.3 alternateBounds

Used for collapsible containers. When `collapsed="1"` is set on an mxCell, the geometry swaps between normal bounds and `alternateBounds`:

```xml
<mxCell id="10" value="Server Group" style="swimlane;" vertex="1" collapsed="1" parent="1">
  <mxGeometry x="100" y="100" width="300" height="200" as="geometry">
    <mxRectangle x="100" y="100" width="160" height="30" as="alternateBounds" />
  </mxGeometry>
</mxCell>
```

When collapsed, the cell renders at 160x30. When expanded, it renders at 300x200. The `swap()` method toggles between these states internally.

### 3.4 offset

The `<mxPoint>` with `as="offset"` inside mxGeometry provides an additional pixel offset:

```xml
<mxGeometry x="0.5" y="0" relative="1" as="geometry">
  <mxPoint x="10" y="-5" as="offset" />
</mxGeometry>
```

For edges: offset from the position calculated by x and y.
For absolute vertices: label offset from the default label position.
For relative vertices (inside containers): absolute offset added after relative position is computed.

---

## 4. Waypoints and Points

Edges can be routed through intermediate waypoints using an `<Array>` element inside `<mxGeometry>`.

### 4.1 Waypoint Array

```xml
<mxCell id="4" edge="1" source="2" target="3" parent="1"
        style="edgeStyle=orthogonalEdgeStyle;">
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="300" y="150" />
      <mxPoint x="300" y="250" />
    </Array>
  </mxGeometry>
</mxCell>
```

The `<Array as="points">` contains `<mxPoint x="..." y="..." />` elements that define intermediate routing points. These are absolute canvas coordinates. The edge routing algorithm (determined by `edgeStyle` in the style) uses these points as anchors:

- **orthogonalEdgeStyle**: Routes with right angles through the waypoints.
- **elbowEdgeStyle**: Single-elbow routing using a midpoint hint.
- **entityRelationEdgeStyle**: ER diagram-style routing.
- **isometricEdgeStyle**: Isometric projection routing.
- No edgeStyle (straight): Direct lines through each waypoint in sequence.

### 4.2 sourcePoint and targetPoint

When an edge is NOT connected to a source or target cell, terminal points define where the edge starts/ends:

```xml
<mxCell id="5" edge="1" parent="1" style="edgeStyle=orthogonalEdgeStyle;">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="100" y="200" as="sourcePoint" />
    <mxPoint x="400" y="350" as="targetPoint" />
    <Array as="points">
      <mxPoint x="250" y="200" />
      <mxPoint x="250" y="350" />
    </Array>
  </mxGeometry>
</mxCell>
```

- `sourcePoint`: Used when no `source` attribute is set on the mxCell. Defines the starting coordinate.
- `targetPoint`: Used when no `target` attribute is set on the mxCell. Defines the ending coordinate.
- These are absolute canvas coordinates and are only relevant for floating (unconnected) edge endpoints.

### 4.3 How Waypoints Affect Routing

The interaction between waypoints and edge styles:

1. **With orthogonalEdgeStyle**: Waypoints act as anchor points that the orthogonal router must pass through, creating L-shaped segments between each pair.
2. **With curved=1**: Waypoints become control points for curved routing, creating smooth Bezier-like curves.
3. **Without edgeStyle**: Waypoints create straight-line segments. The edge goes: source → waypoint1 → waypoint2 → ... → target.
4. **With elbowEdgeStyle**: The first waypoint's position determines where the elbow bend occurs.

---

## 5. UserObject / object Wrapper

For attaching custom metadata (key-value properties) to diagram elements, wrap the `<mxCell>` in a `<UserObject>` or `<object>` element. Both names are functionally identical; `<object>` is the shorter alias.

### 5.1 Structure

```xml
<object id="srv1" label="Web Server" tooltip="Primary web server"
        link="https://example.com" placeholders="1"
        ip="10.0.1.10" environment="production" owner="ops-team">
  <mxCell style="shape=mxgraph.aws4.ec2;whiteSpace=wrap;html=1;"
          vertex="1" parent="1">
    <mxGeometry x="200" y="100" width="78" height="78" as="geometry" />
  </mxCell>
</object>
```

### 5.2 Reserved Attributes

| Attribute | Purpose |
|-----------|---------|
| `id` | Unique identifier (moves from mxCell to the wrapper) |
| `label` | Display text (replaces mxCell's `value` attribute) |
| `tooltip` | Hover text shown in the editor |
| `link` | URL or page link (`data:page/id,<pageId>` for internal links) |
| `placeholders` | Set to `"1"` to enable `%variable%` substitution in label and tooltip |
| `tags` | Comma-separated tags for search/filter |

### 5.3 Custom Attributes

Any additional attribute on `<object>` or `<UserObject>` becomes a custom property visible in Draw.io's "Edit Data" dialog (Edit > Edit Data or Ctrl+M). These are arbitrary key-value pairs:

```xml
<object id="db1" label="PostgreSQL" ip="10.0.2.5" port="5432"
        region="eu-west-1" cost_center="CC-4200">
```

### 5.4 When to Use UserObject vs Plain mxCell

| Use Case | Approach |
|----------|----------|
| Simple shape with text | `<mxCell value="Hello" ...>` |
| Shape with tooltip | `<object label="Hello" tooltip="Details...">` |
| Shape with hyperlink | `<object label="Hello" link="https://...">` |
| Shape with custom metadata | `<object label="Hello" customKey="customValue">` |
| Shape with placeholder substitution | `<object label="%name%" placeholders="1" name="Server">` |
| Plain edge with label | `<mxCell value="connects" edge="1" ...>` |
| Edge with metadata | `<object label="connects" protocol="HTTPS">` wrapping the mxCell |

IMPORTANT: When using `<object>` or `<UserObject>`, the `id` and `label` attributes move to the wrapper element. The inner `<mxCell>` does NOT have `id` or `value` attributes.

---

## 6. Compression Format

Draw.io supports two storage formats for diagram content within the `<diagram>` element.

### 6.1 Uncompressed Format

The `<mxGraphModel>` is stored directly as a child element:

```xml
<diagram id="page-1" name="Page-1">
  <mxGraphModel>
    <root>
      <mxCell id="0" />
      <mxCell id="1" parent="0" />
      <!-- ... -->
    </root>
  </mxGraphModel>
</diagram>
```

### 6.2 Compressed Format

The diagram content is a text node inside `<diagram>`:

```xml
<diagram id="page-1" name="Page-1">
  dZHBDoMgDIafhmMJ6nS3qYfdnB5ckUlHE4EQ3HR7+lWpOpeYkP6k/b62hSS82Z+9bPQbcDAk
  JjtCToSQZJvSi4L9KKyjIBNKRxYbWJgP2BCLdpJDOwl0iMaptRm2aFtoXMBk3uM4Trui5+mv
  ...
</diagram>
```

### 6.3 Exact Algorithm

**Compression (XML to stored string):**

1. Start with the raw `<mxGraphModel>...</mxGraphModel>` XML string.
2. URL-encode the XML string (encodeURIComponent in JavaScript).
3. Apply raw DEFLATE compression (RFC 1951 — raw deflate, NO zlib headers, NO gzip wrapper).
4. Base64-encode the compressed byte stream.
5. Store the resulting string as the text content of the `<diagram>` element.

**Decompression (stored string to XML):**

1. Base64-decode the string to get compressed bytes.
2. Raw INFLATE (decompress without expecting zlib/gzip headers).
3. URL-decode the resulting string (decodeURIComponent).
4. Parse the resulting XML as `<mxGraphModel>`.

### 6.4 Why AI MUST NEVER Generate Compressed Format

AI systems (LLMs) MUST ALWAYS generate uncompressed XML. The reasons are absolute:

1. **LLMs cannot perform binary operations.** DEFLATE compression is a binary algorithm involving Huffman coding and LZ77 matching. No language model can execute this.
2. **Base64 of compressed data is not predictable.** The output of DEFLATE is binary data that has no human-readable pattern.
3. **Draw.io accepts both formats.** When opening a file with uncompressed XML, Draw.io renders it correctly without any additional steps.
4. **Validation is impossible.** Compressed content cannot be visually inspected or debugged by humans or AI.

Set `compressed="false"` on the `<mxfile>` element to signal uncompressed content.

---

## 7. Simplified vs Full Format

### 7.1 Simplified Format

The minimum valid Draw.io XML starts at `<mxGraphModel>`:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Hello" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

When Draw.io opens this format, it automatically wraps it in `<mxfile>` and `<diagram>` elements. This is the recommended format for AI generation because:

- It is the simplest valid structure.
- It avoids the need to generate metadata attributes (host, modified, etag, version).
- Draw.io's import and open dialogs accept it without issues.

### 7.2 Full Format

The full format includes `<mxfile>` and `<diagram>` wrappers. This is REQUIRED when:

- **Multi-page diagrams**: Each page needs its own `<diagram>` element.
- **File-level variables**: The `vars` attribute only exists on `<mxfile>`.
- **Metadata tracking**: Host, modified date, version, and type information.

### 7.3 Implications for Multi-Page Diagrams

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" /><mxCell id="1" parent="0" />
        <!-- Page 1 content -->
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Detail View">
    <mxGraphModel>
      <root>
        <mxCell id="0" /><mxCell id="1" parent="0" />
        <!-- Page 2 content -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Each page has its own independent `<mxGraphModel>` with its own root and structural cells. Cell IDs MUST be unique across all pages in the file (not just within a single page).

---

## 8. File-Level Variables

### 8.1 Defining Variables

File-level variables are defined as a JSON string in the `vars` attribute of `<mxfile>`:

```xml
<mxfile vars='{"project":"Atlas","version":"2.1","author":"Jane Doe","env":"staging"}'>
```

### 8.2 Placeholder Syntax

Use `%variableName%` in labels and tooltips. The containing element (or an ancestor) MUST have `placeholders="1"`:

```xml
<object id="2" label="Project: %project% v%version%" placeholders="1">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="200" height="60" as="geometry" />
  </mxCell>
</object>
```

This renders as: "Project: Atlas v2.1"

### 8.3 Variable Resolution Order

When a `%placeholder%` is encountered, Draw.io resolves it by walking up the containment hierarchy. The first match wins:

1. **Cell level**: Custom properties on the cell itself (attributes on the `<object>` wrapper).
2. **Parent container**: Properties on the immediate parent group/container.
3. **Ancestor containers**: Continue up through nested containers.
4. **Layer level**: Properties on the layer cell (mxCell with parent="0").
5. **Root level**: Properties on the root cell (mxCell id="0").
6. **File level**: Variables in the `vars` attribute of `<mxfile>`.

If no match is found at any level, the placeholder renders as blank text.

### 8.4 Predefined Placeholders

Draw.io provides built-in placeholders that do not require custom properties:

| Placeholder | Value |
|-------------|-------|
| `%id%` | The cell's ID |
| `%width%` | Cell width in pixels |
| `%height%` | Cell height in pixels |
| `%length%` | Edge length (edges only) |
| `%date%` | Current date |
| `%time%` | Current time |
| `%timestamp%` | Full timestamp |
| `%date{format}%` | Formatted date (Java SimpleDateFormat) |
| `%pagenumber%` | Current page number |
| `%pagecount%` | Total number of pages |
| `%page%` | Current page name |
| `%filename%` | File name |

Unit variants: `%width:mm%`, `%height:in%`, `%width:m%` convert pixel values to physical units.

### 8.5 Escaping

To display a literal `%` character without triggering placeholder substitution, use `%%`:

```
Battery: 80%% charged
```

Renders as: "Battery: 80% charged"

---

## 9. HTML Labels

Draw.io supports rich HTML content in cell labels when the style includes `html=1`.

### 9.1 Enabling HTML Labels

The `html=1` style property MUST be present:

```xml
<mxCell id="2" value="&lt;b&gt;Bold&lt;/b&gt; and &lt;i&gt;italic&lt;/i&gt;"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

### 9.2 XML Escaping Requirements

Because the `value` attribute is inside an XML document, ALL HTML must be XML-escaped:

| Character | Escape | Example |
|-----------|--------|---------|
| `<` | `&lt;` | `&lt;b&gt;Bold&lt;/b&gt;` |
| `>` | `&gt;` | (see above) |
| `&` | `&amp;` | `&lt;b&gt;AT&amp;amp;T&lt;/b&gt;` |
| `"` | `&quot;` | `style=&quot;color:red&quot;` |

### 9.3 Supported HTML Tags

Draw.io supports a subset of HTML in labels:

- **Text formatting**: `<b>`, `<i>`, `<u>`, `<s>`, `<sup>`, `<sub>`, `<br>`
- **Block elements**: `<p>`, `<div>`, `<hr>`
- **Lists**: `<ul>`, `<ol>`, `<li>`
- **Tables**: `<table>`, `<tr>`, `<td>`, `<th>` (very powerful for structured labels)
- **Spans**: `<span>` with inline styles
- **Font**: `<font>` with `color`, `face`, `size` attributes
- **Links**: `<a href="...">` (rendered clickable)

### 9.4 Inline CSS in HTML Labels

Use the `style` attribute on HTML elements (XML-escaped):

```xml
value="&lt;div style=&quot;text-align:left;font-size:14px;&quot;&gt;
  &lt;b style=&quot;color:#333;&quot;&gt;Server Name&lt;/b&gt;&lt;br&gt;
  &lt;span style=&quot;color:#999;font-size:11px;&quot;&gt;10.0.1.10&lt;/span&gt;
&lt;/div&gt;"
```

### 9.5 Tables in Labels

Tables are especially useful for database entities and structured content:

```xml
value="&lt;table style=&quot;width:100%;font-size:12px;&quot;&gt;
  &lt;tr&gt;&lt;th colspan=&quot;2&quot; style=&quot;background:#DAE8FC;&quot;&gt;users&lt;/th&gt;&lt;/tr&gt;
  &lt;tr&gt;&lt;td&gt;id&lt;/td&gt;&lt;td&gt;INT PK&lt;/td&gt;&lt;/tr&gt;
  &lt;tr&gt;&lt;td&gt;name&lt;/td&gt;&lt;td&gt;VARCHAR(255)&lt;/td&gt;&lt;/tr&gt;
  &lt;tr&gt;&lt;td&gt;email&lt;/td&gt;&lt;td&gt;VARCHAR(255)&lt;/td&gt;&lt;/tr&gt;
&lt;/table&gt;"
```

### 9.6 whiteSpace=wrap

The `whiteSpace=wrap` style property enables text wrapping within the cell bounds. Without it, text overflows the shape boundary. ALWAYS include `whiteSpace=wrap` when using `html=1`.

---

## 10. Pages and Layers

### 10.1 Multi-Page Diagrams

Multiple pages are represented by multiple `<diagram>` elements inside `<mxfile>`. Each page is independent with its own graph model, root, and cell hierarchy:

```xml
<mxfile compressed="false">
  <diagram id="arch" name="Architecture">
    <mxGraphModel>
      <root>
        <mxCell id="0" /><mxCell id="1" parent="0" />
        <!-- Architecture diagram cells -->
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="flow" name="Data Flow">
    <mxGraphModel>
      <root>
        <mxCell id="0" /><mxCell id="1" parent="0" />
        <!-- Data flow diagram cells -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Page order in the Draw.io tab bar matches the order of `<diagram>` elements in the XML.

### 10.2 Layers

Layers are mxCell elements with `parent="0"` (children of the root container). The default layer has `id="1"`, but additional layers can be added:

```xml
<root>
  <mxCell id="0" />
  <mxCell id="1" parent="0" />                              <!-- Default layer -->
  <mxCell id="layer-bg" value="Background" parent="0" />    <!-- Background layer -->
  <mxCell id="layer-anno" value="Annotations" parent="0" /> <!-- Annotations layer -->

  <!-- Cell on default layer -->
  <mxCell id="2" value="Main" vertex="1" parent="1" style="..." >
    <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
  </mxCell>

  <!-- Cell on background layer -->
  <mxCell id="3" value="BG Element" vertex="1" parent="layer-bg" style="..." >
    <mxGeometry x="50" y="50" width="500" height="400" as="geometry" />
  </mxCell>
</root>
```

### 10.3 Layer Visibility

Layer visibility is controlled by the `visible` attribute on the layer cell:

```xml
<mxCell id="layer-anno" value="Annotations" parent="0" visible="0" />
```

Setting `visible="0"` hides all cells on that layer. The default is `visible="1"` (shown).

### 10.4 Layer Ordering

Layers render in the order they appear in the XML. Earlier layers render behind later layers. The first layer cell (typically `id="1"`) is the bottommost, and subsequent layer cells stack on top.

### 10.5 Layer Metadata

Layers can also use the `<object>` wrapper for custom metadata:

```xml
<object id="layer-infra" label="Infrastructure" locked="1" parent="0">
  <mxCell style="" parent="0" />
</object>
```

The `locked="1"` attribute prevents editing of cells on that layer.

---

## 11. Version History and Compatibility

### 11.1 mxGraph 4.x Format

The current Draw.io format is based on mxGraph 4.x, which established the XML schema that remains in use today. Draw.io (diagrams.net) forked from the original mxGraph project and continues to maintain backward compatibility.

Key mxGraph 4.x characteristics:
- The `<mxfile>` wrapper with metadata attributes.
- Compression support (DEFLATE + Base64).
- The `<mxGraphModel>` with canvas configuration attributes.
- The two-cell structural requirement (id="0" root, id="1" default layer).
- Style strings as semicolon-separated key=value pairs.

### 11.2 Differences from Earlier Versions

mxGraph 3.x and earlier used a simpler format:
- No `<mxfile>` wrapper — files started directly with `<mxGraphModel>`.
- No compression support.
- No multi-page support (single diagram per file).
- No file-level variables or placeholders.
- Fewer style properties and shape types.

Draw.io maintains full backward compatibility: files created with older mxGraph versions open correctly in current Draw.io. The editor automatically upgrades the format to the current version when saving.

### 11.3 Current State (2026)

Draw.io is now fully open source under the Apache 2.0 license. The mxGraph JavaScript library has been superseded by maxGraph (a TypeScript rewrite), but the XML file format remains identical. Draw.io continues to read and write the same mxGraph 4.x XML format regardless of the internal rendering engine.

The `.drawio` file extension is the standard, though `.drawio.xml`, `.drawio.svg` (with embedded XML), and `.drawio.png` (with embedded XML) are also supported.

---

## 12. Critical Rules for Programmatic Generation

These rules MUST be followed by any system (AI or otherwise) generating Draw.io XML programmatically. Violating any of these rules will produce invalid or broken diagrams.

### Rule 1: ALWAYS Include Both Structural Cells

Every `<root>` MUST contain:
```xml
<mxCell id="0" />
<mxCell id="1" parent="0" />
```
Without these, Draw.io cannot render any content.

### Rule 2: NEVER Generate Compressed XML

ALWAYS use uncompressed XML with `<mxGraphModel>` as a child element of `<diagram>`. Set `compressed="false"` on `<mxfile>` if using the full format.

### Rule 3: ALWAYS Use Unique IDs

Every cell ID MUST be unique across the entire file (all pages). Use sequential integers for simplicity: `"2"`, `"3"`, `"4"`, etc.

### Rule 4: vertex="1" and edge="1" Are Mutually Exclusive

A cell is EITHER a vertex (shape) OR an edge (connector). NEVER set both on the same cell. NEVER omit both on content cells.

### Rule 5: Edges MUST Reference Valid Source/Target IDs

If an edge has `source` or `target` attributes, those IDs MUST exist as vertex cells in the same diagram. Referencing a non-existent ID produces a broken connection.

### Rule 6: Style Format Is Strict

Styles are semicolon-separated key=value pairs with NO spaces around `=` or `;`:
```
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;
```
A trailing semicolon is conventional but not required.

### Rule 7: Match Perimeters to Shapes

Non-rectangular shapes NEED a matching `perimeter` style value. Without it, edges connect at incorrect points:

| Shape | Required Perimeter |
|-------|-------------------|
| `shape=ellipse` | `perimeter=ellipsePerimeter` |
| `shape=rhombus` | `perimeter=rhombusPerimeter` |
| `shape=triangle` | `perimeter=trianglePerimeter` |
| `shape=hexagon` | `perimeter=hexagonPerimeter2` |
| `shape=parallelogram` | `perimeter=parallelogramPerimeter` |
| `shape=trapezoid` | `perimeter=trapezoidPerimeter` |

Rectangles and rounded rectangles use the default perimeter and do not need an explicit value.

### Rule 8: XML-Escape ALL HTML in value Attributes

When using HTML labels (`html=1` in style), every `<`, `>`, `&`, and `"` in the `value` attribute MUST be XML-escaped. Failure to escape produces malformed XML that will not parse.

### Rule 9: ALWAYS Include html=1 and whiteSpace=wrap

For every vertex cell, include both `html=1` (enables rich text) and `whiteSpace=wrap` (enables text wrapping) in the style string. These are the two most commonly forgotten properties and their absence causes rendering issues.

### Rule 10: Set parent Correctly

- Content cells: `parent="1"` (or the ID of their layer/container).
- Layer cells: `parent="0"`.
- The root cell (id="0"): No parent attribute.
- Group children: `parent="<groupId>"` with coordinates relative to the group's top-left corner.

### Rule 11: Use the Simplified Format When Possible

For single-page diagrams without variables, generate only `<mxGraphModel>` through `</mxGraphModel>`. Draw.io will auto-wrap with `<mxfile>` and `<diagram>`. This reduces complexity and potential for errors.

### Rule 12: Validate Before Delivery

Every generated diagram SHOULD be validated for:
- Well-formed XML (parseable).
- Presence of structural cells (id="0" and id="1").
- Unique IDs.
- Valid source/target references on edges.
- Correct parent references (no orphaned cells).
- Proper XML escaping in value attributes.

---

## Sources

- [Generate and validate draw.io diagrams with AI](https://www.drawio.com/doc/faq/ai-drawio-generation)
- [draw.io Style Reference for AI File Generation](https://www.drawio.com/doc/faq/drawio-style-reference)
- [mxGeometry JavaScript API](https://jgraph.github.io/mxgraph/docs/js-api/files/model/mxGeometry-js.html)
- [mxCell JavaScript API](https://jgraph.github.io/mxgraph/docs/js-api/files/model/mxCell-js.html)
- [Predefined placeholders](https://www.drawio.com/doc/faq/predefined-placeholders)
- [Placeholder scope](https://www.drawio.com/blog/placeholder-scope)
- [Shape data in diagrams](https://www.drawio.com/blog/shape-data)
