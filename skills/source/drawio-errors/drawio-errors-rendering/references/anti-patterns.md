# Draw.io Rendering Errors — Anti-Patterns

> What NOT to do when diagnosing and fixing Draw.io rendering issues.
> Every anti-pattern includes the wrong approach, why it fails, and the correct fix.

---

## AP-01: Making Shapes Fully Transparent Without Intent

### Wrong

```xml
<mxCell id="2" value="Invisible" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=none;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Setting both `fillColor=none` and `strokeColor=none` renders the shape completely invisible. The shape exists in the XML and occupies space, but the user cannot see or interact with it visually. The label still renders (if `textOpacity > 0`), creating a floating text effect that confuses viewers.

### Correct

```xml
<mxCell id="2" value="Visible" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

NEVER set both `fillColor=none` and `strokeColor=none` unless the shape is intentionally used as an invisible spacer or click target.

---

## AP-02: Ignoring Perimeter-Shape Mismatch

### Wrong

```xml
<mxCell id="2" value="Decision" style="rhombus;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
</mxCell>
```

### Why It Fails

The rhombus shape has no explicit `perimeter` set. While some shapes inherit the correct perimeter from Draw.io defaults, relying on implicit behavior is fragile. If the shape is loaded in a different context or the default behavior changes, edges will connect at the rectangular bounding box instead of the diamond's angled sides.

### Correct

```xml
<mxCell id="2" value="Decision" style="rhombus;whiteSpace=wrap;html=1;perimeter=rhombusPerimeter;fillColor=#FFF2CC;strokeColor=#D6B656;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
</mxCell>
```

### Rule

ALWAYS explicitly set the `perimeter` property on non-rectangular shapes. NEVER rely on implicit perimeter inheritance for AI-generated diagrams.

---

## AP-03: Using overflow=hidden to "Fix" Long Labels

### Wrong

```xml
<mxCell id="3" value="This important text gets cut off and the user misses critical information" style="rounded=1;whiteSpace=wrap;html=1;overflow=hidden;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="200" width="80" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

Setting `overflow=hidden` on a shape that is too small silently clips the label. The user sees only the first few words. This hides information instead of fixing the root cause (insufficient shape size).

### Correct

```xml
<mxCell id="3" value="This important text now fits properly in the larger shape" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="200" width="200" height="80" as="geometry" />
</mxCell>
```

### Rule

NEVER use `overflow=hidden` to mask a sizing problem. ALWAYS resize the shape to fit its content, or reduce the text length. Use `overflow=hidden` ONLY when deliberate text clipping is the design intent (e.g., table cells with known fixed content).

---

## AP-04: Placing Children with Absolute Page Coordinates

### Wrong

```xml
<!-- Container at page position (200, 100) -->
<mxCell id="grp" value="Group" style="swimlane;startSize=30;container=1;html=1;" vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="300" height="200" as="geometry" />
</mxCell>
<!-- Child using absolute page coordinates instead of relative -->
<mxCell id="c1" value="Child" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="grp">
  <mxGeometry x="220" y="150" width="100" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

The child `c1` uses absolute page coordinates `(220, 150)`. Since children in a container use RELATIVE coordinates, this actually places the child at page position `(200+220, 100+150) = (420, 250)`, which is far outside the container's visual bounds.

### Correct

```xml
<mxCell id="c1" value="Child" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="grp">
  <mxGeometry x="20" y="40" width="100" height="40" as="geometry" />
</mxCell>
```

### Rule

ALWAYS use container-relative coordinates for children. To convert: `child_relative_x = child_absolute_x - container_x`, `child_relative_y = child_absolute_y - container_y`.

---

## AP-05: Forgetting container=1 on Group Shapes

### Wrong

```xml
<mxCell id="grp" value="Process Group" style="swimlane;startSize=30;html=1;fillColor=#F5F5F5;" vertex="1" parent="1">
  <mxGeometry x="50" y="50" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="c1" value="Step 1" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="grp">
  <mxGeometry x="20" y="40" width="100" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

The swimlane shape is missing `container=1`. Without this property, the parent-child relationship is not fully established. Children will not move with the parent when dragged, and the container will not auto-resize to fit children.

### Correct

```xml
<mxCell id="grp" value="Process Group" style="swimlane;startSize=30;container=1;html=1;fillColor=#F5F5F5;" vertex="1" parent="1">
  <mxGeometry x="50" y="50" width="300" height="200" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `container=1` in the style of any shape that holds children. This applies to swimlanes, groups, and any custom container shape.

---

## AP-06: Setting Shadow on Cells Without Model-Level Shadow

### Wrong

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow Box" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

The cell has `shadow=1` in its style, but the `<mxGraphModel>` element has no `shadow` attribute (defaults to `0`). Draw.io requires the model-level `shadow="1"` to enable shadow rendering. Without it, ALL per-cell shadow properties are ignored.

