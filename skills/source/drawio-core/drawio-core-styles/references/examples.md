# Draw.io Core Styles — Working XML Examples

> Every example is valid mxGraph XML that renders correctly in Draw.io / diagrams.net.

---

## 1. Basic Shapes with Correct Styles

### 1.1 Rectangle (Default Shape)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Rectangle" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 1.2 Rounded Rectangle

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Rounded" style="rounded=1;whiteSpace=wrap;html=1;arcSize=10;fillColor=#D5E8D4;strokeColor=#82B366;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 1.3 Ellipse with Correct Perimeter

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Ellipse" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;fillColor=#E1D5E7;strokeColor=#9673A6;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 1.4 Diamond with Correct Perimeter

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Decision?" style="rhombus;whiteSpace=wrap;html=1;perimeter=rhombusPerimeter;fillColor=#FFF2CC;strokeColor=#D6B656;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 1.5 Triangle with Correct Perimeter

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="" style="triangle;whiteSpace=wrap;html=1;perimeter=trianglePerimeter;fillColor=#F8CECC;strokeColor=#B85450;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="80" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 1.6 Hexagon with Correct Perimeter

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Hexagon" style="shape=hexagon;whiteSpace=wrap;html=1;perimeter=hexagonPerimeter;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 1.7 Cylinder (Database)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;size=15;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="80" height="100" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Color System Examples

### 2.1 Custom Fill and Stroke Colors

```xml
<mxCell id="2" value="Blue fill" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;fontColor=#333333;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 2.2 Transparent Fill (none)

```xml
<mxCell id="2" value="Transparent" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#000000;strokeWidth=2;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 2.3 Gradient Fill

```xml
<mxCell id="2" value="Gradient" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;gradientColor=#FFFFFF;gradientDirection=south;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 2.4 Theme Default Colors

```xml
<mxCell id="2" value="Theme Default" style="rounded=1;whiteSpace=wrap;html=1;fillColor=default;strokeColor=default;fontColor=default;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 3. fontStyle Bitfield Examples

### 3.1 Bold Text (fontStyle=1)

```xml
<mxCell id="2" value="Bold Label" style="rounded=1;whiteSpace=wrap;html=1;fontStyle=1;fontSize=14;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 3.2 Bold + Italic (fontStyle=3)

```xml
<mxCell id="2" value="Bold Italic" style="rounded=1;whiteSpace=wrap;html=1;fontStyle=3;fontSize=14;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 3.3 Bold + Underline (fontStyle=5)

```xml
<mxCell id="2" value="Bold Underlined" style="rounded=1;whiteSpace=wrap;html=1;fontStyle=5;fontSize=14;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 3.4 Bold + Italic + Underline (fontStyle=7)

```xml
<mxCell id="2" value="All Three" style="rounded=1;whiteSpace=wrap;html=1;fontStyle=7;fontSize=14;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 3.5 Strikethrough (fontStyle=8)

```xml
<mxCell id="2" value="Deprecated" style="rounded=1;whiteSpace=wrap;html=1;fontStyle=8;fontSize=14;fontColor=#999999;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 4. Edge / Connector Examples

### 4.1 Standard Arrow

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="a" value="A" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="b" value="B" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="350" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 4.2 Orthogonal Connector

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.3 Dashed Dependency Arrow

```xml
<mxCell id="e1" style="endArrow=open;dashed=1;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.4 Custom Dash Pattern

```xml
<mxCell id="e1" style="endArrow=classic;html=1;dashed=1;dashPattern=8 4;strokeWidth=2;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.5 Bidirectional Arrow

```xml
<mxCell id="e1" style="startArrow=classic;endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.6 No Arrows (Association Line)

```xml
<mxCell id="e1" style="endArrow=none;startArrow=none;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.7 UML Inheritance (Hollow Triangle)

```xml
<mxCell id="e1" style="endArrow=block;endFill=0;html=1;edgeStyle=orthogonalEdgeStyle;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.8 UML Composition (Filled Diamond)

```xml
<mxCell id="e1" style="startArrow=diamond;startFill=1;endArrow=open;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.9 UML Aggregation (Hollow Diamond)

```xml
<mxCell id="e1" style="startArrow=diamond;startFill=0;endArrow=open;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.10 Curved Connector

```xml
<mxCell id="e1" style="curved=1;endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 4.11 Edge with Fixed Connection Points

```xml
<mxCell id="e1" style="endArrow=classic;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

