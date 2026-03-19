# Vooronderzoek: Draw.io Integration & Conversion — Complete Technical Reference

> **Datum:** 2026-03-19
> **Auteur:** Claude Code (Opus 4.6)
> **Bronnen geraadpleegd:** drawio.com/doc/faq/ai-drawio-generation, jgraph.github.io/drawio-tools/, drawio.com/blog/insert-from-csv, drawio.com/doc/faq/embed-mode, drawio.com/blog/mermaid-diagrams, drawio.com/doc/faq/export-diagram, github.com/jgraph/drawio-mcp, github.com/lgazo/drawio-mcp-server
> **Verwerkt:** Nee

---

## Table of Contents

1. [CSV Import](#1-csv-import)
2. [Mermaid Conversion](#2-mermaid-conversion)
3. [Template System](#3-template-system)
4. [Export Formats](#4-export-formats)
5. [URL Parameters](#5-url-parameters)
6. [Programmatic Access](#6-programmatic-access)
7. [Compression / Decompression](#7-compression--decompression)
8. [Placeholder System](#8-placeholder-system)
9. [Embed Modes](#9-embed-modes)
10. [MCP Server Comparison](#10-mcp-server-comparison)

---

## 1. CSV Import

Draw.io provides a powerful CSV import feature that converts tabular data into diagrams. The CSV format uses `#` directive lines to configure how rows map to shapes, connections, styles, and layout.

### 1.1 Directive Lines

All directives start with `#` and MUST appear before the CSV data rows. Lines starting with `##` are treated as comments and ignored.

| Directive | Syntax | Purpose |
|-----------|--------|---------|
| `label` | `# label: %col1%<br>%col2%` | Defines the label template using column placeholders wrapped in `%` |
| `style` | `# style: rounded=1;fillColor=%fill%;` | Sets the mxGraph style string for all shapes; supports column placeholders |
| `stylename` | `# stylename: columnName` | Names the column used for conditional style selection |
| `styles` | `# styles: {"value1": "style1;", "value2": "style2;"}` | JSON map of column values to style strings |
| `identity` | `# identity: columnName` | Designates which column provides unique shape identifiers |
| `namespace` | `# namespace: csvimport-` | Prefix added to all cell IDs to avoid collisions |
| `connect` | `# connect: {"from":"col1", "to":"col2", ...}` | Defines a connection between shapes (see below) |
| `layout` | `# layout: auto` | Automatic layout algorithm; accepts layout names from Arrange > Layout |
| `width` | `# width: auto` or `# width: 120` | Shape width in pixels or `auto` |
| `height` | `# height: auto` or `# height: 60` | Shape height in pixels or `auto` |
| `padding` | `# padding: -12` | Padding around labels in pixels (negative values reduce padding) |
| `ignore` | `# ignore: col1,col2,col3` | Columns to exclude from shape metadata/tooltip |
| `link` | `# link: urlColumn` | Column providing hyperlinks for shapes |
| `parentstyle` | `# parentstyle: swimlane;...` | Style for automatically created parent/container shapes |
| `nodespacing` | `# nodespacing: 40` | Horizontal spacing between nodes in pixels |
| `levelspacing` | `# levelspacing: 100` | Vertical spacing between hierarchy levels in pixels |
| `edgespacing` | `# edgespacing: 40` | Spacing between parallel edges in pixels |

### 1.2 Connection Directive Details

The `connect` directive accepts a JSON object with these properties:

| Property | Type | Required | Description |
|----------|------|----------|-------------|
| `from` | string | YES | Source column name |
| `to` | string | YES | Target column name (matched against identity or first column) |
| `invert` | boolean | NO | If `true`, reverses arrow direction (target becomes source) |
| `label` | string | NO | Text label displayed on the connection |
| `style` | string | NO | mxGraph style string for the edge |

Multiple connections require multiple `# connect:` lines. Use backslash `\` at line end for readability when breaking long directives.

### 1.3 Conditional Styles

To apply different styles based on column values, use the `stylename` and `styles` directives together:

```
# stylename: type
# styles: {"decision": "rhombus;fillColor=#dae8fc;strokeColor=#6c8ebf;", "process": "rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;", "terminal": "ellipse;fillColor=#f8cecc;strokeColor=#b85450;"}
```

Similarly, connector styles can be conditional using `# connectorstyle:` and `# connectorstyles:` directives.

### 1.4 Complete Working Example: Org Chart

```csv
## Organizational chart with images and email links
# label: %name%<br><i style="color:gray;">%position%</i><br><a href="mailto:%email%">Email</a>
#
# style: label;image=%image%;whiteSpace=wrap;html=1;rounded=1;fillColor=%fill%;strokeColor=%stroke%;
# parentstyle: swimlane;whiteSpace=wrap;html=1;childLayout=stackLayout;horizontal=1;horizontalStack=0;resizeParent=1;resizeLast=0;collapsible=1;
#
# namespace: csvimport-
#
# connect: {"from": "manager", "to": "name", "invert": true, "label": "manages", \
#   "style": "curved=1;endArrow=blockThin;endFill=1;fontSize=11;"}
# connect: {"from": "refs", "to": "id", "style": "curved=1;fontSize=11;"}
#
# width: auto
# height: auto
# padding: -12
#
# ignore: id,image,fill,stroke,refs,manager
#
# link: url
#
# nodespacing: 40
# levelspacing: 100
# edgespacing: 40
#
# layout: auto
#
name,position,id,location,manager,email,fill,stroke,refs,url,image
Tessa Miller,CFO,emi,Office 1,,[email protected],#dae8fc,#6c8ebf,,https://www.draw.io,https://example.com/avatar1.png
Edward Morrison,Brand Manager,emo,Office 2,Tessa Miller,[email protected],#d5e8d4,#82b366,,https://www.draw.io,https://example.com/avatar2.png
```

### 1.5 Complete Working Example: Flowchart with Conditional Styles

```csv
## Flowchart with different shape types
# label: %name%
# stylename: type
# styles: {"decision": "rhombus;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;", \
#   "process": "rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;", \
#   "terminal": "ellipse;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;"}
# connect: {"from": "next", "to": "id", "style": "endArrow=classic;html=1;"}
# identity: id
# namespace: flow-
# width: 120
# height: 60
# layout: auto
# ignore: id,next,type
#
id,name,type,next
start,Start,terminal,step1
step1,Process Data,process,check
check,Valid?,decision,step2
step2,Save Result,process,end
end,End,terminal,
```

### 1.6 Key Rules for CSV Import

- Each row in the CSV data produces exactly one shape
- The first non-directive, non-comment line MUST be the column header row
- Column names referenced in `%placeholder%` syntax in labels and styles are replaced with row values
- Columns NOT listed in `# ignore:` become metadata attributes visible in the shape's properties
- The `# identity:` column (or the first column by default) is used for connection matching
- Dynamic colors work by placing hex values in columns and referencing them: `fillColor=%fill%;strokeColor=%stroke%`

---

## 2. Mermaid Conversion

### 2.1 Supported Mermaid Diagram Types

Draw.io supports converting the following Mermaid diagram types:

| Mermaid Type | Keyword | Support Level |
|-------------|---------|---------------|
| Flowchart | `graph`, `flowchart` | Full |
| Sequence Diagram | `sequenceDiagram` | Full |
| Class Diagram | `classDiagram` | Full |
| State Diagram | `stateDiagram` | Full |
| ER Diagram | `erDiagram` | Full |
| Gantt Chart | `gantt` | Full |
| Pie Chart | `pie` | Full |
| Git Graph | `gitgraph` | Full |
| Mindmap | `mindmap` | Full |
| Requirement Diagram | `requirementDiagram` | Full |
| User Journey | `journey` | Full |
| C4 Context | `C4Context` | Full |

### 2.2 How Conversion Works

Users insert Mermaid diagrams via **Arrange > Insert > Mermaid** or the `+` toolbar icon > Mermaid. The Mermaid text is pasted into a dialog, and Draw.io renders it on the canvas.

Draw.io also recently added support for the **Mermaid ELK layout option**, which produces more compact versions of complex flowcharts.

### 2.3 CRITICAL Limitation: Single Compound Shape

**This is the most important fact about Mermaid conversion in Draw.io:**

When a Mermaid diagram is inserted, it becomes a **single compound shape** on the drawing canvas — NOT individual mxCells. The entire diagram is one grouped object. To view or edit the Mermaid source, select the shape and press `Enter`.

This has significant implications for programmatic manipulation:

| Aspect | Native mxGraph XML | Mermaid Import |
|--------|-------------------|----------------|
| Individual cell access | YES — each shape is a separate `<mxCell>` | NO — entire diagram is one shape |
| Style editing per shape | YES — modify any cell's style independently | NO — must edit Mermaid source text |
| Programmatic connection | YES — create edges between any cells | NO — connections are internal to the compound shape |
| MCP server manipulation | YES — CRUD operations on individual cells | NO — can only replace the entire Mermaid block |
| Layout control | YES — exact pixel positioning | LIMITED — Mermaid's layout engine decides |

### 2.4 When to Use Native XML vs. Mermaid

**Use native mxGraph XML when:**
- Individual shapes need to be programmatically manipulated after creation
- Precise pixel-level positioning is required
- The diagram will be edited via MCP server CRUD operations
- Complex custom styling is needed per shape
- The diagram needs to integrate with other shapes on the canvas

**Use Mermaid when:**
- Rapid prototyping from text descriptions
- The diagram is self-contained and will not be modified programmatically
- Human readability of the source format is more important than editability
- The diagram type maps naturally to Mermaid syntax (sequence diagrams, ER diagrams)

### 2.5 Mermaid via URL and MCP

Mermaid can also be passed via URL parameter:
```json
{"type": "mermaid", "compressed": true, "data": "BASE64_DEFLATED_MERMAID_TEXT"}
```

And via the official MCP tool server's `open_drawio_mermaid` tool, which opens the rendered diagram in the Draw.io editor.

---

## 3. Template System

### 3.1 How Templates Work

Draw.io templates are pre-built diagram files (`.drawio` / XML) that serve as starting points for new diagrams. When a user creates a new diagram, the template library presents categorized options.

### 3.2 Built-in Template Categories

Draw.io ships with templates in these categories:

- **Basic** — simple flowcharts, grids, mind maps
- **Business** — org charts, value chains, SWOT analysis
- **Charts** — bar, pie, line charts
- **Engineering** — circuit diagrams, floor plans
- **Flowcharts** — process flows, decision trees, swimlanes
- **Mindmaps** — mind map layouts
- **Mockups** — wireframes, UI mockups
- **Network** — network topology, rack diagrams
- **Software** — UML class, sequence, activity, ER diagrams
- **Tables** — data tables, comparison grids
- **Other** — miscellaneous templates

### 3.3 Template XML Structure

A template is simply a valid `.drawio` file. The XML structure is identical to any Draw.io diagram:

```xml
<mxfile>
  <diagram id="template-1" name="Template Page">
    <mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="850" pageHeight="1100">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Template shapes and edges -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 3.4 Custom Templates

**For Confluence Cloud:**
Custom templates are stored in the "draw.io Configurations space" as child pages. Each template category is a child page, and each template consists of three files: `.drawio`, `.svg` preview, and `.png` preview. Administrators manage access via read permissions on the Configurations space.

**For Desktop / Web:**
Custom template libraries can be configured via the Draw.io configuration JSON. Templates are loaded from configured URLs or local file paths.

**For Programmatic Use:**
Templates can be loaded via the embed mode `template` action:
```json
{"action": "template"}
```
With `callback: true`, this returns `{event: 'template', xml: '...', blank: boolean, name: '...'}`.

---

## 4. Export Formats

### 4.1 Format Overview

| Format | Embeds XML | Editable | Vector | Best For |
|--------|-----------|----------|--------|----------|
| PNG | Optional (xmlpng) | With embedded XML | No | Documents, presentations |
| SVG | Optional (xmlsvg) | With embedded XML | Yes | Web, animated connectors |
| JPEG | No | No | No | Web pages (small size) |
| WebP | No | No | No | Web (smallest size) |
| PDF | Optional | With embedded XML | Yes | Print, archival |
| HTML | No (references JS) | Via viewer library | N/A | Web embedding |
| XML/.drawio | Yes (native) | Always | N/A | Source format |

### 4.2 PNG Export

PNG export supports these parameters:
- **Scale** — zoom factor for the export
- **Border** — pixel border around the diagram
- **Transparent background** — removes the white background
- **Shadow** — includes drop shadows
- **Grid** — includes the editor grid
- **DPI** — resolution for print quality
- **Selection only** — exports only selected shapes

The `xmlpng` format embeds the full diagram XML inside the PNG file's metadata, allowing the PNG to be reopened and edited in Draw.io.

### 4.3 SVG Export

SVG export parameters:
- **embedImages** — inline images as data URIs vs. external references
- **scale** — zoom factor
- **layerIds** — export specific layers only
- **border** — pixel border
- **shadow** — include shadows
- **keepTheme** — preserve current theme
- **background** — background color

SVG supports **animated connectors** and preserves **hyperlinks**. The `xmlsvg` variant embeds the full diagram XML for re-editing.

### 4.4 PDF Export

PDF export generates a portable document. Optionally embeds diagram data for re-importing into Draw.io. Supports the same common parameters (border, background, grid, etc.).

### 4.5 HTML Export

HTML export creates a self-contained web page that uses the Draw.io JavaScript viewer library hosted on diagrams.net servers. This requires internet connectivity for display. Two variants exist: `html` and `html2`.

### 4.6 Programmatic Export via Embed Mode

The embed mode `export` action supports programmatic export:

```json
{"action": "export", "format": "svg"}
{"action": "export", "format": "xmlsvg"}
{"action": "export", "format": "png"}
{"action": "export", "format": "xmlpng"}
{"action": "export", "format": "html"}
{"action": "export", "format": "html2"}
```

PNG/XMLPNG additional parameters: `spin`, `message`, `scale`, `layerIds`, `pageId`, `currentPage`, `width`, `border`, `shadow`, `grid`, `keepTheme`, `transparent`, `background`, `size`.

SVG/XMLSVG additional parameters: `embedImages`, `scale`, `layerIds`, `border`, `shadow`, `keepTheme`, `background`.

---

## 5. URL Parameters

### 5.1 The `#create` Parameter

Draw.io supports opening diagrams via a URL with the `#create` fragment:

```
https://app.diagrams.net/?grid=0&pv=0#create=ENCODED_JSON
```

The `#create` value is a URL-encoded JSON object:

```json
{
  "type": "xml",
  "compressed": true,
  "data": "BASE64_DEFLATED_CONTENT"
}
```

The `type` field accepts three values:
- `"xml"` — mxGraph XML content
- `"csv"` — Draw.io CSV format (with directives)
- `"mermaid"` — Mermaid syntax

### 5.2 URL Generation (JavaScript)

```javascript
function generateDrawioEditUrl(xml) {
  var encoded = encodeURIComponent(xml);
  var compressed = pako.deflateRaw(encoded);
  var base64 = btoa(Array.from(compressed, function(b) {
    return String.fromCharCode(b);
  }).join(""));
  var createObj = { type: "xml", compressed: true, data: base64 };
  return "https://app.diagrams.net/?pv=0&grid=0#create="
    + encodeURIComponent(JSON.stringify(createObj));
}
```

### 5.3 Editor Query Parameters

| Parameter | Values | Effect |
|-----------|--------|--------|
| `lightbox=1` | 0/1 | Read-only lightbox view |
| `edit=_blank` | `_blank` | Edit button opens editor in new tab |
| `dark=1` | 0/1 | Enable dark mode |
| `grid=0` | 0/1 | Show/hide grid |
| `pv=0` | 0/1 | Show/hide page view selector |
| `border=10` | pixels | Border size |
| `embed=1` | 0/1 | Enable embed mode |
| `spin=1` | 0/1 | Show loading spinner |
| `libraries=1` | 0/1 | Enable shape libraries panel |
| `noSaveBtn=1` | 0/1 | Replace Save with Save and Exit |
| `saveAndExit=1` | 0/1 | Add separate Save and Exit button |
| `noExitBtn=1` | 0/1 | Hide Exit button |
| `proto=json` | `json` | Enable JSON protocol for messaging |
| `configure=1` | 0/1 | Send configure event before initialization |

---

## 6. Programmatic Access

### 6.1 Draw.io Embed Mode (postMessage API)

The embed mode transforms Draw.io into an embeddable editor component via iframe. It is hosted at `https://embed.diagrams.net` and activated with the `embed=1` URL parameter.

**Communication Protocol:**
1. Parent page creates iframe pointing to `https://embed.diagrams.net/?embed=1&proto=json`
2. Editor sends `{event: 'init'}` when ready
3. Parent responds with load action containing diagram data
4. Editor sends save/autosave events when user saves
5. Parent processes and acknowledges

**Load Action:**
```json
{"action": "load", "xml": "<mxGraphModel>...</mxGraphModel>"}
```

The load action also accepts descriptors for CSV and Mermaid:
```json
{"action": "load", "descriptor": {"format": "csv", "data": "..."}}
{"action": "load", "descriptor": {"format": "mermaid", "data": "..."}}
```

**Supported input formats for load:**
- Standard Draw.io XML
- SVG or PNG files with embedded XML
- PNG/SVG data URIs (base64 or UTF-8)
- Visio files (`data:application/vnd.visio;base64,...`)
- Lucidchart and Gliffy JSON strings

**Key Actions (Host to Editor):**

| Action | Purpose | Example |
|--------|---------|---------|
| `load` | Load diagram data | `{"action": "load", "xml": "..."}` |
| `merge` | Merge XML into current diagram | `{"action": "merge", "xml": "..."}` |
| `export` | Export in specified format | `{"action": "export", "format": "svg"}` |
| `template` | Open template dialog | `{"action": "template"}` |
| `layout` | Apply layout algorithm | `{"action": "layout", "layouts": [...]}` |
| `status` | Set status bar message | `{"action": "status", "message": "..."}` |
| `spinner` | Show/hide spinner | `{"action": "spinner", "show": true}` |
| `dialog` | Show dialog box | `{"action": "dialog", "title": "..."}` |
| `prompt` | Show input prompt | `{"action": "prompt", "title": "..."}` |
| `textContent` | Get text content of diagram | `{"action": "textContent"}` |
| `viewport` | Set viewport position/scale | `{"action": "viewport", "viewport": {...}}` |

**Key Events (Editor to Host):**

| Event | Trigger | Data |
|-------|---------|------|
| `init` | Editor loaded | None |
| `save` | User saves | `{event: 'save', xml: '...'}` |
| `autosave` | Auto-save triggered | `{event: 'autosave', xml: '...'}` |
| `exit` | User exits | `{event: 'exit', modified: boolean}` |
| `merge` | Merge completed | `{event: 'merge', error: null}` |
| `prompt` | User responded to prompt | `{event: 'prompt', value: '...'}` |
| `template` | Template selected | `{event: 'template', xml: '...'}` |
| `openLink` | Link clicked | `{event: 'openLink', href: '...'}` |
| `textContent` | Text content retrieved | `{event: 'textContent', data: '...'}` |

### 6.2 Draw.io Viewer Library (Read-Only Embedding)

For non-editable display of diagrams in web pages:

```html
<script src="https://viewer.diagrams.net/js/viewer-static.min.js" async></script>

<div class="mxgraph" data-mxgraph='{"highlight":"#0000ff","nav":true,"resize":true,"toolbar":"zoom layers tags","xml":"<mxGraphModel>...</mxGraphModel>"}'></div>
```

Configuration options in the `data-mxgraph` JSON:
- `xml` — uncompressed diagram XML
- `highlight` — hover highlight color
- `nav` — enable navigation controls
- `resize` — allow viewer resizing
- `toolbar` — space-separated button list (e.g., `"zoom layers tags"`)
- `dark-mode` — set to `"auto"` for system preference following

After dynamically adding diagram containers, call:
```javascript
GraphViewer.processElements();
```

### 6.3 MCP Server APIs

See [Section 10: MCP Server Comparison](#10-mcp-server-comparison) for detailed coverage of the `drawio-mcp-server` CRUD API and `@drawio/mcp` official tools.

---

## 7. Compression / Decompression

### 7.1 How Draw.io Compresses XML

Draw.io uses a three-step compression pipeline:

1. **URL-encode** the XML string with `encodeURIComponent()`
2. **Deflate** the encoded string using raw DEFLATE (no zlib headers)
3. **Base64-encode** the compressed bytes

**Compression (JavaScript using pako):**
```javascript
function compressDrawioXml(xml) {
  var encoded = encodeURIComponent(xml);
  var compressed = pako.deflateRaw(encoded);
  return btoa(Array.from(compressed, function(b) {
    return String.fromCharCode(b);
  }).join(""));
}
```

**Decompression reverses the pipeline:**
1. Base64-decode the string
2. Raw DEFLATE decompress
3. URL-decode with `decodeURIComponent()`

### 7.2 Why AI MUST Generate Uncompressed XML

The official documentation explicitly states: *"Compressed XML uses more tokens (the Base64 encoding is larger than the raw XML), is not human-readable, and cannot be validated or debugged without decompression."*

| Aspect | Uncompressed XML | Compressed (Base64) |
|--------|-----------------|-------------------|
| Token count | LOWER | HIGHER (Base64 bloat) |
| Human-readable | YES | NO |
| Debuggable | YES — inspect directly | NO — requires decompression |
| Validatable | YES — against mxfile.xsd | NO — must decompress first |
| Editable | YES — text editor | NO — binary-like |

**Rule: ALWAYS generate uncompressed XML.** Only compress when:
- Passing diagrams via URL `#create` parameter (required)
- File size is a critical constraint (rare)

### 7.3 Tools for Conversion

The Draw.io Tools page at `jgraph.github.io/drawio-tools/` provides online utilities for:
- Compressing/decompressing Draw.io XML
- Base64 encoding/decoding
- URL encoding/decoding
- Converting between compressed and uncompressed formats

---

## 8. Placeholder System

### 8.1 Overview

Draw.io supports a placeholder system that substitutes `%variableName%` tokens in labels with values from properties and variables. This enables dynamic, data-driven diagrams.

### 8.2 Enabling Placeholders

To enable placeholder substitution on a cell, set `placeholders="1"` on the containing `<UserObject>` or `<object>` element:

```xml
<UserObject id="2" label="Project: %project% v%version%" placeholders="1">
  <mxCell style="text;html=1;align=center;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="200" height="40" as="geometry" />
  </mxCell>
</UserObject>
```

### 8.3 File-Level Variables

Variables defined at the file level are available to all cells in all pages:

```xml
<mxfile vars='{"project":"Atlas","version":"2.1","author":"Jane Doe"}'>
  <diagram id="page-1" name="Page-1">
    ...
  </diagram>
</mxfile>
```

**IMPORTANT:** File-level variables require the full `<mxfile>` wrapper. They are NOT available with the simplified `<mxGraphModel>`-only format.

### 8.4 Cell-Level Properties

Properties defined directly on the `<UserObject>` or `<object>` element act as cell-scoped variables:

```xml
<object id="3" label="Server: %hostname%" placeholders="1" hostname="web-prod-01" env="production">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="200" y="200" width="160" height="80" as="geometry" />
  </mxCell>
</object>
```

### 8.5 Resolution Hierarchy

When a placeholder `%name%` is resolved, Draw.io searches in this order (first match wins):

1. **Cell attributes** — properties on the `<object>` or `<UserObject>` itself
2. **Parent container attributes** — properties on the parent group or swimlane
3. **Layer cell attributes** — properties on the layer cell (`parent="0"`)
4. **Root container cell** — properties on `<mxCell id="0" />`
5. **File-level `vars`** — JSON variables on the `<mxfile>` element

### 8.6 Complete Scoping Example

```xml
<mxfile vars='{"env":"staging"}'>
  <diagram id="page-1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <object id="1" label="Production" env="production">
          <mxCell parent="0" />
        </object>
        <object id="2" label="Environment: %env%" placeholders="1">
          <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

In this example, cell `id="2"` has `parent="1"`. The parent object (`id="1"`) has `env="production"`. Because parent attributes (level 2) take precedence over file-level vars (level 5), the rendered label shows **"Environment: production"** — NOT "staging".

### 8.7 Use Cases for Placeholders

- **Data-driven diagrams** — display metadata from external sources
- **Reusable templates** — change variables at file level, all shapes update
- **Environment indicators** — show deployment environment, version, dates
- **Tooltip enrichment** — cell properties show as tooltips on hover

---

## 9. Embed Modes

### 9.1 Web Embedding (Viewer Library)

For read-only display on any web page:

```html
<script src="https://viewer.diagrams.net/js/viewer-static.min.js" async></script>
<div class="mxgraph" data-mxgraph='{"highlight":"#0000ff","nav":true,"resize":true,"toolbar":"zoom layers tags","xml":"DIAGRAM_XML"}'></div>
```

### 9.2 Web Embedding (Full Editor via iframe)

For editable embedding using the postMessage API:

```html
<iframe src="https://embed.diagrams.net/?embed=1&proto=json&spin=1" style="width:100%;height:600px;border:none;"></iframe>
```

See [Section 6.1](#61-draw-io-embed-mode-postmessage-api) for the full communication protocol.

### 9.3 Confluence

Draw.io is deeply integrated with Confluence (Cloud and Data Center):
- Native draw.io macro for embedding diagrams
- Custom template libraries via the Configurations space
- Diagrams stored as Confluence attachments
- Collaborative editing support
- Version history tied to Confluence page versions

### 9.4 GitHub

Draw.io diagrams can be embedded in GitHub in several ways:
- **VS Code extension** — edit `.drawio` files directly in VS Code (also works with GitHub Codespaces)
- **GitHub Actions** — export diagrams to PNG/SVG as part of CI/CD
- **README embedding** — reference exported PNG/SVG in markdown files
- **`.drawio.svg`** — SVG files with embedded Draw.io XML that render in GitHub and remain editable

### 9.5 VS Code

The **Draw.io Integration** VS Code extension (by Henning Dieterichs) provides:
- Native editor for `.drawio`, `.drawio.svg`, and `.drawio.png` files
- Side-by-side editing with code
- Supports all Draw.io features
- Files with `.drawio.svg` extension render as SVG in previews but open in the Draw.io editor

### 9.6 Notion

Notion does not have a native Draw.io integration. Diagrams are typically embedded via:
- Export to PNG/SVG and upload as image
- Embed the Draw.io viewer URL in a Notion embed block
- Use the HTML export URL with `lightbox=1` parameter

### 9.7 Configuration for Embed

To hide all editor UI buttons (for a minimal embed experience):
```
?saveAndExit=0&noSaveBtn=1&noExitBtn=1
```

To configure the editor before initialization (e.g., custom fonts):
```json
{"action": "configure", "config": {"defaultFonts": ["Humor Sans", "Comic Sans MS"]}}
```

This requires the `configure=1` URL parameter.

---

## 10. MCP Server Comparison

### 10.1 Overview

Three MCP server options exist for programmatic Draw.io integration:

| Server | Package | Author | Stars | License |
|--------|---------|--------|-------|---------|
| Official (@drawio/mcp) | `@drawio/mcp` | jgraph | 1400+ | Apache-2.0 |
| drawio-mcp-server | `drawio-mcp-server` | lgazo | 1100+ | Open source |
| Custom (future) | N/A | This project | N/A | N/A |

### 10.2 Official @drawio/mcp (jgraph)

**Installation:** `npx -y @drawio/mcp`

**Four integration methods:**

| Method | Output | XML | CSV | Mermaid | Requires |
|--------|--------|-----|-----|---------|----------|
| MCP App Server | Inline iframes | YES | NO | NO | MCP Apps extension |
| MCP Tool Server | Opens in editor | YES | YES | YES | npm |
| Skill + CLI | `.drawio` files + export | YES | YES | YES | Draw.io Desktop CLI |
| Project Instructions | Clickable URLs | YES | YES | YES | Nothing |

**MCP Tool Server tools:**
- `open_drawio_xml` — opens XML diagram in Draw.io editor
- `open_drawio_csv` — converts CSV to diagram and opens
- `open_drawio_mermaid` — converts Mermaid to diagram and opens

**Key characteristics:**
- Official product from the Draw.io makers (jgraph)
- Lightweight — opens diagrams in the editor but does NOT provide CRUD operations
- No ability to read back diagram state or modify individual cells
- Best for "generate and display" workflows

### 10.3 drawio-mcp-server (lgazo)

**Installation:** `npx -y drawio-mcp-server --editor`

**Two deployment modes:**

| Mode | Flag | How It Works |
|------|------|-------------|
| Built-in Editor | `--editor` | Hosts Draw.io at `http://localhost:3000/` |
| Browser Extension | (no flag) | Connects to Draw.io in browser via extension |

**Capabilities:**
- **Full CRUD operations** — create, read, update, delete shapes and edges
- **Layer management** — create layers, switch layers, move elements between layers
- **Diagram inspection** — read shapes, layers, cell properties
- **Label manipulation** — modify text content of shapes
- **Real-time editing** — changes appear immediately in the hosted editor

**Key characteristics:**
- v1.8.0+, TypeScript/JavaScript
- 71 commits, actively maintained
- Built-in editor mode provides self-contained experience
- Enables AI agents to iteratively build and modify diagrams
- Best for "programmatic manipulation" workflows

### 10.4 Custom MCP Server (Future — This Project)

The planned custom MCP server (in the `mcp-server/` directory) will expose 18 tools:

| Category | Tools |
|----------|-------|
| Generation | `create_diagram`, `add_cell`, `add_connection`, `add_page` |
| Editing | `edit_cell`, `delete_cell`, `move_cell`, `restyle` |
| Query | `read_diagram`, `list_cells`, `get_cell` |
| Conversion | `from_csv`, `from_mermaid`, `to_svg`, `to_png` |
| Templates | `from_template`, `list_templates` |
| Validation | `validate` |

### 10.5 Decision Matrix: Which MCP Server to Use

| Scenario | Recommended Server | Reason |
|----------|-------------------|--------|
| Quick diagram generation, no editing needed | Official (@drawio/mcp) | Lightweight, opens in editor |
| Iterative building with AI agent | drawio-mcp-server (lgazo) | Full CRUD, real-time editing |
| CSV data to diagram | Official (@drawio/mcp) | Native CSV support |
| Mermaid to diagram | Official (@drawio/mcp) | Native Mermaid support |
| Programmatic style changes | drawio-mcp-server (lgazo) | Can modify individual cells |
| Layer-based organization | drawio-mcp-server (lgazo) | Layer management tools |
| Validation and export | Custom (future) | Planned validation + export tools |
| Template-based generation | Custom (future) | Planned template tools |

### 10.6 Configuration (.mcp.json)

Both servers are configured in the project's `.mcp.json`:

```json
{
  "mcpServers": {
    "drawio-editor": {
      "command": "npx",
      "args": ["-y", "drawio-mcp-server", "--editor"]
    },
    "drawio-official": {
      "command": "npx",
      "args": ["-y", "@drawio/mcp"]
    }
  }
}
```

---

## Appendix A: Quick Reference — XML Structure

```xml
<mxfile vars='{"key":"value"}'>
  <diagram id="page-1" name="Page-1">
    <mxGraphModel dx="0" dy="0" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="850" pageHeight="1100"
                  math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Vertex (shape) -->
        <mxCell id="2" value="Label" style="rounded=1;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
        <!-- Edge (connection) -->
        <mxCell id="e1" value="" style="endArrow=classic;html=1;"
                edge="1" parent="1" source="2" target="3">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

## Appendix B: Quick Reference — AI Generation Rules

1. ALWAYS include the two structural cells: `<mxCell id="0"/>` and `<mxCell id="1" parent="0"/>`
2. ALWAYS use unique IDs within a diagram
3. ALWAYS set `vertex="1"` on shapes and `edge="1"` on connections (mutually exclusive)
4. ALWAYS use semicolon-separated `key=value;` pairs for styles
5. ALWAYS set matching `perimeter=` for non-rectangular shapes (e.g., `perimeter=ellipsePerimeter`)
6. ALWAYS use XML escaping for HTML in `value` attributes (`&lt;`, `&gt;`, `&amp;`, `&quot;`)
7. ALWAYS generate uncompressed XML
8. NEVER use compressed/Base64 format unless passing via URL parameter
9. Coordinate origin (0,0) is top-left; x increases rightward, y increases downward
10. Group children use relative coordinates to their parent, NOT canvas coordinates
