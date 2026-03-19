# Methods Reference: Draw.io Syntax Metadata

Complete attribute reference for multi-page diagrams, layers, file-level variables, placeholders, tooltips, links, and MathJax.

---

## 1. mxfile Element Attributes

The outermost container for a Draw.io file.

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `host` | String | No | `"app.diagrams.net"` | Application that created the file |
| `modified` | String | No | — | ISO 8601 timestamp of last modification |
| `agent` | String | No | — | User-agent string of the creating application |
| `etag` | String | No | — | Change tracking identifier |
| `version` | String | No | — | Draw.io editor version (e.g., `"24.0.0"`) |
| `type` | String | No | `"device"` | Storage backend: `"device"`, `"google"`, `"github"`, `"gitlab"`, `"dropbox"`, `"onedrive"`, `"browser"` |
| `compressed` | `"true"` / `"false"` | No | `"true"` | Whether diagram content is deflated. ALWAYS set to `"false"` for AI-generated XML. |
| `vars` | String | No | — | File-level variables as single-quoted JSON string: `vars='{"key":"value"}'` |

### vars Attribute Rules

- The JSON string MUST use double quotes for keys and values (valid JSON).
- The `vars` attribute MUST use single quotes as the XML attribute delimiter.
- Values are strings only. Numbers and booleans are stored as strings: `'{"count":"42","enabled":"true"}'`.
- Variables are available to ALL cells on ALL pages via `%variableName%` when `placeholders="1"` is set.

---

## 2. diagram Element Attributes

Each `<diagram>` represents one page/tab in the file.

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `id` | String | ALWAYS | — | Unique identifier for the page. MUST be unique across the entire file. |
| `name` | String | ALWAYS | `"Page-1"` | Display name shown on the page tab in the editor. |

### diagram Content

The content of a `<diagram>` element is ALWAYS an `<mxGraphModel>` child element (for uncompressed AI-generated XML). NEVER place compressed/encoded content.

---

## 3. mxGraphModel Attributes

Controls canvas and editor behavior for a single page.

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `dx` | Number | `0` | Horizontal scroll offset |
| `dy` | Number | `0` | Vertical scroll offset |
| `grid` | `0` / `1` | `1` | Show grid |
| `gridSize` | Number | `10` | Grid spacing in pixels |
| `guides` | `0` / `1` | `1` | Enable snap guides |
| `tooltips` | `0` / `1` | `1` | Show tooltips on hover |
| `connect` | `0` / `1` | `1` | Enable connection handling |
| `arrows` | `0` / `1` | `1` | Show connection arrows |
| `fold` | `0` / `1` | `1` | Enable group folding/collapsing |
| `page` | `0` / `1` | `1` | Show page boundary |
| `pageScale` | Number | `1` | Page zoom scale factor |
| `pageWidth` | Number | `1169` | Page width in pixels (A4 landscape at 96 DPI) |
| `pageHeight` | Number | `827` | Page height in pixels |
| `math` | `0` / `1` | `0` | Enable LaTeX/MathJax rendering. Set to `1` to activate. |
| `shadow` | `0` / `1` | `0` | Enable global shadow on all shapes |
| `background` | Color string | `none` | Canvas background color |

---

## 4. Layer Cell Attributes

Layers are `<mxCell>` elements with `parent="0"`.

| Attribute | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `id` | String | ALWAYS | — | Unique identifier. `"1"` is the default layer. |
| `parent` | `"0"` | ALWAYS | — | MUST be `"0"` (root container) |
| `value` | String | ALWAYS | — | Display name shown in the Layers panel |
| `visible` | `"0"` / `"1"` | No | `"1"` | Set to `"0"` to hide the layer and all its content |
| `style` | String | No | — | Optional: `"locked=1"` prevents editing content on this layer |

### Layer Stacking Order

XML document order determines rendering order. Layers declared EARLIER in the XML render BEHIND layers declared LATER. The default layer (`id="1"`) is the first visible layer.