---

## 5. Container and Swimlane Examples

### 5.1 Horizontal Swimlane with Child

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="lane1" value="Process Lane" style="swimlane;horizontal=1;startSize=30;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;html=1;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="400" height="200" as="geometry" />
    </mxCell>
    <mxCell id="step1" value="Step 1" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="lane1">
      <mxGeometry x="20" y="50" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="step2" value="Step 2" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;" vertex="1" parent="lane1">
      <mxGeometry x="200" y="50" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="endArrow=classic;html=1;" edge="1" source="step1" target="step2" parent="lane1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### 5.2 Vertical Swimlane

```xml
<mxCell id="lane1" value="Column" style="swimlane;horizontal=0;startSize=30;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;html=1;whiteSpace=wrap;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="200" height="400" as="geometry" />
</mxCell>
```

### 5.3 Group Container (Non-Swimlane)

```xml
<mxCell id="group1" value="Group" style="rounded=1;whiteSpace=wrap;html=1;container=1;collapsible=0;fillColor=#F5F5F5;strokeColor=#666666;strokeWidth=2;dashed=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="child1" value="Inside" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="group1">
  <mxGeometry x="20" y="30" width="100" height="50" as="geometry" />
</mxCell>
```

---

## 6. Label Positioning Examples

### 6.1 Label Below Shape

```xml
<mxCell id="2" value="Below" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;verticalLabelPosition=bottom;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

### 6.2 Label to the Right of Shape

```xml
<mxCell id="2" value="Right Side" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;labelPosition=right;align=left;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

### 6.3 Label Above Shape

```xml
<mxCell id="2" value="Above" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;verticalLabelPosition=top;verticalAlign=bottom;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

---

## 7. Decorative Effect Examples

### 7.1 Dashed Border with Shadow

```xml
<mxGraphModel shadow="1">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;dashed=1;fillColor=#FFFFFF;strokeColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Note: the `<mxGraphModel shadow="1">` is REQUIRED for per-cell shadow to render.

### 7.2 Glass Effect

```xml
<mxCell id="2" value="Glossy" style="rounded=1;whiteSpace=wrap;html=1;glass=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 7.3 Sketch / Hand-Drawn Style

```xml
<mxCell id="2" value="Sketchy" style="rounded=1;whiteSpace=wrap;html=1;sketch=1;jiggle=2;fillStyle=hachure;hachureGap=4;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 8. Behavior / Lock Examples

### 8.1 Locked Read-Only Shape

```xml
<mxCell id="2" value="Locked" style="rounded=1;whiteSpace=wrap;html=1;movable=0;resizable=0;editable=0;deletable=0;fillColor=#F5F5F5;strokeColor=#666666;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### 8.2 Auto-Sizing Shape

```xml
<mxCell id="2" value="Auto Size" style="rounded=1;whiteSpace=wrap;html=1;autosize=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 9. Complete Flowchart Example

A complete diagram with multiple shapes, edges, and correct styles:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- Start -->
    <mxCell id="start" value="Start" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;fillColor=#D5E8D4;strokeColor=#82B366;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="100" height="50" as="geometry" />
    </mxCell>
    <!-- Process -->
    <mxCell id="proc" value="Process Data" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="190" y="140" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Decision -->
    <mxCell id="dec" value="Valid?" style="rhombus;whiteSpace=wrap;html=1;perimeter=rhombusPerimeter;fillColor=#FFF2CC;strokeColor=#D6B656;" vertex="1" parent="1">
      <mxGeometry x="200" y="250" width="100" height="80" as="geometry" />
    </mxCell>
    <!-- End -->
    <mxCell id="end" value="End" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;fillColor=#F8CECC;strokeColor=#B85450;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="200" y="400" width="100" height="50" as="geometry" />
    </mxCell>
    <!-- Error -->
    <mxCell id="err" value="Handle Error" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;" vertex="1" parent="1">
      <mxGeometry x="380" y="260" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Edges -->
    <mxCell id="e1" style="endArrow=classic;html=1;" edge="1" source="start" target="proc" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=classic;html=1;" edge="1" source="proc" target="dec" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" value="Yes" style="endArrow=classic;html=1;" edge="1" source="dec" target="end" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="No" style="endArrow=classic;html=1;" edge="1" source="dec" target="err" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="endArrow=classic;html=1;dashed=1;" edge="1" source="err" target="proc" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
