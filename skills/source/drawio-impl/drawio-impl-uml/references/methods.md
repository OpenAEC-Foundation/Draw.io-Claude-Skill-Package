# Methods Reference: UML Diagram Implementation

Complete style strings and attribute reference for all UML diagram shapes and connections.

---

## 1. Class Diagram Styles

### Class Container (3-Compartment Swimlane)

```
swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;
```

With colors:

```
swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

### Style Property Breakdown

| Property | Value | Purpose |
|----------|-------|---------|
| `swimlane` | Required | Renders as compartmented container |
| `fontStyle=1` | Bold | Bold class name in header |
| `align=center` | Center | Centers class name |
| `startSize=26` | 26px | Height of the name compartment |
| `container=1` | Required | Enables child cell attachment |
| `collapsible=0` | Recommended | Prevents accidental collapse |
| `childLayout=stackLayout` | Required | Stacks compartments vertically |

### Abstract Class Container

```
swimlane;fontStyle=3;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;fillColor=#e1d5e7;strokeColor=#9673a6;
```

`fontStyle=3` = bold + italic. The italic signals abstract per UML convention.

### Interface Container

```
swimlane;fontStyle=3;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;fillColor=#e1d5e7;strokeColor=#9673a6;
```

Same as abstract. Differentiated by the `<<interface>>` stereotype in the value.

---

## 2. Class Compartment Styles

### Attributes Compartment

```
text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;
```

| Property | Value | Purpose |
|----------|-------|---------|
| `text` | Required | Text-only cell |
| `strokeColor=none` | Required | No border |
| `fillColor=none` | Required | Transparent |
| `align=left` | Required | Left-aligns UML notation |
| `verticalAlign=top` | Required | Top-aligns multi-line text |
| `html=0` | Required | Uses `&#xa;` for line breaks |

### Separator Line

```
line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;
```

With matching stroke color:

```
line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;strokeColor=#6c8ebf;
```

### Operations Compartment

Same style as attributes compartment:

```
text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;
```

---

## 3. Sequence Diagram Styles

### Lifeline

```
shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;size=40;
```

| Property | Value | Purpose |
|----------|-------|---------|
| `shape=umlLifeline` | Required | Renders header + dashed line |
| `perimeter=lifelinePerimeter` | Required | Connection points on lifeline |
| `container=1` | Required | Holds activation bars |
| `recursiveResize=0` | Required | Prevents children from resizing parent |
| `outlineConnect=0` | Required | Clean connection behavior |
| `size=40` | 40px | Height of participant header |

### Activation Bar

```
html=1;points=[];perimeter=orthogonalPerimeter;outlineConnect=0;targetShapes=umlLifeline;portConstraint=eastwest;newEdgeStyle={"curved":0,"rounded":0};
```

Dimensions: width=10, x=45 (centers on 100px lifeline).

### Synchronous Message

```
html=1;verticalAlign=bottom;endArrow=block;endFill=1;
```

### Asynchronous Message

```
html=1;verticalAlign=bottom;endArrow=open;endFill=1;
```

### Return Message

```
html=1;verticalAlign=bottom;endArrow=open;endFill=0;dashed=1;
```

### Self-Message

Uses two waypoints to create a loop back to the same lifeline:

```
html=1;verticalAlign=bottom;endArrow=block;endFill=1;curved=1;
```

---

## 4. Use Case Diagram Styles

### Actor

```
shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;
```

Dimensions: width=30, height=55.

### Use Case Ellipse

```
ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Dimensions: width=180, height=60.

### System Boundary

```
rounded=1;whiteSpace=wrap;html=1;container=1;collapsible=0;fillColor=none;strokeColor=#666666;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=14;
```

### Actor-to-UseCase Association

```
endArrow=none;html=1;
```

### Include Relationship

```
endArrow=open;endFill=1;dashed=1;html=1;
```

Value: `<<include>>`

### Extend Relationship

```
endArrow=open;endFill=1;dashed=1;html=1;
```

Value: `<<extend>>`

---

## 5. State Machine Styles

### Initial State

```
ellipse;fillColor=#000000;strokeColor=#000000;
```

Dimensions: width=30, height=30.

### Regular State

```
rounded=1;whiteSpace=wrap;html=1;align=center;verticalAlign=top;arcSize=15;
```

Value format: `<b>StateName</b><hr>entry / action()<br>exit / action()`

### Final State

```
ellipse;html=1;shape=doubleCircle;fillColor=#000000;strokeColor=#000000;
```

Dimensions: width=30, height=30.

### State Transition

```
endArrow=open;endFill=1;html=1;
```

Label format: `event [guard] / action`

---

## 6. Activity Diagram Styles

### Action Node

```
rounded=1;whiteSpace=wrap;html=1;
```

### Decision Node

```
rhombus;whiteSpace=wrap;html=1;
```

Dimensions: width=40, height=40.

### Fork/Join Bar (Horizontal)

```
shape=line;html=1;strokeWidth=6;strokeColor=#000000;fillColor=#000000;
```

Dimensions: width=200, height=10.

### Fork/Join Bar (Vertical)

```
shape=line;html=1;strokeWidth=6;strokeColor=#000000;fillColor=#000000;direction=south;
```

Dimensions: width=10, height=200.

### Activity Edge

```
endArrow=open;endFill=1;html=1;edgeStyle=orthogonalEdgeStyle;
```

---

## 7. UML Relationship Edge Styles

### Association

```
endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;
```

### Directed Association

```
endArrow=open;endFill=1;html=1;edgeStyle=orthogonalEdgeStyle;
```

### Generalization (Inheritance)

```
endArrow=block;endFill=0;html=1;edgeStyle=orthogonalEdgeStyle;
```

### Realization (Interface Implementation)

```
endArrow=block;endFill=0;dashed=1;html=1;edgeStyle=orthogonalEdgeStyle;
```

### Aggregation (Shared Has-A)

```
startArrow=diamond;startFill=0;endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;
```

### Composition (Owned Has-A)

```
startArrow=diamond;startFill=1;endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;
```

### Dependency (Uses)

```
endArrow=open;endFill=1;dashed=1;html=1;edgeStyle=orthogonalEdgeStyle;
```

---

## 8. Multiplicity Labels on Edges

Add multiplicity as the edge `value` or via separate label cells:

```xml
<mxCell id="edge1" value="1..*" style="endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="cls1" target="cls2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

For separate source/target multiplicity labels, use `mxPoint` offsets on the edge geometry.
