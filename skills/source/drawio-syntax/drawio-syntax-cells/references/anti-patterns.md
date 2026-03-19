# Anti-Patterns: Draw.io Syntax Cells

What NOT to do when creating cells in Draw.io XML, with explanations of why each pattern fails.

---

## AP-01: Missing vertex="1" on a Shape

### WRONG

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
        parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `vertex="1"`, Draw.io does NOT recognize the cell as a shape. The cell exists in the model but is invisible and cannot be connected to. ALWAYS set `vertex="1"` on every shape.

---

## AP-02: Missing edge="1" on a Connector

### WRONG

```xml
<mxCell id="4" value="" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" value="" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Without `edge="1"`, Draw.io renders the cell as a shape (or ignores it entirely), not as a connector. The `source` and `target` attributes are ignored. ALWAYS set `edge="1"` on every connector.

---

## AP-03: Setting Both vertex="1" AND edge="1"

### WRONG

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" edge="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

A cell is EITHER a vertex OR an edge, NEVER both. Setting both produces unpredictable rendering behavior. Draw.io treats the cell inconsistently — it may render as a shape that ignores connections, or fail to display at all.

---

## AP-04: Missing parent Attribute

### WRONG

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `parent`, the cell has no position in the hierarchy. Draw.io cannot determine which layer the cell belongs to and will NOT render it. ALWAYS set `parent` to `"1"` (default layer) or the ID of a container/layer.

---

## AP-05: Edge Referencing Non-Existent Source/Target

### WRONG

```xml
<mxCell id="2" value="Box" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="3" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="99" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Box A" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="3" value="Box B" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="350" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Cell id="99" does not exist. The edge renders as a broken connector — it draws from the source vertex but the target endpoint floats at position (0,0) or disappears entirely. ALWAYS verify that `source` and `target` IDs reference existing vertex cells.

---

## AP-06: Unescaped HTML in value Attribute

### WRONG

```xml
<mxCell id="2" value="<b>Title</b><br>Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="&lt;b&gt;Title&lt;/b&gt;&lt;br&gt;Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Raw `<b>`, `<br>`, etc. inside an XML attribute makes the XML malformed. XML parsers interpret `<b>` as the start of a new XML element, not as HTML content. The file will NOT parse and Draw.io will refuse to open it. ALWAYS XML-escape all HTML characters in `value` attributes.

---

## AP-07: HTML Label Without html=1 in Style

### WRONG

```xml
<mxCell id="2" value="&lt;b&gt;Title&lt;/b&gt;&lt;br&gt;Subtitle"
        style="rounded=1;whiteSpace=wrap;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="&lt;b&gt;Title&lt;/b&gt;&lt;br&gt;Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `html=1` in the style, Draw.io renders the value as plain text. The user sees the literal escaped HTML tags (`<b>Title</b>`) instead of bold formatting. ALWAYS include `html=1` when using HTML in labels.

---

## AP-08: Putting id and value on mxCell When Using object Wrapper

### WRONG

```xml
<object id="srv1" label="Web Server" ip="10.0.1.10">
  <mxCell id="srv1" value="Web Server"
          style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="200" y="100" width="120" height="60" as="geometry" />
  </mxCell>
</object>
```

### RIGHT

```xml
<object id="srv1" label="Web Server" ip="10.0.1.10">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="200" y="100" width="120" height="60" as="geometry" />
  </mxCell>
</object>
```

### Why It Fails

When using `<object>`, the `id` and display text (`label`) belong on the wrapper element. Duplicating `id` on the inner mxCell creates a conflict (two elements with the same ID). Putting `value` on the mxCell when `label` is on `<object>` creates ambiguity about which text to display. ALWAYS put `id` and `label` on `<object>` ONLY; NEVER put `id` or `value` on the inner mxCell.

---

## AP-09: Container Children Using Absolute Coordinates

### WRONG

```xml
<mxCell id="10" value="Group" style="rounded=1;whiteSpace=wrap;html=1;container=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="11" value="Child" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="220" y="230" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="10" value="Group" style="rounded=1;whiteSpace=wrap;html=1;container=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="11" value="Child" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="20" y="30" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

When a cell has a parent container, its geometry coordinates are RELATIVE to the parent's top-left corner. Using absolute canvas coordinates (220, 230) positions the child far outside the visible container bounds (it would render at parent.x + 220 = 420, parent.y + 230 = 430 — outside the 300x200 container). ALWAYS use relative coordinates for children of containers and groups.

---

## AP-10: Missing Perimeter on Non-Rectangular Shapes

### WRONG

```xml
<mxCell id="2" value="Decision" style="shape=rhombus;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="120" height="80" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Decision" style="shape=rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="120" height="80" as="geometry" />
</mxCell>
```

### Why It Fails

Without the matching `perimeter` value, edges connect to the shape using the default rectangular perimeter calculation. This means connectors attach to the invisible rectangular bounding box, NOT to the diamond's actual edges. The result is visible gaps or overlapping arrows. ALWAYS pair non-rectangular shapes with their matching perimeter.

---

## AP-11: Using placeholders="1" Without object Wrapper

### WRONG

```xml
<mxCell id="2" value="Server: %name%" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="200" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<object id="2" label="Server: %name%" placeholders="1" name="web-01">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="200" height="60" as="geometry" />
  </mxCell>
</object>
```

### Why It Fails

Placeholder substitution requires two things: (1) `placeholders="1"` on the element or an ancestor, and (2) the variable defined as an attribute. Plain `<mxCell>` does not support `placeholders` as an attribute, and `%name%` on a plain mxCell renders as the literal text "%name%". ALWAYS use `<object>` wrapper with `placeholders="1"` for variable substitution.

---

## AP-12: Duplicate Cell IDs

### WRONG

```xml
<mxCell id="2" value="Box A" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="2" value="Box B" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Box A" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="3" value="Box B" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Cell IDs MUST be unique across the entire file (all pages). Duplicate IDs cause Draw.io to overwrite the first cell with the second, losing content. Edges referencing the duplicated ID connect to an unpredictable cell. ALWAYS use unique IDs — sequential integers are the safest approach.

---

## AP-13: Edge Without relative="1" on Geometry

### WRONG

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Edge geometry ALWAYS requires `relative="1"`. Without it, Draw.io interprets the geometry as absolute vertex positioning, causing the edge label to render at unexpected coordinates and the edge routing to behave incorrectly. ALWAYS include `relative="1"` on edge geometry.
