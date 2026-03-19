# Methods Reference: Flowchart Implementation

Complete style strings and attribute reference for all flowchart shapes and connections.

---

## 1. Shape Styles

### Process (Rectangle)

```
rounded=0;whiteSpace=wrap;html=1;
```

Standard rectangular task block. Add fill/stroke colors as needed:

```
rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

### Decision (Rhombus / Diamond)

```
rhombus;whiteSpace=wrap;html=1;
```

ALWAYS use `rhombus` for conditional branching. The shape renders as a diamond rotated 45 degrees. Recommended dimensions: 120 x 80 (wider than tall produces a readable diamond).

With colors:

```
rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;
```

### Terminator (Start/End — Stadium Shape)

```
rounded=1;whiteSpace=wrap;html=1;arcSize=50;
```

The `arcSize=50` value is critical — it produces the ISO 5807 stadium (pill) shape. Lower values produce a rounded rectangle instead. Recommended dimensions: 120 x 40.

Start color:

```
rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;
```

End color:

```
rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;
```

### Data I/O (Parallelogram)

```
shape=parallelogram;whiteSpace=wrap;html=1;
```

Represents input/output operations. The slanted sides visually distinguish I/O from process steps.

```
shape=parallelogram;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;
```

### Document

```
shape=document;whiteSpace=wrap;html=1;
```

Renders a rectangle with a wavy bottom edge. Used for document outputs (reports, invoices, printouts).

```
shape=document;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;
```

### Predefined Process (Subprocess)

```
shape=process;whiteSpace=wrap;html=1;
```

Renders as a rectangle with double vertical bars on the left and right sides. Used to reference a subprocess defined elsewhere.

```
shape=process;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

### Manual Input

```
shape=manualInput;whiteSpace=wrap;html=1;
```

Renders as a rectangle with a sloped top edge (higher on the right). Used for steps where a user manually enters data.

```
shape=manualInput;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;
```

### Preparation (Hexagon)

```
shape=hexagon;whiteSpace=wrap;html=1;
```

Six-sided shape used for setup or initialization steps. The `perimeter=hexagonPerimeter2` attribute is automatically applied by Draw.io.

```
shape=hexagon;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;
```

### Database (Cylinder)

```
shape=cylinder3;whiteSpace=wrap;html=1;
```

Renders as a 3D cylinder. Used for data stores and databases. Recommended dimensions: 120 x 80 (taller than wide for visual clarity).

```
shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;
```

---

## 2. Edge Styles

### Standard Flowchart Edge

```
edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;
```

Produces right-angle connector lines with a filled arrowhead. This is the default edge style for flowcharts.

### Labeled Edge (Decision Branch)

Add a `value` attribute to the `mxCell` element:

```xml
<mxCell id="e1" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="next">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

The label renders inline on the edge. ALWAYS use this pattern for decision branches.

### Curved Edge (Alternative)

```
edgeStyle=orthogonalEdgeStyle;curved=1;endArrow=classic;html=1;
```

Adds rounded corners to orthogonal edges. Use when the diagram has many crossing edges for improved readability.

### Straight Edge (No Routing)

```
endArrow=classic;html=1;
```

Omitting `edgeStyle` produces a straight-line connector. Use ONLY when shapes are directly aligned (same x or same y coordinate).

---

## 3. Edge Geometry

### Standard (Auto-Routed)

```xml
<mxGeometry relative="1" as="geometry" />
```

ALWAYS use `relative="1"` for edge geometry. Draw.io auto-routes the connector between source and target.

### With Exit/Entry Points

Control which side of a shape the edge connects to:

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;"
        edge="1" parent="1" source="dec1" target="alt_step">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

Exit/entry point coordinates (0-1 range):
- **Top center:** `x=0.5; y=0`
- **Right center:** `x=1; y=0.5`
- **Bottom center:** `x=0.5; y=1`
- **Left center:** `x=0; y=0.5`

---

## 4. Layout Attributes

### mxGraphModel Settings for Flowcharts

| Attribute | Recommended Value | Purpose |
|-----------|------------------|---------|
| `grid` | `1` | Enable grid for alignment |
| `gridSize` | `10` | 10px grid spacing |
| `guides` | `1` | Enable alignment guides |
| `connect` | `1` | Enable connection handling |
| `arrows` | `1` | Show connection arrows |
| `pageWidth` | `1169` | A4 landscape width |
| `pageHeight` | `827` | A4 landscape height |

### Spacing Guidelines

| Between | Distance |
|---------|----------|
| Sequential shapes (vertical) | 40px gap |
| Decision to branch target (horizontal) | 60px gap |
| Parallel branches (horizontal) | 200px apart |
| Shape and page edge | 40px minimum margin |

---

## 5. Text Formatting in Labels

### HTML Labels

When `html=1` is in the style, the `value` attribute supports HTML:

```xml
<mxCell id="step1" value="Validate&lt;br&gt;Order Data" ... />
```

Common HTML in labels:
- `&lt;br&gt;` — Line break
- `&lt;b&gt;text&lt;/b&gt;` — Bold
- `&lt;i&gt;text&lt;/i&gt;` — Italic
- `&lt;font color=&quot;#FF0000&quot;&gt;text&lt;/font&gt;` — Colored text

### Font Styling via Style String

| Property | Values | Example |
|----------|--------|---------|
| `fontSize` | Number | `fontSize=14;` |
| `fontStyle` | Bitmask: 1=bold, 2=italic, 4=underline | `fontStyle=1;` (bold) |
| `fontColor` | Hex color | `fontColor=#333333;` |
| `align` | `left`, `center`, `right` | `align=center;` |
| `verticalAlign` | `top`, `middle`, `bottom` | `verticalAlign=middle;` |