### Correct

```xml
<mxGraphModel shadow="1">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow Box" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Rule

ALWAYS set `shadow="1"` on the `<mxGraphModel>` element when any cell uses `shadow=1`. Check the model-level attribute FIRST when diagnosing missing shadows.

---

## AP-07: Using true/false for Boolean Style Properties

### Wrong

```xml
<mxCell id="4" value="Styled" style="rounded=true;dashed=true;shadow=true;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="300" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Draw.io uses `0`/`1` for ALL boolean style properties. The values `true` and `false` are not recognized and are silently ignored. The shape renders with `rounded=0`, `dashed=0`, and `shadow=0` (all defaults).

### Correct

```xml
<mxCell id="4" value="Styled" style="rounded=1;dashed=1;shadow=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="300" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

NEVER use `true` or `false` for Draw.io style properties. ALWAYS use `1` (on) or `0` (off).

---

## AP-08: Missing html=1 Causing Plain Text Labels

### Wrong

```xml
<mxCell id="5" value="&lt;b&gt;Bold Title&lt;/b&gt;&lt;br&gt;Description" style="rounded=1;whiteSpace=wrap;fillColor=#DAE8FC;" vertex="1" parent="1">
  <mxGeometry x="100" y="400" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `html=1`, the value is rendered as plain text. The HTML tags `<b>` and `<br>` display as literal characters instead of formatting the text as bold with a line break.

### Correct

```xml
<mxCell id="5" value="&lt;b&gt;Bold Title&lt;/b&gt;&lt;br&gt;Description" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;" vertex="1" parent="1">
  <mxGeometry x="100" y="400" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `html=1` in every vertex and edge style string. This is mandatory for all AI-generated Draw.io diagrams.

---

## AP-09: Conflicting labelPosition and align Values

### Wrong

```xml
<mxCell id="6" value="Label" style="rounded=1;whiteSpace=wrap;html=1;labelPosition=left;align=left;" vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="80" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

Both `labelPosition=left` and `align=left` push the label in the same direction. The label renders far to the left of the shape, detached from it. The `align` property controls text alignment WITHIN the label bounds, and it MUST oppose `labelPosition` to keep the label visually attached.

### Correct

```xml
<mxCell id="6" value="Label" style="rounded=1;whiteSpace=wrap;html=1;labelPosition=left;align=right;" vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="80" height="40" as="geometry" />
</mxCell>
```

### Rule

When `labelPosition` is `left`, set `align=right`. When `labelPosition` is `right`, set `align=left`. The same applies vertically: `verticalLabelPosition=top` requires `verticalAlign=bottom`, and vice versa. NEVER set both properties to the same non-center value.

---

## AP-10: Missing Edge relative="1" Causing Label Drift

### Wrong

```xml
<mxCell id="e1" value="connects to" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

### Why It Fails

Without `relative="1"` on the edge's `<mxGeometry>`, label positioning and waypoint calculations use absolute coordinates. The label drifts to an unexpected position, and any `<mxPoint>` waypoints inside the geometry are misinterpreted.

### Correct

```xml
<mxCell id="e1" value="connects to" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `relative="1"` on every edge `<mxGeometry>`. NEVER omit this attribute on edges.

---

## AP-11: Relying on Custom Fonts in Export

### Wrong

```xml
<mxCell id="7" value="Fancy Text" style="rounded=1;whiteSpace=wrap;html=1;fontFamily=MyCustomFont;" vertex="1" parent="1">
  <mxGeometry x="100" y="500" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Custom fonts like `MyCustomFont` are available only when that font is installed on the system running the Draw.io editor. SVG and PNG exports do not embed custom fonts. The exported diagram falls back to a default font, changing the visual appearance and potentially breaking label sizing.

### Correct

```xml
<mxCell id="7" value="Fancy Text" style="rounded=1;whiteSpace=wrap;html=1;fontFamily=Helvetica;" vertex="1" parent="1">
  <mxGeometry x="100" y="500" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

ALWAYS use web-safe fonts for AI-generated diagrams: `Helvetica`, `Arial`, `Verdana`, `Times New Roman`, `Courier New`. NEVER rely on custom fonts unless the diagram is for local use only and will not be exported.

---

## AP-12: Setting dashPattern Without dashed=1

### Wrong

```xml
<mxCell id="8" value="Dashed?" style="rounded=1;whiteSpace=wrap;html=1;dashPattern=8 4;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="600" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

The `dashPattern` property defines the pattern, but it has no effect unless `dashed=1` is also set. Without the `dashed` flag, the stroke renders as a solid line regardless of the pattern.

### Correct

```xml
<mxCell id="8" value="Dashed!" style="rounded=1;whiteSpace=wrap;html=1;dashed=1;dashPattern=8 4;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="600" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

ALWAYS set `dashed=1` alongside `dashPattern`. The pattern property alone does nothing.
