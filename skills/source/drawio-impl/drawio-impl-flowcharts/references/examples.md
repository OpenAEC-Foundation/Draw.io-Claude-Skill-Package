# Examples: Flowchart Implementation

Working XML examples for flowchart patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal Flowchart (3 Shapes)

The simplest valid flowchart: Start, one process step, End.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="step1" value="Do Something" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
    </mxCell>
    <mxCell id="end" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="200" y="220" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="start" target="step1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="step1" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Single Decision Branch

A flowchart with one Yes/No decision point.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
    </mxCell>

    <mxCell id="check" value="Check&lt;br&gt;Condition" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="200" y="120" width="120" height="80" as="geometry" />
    </mxCell>

    <mxCell id="yes_action" value="Handle Yes" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="240" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="no_action" value="Handle No" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="400" y="140" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="end" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="200" y="340" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="start" target="check">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="check" target="yes_action">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="check" target="no_action">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="yes_action" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="no_action" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Loop Pattern (While Loop)

A process step with a decision that loops back.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
    </mxCell>

    <mxCell id="init" value="Initialize&lt;br&gt;Counter" style="shape=hexagon;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="process" value="Process&lt;br&gt;Item" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="220" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="more" value="More&lt;br&gt;Items?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="200" y="320" width="120" height="80" as="geometry" />
    </mxCell>

    <mxCell id="end" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="200" y="440" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="start" target="init">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="init" target="process">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="process" target="more">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="more" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <!-- Loop back: Yes exits right, goes up, re-enters process from right -->
    <mxCell id="e5" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=1;entryY=0.5;entryDx=0;entryDy=0;" edge="1" parent="1" source="more" target="process">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="380" y="360" />
          <mxPoint x="380" y="250" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

Key points for loops:
- The loop-back edge uses explicit `exitX/exitY` and `entryX/entryY` to route the edge around the shapes.
- Waypoints (`<Array as="points">`) define the path of the loop-back connector.
- The "Yes" label on the loop-back edge indicates "continue looping."

---

## 4. Multi-Shape Type Flowchart

Demonstrates all ISO 5807 shape types in a single flowchart.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Terminator: Start -->
    <mxCell id="s1" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="200" y="20" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Manual Input -->
    <mxCell id="s2" value="Enter&lt;br&gt;Username" style="shape=manualInput;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="190" y="100" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Data I/O -->
    <mxCell id="s3" value="Read User&lt;br&gt;Record" style="shape=parallelogram;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;" vertex="1" parent="1">
      <mxGeometry x="190" y="200" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Preparation -->
    <mxCell id="s4" value="Initialize&lt;br&gt;Session" style="shape=hexagon;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="190" y="300" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Decision -->
    <mxCell id="s5" value="Authorized?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="200" y="400" width="120" height="80" as="geometry" />
    </mxCell>

    <!-- Process -->
    <mxCell id="s6" value="Load&lt;br&gt;Dashboard" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="520" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Predefined Process -->
    <mxCell id="s7" value="Audit Log&lt;br&gt;Routine" style="shape=process;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="620" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Document -->
    <mxCell id="s8" value="Generate&lt;br&gt;Report" style="shape=document;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="1">
      <mxGeometry x="190" y="720" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Database -->
    <mxCell id="s9" value="Save to&lt;br&gt;Database" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;" vertex="1" parent="1">
      <mxGeometry x="200" y="820" width="120" height="80" as="geometry" />
    </mxCell>

    <!-- Terminator: End -->
    <mxCell id="s10" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="200" y="940" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Error path -->
    <mxCell id="s11" value="Show Error" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="400" y="420" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Connections (main path) -->
    <mxCell id="c1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s1" target="s2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s2" target="s3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c3" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s3" target="s4">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c4" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s4" target="s5">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c5" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s5" target="s6">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c6" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s5" target="s11">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c7" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s6" target="s7">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c8" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s7" target="s8">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c9" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s8" target="s9">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c10" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s9" target="s10">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c11" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="s11" target="s10">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Left-to-Right Flowchart

Same logic as top-to-bottom, but with horizontal flow direction.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="40" y="200" width="120" height="40" as="geometry" />
    </mxCell>

    <mxCell id="step1" value="Process&lt;br&gt;Request" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="200" y="190" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="dec1" value="Approved?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="380" y="180" width="120" height="80" as="geometry" />
    </mxCell>

    <mxCell id="approve" value="Execute" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="560" y="190" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="reject" value="Reject" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="370" y="320" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="end" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="740" y="200" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="start" target="step1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="step1" target="dec1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="dec1" target="approve">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="dec1" target="reject">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="approve" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e6" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="reject" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Key difference for left-to-right: the primary path advances along the x-axis, and alternate branches exit downward (increasing y).
