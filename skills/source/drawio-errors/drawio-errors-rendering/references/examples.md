# Draw.io Rendering Errors — Diagnostic Examples

> Every example shows a broken diagram, the diagnosis, and the corrected XML.

---

## 1. Invisible Shape — Both Colors Set to None

### Broken XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Ghost Shape" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=none;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Diagnosis

The shape has `fillColor=none` AND `strokeColor=none`. Both the fill and border are transparent, making the shape completely invisible on the canvas.

### Fixed XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Visible Shape" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Invisible Shape — Zero Opacity

### Broken XML

```xml
<mxCell id="3" value="Faded Away" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;opacity=0;" vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="60" as="geometry" />
</mxCell>
```

### Diagnosis

`opacity=0` makes the entire shape (fill, stroke, and label) fully transparent.

### Fixed XML

```xml
<mxCell id="3" value="Visible Again" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;opacity=100;" vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 3. Wrong Perimeter — Ellipse with Rectangle Perimeter

### Broken XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="ellipse;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;fillColor=#E1D5E7;strokeColor=#9673A6;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
    </mxCell>
    <mxCell id="3" value="End" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="endArrow=classic;html=1;" edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Diagnosis

The ellipse shape uses `perimeter=rectanglePerimeter`. The edge routing algorithm calculates the connection point on a rectangular bounding box instead of the ellipse curve. The edge endpoint visibly floats away from the ellipse outline.

### Fixed XML

```xml
<mxCell id="2" value="Start" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;fillColor=#E1D5E7;strokeColor=#9673A6;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
</mxCell>
```

---

## 4. Label Truncated — Missing whiteSpace=wrap

### Broken XML

```xml
<mxCell id="4" value="This is a very long label that extends far beyond the shape boundaries" style="rounded=1;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;" vertex="1" parent="1">
  <mxGeometry x="100" y="300" width="120" height="60" as="geometry" />
</mxCell>
```

### Diagnosis

Without `whiteSpace=wrap`, the label renders as a single line that extends beyond the 120px shape width. The text overflows visually, creating an unreadable layout.

### Fixed XML

```xml
<mxCell id="4" value="This is a very long label that extends far beyond the shape boundaries" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;" vertex="1" parent="1">
  <mxGeometry x="100" y="300" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 5. Label Missing — noLabel=1

### Broken XML

```xml
<mxCell id="5" value="Important Text" style="rounded=1;whiteSpace=wrap;html=1;noLabel=1;fillColor=#F8CECC;strokeColor=#B85450;" vertex="1" parent="1">
  <mxGeometry x="100" y="400" width="120" height="60" as="geometry" />
</mxCell>
```

### Diagnosis

`noLabel=1` suppresses the label entirely. The shape renders but the text "Important Text" is hidden.

### Fixed XML

```xml
<mxCell id="5" value="Important Text" style="rounded=1;whiteSpace=wrap;html=1;noLabel=0;fillColor=#F8CECC;strokeColor=#B85450;" vertex="1" parent="1">
  <mxGeometry x="100" y="400" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 6. Label Detached — Same labelPosition and align

### Broken XML

```xml
<mxCell id="6" value="Detached Label" style="rounded=1;whiteSpace=wrap;html=1;labelPosition=right;align=right;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="500" width="120" height="60" as="geometry" />
</mxCell>
```

### Diagnosis

Both `labelPosition=right` and `align=right` push the label to the right. The label renders far away from the shape instead of adjacent to it. When `labelPosition` is not `center`, `align` MUST be the opposite value.

### Fixed XML

```xml
<mxCell id="6" value="Adjacent Label" style="rounded=1;whiteSpace=wrap;html=1;labelPosition=right;align=left;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="500" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 7. Edge Label Misplaced — Missing relative="1"

### Broken XML

```xml
<mxCell id="e2" value="sends data" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

### Diagnosis

The edge `<mxGeometry>` is missing `relative="1"`. Without it, the edge label position and any waypoints use absolute coordinates instead of relative positioning along the edge path. The label renders at the wrong location.

### Fixed XML

```xml
<mxCell id="e2" value="sends data" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

---

## 8. Container Children at Wrong Position — Missing container=1

### Broken XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="grp" value="My Group" style="swimlane;horizontal=1;startSize=30;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;html=1;" vertex="1" parent="1">
      <mxGeometry x="50" y="50" width="300" height="200" as="geometry" />
    </mxCell>
    <mxCell id="c1" value="Child A" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="grp">
      <mxGeometry x="20" y="40" width="100" height="40" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Diagnosis

The swimlane `grp` is missing `container=1`. Without it, the child `c1` does not behave as a contained element — it will not move with the parent and coordinate interpretation may be incorrect.

### Fixed XML

```xml
<mxCell id="grp" value="My Group" style="swimlane;horizontal=1;startSize=30;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;container=1;html=1;" vertex="1" parent="1">
  <mxGeometry x="50" y="50" width="300" height="200" as="geometry" />
</mxCell>
```

---

## 9. Children Overlap Swimlane Header

### Broken XML

```xml
<mxCell id="sw" value="Process" style="swimlane;horizontal=1;startSize=30;container=1;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="50" y="50" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="ch1" value="Step 1" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="sw">
  <mxGeometry x="20" y="5" width="100" height="40" as="geometry" />
</mxCell>
```

### Diagnosis

The child shape starts at `y=5`, but the swimlane header is 30px tall (`startSize=30`). The child overlaps the header text. First child y-coordinate MUST be >= startSize.

### Fixed XML

```xml
<mxCell id="ch1" value="Step 1" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="sw">
  <mxGeometry x="20" y="40" width="100" height="40" as="geometry" />
</mxCell>
```

---

## 10. Shadow Not Rendering — Missing Model-Level Shadow

### Broken XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow Box" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Diagnosis

The cell has `shadow=1` in its style, but the `<mxGraphModel>` element does not have `shadow="1"`. Per-cell shadow properties are ONLY rendered when the model-level shadow attribute is also enabled.

### Fixed XML

```xml
<mxGraphModel shadow="1">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow Box" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 11. Boolean Property Ignored — Using true/false

### Broken XML

```xml
<mxCell id="7" value="Styled Box" style="rounded=true;whiteSpace=wrap;html=1;dashed=true;shadow=true;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="600" width="120" height="60" as="geometry" />
</mxCell>
```

### Diagnosis

Properties `rounded=true`, `dashed=true`, and `shadow=true` use string booleans. Draw.io ALWAYS uses `0`/`1` for booleans. String values like `true`/`false` are silently ignored, so none of these effects render.

### Fixed XML

```xml
<mxCell id="7" value="Styled Box" style="rounded=1;whiteSpace=wrap;html=1;dashed=1;shadow=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="600" width="120" height="60" as="geometry" />
</mxCell>
```

---

## 12. Connection Points Outside 0–1 Range

### Broken XML

```xml
<mxCell id="e3" style="endArrow=classic;html=1;exitX=1.5;exitY=0.5;exitDx=0;exitDy=0;entryX=-0.5;entryY=0.5;entryDx=0;entryDy=0;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Diagnosis

`exitX=1.5` places the departure point 50% beyond the right edge of the source shape. `entryX=-0.5` places the arrival point 50% beyond the left edge of the target shape. Both endpoints float in empty space away from the shapes.

### Fixed XML

```xml
<mxCell id="e3" style="endArrow=classic;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;entryX=0;entryY=0.5;entryDx=0;entryDy=0;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```
