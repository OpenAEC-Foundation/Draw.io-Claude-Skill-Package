# Draw.io Core Styles — Anti-Patterns

> What NOT to do when styling Draw.io diagrams. Every anti-pattern includes the wrong
> approach, why it fails, and the correct fix.

---

## AP-01: Missing html=1

### Wrong

```xml
<mxCell id="2" value="My Label" style="rounded=1;whiteSpace=wrap;fillColor=#DAE8FC;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `html=1`, Draw.io renders labels as plain text. All HTML formatting (line breaks,
bold, colors within labels) is lost. Rich text features like `<br>` tags in the `value`
attribute are displayed as literal text.

### Correct

```xml
<mxCell id="2" value="My Label" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `html=1` in every vertex and edge style string.

---

## AP-02: Wrong Perimeter for Shape

### Wrong

```xml
<!-- Ellipse with rectangle perimeter -->
<mxCell id="2" value="Circle" style="ellipse;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
</mxCell>
```

### Why It Fails

The perimeter function calculates where edges connect to the shape boundary. When the
perimeter does not match the shape, edges connect at positions calculated for a different
geometry. For an ellipse with `rectanglePerimeter`, edges connect at the bounding box
corners/sides instead of the curved boundary, creating visible gaps.

### Correct

```xml
<mxCell id="2" value="Circle" style="ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="100" height="100" as="geometry" />
</mxCell>
```

### Rule

ALWAYS match the perimeter to the shape type. Reference the perimeter-shape mapping table
in SKILL.md Section 5.

---

## AP-03: Using true/false Instead of 0/1

### Wrong

```
rounded=true;dashed=true;shadow=true;html=true;
```

### Why It Fails

Draw.io boolean properties use `0` and `1` as integers, NOT string values `"true"` and
`"false"`. String boolean values are silently ignored — the property reverts to its
default, and no error is thrown.

### Correct

```
rounded=1;dashed=1;shadow=1;html=1;
```

### Rule

ALWAYS use `0` (false) and `1` (true) for boolean style properties. NEVER use `true`,
`false`, `yes`, `no`, or any other boolean representation.

---

## AP-04: Conflicting labelPosition and align

### Wrong

```
labelPosition=right;align=right;html=1;whiteSpace=wrap;
```

### Why It Fails

When `labelPosition=right`, the label is placed to the right of the shape. If `align` is
also `right`, the text within the label is right-aligned — pushing it AWAY from the shape.
This creates a visual disconnect where the label floats far from its shape.

### Correct

```
labelPosition=right;align=left;html=1;whiteSpace=wrap;
```

### Rule

When `labelPosition` is NOT `center`, ALWAYS set `align` to the OPPOSITE direction.
When `verticalLabelPosition` is NOT `middle`, ALWAYS set `verticalAlign` to the OPPOSITE direction.

| labelPosition | Required align |
|---------------|---------------|
| `left` | `right` |
| `right` | `left` |
| `center` | any (no constraint) |

| verticalLabelPosition | Required verticalAlign |
|-----------------------|-----------------------|
| `top` | `bottom` |
| `bottom` | `top` |
| `middle` | any (no constraint) |

---

## AP-05: Missing whiteSpace=wrap

### Wrong

```xml
<mxCell id="2" value="This is a very long label that will overflow" style="html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `whiteSpace=wrap`, long labels render as a single line that extends beyond the
shape boundaries. The text overflows and overlaps with neighboring shapes.

### Correct

```xml
<mxCell id="2" value="This is a very long label that will wrap" style="whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `whiteSpace=wrap` for shapes that have text labels.

---

## AP-06: Edge Missing relative="1" on Geometry

### Wrong

```xml
<mxCell id="e1" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

### Why It Fails

Edge geometry uses a relative coordinate system where positions along the edge are
expressed as values between -1 and 1 (0 = midpoint). Without `relative="1"`, the
geometry uses absolute coordinates, causing edge labels and waypoints to be positioned
incorrectly — often appearing at the canvas origin instead of along the edge path.

### Correct

```xml
<mxCell id="e1" style="endArrow=classic;html=1;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `relative="1"` on the `mxGeometry` element of every edge.

---

## AP-07: Applying Vertex-Only Properties to Edges

### Wrong

```xml
<!-- fillColor on an edge — silently ignored -->
<mxCell id="e1" style="endArrow=classic;html=1;fillColor=#DAE8FC;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`fillColor` is a vertex-only property. When applied to an edge, it is silently ignored.
The edge renders with default stroke color. This wastes style string space and confuses
readers who expect the edge to be colored.

### Correct

```xml
<!-- Use strokeColor for edge color -->
<mxCell id="e1" style="endArrow=classic;html=1;strokeColor=#6C8EBF;" edge="1" source="a" target="b" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Rule

NEVER apply vertex-only properties to edges. Use `strokeColor` for edge color, NOT
`fillColor`.

