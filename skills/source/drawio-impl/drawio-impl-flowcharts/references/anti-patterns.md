# Anti-Patterns: Flowchart Implementation

What NOT to do when generating flowchart diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Using Rectangle for Decisions

### WRONG

```xml
<mxCell id="dec1" value="Is Valid?" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="dec1" value="Is Valid?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="80" as="geometry" />
</mxCell>
```

### Why It Fails

A rectangle is the ISO 5807 symbol for a process step. Using it for a decision makes the diagram semantically wrong — readers cannot distinguish between actions and conditional branches. ALWAYS use `rhombus` for decisions.

---

## AP-02: Using Ellipse for Terminators

### WRONG

```xml
<mxCell id="start" value="Start" style="ellipse;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="40" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

ISO 5807 specifies the stadium (pill/rounded rectangle with `arcSize=50`) for terminators, not an ellipse. Ellipses are visually ambiguous and conflict with other diagram notations (e.g., UML use cases). ALWAYS use `rounded=1;arcSize=50;` for Start/End shapes.

---

## AP-03: Missing Decision Branch Labels

### WRONG

```xml
<mxCell id="e_yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_a">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e_no" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_b">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="e_yes" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_a">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e_no" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_b">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Without labels, readers cannot determine which branch is "Yes" and which is "No." This makes the flowchart ambiguous and unreadable. ALWAYS add `value="Yes"` and `value="No"` (or equivalent labels) to every edge leaving a decision shape.

---

## AP-04: Mixed Flow Directions

### WRONG

```xml
<!-- Step 1 flows down -->
<mxCell id="s1" value="Step 1" ... >
  <mxGeometry x="200" y="40" width="140" height="60" as="geometry" />
</mxCell>
<!-- Step 2 flows right -->
<mxCell id="s2" value="Step 2" ... >
  <mxGeometry x="400" y="40" width="140" height="60" as="geometry" />
</mxCell>
<!-- Step 3 flows down again -->
<mxCell id="s3" value="Step 3" ... >
  <mxGeometry x="400" y="160" width="140" height="60" as="geometry" />
</mxCell>
<!-- Step 4 flows LEFT (backwards!) -->
<mxCell id="s4" value="Step 4" ... >
  <mxGeometry x="200" y="160" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Consistent top-to-bottom flow -->
<mxCell id="s1" value="Step 1" ... >
  <mxGeometry x="200" y="40" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="s2" value="Step 2" ... >
  <mxGeometry x="200" y="140" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="s3" value="Step 3" ... >
  <mxGeometry x="200" y="240" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="s4" value="Step 4" ... >
  <mxGeometry x="200" y="340" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Mixing flow directions forces readers to scan the diagram in multiple directions, breaking the natural reading order. The only acceptable exception is decision branches exiting to the side, which MUST rejoin the main flow without backtracking.

---

## AP-05: Missing whiteSpace and html Attributes

### WRONG

```xml
<mxCell id="step1" value="Process the incoming order data" style="rounded=0;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="step1" value="Process the incoming order data" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `whiteSpace=wrap`, long text overflows beyond the shape boundary. Without `html=1`, HTML markup in labels (like `&lt;br&gt;` for line breaks) renders as literal text instead of being interpreted. ALWAYS include both properties in every shape style.

---

## AP-06: Hard-Coded Waypoints on Simple Paths

### WRONG

```xml
<mxCell id="e1" style="endArrow=classic;html=1;" edge="1" parent="1" source="step1" target="step2">
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="260" y="180" />
      <mxPoint x="260" y="200" />
      <mxPoint x="260" y="220" />
    </Array>
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="step1" target="step2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Hard-coded waypoints on straight or simple orthogonal paths create maintenance problems: if shapes are moved in the editor, the waypoints remain fixed and the edge no longer routes correctly. ALWAYS use `edgeStyle=orthogonalEdgeStyle` and let Draw.io auto-route. Only use explicit waypoints for loop-back edges or complex routing that auto-routing cannot handle.

---

## AP-07: Decision with Single Exit

### WRONG

```xml
<!-- Decision with only one outgoing edge -->
<mxCell id="dec1" value="Is Ready?" style="rhombus;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="80" as="geometry" />
</mxCell>
<mxCell id="e1" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="next">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<!-- No "No" branch exists -->
```

### RIGHT

```xml
<mxCell id="dec1" value="Is Ready?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="80" as="geometry" />
</mxCell>
<mxCell id="e1" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="next">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="wait_step">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

A decision with a single exit is not a decision — it is a process step. Every decision diamond MUST have at least two outgoing edges, each with a label. If there is genuinely only one path forward, use a process rectangle instead.

---

## AP-08: Edges Without Source or Target

### WRONG

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="step1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="260" y="300" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="step1" target="step2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Dangling edges (connected on one end but floating on the other) break the flowchart structure. If a shape is moved, the floating end stays at fixed coordinates instead of following. ALWAYS connect both `source` and `target` to valid cell IDs.
