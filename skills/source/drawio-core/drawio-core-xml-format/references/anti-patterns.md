# Anti-Patterns: Draw.io Core XML Format

What NOT to do when generating Draw.io XML, with explanations of why each pattern fails.

---

## AP-01: Generating Compressed/Base64 Content

### WRONG

```xml
<diagram id="page-1" name="Page-1">
  dZHBDoMgDIafhmMJ6nS3qYfdnB5ckUlHE4EQ3HR7+lWpOpeYkP6k/b62hSS82Z+9bPQbcDAk
  JjtCToSQZJvSi4L9KKyjIBNKRxYbWJgP2BCLdpJDOwl0iMaptRm2aFtoXMBk3uM4Trui5+mv
</diagram>
```

### RIGHT

```xml
<diagram id="page-1" name="Page-1">
  <mxGraphModel>
    <root>
      <mxCell id="0" />
      <mxCell id="1" parent="0" />
      <!-- diagram content -->
    </root>
  </mxGraphModel>
</diagram>
```

### Why It Fails

LLMs cannot perform DEFLATE compression. Any attempt to generate Base64-encoded compressed content produces garbage data that Draw.io cannot decode. ALWAYS use uncompressed XML.

---

## AP-02: Missing Structural Cells

### WRONG

```xml
<mxGraphModel>
  <root>
    <mxCell id="2" value="Hello" style="rounded=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### RIGHT

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Hello" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

Draw.io requires `id="0"` (root container) and `id="1" parent="0"` (default layer) to build its internal cell hierarchy. Without them, the renderer has no layer to place content on and the diagram appears blank or throws errors.

---

## AP-03: Duplicate Cell IDs

### WRONG

```xml
<mxCell id="2" value="Box A" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="2" value="Box B" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Box A" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="3" value="Box B" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Draw.io uses IDs as dictionary keys in its internal model. Duplicate IDs cause the second cell to overwrite the first, resulting in missing shapes. IDs MUST be unique across the entire file, including across pages.

---

## AP-04: Setting Both vertex="1" and edge="1"

### WRONG

```xml
<mxCell id="2" value="Something" vertex="1" edge="1" parent="1"
        style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

Choose one:

```xml
<!-- As a vertex (shape) -->
<mxCell id="2" value="Something" vertex="1" parent="1"
        style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>

<!-- OR as an edge (connector) -->
<mxCell id="2" value="Something" edge="1" source="3" target="4" parent="1"
        style="edgeStyle=orthogonalEdgeStyle;html=1;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

A cell is EITHER a vertex OR an edge. Setting both produces undefined behavior in Draw.io's rendering engine. The cell type determines how geometry is interpreted, how connections work, and how the cell is drawn.

---

## AP-05: Edge Referencing Non-Existent Source/Target

### WRONG

```xml
<mxCell id="2" value="Box" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="3" edge="1" source="2" target="99" parent="1"
        style="edgeStyle=orthogonalEdgeStyle;html=1;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Box A" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="3" value="Box B" vertex="1" parent="1" style="rounded=1;whiteSpace=wrap;html=1;">
  <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
</mxCell>
<mxCell id="4" edge="1" source="2" target="3" parent="1"
        style="edgeStyle=orthogonalEdgeStyle;html=1;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

When `source` or `target` references an ID that does not exist as a vertex in the diagram, the edge endpoint becomes a dangling reference. Draw.io renders the edge as disconnected or not at all.

---

## AP-06: Spaces in Style Strings

### WRONG

```xml
style="rounded = 1; whiteSpace = wrap; html = 1; fillColor = #DAE8FC;"
```

### RIGHT

```xml
style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;"
```

### Why It Fails

Draw.io's style parser splits on `;` and then on `=`. Spaces around these delimiters produce property names like `" rounded "` or values like `" 1"`, which do not match the expected keys. The properties are silently ignored.

---

## AP-07: Missing html=1 with HTML Labels

### WRONG

```xml
<mxCell id="2" value="&lt;b&gt;Bold Text&lt;/b&gt;"
        style="rounded=1;whiteSpace=wrap;" vertex="1" parent="1">
```

### RIGHT

```xml
<mxCell id="2" value="&lt;b&gt;Bold Text&lt;/b&gt;"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

### Why It Fails

Without `html=1`, Draw.io treats the value as plain text. The literal string `<b>Bold Text</b>` (after XML unescaping) is displayed instead of rendering "**Bold Text**" with bold formatting.