### Layer with object Wrapper

To attach custom properties to a layer for placeholder inheritance:

```xml
<object id="layer-prod" label="Production" env="production" region="eu-west-1">
  <mxCell parent="0" />
</object>
```

---

## 5. object / UserObject Wrapper Attributes

### Reserved Attributes

| Attribute | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | String | ALWAYS | Unique identifier. Moves from inner mxCell to wrapper. |
| `label` | String | ALWAYS | Display text. Replaces mxCell `value`. Supports `%placeholder%` tokens. |
| `tooltip` | String | No | Hover text in the editor. Supports `%placeholder%` tokens when `placeholders="1"`. |
| `link` | String | No | URL (`https://...`) or internal page link (`data:page/id,<diagramId>`). |
| `placeholders` | `"1"` | No | Set to `"1"` to enable `%variable%` substitution in label and tooltip. |
| `tags` | String | No | Comma-separated tags for search and filter in the editor. |

### Custom Attributes

Any attribute on `<object>` that is NOT in the reserved list becomes a custom property:

- Visible in Edit Data dialog (Ctrl+M)
- Available as `%attributeName%` placeholder when `placeholders="1"` is set
- Inherited by child cells during placeholder resolution

---

## 6. Placeholder System

### Predefined Placeholders (No Custom Properties Needed)

| Placeholder | Value | Requires placeholders="1" |
|-------------|-------|---------------------------|
| `%id%` | Cell ID | YES |
| `%width%` | Cell width in pixels | YES |
| `%height%` | Cell height in pixels | YES |
| `%length%` | Edge length (edges only) | YES |
| `%date%` | Current date | YES |
| `%time%` | Current time | YES |
| `%timestamp%` | Full timestamp | YES |
| `%date{format}%` | Formatted date (Java SimpleDateFormat) | YES |
| `%page%` | Current page name | YES |
| `%pagenumber%` | Current page number | YES |
| `%pagecount%` | Total page count | YES |
| `%filename%` | File name | YES |

### Unit Conversion Suffixes

Append a colon and unit to width/height placeholders:

| Suffix | Unit | Example |
|--------|------|---------|
| `:mm` | Millimeters | `%width:mm%` |
| `:in` | Inches | `%height:in%` |
| `:m` | Meters | `%width:m%` |

### Resolution Hierarchy

| Priority | Scope | Where Defined |
|----------|-------|---------------|
| 1 (highest) | Cell | Attributes on the `<object>` element |
| 2 | Parent container | Attributes on the parent group/swimlane `<object>` |
| 3 | Ancestor containers | Continue upward through nesting |
| 4 | Layer | Attributes on the layer cell's `<object>` wrapper |
| 5 | Root cell | Attributes on `<mxCell id="0" />` or its `<object>` wrapper |
| 6 (lowest) | File | JSON in `vars` attribute on `<mxfile>` |

### Escape Sequence

`%%` produces a literal `%` character. Example: `80%% complete` renders as `80% complete`.

---

## 7. Link Formats

| Format | Syntax | Description |
|--------|--------|-------------|
| External URL | `link="https://example.com"` | Opens in browser |
| Internal page | `link="data:page/id,<diagramId>"` | Navigates to another page in the file |
| Mailto | `link="mailto:user@example.com"` | Opens email client |
| HTML anchor | `&lt;a href=&quot;url&quot;&gt;text&lt;/a&gt;` in `value` | Inline link in HTML labels |

---

## 8. MathJax Configuration

| Setting | Location | Value | Description |
|---------|----------|-------|-------------|
| `math` | `<mxGraphModel>` attribute | `"1"` | Enables LaTeX rendering for the page |
| `$$...$$` | Cell `value` or `label` | LaTeX expression | Inline/display math delimiters |
| `html=1` | Cell `style` | Required | MathJax requires HTML rendering mode |
