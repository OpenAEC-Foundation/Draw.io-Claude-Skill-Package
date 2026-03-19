# Examples: Draw.io Syntax Connections

Working XML examples for every connection pattern. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Floating Connection (Auto-Routed)

The simplest edge. Draw.io chooses attachment points automatically.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Source" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Target" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Fixed Connection (Explicit Entry/Exit Points)

Edge exits from the right-center of source, enters the left-center of target.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Source" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Target" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="250" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Decision Diamond with Yes/No Branches

Fixed connections from specific sides of a diamond shape.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Approved?" style="shape=rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="120" height="80" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Process" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="110" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="Reject" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="260" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="5" value="Yes" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="6" value="No" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;"
            edge="1" source="2" target="4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. Self-Loop (State Machine)

Edge that connects a shape to itself using `loopEdgeStyle`.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Processing" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="120" height="80" as="geometry" />
    </mxCell>
    <mxCell id="3" value="retry" style="edgeStyle=loopEdgeStyle;html=1;"
            edge="1" source="2" target="2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Edge with Waypoints

Orthogonal edge forced through specific intermediate points.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="300" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="160" y="250" />
          <mxPoint x="460" y="250" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 6. Curved Edge

Smooth curved path using `curved=1`.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="End" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="300" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="curved=1;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="350" y="100" />
          <mxPoint x="150" y="300" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 7. Edge Label at Custom Position

Label placed near the source end, offset above the edge path.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Client" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Server" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="HTTP GET" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry x="-0.5" y="-15" relative="1" as="geometry">
        <mxPoint as="offset" />
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 8. Multiple Labels on One Edge

Source-end and target-end labels using edge label children.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Order" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Product" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="contains" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="5" value="1" style="edgeLabel;html=1;align=left;verticalAlign=bottom;fontSize=11;"
            vertex="1" connectable="0" parent="4">
      <mxGeometry x="-0.8" y="0" relative="1" as="geometry">
        <mxPoint as="offset" />
      </mxGeometry>
    </mxCell>
    <mxCell id="6" value="*" style="edgeLabel;html=1;align=right;verticalAlign=bottom;fontSize=11;"
            vertex="1" connectable="0" parent="4">
      <mxGeometry x="0.8" y="0" relative="1" as="geometry">
        <mxPoint as="offset" />
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 9. Entity Relation Edge Style

ER diagram style with fixed-length stubs at both ends.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Customer" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="180" height="90" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Order" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="100" width="180" height="90" as="geometry" />
    </mxCell>
    <mxCell id="4" value="" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=manyOptional;startArrow=none;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 10. Straight Line (No Edge Style)

Direct point-to-point connection with no routing algorithm.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="A" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="80" height="80" as="geometry" />
    </mxCell>
    <mxCell id="3" value="B" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;"
            vertex="1" parent="1">
      <mxGeometry x="350" y="250" width="80" height="80" as="geometry" />
    </mxCell>
    <mxCell id="4" style="html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 11. Dashed Dependency Arrow

UML dependency with open arrow and dashed line.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Controller" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Service" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="&lt;i&gt;uses&lt;/i&gt;" style="edgeStyle=orthogonalEdgeStyle;html=1;dashed=1;endArrow=open;endFill=0;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 12. Shape with Custom Connection Points

A shape that restricts edge connections to four specific points.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Router" style="rounded=1;whiteSpace=wrap;html=1;points=[[0.5,0],[1,0.5],[0.5,1],[0,0.5]];"
            vertex="1" parent="1">
      <mxGeometry x="200" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Server A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="450" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 13. Isometric Edge

30-degree angle routing for isometric diagrams.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Node A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Node B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="350" y="250" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=isometricEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