**Vertex-only properties:** `fillColor`, `shape` (except `connector`), `container`,
`collapsible`, `swimlane`, `glass`.

**Edge-only properties:** `edgeStyle`, `startArrow`, `endArrow`, `curved`, `jettySize`,
`exitX/Y`, `entryX/Y`, `sourceJettySize`, `targetJettySize`.

---

## AP-08: Shadow Without Global Shadow

### Wrong

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow?" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

The per-cell `shadow=1` property ONLY renders when the `<mxGraphModel>` element also has
`shadow="1"`. Without the model-level attribute, individual cell shadows are invisible.

### Correct

```xml
<mxGraphModel shadow="1">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Shadow!" style="rounded=1;whiteSpace=wrap;html=1;shadow=1;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Rule

When using `shadow=1` on any cell, ALWAYS set `shadow="1"` on the `<mxGraphModel>` element.

---

## AP-09: Incorrect Dash Pattern Format

### Wrong

```
dashed=1;dashPattern=84;
```

### Why It Fails

The `dashPattern` value is a **space-separated** list of dash and gap lengths in pixels.
The value `84` is interpreted as a single 84-pixel dash with no gap, creating what appears
to be a solid line.

### Correct

```
dashed=1;dashPattern=8 4;
```

### Rule

ALWAYS use space-separated values for `dashPattern` (e.g., `"8 4"` = 8px dash, 4px gap).
ALWAYS set `dashed=1` alongside `dashPattern` — the pattern alone does nothing.

---

## AP-10: Forgetting container=1 for Groups

### Wrong

```xml
<mxCell id="group1" value="Group" style="swimlane;html=1;startSize=30;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="400" height="300" as="geometry" />
</mxCell>
<mxCell id="child1" value="Child" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="group1">
  <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `container=1`, Draw.io does not treat the shape as a container. Child shapes
referenced via `parent="group1"` are rendered, but:
- Children do NOT move when the parent is dragged
- Children are NOT clipped to parent bounds
- Coordinates may not be relative to parent origin as expected

### Correct

```xml
<mxCell id="group1" value="Group" style="swimlane;html=1;startSize=30;container=1;collapsible=0;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="400" height="300" as="geometry" />
</mxCell>
<mxCell id="child1" value="Child" style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="group1">
  <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
</mxCell>
```

### Rule

ALWAYS include `container=1` on any shape that holds child shapes. For swimlanes, ALWAYS
include both `container=1` and `collapsible=0` (unless collapse is explicitly desired).

---

## AP-11: Invalid Color Values

### Wrong

```
fillColor=red;strokeColor=rgb(0,0,255);fontColor=#FFF;
```

### Why It Fails

Draw.io does NOT support:
- Named CSS colors (`red`, `blue`, `green`)
- RGB function syntax (`rgb(0,0,255)`)
- Short hex notation (`#FFF`, `#000`)

These values are silently ignored or cause unpredictable rendering. The property reverts
to its default.

### Correct

```
fillColor=#FF0000;strokeColor=#0000FF;fontColor=#FFFFFF;
```

### Rule

ALWAYS use `#RRGGBB` (6-digit hex), `none`, or `default` for color values. NEVER use
named colors, short hex, RGB functions, HSL, or any other CSS color format.

---

## AP-12: Missing Trailing Semicolon

### Wrong

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC
```

### Why It Fails

While Draw.io MAY parse a style string without a trailing semicolon, omitting it creates
fragility. When additional properties are appended programmatically, the last property
merges with the new one (e.g., `fillColor=#DAE8FCnewProp=value`), causing both to fail
silently.

### Correct

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;
```

### Rule

ALWAYS terminate style strings with a semicolon. This prevents concatenation errors when
properties are added dynamically.

---

## AP-13: Using fontStyle as Non-Bitmask

### Wrong

```
fontStyle=bold;
```

### Why It Fails

The `fontStyle` property takes an **integer bitmask**, not a string keyword. The value
`"bold"` is not a valid integer and is ignored. The text renders as normal (non-bold).

### Correct

```
fontStyle=1;
```

### Rule

ALWAYS use the integer bitmask for `fontStyle`: 1=bold, 2=italic, 4=underline,
8=strikethrough. Combine by adding values (bold+italic = 3).

---

## AP-14: Spaces Around = or ; in Style Strings

### Wrong

```
rounded = 1; whiteSpace = wrap; html = 1;
```

### Why It Fails

Style string parsing is exact. Spaces around `=` cause the property name to include a
trailing space and the value to include a leading space. The property ` rounded ` (with
space) does not match `rounded` and is ignored.

### Correct

```
rounded=1;whiteSpace=wrap;html=1;
```

### Rule

NEVER include spaces around `=` or after `;` in style strings. The format is strictly
`key=value;key=value;`.
