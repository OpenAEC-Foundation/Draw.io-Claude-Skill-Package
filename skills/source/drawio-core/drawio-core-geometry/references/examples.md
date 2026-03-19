# Geometry Examples

All examples produce valid mxGraph XML that Draw.io renders correctly.

---

## 1. Basic Vertex Positioning

A single rectangle at canvas position (200, 150), sized 120x60:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="150" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

## 2. Multiple Shapes in a Row

Three shapes spaced horizontally with 40px gaps:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Input" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="40" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="Output" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="360" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Layout math: shape width (120) + gap (40) = 160px spacing. Positions: 40, 200, 360.

## 3. Connected Edge with Relative Geometry

Two shapes connected by an edge with a label at the midpoint:

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
      <mxGeometry x="400" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="connects" style="endArrow=classic;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

## 4. Edge Label Positioning

Edge with label shifted toward the target and offset below the line:

```xml
<mxCell id="4" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry x="0.6" y="20" relative="1" as="geometry" />
</mxCell>
```

- `x="0.6"` = 60% along the edge path (closer to target)
- `y="20"` = 20 pixels below the edge path

## 5. Edge Label with Offset Fine-Tuning

Label at midpoint with additional pixel-level offset:

```xml
<mxCell id="4" value="Label" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry x="0" y="0" relative="1" as="geometry">
    <mxPoint x="15" y="-10" as="offset" />
  </mxGeometry>
</mxCell>
```

- `x="0"` = midpoint of edge
- Offset shifts the label 15px right and 10px up from the calculated midpoint

## 6. Edge with Waypoints

Orthogonal edge routed through two intermediate points:

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
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="300" y="130" />
          <mxPoint x="300" y="330" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

Route: A -> right to x=300 -> down to y=330 -> right to B.

## 7. Unconnected (Floating) Edge

Edge with explicit start and end coordinates, no source/target cells:

```xml
<mxCell id="5" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="100" y="200" as="sourcePoint" />
    <mxPoint x="400" y="350" as="targetPoint" />
    <Array as="points">
      <mxPoint x="250" y="200" />
      <mxPoint x="250" y="350" />
    </Array>
  </mxGeometry>
</mxCell>
```

## 8. Container with Relative Child Positioning

Group container with two children using relative coordinates:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- Container at (100, 100) on the canvas -->
    <mxCell id="10" value="Server Group" style="group;rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="300" height="200" as="geometry" />
    </mxCell>
    <!-- Child 1: relative (20, 20) = canvas (120, 120) -->
    <mxCell id="11" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="10">
      <mxGeometry x="20" y="20" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Child 2: relative (160, 20) = canvas (260, 120) -->
    <mxCell id="12" value="DB Server" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="10">
      <mxGeometry x="160" y="20" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Edge between children (parent = container) -->
    <mxCell id="13" style="endArrow=classic;html=1;"
            edge="1" source="11" target="12" parent="10">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

## 9. Nested Containers (Multi-Level Relative Coordinates)

Container inside a container — each level is relative to its direct parent:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- Outer container at canvas (50, 50) -->
    <mxCell id="10" value="Department" style="group;rounded=1;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="50" y="50" width="500" height="400" as="geometry" />
    </mxCell>
    <!-- Inner container at (20, 40) relative to outer = canvas (70, 90) -->
    <mxCell id="20" value="Team A" style="group;rounded=1;html=1;"
            vertex="1" parent="10">
      <mxGeometry x="20" y="40" width="200" height="150" as="geometry" />
    </mxCell>
    <!-- Shape at (10, 30) relative to inner = canvas (80, 120) -->
    <mxCell id="21" value="Alice" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="20">
      <mxGeometry x="10" y="30" width="80" height="40" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Canvas position calculation: outer.x + inner.x + shape.x = 50 + 20 + 10 = 80.

## 10. Collapsible Swimlane with alternateBounds

```xml
<mxCell id="10" value="Backend Services" style="swimlane;startSize=30;html=1;"
        vertex="1" collapsed="1" parent="1">
  <mxGeometry x="100" y="100" width="300" height="200" as="geometry">
    <mxRectangle x="100" y="100" width="160" height="30" as="alternateBounds" />
  </mxGeometry>
</mxCell>
<mxCell id="11" value="API Gateway" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="20" y="40" width="120" height="40" as="geometry" />
</mxCell>
```

Expanded: 300x200, children visible. Collapsed: 160x30, children hidden.

## 11. Fixed Connection Points

Edge forced to exit from the bottom of source and enter at the top of target:

```xml
<mxCell id="4" style="exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

- `exitX=0.5;exitY=1` = bottom-center of source
- `entryX=0.5;entryY=0` = top-center of target

## 12. Right-to-Left Connection

Edge exits the right side of source, enters the left side of target:

```xml
<mxCell id="4" style="exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

## 13. Vertex Label Outside the Shape

Label positioned to the right of the shape:

```xml
<mxCell id="2" value="Server" style="shape=ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;labelPosition=right;align=left;verticalLabelPosition=middle;verticalAlign=middle;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

Note: `labelPosition=right` paired with `align=left`.

## 14. Label Below the Shape

```xml
<mxCell id="2" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;verticalLabelPosition=bottom;verticalAlign=top;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="80" height="80" as="geometry" />
</mxCell>
```

Note: `verticalLabelPosition=bottom` paired with `verticalAlign=top`.

## 15. Non-Rectangular Shape with Correct Perimeter

Diamond (decision) shape with perimeter for correct edge attachment:

```xml
<mxCell id="5" value="Approve?" style="rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="100" height="100" as="geometry" />
</mxCell>
```

## 16. Complete Flowchart with Mixed Geometry

Full example combining vertices, edges, waypoints, and connection points:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- Start -->
    <mxCell id="2" value="Start" style="ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="80" height="80" as="geometry" />
    </mxCell>
    <!-- Process -->
    <mxCell id="3" value="Process Data" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="180" y="170" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Decision -->
    <mxCell id="4" value="Valid?" style="rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="190" y="280" width="100" height="100" as="geometry" />
    </mxCell>
    <!-- End -->
    <mxCell id="5" value="End" style="ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="440" width="80" height="80" as="geometry" />
    </mxCell>
    <!-- Error -->
    <mxCell id="6" value="Handle Error" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;"
            vertex="1" parent="1">
      <mxGeometry x="380" y="300" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Edge: Start -> Process (bottom-center to top-center) -->
    <mxCell id="7" style="exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endArrow=classic;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <!-- Edge: Process -> Decision -->
    <mxCell id="8" style="exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endArrow=classic;html=1;"
            edge="1" source="3" target="4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <!-- Edge: Decision -> End (Yes) -->
    <mxCell id="9" value="Yes" style="exitX=0.5;exitY=1;exitDx=0;exitDy=0;entryX=0.5;entryY=0;entryDx=0;entryDy=0;endArrow=classic;html=1;"
            edge="1" source="4" target="5" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <!-- Edge: Decision -> Error (No, exits right side) -->
    <mxCell id="10" value="No" style="exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;endArrow=classic;html=1;"
            edge="1" source="4" target="6" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <!-- Edge: Error -> Process (loop back with waypoints) -->
    <mxCell id="11" style="exitX=0.5;exitY=0;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
            edge="1" source="6" target="3" parent="1">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="440" y="200" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```
