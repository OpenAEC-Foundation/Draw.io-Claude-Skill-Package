# Methods Reference: Template Implementation

Complete attribute and structure reference for Draw.io templates.

---

## 1. mxfile Wrapper Attributes

The `<mxfile>` element is the root of every template file.

| Attribute | Required | Example Value | Purpose |
|-----------|----------|---------------|---------|
| `host` | Yes | `"app.diagrams.net"` | Identifies the editor |
| `modified` | No | `"2024-01-01T00:00:00.000Z"` | Last modification timestamp |
| `agent` | No | `"Claude"` | User agent that created the file |
| `type` | No | `"device"` | Storage type: `device`, `google`, `onedrive`, `dropbox` |
| `version` | No | `"21.0.0"` | Draw.io version |

Minimal valid `<mxfile>`:

```xml
<mxfile host="app.diagrams.net">
  <diagram id="d1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 2. diagram Element Attributes

Each page in a template is a `<diagram>` element.

| Attribute | Required | Example Value | Purpose |
|-----------|----------|---------------|---------|
| `id` | Yes | `"flowchart-01"` | Unique identifier for the page |
| `name` | Yes | `"Process Flow"` | Tab name shown in the editor |

---

## 3. mxGraphModel Attributes

Controls the canvas and editor behavior.

| Attribute | Default | Recommended | Purpose |
|-----------|---------|-------------|---------|
| `dx` | `0` | `1000` | Horizontal scroll offset |
| `dy` | `0` | `600` | Vertical scroll offset |
| `grid` | `0` | `1` | Enable grid display |
| `gridSize` | `10` | `10` | Grid spacing in pixels |
| `guides` | `0` | `1` | Enable alignment guides |
| `tooltips` | `1` | `1` | Show tooltips on hover |
| `connect` | `1` | `1` | Enable connection handling |
| `arrows` | `1` | `1` | Show arrows on connections |
| `fold` | `1` | `1` | Enable container folding |
| `page` | `0` | `1` | Show page boundaries |
| `pageScale` | `1` | `1` | Page scale factor |
| `pageWidth` | `850` | `1169` | Page width (A4 landscape) |
| `pageHeight` | `1100` | `827` | Page height (A4 landscape) |
| `math` | `0` | `0` | Enable LaTeX math rendering |
| `shadow` | `0` | `0` | Enable drop shadows |
| `background` | none | `"#ffffff"` | Canvas background color |

---

## 4. Template Placeholder Conventions

Use consistent placeholder notation for content that users MUST replace:

| Pattern | Use For | Example |
|---------|---------|---------|
| `[Text]` | Shape labels | `value="[Process Name]"` |
| `[Text 1]`, `[Text 2]` | Sequential items | `value="[Step 1]"`, `value="[Step 2]"` |
| `[Category: Detail]` | Categorized items | `value="[Role: Manager]"` |
| Fixed text | Labels that NEVER change | `value="Start"`, `value="End"` |

---

## 5. Template Edge Styles by Diagram Type

| Diagram Type | Edge Style | Arrow | Example |
|-------------|-----------|-------|---------|
| Flowchart | `edgeStyle=orthogonalEdgeStyle;` | `endArrow=classic;` | Directed process flow |
| Org Chart | none (straight line) | `endArrow=none;` | Hierarchy lines |
| Network | none (straight line) | `endArrow=none;` | Connections between nodes |
| UML Class | `edgeStyle=orthogonalEdgeStyle;` | Varies by relationship | Associations, inheritance |
| Mind Map | `edgeStyle=entityRelationEdgeStyle;` | `endArrow=none;` | Organic branches |
| ER Diagram | `edgeStyle=orthogonalEdgeStyle;` | `endArrow=ERmany;` or similar | Entity relationships |
| BPMN | `edgeStyle=orthogonalEdgeStyle;` | `endArrow=classic;` | Sequence flows |

---

## 6. Coordinate Strategies for Templates

### Centered Layout (Single Column)

Center shapes on x=260 (for shapes of width 120-140):

```
x = (pageWidth / 2) - (shapeWidth / 2)
y = previous_y + previous_height + gap (40px)
```

### Grid Layout (Multiple Columns)

For templates with columns (e.g., comparison tables, swimlanes):

```
Column 1: x = 40
Column 2: x = 300
Column 3: x = 560
Row gap: 80px
Column gap: 260px (includes shape width 200 + margin 60)
```

### Tree Layout (Org Charts)

Calculate horizontal spread based on leaf count:

```
Level 0 (root): x = total_width / 2 - shape_width / 2
Level 1: evenly distribute across total_width
Level 2: center under parent
Vertical gap between levels: 80px
```

---

## 7. Style Strings for Common Template Shapes

### Container (Group/Swimlane Header)

```
swimlane;startSize=30;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

### Title Block

```
text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=18;fontStyle=1;
```

### Separator Line

```
line;strokeWidth=2;html=1;fillColor=none;strokeColor=#666666;
```

### Note / Annotation

```
shape=note;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;size=15;
```

### Image Placeholder

```
shape=image;imageAspect=0;aspect=fixed;verticalLabelPosition=bottom;verticalAlign=top;html=1;image=;
```

---

## 8. Compressed XML Format

Draw.io files MAY store `mxGraphModel` content as compressed (deflate + base64) text inside the `<diagram>` element instead of raw XML. When creating templates programmatically, ALWAYS use uncompressed XML for readability. The editor accepts both formats.

Compressed format (for reference only):

```xml
<mxfile host="app.diagrams.net">
  <diagram id="d1" name="Page-1">
    jZLBbsMgDIafJtcKktFeTbtu0i7dObLgJmgEIsxKs6efGUhStaq0C/j77R/bkORVfz6Y1h8/0IJO
    ...base64 encoded deflated XML...
  </diagram>
</mxfile>
```

NEVER generate compressed templates. ALWAYS output raw XML.
