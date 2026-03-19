# Methods Reference: Mermaid Conversion

Complete reference for all Mermaid-to-Draw.io conversion methods and their parameters.

---

## 1. MCP Tool: open_drawio_mermaid

The primary programmatic method for Mermaid conversion.

### Tool Signature

```
open_drawio_mermaid(
  content: string,    // REQUIRED — Mermaid diagram definition
  dark?: string,      // OPTIONAL — "auto" | "true" | "false" (default: "auto")
  lightbox?: boolean  // OPTIONAL — read-only view (default: false)
)
```

### Parameter: content

The `content` parameter accepts raw Mermaid syntax as a string. Newlines MUST be represented as `\n` in the string value.

ALWAYS start with a valid Mermaid keyword:
- `graph TD`, `graph LR`, `flowchart TD`, `flowchart LR`
- `sequenceDiagram`
- `classDiagram`
- `stateDiagram-v2`
- `erDiagram`
- `gantt`
- `pie`
- `gitgraph`
- `mindmap`
- `requirementDiagram`
- `journey`
- `C4Context`
- `quadrantChart`

### Parameter: dark

Controls dark mode rendering:

| Value | Behavior |
|-------|----------|
| `"auto"` | Follows system/browser preference (default) |
| `"true"` | Forces dark background and light text |
| `"false"` | Forces light background and dark text |

### Parameter: lightbox

When `true`, the diagram opens in read-only lightbox mode — the user can zoom and pan but CANNOT edit. Use this for presentation or review scenarios.

---

## 2. URL Parameter Method

For embedding Mermaid diagrams via Draw.io URL.

### URL Format

```
https://app.diagrams.net/?p=data#<ENCODED_DESCRIPTOR>
```

### Descriptor Format

```json
{
  "type": "mermaid",
  "compressed": true,
  "data": "<BASE64_DEFLATED_MERMAID_TEXT>"
}
```

The `data` field contains the Mermaid text that has been:
1. Deflated (zlib compression)
2. Base64-encoded

### When to Use

Use URL parameters when generating shareable links or embedding diagrams in documentation. NEVER use this method for programmatic generation — use `open_drawio_mermaid` instead.

---

## 3. Embed Mode (postMessage API)

For applications that embed Draw.io in an iframe.

### Load Action

```json
{
  "action": "load",
  "descriptor": {
    "format": "mermaid",
    "data": "graph TD\n  A-->B\n  B-->C"
  }
}
```

### Requirements

- The Draw.io editor MUST be loaded in embed mode (`?embed=1`)
- The parent window sends the message via `postMessage`
- The `format` field MUST be `"mermaid"` (not `"type"`)

---

## 4. Manual UI Method

For human users inserting Mermaid via the Draw.io interface.

### Steps

1. Open Draw.io editor
2. Click **Arrange > Insert > Mermaid** (or `+` toolbar icon > Mermaid)
3. Paste Mermaid text into the dialog
4. Click **Insert**

### Editing After Insertion

1. Select the compound shape on the canvas
2. Press **Enter** (or double-click)
3. The Mermaid source text editor opens
4. Modify the Mermaid text
5. Click **Apply** — the entire shape re-renders

---

## 5. ELK Layout Engine

Mermaid supports the ELK (Eclipse Layout Kernel) for improved automatic layout.

### Activation

Add this directive at the top of the Mermaid source:

```
%%{init: {'flowchart': {'defaultRenderer': 'elk'}}}%%
```

### Full Example

```
%%{init: {'flowchart': {'defaultRenderer': 'elk'}}}%%
graph TD
  A[Start] --> B{Check}
  B -->|Yes| C[Process A]
  B -->|No| D[Process B]
  C --> E[End]
  D --> E
```

### When to Use ELK

- Complex flowcharts with many crossing edges
- Diagrams where the default Dagre layout produces excessive edge crossings
- NEVER use ELK for simple diagrams — it adds unnecessary processing overhead

---

## 6. Mermaid Node Shape Reference

### Flowchart Node Shapes

| Syntax | Shape | mxGraph Equivalent |
|--------|-------|-------------------|
| `[text]` | Rectangle | `rounded=0;whiteSpace=wrap;html=1;` |
| `(text)` | Rounded rectangle | `rounded=1;whiteSpace=wrap;html=1;` |
| `{text}` | Diamond/rhombus | `rhombus;whiteSpace=wrap;html=1;` |
| `([text])` | Stadium/pill | `rounded=1;whiteSpace=wrap;html=1;arcSize=50;` |
| `[[text]]` | Subroutine | `shape=process;whiteSpace=wrap;html=1;` |
| `[(text)]` | Cylinder | `shape=cylinder3;whiteSpace=wrap;html=1;` |
| `((text))` | Circle | `ellipse;whiteSpace=wrap;html=1;aspect=fixed;` |
| `>text]` | Asymmetric | `shape=callout;whiteSpace=wrap;html=1;` |
| `{{text}}` | Hexagon | `shape=hexagon;whiteSpace=wrap;html=1;` |

### Flowchart Arrow Types

| Syntax | Description |
|--------|-------------|
| `-->` | Solid line with arrow |
| `---` | Solid line without arrow |
| `-.->` | Dotted line with arrow |
| `==>` | Thick line with arrow |
| `--text-->` | Labeled solid arrow |
| `-->\|text\|` | Labeled solid arrow (alternate) |

### Sequence Diagram Arrow Types

| Syntax | Description |
|--------|-------------|
| `->>` | Solid line with arrowhead |
| `-->>` | Dashed line with arrowhead |
| `-x` | Solid line with cross |
| `--x` | Dashed line with cross |
| `-)` | Solid line with open arrow |
| `--)` | Dashed line with open arrow |

### ER Diagram Cardinality

| Syntax | Meaning |
|--------|---------|
| `\|\|` | Exactly one |
| `o\|` | Zero or one |
| `}\|` | One or more |
| `}o` | Zero or more |
