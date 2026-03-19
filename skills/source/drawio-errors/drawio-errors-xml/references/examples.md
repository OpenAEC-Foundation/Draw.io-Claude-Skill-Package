# Examples Reference: Draw.io XML Error Diagnosis

Concrete before/after examples for every error category.

---

## Example 1: Missing Structural Cells (E-002, E-003)

### BROKEN — Missing id="0" and id="1"

```xml
<mxGraphModel>
  <root>
    <mxCell id="2" value="Start" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

**Result:** Diagram fails to render. Parent "1" does not exist.

### FIXED — Structural cells added

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## Example 2: Duplicate IDs (E-005)

### BROKEN — Two cells share id="2"

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Server A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="2" value="Server B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

**Result:** "Server A" disappears. Only "Server B" renders because it overwrites the first cell.

### FIXED — Unique IDs

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Server A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Server B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## Example 3: Broken Parent Reference (E-006)

### BROKEN — Cell references nonexistent parent "5"

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Orphan Shape" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="5">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

**Result:** Shape disappears or throws a console error. Parent "5" does not exist.

### FIXED — Correct parent reference

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Visible Shape" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## Example 4: Missing XML Escaping (E-009)

### BROKEN — Raw HTML in value attribute

```xml
<mxCell id="2" value="<b>Bold Title</b><br>Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** XML parse error. The `<b>` tag breaks the XML structure.

### FIXED — Properly escaped HTML

```xml
<mxCell id="2" value="&lt;b&gt;Bold Title&lt;/b&gt;&lt;br&gt;Subtitle"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 5: Double Escaping (E-008)

### BROKEN — Entities escaped twice

```xml
<mxCell id="2" value="&amp;lt;b&amp;gt;Title&amp;lt;/b&amp;gt;"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** Label displays literal text `&lt;b&gt;Title&lt;/b&gt;` instead of **Title**.

### FIXED — Single level of escaping

```xml
<mxCell id="2" value="&lt;b&gt;Title&lt;/b&gt;"
        style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 6: Missing html=1 (E-007)

### BROKEN — No html=1 in style

```xml
<mxCell id="2" value="&lt;b&gt;Important&lt;/b&gt;"
        style="rounded=1;whiteSpace=wrap;fillColor=#DAE8FC;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** Label shows literal `<b>Important</b>` as plain text.

### FIXED — html=1 added

```xml
<mxCell id="2" value="&lt;b&gt;Important&lt;/b&gt;"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 7: Missing relative="1" on Edge (E-014)

### BROKEN — Edge geometry without relative

```xml
<mxCell id="4" value="Yes" style="endArrow=classic;html=1;" edge="1"
        source="2" target="3" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

**Result:** Edge label "Yes" appears at canvas origin (0,0) instead of along the edge.

### FIXED — relative="1" added

```xml
<mxCell id="4" value="Yes" style="endArrow=classic;html=1;" edge="1"
        source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

---

## Example 8: Perimeter Mismatch (E-010)

### BROKEN — Ellipse with rectangle perimeter

```xml
<mxCell id="2" value="Start" style="ellipse;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="80" height="80" as="geometry" />
</mxCell>
```

**Result:** Edges connect at the bounding box corners instead of the ellipse boundary, creating visible gaps.

### FIXED — Correct perimeter

```xml
<mxCell id="2" value="Start" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="80" height="80" as="geometry" />
</mxCell>
```

---

## Example 9: Invented Shape Name (E-019)

### BROKEN — AI-invented shape name

```xml
<mxCell id="2" value="API Gateway"
        style="shape=api-gateway;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** Renders as a plain rectangle. "api-gateway" is not a real Draw.io shape.

### FIXED — Using a real shape with descriptive label

```xml
<mxCell id="2" value="API Gateway"
        style="shape=mxgraph.aws4.api_gateway;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="78" height="78" as="geometry" />
</mxCell>
```

**Alternative Fix — Using basic rectangle with label:**

```xml
<mxCell id="2" value="API Gateway"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 10: Missing container=1 on Group (E-017)

### BROKEN — Swimlane without container flag

```xml
<mxCell id="10" value="Server Group" style="swimlane;html=1;startSize=30;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="11" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** Child "Web Server" does not move when "Server Group" is dragged. Coordinates may behave as absolute.

### FIXED — container=1 added

```xml
<mxCell id="10" value="Server Group"
        style="swimlane;html=1;startSize=30;container=1;collapsible=0;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="11" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 11: Boolean true/false Instead of 1/0 (E-011)

### BROKEN — String booleans

```xml
<mxCell id="2" value="Process"
        style="rounded=true;dashed=true;whiteSpace=wrap;html=1;shadow=true;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** Rounding, dashing, and shadow are all silently ignored. Shape appears as a plain rectangle.

### FIXED — Numeric booleans

```xml
<mxCell id="2" value="Process"
        style="rounded=1;dashed=1;whiteSpace=wrap;html=1;shadow=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 12: Style String Syntax Error (E-013)

### BROKEN — Spaces around equals, missing semicolons

```xml
<mxCell id="2" value="Error"
        style="rounded = 1 whiteSpace=wrap html=1 fillColor=#DAE8FC"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Result:** Most properties are ignored due to parsing failures.

### FIXED — Correct syntax

```xml
<mxCell id="2" value="Error"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## Example 13: Compressed Content (E-004)

### BROKEN — AI-generated fake Base64

```xml
<mxfile compressed="true">
  <diagram id="page-1" name="Page-1">
    dZHBDoMgDIafhmMJ6nS3qYfdnB5ckUlHE4EQ3HR7+lWpOpeYkP6k
  </diagram>
</mxfile>
```

**Result:** If the Base64 is fake (which it ALWAYS is from AI), Draw.io shows a blank page or parse error.

### FIXED — Uncompressed XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Hello World" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
