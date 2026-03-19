# Anti-Patterns: UML Diagram Implementation

What NOT to do when generating UML diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Using Generic Arrows Instead of UML-Specific Markers

### WRONG

```xml
<mxCell id="gen1" style="endArrow=classic;html=1;"
        edge="1" parent="1" source="cls_dog" target="cls_animal">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="gen1" style="endArrow=block;endFill=0;html=1;edgeStyle=orthogonalEdgeStyle;"
        edge="1" parent="1" source="cls_dog" target="cls_animal">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`endArrow=classic` produces a generic arrowhead that conveys no UML semantics. Generalization MUST use `endArrow=block;endFill=0` (hollow triangle). Without the correct marker, the diagram is ambiguous — readers cannot distinguish inheritance from dependency or association.

---

## AP-02: Using Filled Triangle for Generalization

### WRONG

```xml
<mxCell id="gen1" style="endArrow=block;endFill=1;html=1;"
        edge="1" parent="1" source="cls_child" target="cls_parent">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="gen1" style="endArrow=block;endFill=0;html=1;"
        edge="1" parent="1" source="cls_child" target="cls_parent">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`endFill=1` produces a FILLED triangle, which is NOT valid UML for generalization. UML specifies a HOLLOW (unfilled) triangle for inheritance. A filled triangle has no defined meaning in UML and will confuse readers.

---

## AP-03: Confusing Aggregation and Composition

### WRONG (aggregation with filled diamond)

```xml
<mxCell id="agg1" style="startArrow=diamond;startFill=1;endArrow=none;html=1;"
        edge="1" parent="1" source="cls_department" target="cls_employee">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT (aggregation with open diamond)

```xml
<mxCell id="agg1" style="startArrow=diamond;startFill=0;endArrow=none;html=1;"
        edge="1" parent="1" source="cls_department" target="cls_employee">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`startFill=1` on a diamond produces COMPOSITION (filled diamond = owned lifecycle). Aggregation MUST use `startFill=0` (open diamond = shared lifecycle). A department does NOT own employees' lifecycle, so composition is semantically wrong. The fill value is the ONLY visual difference between these two relationship types.

---

## AP-04: Using Solid Lines for Return Messages in Sequence Diagrams

### WRONG

```xml
<mxCell id="ret1" value="result" style="html=1;verticalAlign=bottom;endArrow=open;endFill=0;"
        edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="330" y="200" as="sourcePoint" />
    <mxPoint x="130" y="200" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="ret1" value="result" style="html=1;verticalAlign=bottom;endArrow=open;endFill=0;dashed=1;"
        edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="330" y="200" as="sourcePoint" />
    <mxPoint x="130" y="200" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### Why It Fails

UML specifies that return messages MUST be dashed lines. Without `dashed=1`, the return message looks identical to a synchronous call, making the sequence diagram unreadable. Readers cannot distinguish requests from responses.

---

## AP-05: Using shape=ellipse for UML Actors

### WRONG

```xml
<mxCell id="actor1" value="User" style="ellipse;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="120" width="60" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="actor1" value="User" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="120" width="30" height="55" as="geometry" />
</mxCell>
```

### Why It Fails

`shape=ellipse` renders a circle/oval, which is the UML notation for a USE CASE, not an actor. UML actors MUST use the stick-figure symbol (`shape=umlActor`). Using an ellipse for an actor makes it visually identical to a use case, rendering the diagram meaningless.

---

## AP-06: Placing Use Cases Outside the System Boundary

### WRONG

```xml
<!-- Use case at parent="1" instead of parent="sys" -->
<mxCell id="uc1" value="Login" style="ellipse;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="180" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Use case as child of system boundary -->
<mxCell id="uc1" value="Login" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="sys">
  <mxGeometry x="60" y="30" width="180" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Use cases MUST be contained within the system boundary. Placing them at `parent="1"` means they float outside the system, breaking the UML convention that use cases represent functionality PROVIDED BY the system. The system boundary visually communicates scope — use cases outside it imply they belong to a different system.

---

## AP-07: Using Plain Rectangles Instead of umlLifeline for Sequence Participants

### WRONG

```xml
<mxCell id="p1" value="Client" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="40" width="100" height="40" as="geometry" />
</mxCell>
<!-- Manually drawn dashed line below -->
<mxCell id="p1_line" value="" style="endArrow=none;dashed=1;html=1;"
        edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="130" y="80" as="sourcePoint" />
    <mxPoint x="130" y="300" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="ll1" value="Client" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;size=40;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="40" width="100" height="300" as="geometry" />
</mxCell>
```

### Why It Fails

Manually constructing lifelines from rectangles + dashed edges produces fragile diagrams that break when resized or repositioned. The `shape=umlLifeline` renders the header box AND dashed line as a single integrated shape. It also provides `lifelinePerimeter` for correct message attachment points. ALWAYS use the built-in lifeline shape.

---

## AP-08: Missing Separator Line Between Class Compartments

### WRONG

```xml
<mxCell id="cls1" value="User" style="swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;" vertex="1" parent="1">
  <mxGeometry x="100" y="60" width="200" height="120" as="geometry" />
</mxCell>
<mxCell id="attr" value="- name: String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls1">
  <mxGeometry y="26" width="200" height="40" as="geometry" />
</mxCell>
<!-- Missing separator line -->
<mxCell id="ops" value="+ getName(): String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls1">
  <mxGeometry y="66" width="200" height="40" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="cls1" value="User" style="swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;" vertex="1" parent="1">
  <mxGeometry x="100" y="60" width="200" height="130" as="geometry" />
</mxCell>
<mxCell id="attr" value="- name: String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls1">
  <mxGeometry y="26" width="200" height="40" as="geometry" />
</mxCell>
<mxCell id="sep" value="" style="line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;" vertex="1" parent="cls1">
  <mxGeometry y="66" width="200" height="8" as="geometry" />
</mxCell>
<mxCell id="ops" value="+ getName(): String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls1">
  <mxGeometry y="74" width="200" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

Without the `line` separator cell, attributes and operations visually merge into a single block. The horizontal line is a REQUIRED part of UML class notation — it separates the three compartments (name, attributes, operations). Omitting it produces a non-standard class diagram.

---

## AP-09: Using Solid Lines for Dependency Relationships

### WRONG

```xml
<mxCell id="dep1" style="endArrow=open;endFill=1;html=1;"
        edge="1" parent="1" source="cls_controller" target="cls_service">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="dep1" value="&lt;&lt;use&gt;&gt;" style="endArrow=open;endFill=1;dashed=1;html=1;"
        edge="1" parent="1" source="cls_controller" target="cls_service">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

UML dependency and realization MUST use dashed lines (`dashed=1`). A solid line with an open arrow looks like a directed association, which has completely different semantics (structural relationship vs. usage relationship). Missing `dashed=1` changes the meaning of the edge.
