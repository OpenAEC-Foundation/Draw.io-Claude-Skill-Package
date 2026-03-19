# Draw.io Style Properties — Examples

> Complete style string examples for common scenarios.
> Every example is a valid, copy-paste-ready style string.

---

## 1. Basic Shape Styles

### Rectangle (default)

```
whiteSpace=wrap;html=1;
```

### Rounded Rectangle

```
rounded=1;whiteSpace=wrap;html=1;arcSize=10;
```

### Colored Rectangle

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;fontColor=#333333;
```

### Ellipse

```
ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;
```

### Diamond (Decision Node)

```
rhombus;whiteSpace=wrap;html=1;perimeter=rhombusPerimeter;
```

### Triangle

```
triangle;whiteSpace=wrap;html=1;perimeter=trianglePerimeter;
```

### Hexagon

```
shape=hexagon;whiteSpace=wrap;html=1;perimeter=hexagonPerimeter;
```

### Cylinder (Database)

```
shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;size=15;
```

### Cloud

```
ellipse;shape=cloud;whiteSpace=wrap;html=1;
```

### Document

```
shape=document;whiteSpace=wrap;html=1;boundedLbl=1;size=0.27;
```

### Parallelogram

```
shape=parallelogram;whiteSpace=wrap;html=1;perimeter=parallelogramPerimeter;
```

---

## 2. Styled Shapes

### Blue Process Box

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;fontSize=14;fontStyle=1;
```

### Green Success Box

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;
```

### Red Error Box

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;
```

### Orange Warning Box

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#FFE6CC;strokeColor=#D6B656;
```

### Purple Decision Diamond

```
rhombus;whiteSpace=wrap;html=1;perimeter=rhombusPerimeter;fillColor=#E1D5E7;strokeColor=#9673A6;
```

### Gray Neutral Box

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#F5F5F5;strokeColor=#666666;fontColor=#333333;
```

### Transparent Shape (No Fill)

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#000000;
```

### Dashed Border Shape

```
rounded=1;whiteSpace=wrap;html=1;dashed=1;dashPattern=8 4;fillColor=#FFFFFF;strokeColor=#999999;
```

### Bold Header with Shadow

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#1A1A2E;strokeColor=#16213E;fontColor=#FFFFFF;fontStyle=1;fontSize=16;shadow=1;
```

---

## 3. Edge / Connector Styles

### Standard Arrow (Straight)

```
endArrow=classic;html=1;
```

### Orthogonal Connector (Most Common)

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;
```

### Curved Connector

```
curved=1;endArrow=classic;html=1;
```

### Dashed Dependency Arrow

```
endArrow=open;dashed=1;html=1;
```

### Bidirectional Arrow

```
startArrow=classic;endArrow=classic;html=1;
```

### No Arrows (Association Line)

```
endArrow=none;startArrow=none;html=1;
```

### Colored Connector

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;strokeColor=#FF0000;strokeWidth=2;
```