---

## AP-08: Unescaped HTML in value Attribute

### WRONG

```xml
<mxCell id="2" value="<b>Title</b><br>Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

### RIGHT

```xml
<mxCell id="2" value="&lt;b&gt;Title&lt;/b&gt;&lt;br&gt;Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

### Why It Fails

The `value` attribute is inside an XML document. Unescaped `<` and `>` characters break the XML parser entirely. The file becomes malformed XML and Draw.io cannot open it at all. ALWAYS escape: `<` to `&lt;`, `>` to `&gt;`, `&` to `&amp;`, `"` to `&quot;`.

---

## AP-09: Missing Perimeter on Non-Rectangular Shapes

### WRONG

```xml
<mxCell id="2" value="Decision" style="shape=rhombus;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
```

### RIGHT

```xml
<mxCell id="2" value="Decision" style="shape=rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
```

### Why It Fails

Without the matching perimeter, Draw.io uses the default rectangular perimeter for calculating edge connection points. Edges connect to the bounding box corners instead of the diamond's actual edges, producing visually incorrect diagrams with arrows pointing to empty space.

---

## AP-10: Wrong Parent for Content Cells

### WRONG

```xml
<!-- Content cell parented to root container instead of layer -->
<mxCell id="2" value="Oops" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="0">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Correct" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Cells with `parent="0"` are treated as layers, not as visible shapes. A vertex with `parent="0"` becomes an invisible layer in the layer panel. Content cells MUST use `parent="1"` (default layer) or the ID of another layer.

---

## AP-11: Absolute Coordinates for Group Children

### WRONG

```xml
<!-- Group at (200, 200) -->
<mxCell id="2" value="Group" style="group" vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="200" as="geometry" />
</mxCell>
<!-- Child using absolute canvas coordinates — renders outside the group -->
<mxCell id="3" value="Child" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="2">
  <mxGeometry x="220" y="220" width="100" height="40" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Group" style="group" vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="200" as="geometry" />
</mxCell>
<!-- Child using RELATIVE coordinates to group's top-left -->
<mxCell id="3" value="Child" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="2">
  <mxGeometry x="20" y="20" width="100" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

Children of groups use coordinates relative to the parent's top-left corner. Using absolute canvas coordinates places the child at (220,220) relative to the group's origin at (200,200), which means the child renders at canvas position (420,420) — far outside the group bounds.

---

## AP-12: Missing as="geometry" on mxGeometry

### WRONG

```xml
<mxCell id="2" value="Box" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="Box" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

The `as="geometry"` attribute is the binding mechanism that tells the mxCell which child element represents its geometry. Without it, Draw.io does not associate the geometry with the cell. The shape renders at position (0,0) with zero size, making it invisible.

---

## AP-13: id and value on mxCell Inside object Wrapper

### WRONG

```xml
<object id="2" label="Server">
  <mxCell id="2" value="Server" style="rounded=1;whiteSpace=wrap;html=1;"
          vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
  </mxCell>
</object>
```

### RIGHT

```xml
<object id="2" label="Server">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;"
          vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
  </mxCell>
</object>
```

### Why It Fails

When using `<object>` or `<UserObject>`, the `id` and display text (`label`) belong on the wrapper element. Having `id` on both the wrapper and inner mxCell creates a duplicate ID conflict. Having `value` on the mxCell overrides or conflicts with `label` on the wrapper.

---

## AP-14: Missing whiteSpace=wrap on Vertices

### WRONG

```xml
<mxCell id="2" value="This is a very long label that extends beyond the shape boundary"
        style="rounded=1;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="2" value="This is a very long label that extends beyond the shape boundary"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `whiteSpace=wrap`, text does not wrap at the shape boundary. Long labels overflow the shape, overlapping with neighboring elements and producing an unreadable diagram.

---

## AP-15: Using mxGraphModel Attributes as Diagram Content

### WRONG

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxGraphModel dx="100" dy="100">  <!-- WRONG: nested mxGraphModel -->
      <mxCell id="2" value="Box" vertex="1" parent="1" />
    </mxGraphModel>
  </root>
</mxGraphModel>
```

### RIGHT

```xml
<mxGraphModel dx="100" dy="100">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Box" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

There is exactly ONE `<mxGraphModel>` per page. It is NEVER nested. All `<mxCell>` elements go inside `<root>`, which is the direct child of `<mxGraphModel>`. Nesting produces unparseable XML that Draw.io rejects.