### Thick Connector

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;strokeWidth=3;
```

### Entity Relation Edge

```
edgeStyle=entityRelationEdgeStyle;html=1;endArrow=classic;
```

### Self-Loop Edge

```
edgeStyle=loopEdgeStyle;orthogonalLoop=1;html=1;endArrow=classic;
```

---

## 4. UML Relationship Styles

### Inheritance (Generalization)

```
edgeStyle=orthogonalEdgeStyle;html=1;endArrow=block;endFill=0;
```

### Composition (Filled Diamond)

```
edgeStyle=orthogonalEdgeStyle;html=1;startArrow=diamond;startFill=1;endArrow=open;
```

### Aggregation (Hollow Diamond)

```
edgeStyle=orthogonalEdgeStyle;html=1;startArrow=diamond;startFill=0;endArrow=open;
```

### Dependency (Dashed Open Arrow)

```
edgeStyle=orthogonalEdgeStyle;html=1;endArrow=open;dashed=1;
```

### Implementation / Realization (Dashed Hollow Triangle)

```
edgeStyle=orthogonalEdgeStyle;html=1;endArrow=block;endFill=0;dashed=1;
```

### Association (Simple Arrow)

```
edgeStyle=orthogonalEdgeStyle;html=1;endArrow=open;
```

---

## 5. Swimlane / Container Styles

### Horizontal Swimlane

```
swimlane;horizontal=1;startSize=30;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;html=1;whiteSpace=wrap;
```

### Vertical Swimlane

```
swimlane;horizontal=0;startSize=30;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;html=1;whiteSpace=wrap;
```

### Blue Header Swimlane

```
swimlane;horizontal=1;startSize=40;fillColor=#DAE8FC;strokeColor=#6C8EBF;fontStyle=1;fontSize=14;container=1;collapsible=0;html=1;whiteSpace=wrap;swimlaneFillColor=#FFFFFF;
```

### Collapsible Group

```
swimlane;horizontal=1;startSize=30;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;container=1;collapsible=1;html=1;whiteSpace=wrap;
```

### Plain Container (No Header)

```
rounded=1;whiteSpace=wrap;html=1;container=1;collapsible=0;fillColor=#F5F5F5;strokeColor=#CCCCCC;dashed=1;
```

---

## 6. Text and Label Styles

### Bold Header Text

```
text;whiteSpace=wrap;html=1;fontStyle=1;fontSize=18;align=center;
```

### Left-Aligned Text Block

```
text;whiteSpace=wrap;html=1;align=left;verticalAlign=top;spacing=10;
```

### Label Below Shape

```
ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;verticalLabelPosition=bottom;verticalAlign=top;
```

### Label to the Right of Shape

```
ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;labelPosition=right;align=left;
```

### Large Centered Header

```
text;whiteSpace=wrap;html=1;fontSize=24;fontStyle=1;fontColor=#1A1A2E;align=center;
```

---

## 7. Sketch / Hand-Drawn Styles

### Basic Sketch Rectangle

```
rounded=1;whiteSpace=wrap;html=1;sketch=1;jiggle=2;
```

### Sketch with Hachure Fill

```
rounded=1;whiteSpace=wrap;html=1;sketch=1;jiggle=2;fillStyle=hachure;hachureGap=4;fillColor=#DAE8FC;strokeColor=#6C8EBF;
```

### Sketch with Cross-Hatch Fill

```
rounded=1;whiteSpace=wrap;html=1;sketch=1;jiggle=2;fillStyle=cross-hatch;hachureGap=6;fillColor=#D5E8D4;strokeColor=#82B366;
```

### Sketch with Dots Fill

```
rounded=1;whiteSpace=wrap;html=1;sketch=1;jiggle=1;fillStyle=dots;fillColor=#E1D5E7;strokeColor=#9673A6;
```

### Comic Book Style

```
rounded=1;whiteSpace=wrap;html=1;sketch=1;comic=1;jiggle=3;strokeWidth=2;
```

### Sketch Edge

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;sketch=1;jiggle=2;
```

---

## 8. Image Shape Styles

### Basic Image Shape

```
shape=image;image=https://example.com/icon.png;imageWidth=48;imageHeight=48;html=1;
```

### Image with Label Below

```
shape=image;image=https://example.com/icon.png;imageWidth=48;imageHeight=48;html=1;verticalLabelPosition=bottom;verticalAlign=top;
```

### Label Shape (Image + Text Side by Side)

```
shape=label;imageWidth=24;imageHeight=24;imageAlign=left;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;align=left;spacingLeft=30;
```

---

## 9. Connection Point Examples

### Edge from Right-Center to Left-Center

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;exitX=1;exitY=0.5;entryX=0;entryY=0.5;
```

### Edge from Bottom-Center to Top-Center

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;exitX=0.5;exitY=1;entryX=0.5;entryY=0;
```

### Edge from Top-Right to Bottom-Left

```
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;exitX=1;exitY=0;entryX=0;entryY=1;
```

---

## 10. Locked / Read-Only Shapes

### Fully Locked Shape

```
rounded=1;whiteSpace=wrap;html=1;movable=0;resizable=0;editable=0;deletable=0;rotatable=0;connectable=0;
```

### View-Only with Connections Allowed

```
rounded=1;whiteSpace=wrap;html=1;movable=0;resizable=0;editable=0;
```

---

## 11. Stencil Shape Examples

### AWS Lambda Function

```
shape=mxgraph.aws4.lambda_function;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;
```

### Cisco Router

```
shape=mxgraph.cisco.router;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;
```

### UML Component

```
shape=mxgraph.uml.component;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;
```

### BPMN Shape

```
shape=mxgraph.bpmn.shape;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;
```

---

## 12. Complete Diagram Fragment

### Flowchart with Two Boxes and Connector

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="End" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;" vertex="1" parent="1">
      <mxGeometry x="100" y="250" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;" edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Swimlane with Child Shapes

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="lane1" value="Process Lane" style="swimlane;horizontal=1;startSize=30;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;html=1;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="50" y="50" width="400" height="200" as="geometry" />
    </mxCell>
    <mxCell id="s1" value="Step 1" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="lane1">
      <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="s2" value="Step 2" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="lane1">
      <mxGeometry x="220" y="40" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;" edge="1" source="s1" target="s2" parent="lane1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
