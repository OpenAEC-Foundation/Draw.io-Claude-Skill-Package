# Geometry Anti-Patterns

Common mistakes that cause shapes to disappear, edges to misroute, or layouts to break.

---

## AP-01: Missing width and height on Vertices

**Problem:** Shape is invisible (renders as 0x0 pixels).

```xml
<!-- WRONG: no width or height -->
<mxCell id="2" value="Ghost" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="150" as="geometry" />
</mxCell>
```

**Fix:** ALWAYS specify width and height with values > 0.

```xml
<!-- CORRECT -->
<mxCell id="2" value="Visible" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="150" width="120" height="60" as="geometry" />
</mxCell>
```

**Why:** Draw.io has NO implicit sizing. Unlike HTML elements that size to content, mxGraph renders shapes at exactly the specified dimensions. Zero or missing dimensions = invisible.

---

## AP-02: Missing relative="1" on Edge Geometry

**Problem:** Edge renders incorrectly or disappears. Label appears at wrong position.

```xml
<!-- WRONG: no relative="1" -->
<mxCell id="4" value="Label" style="endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

**Fix:** ALWAYS set `relative="1"` on edge geometry.

```xml
<!-- CORRECT -->
<mxCell id="4" value="Label" style="endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Why:** Without `relative="1"`, the geometry x/y are treated as absolute canvas coordinates instead of edge-relative label positioning. The edge routing engine expects relative mode for connected edges.

---

## AP-03: Absolute Coordinates Inside Containers

**Problem:** Child shapes appear at the wrong position, far from the container, or overlapping each other.

```xml
<!-- Container at canvas (300, 200) -->
<mxCell id="10" value="Group" style="group" vertex="1" parent="1">
  <mxGeometry x="300" y="200" width="400" height="300" as="geometry" />
</mxCell>
<!-- WRONG: using canvas coordinates for child -->
<mxCell id="11" value="Server" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="320" y="220" width="120" height="60" as="geometry" />
</mxCell>
```

The child appears at canvas position (300 + 320, 200 + 220) = (620, 420), which is OUTSIDE the container.

**Fix:** NEVER use absolute canvas coordinates for container children. Use coordinates relative to the parent's top-left corner.

```xml
<!-- CORRECT: relative coordinates (20, 20) inside the container -->
<mxCell id="11" value="Server" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="10">
  <mxGeometry x="20" y="20" width="120" height="60" as="geometry" />
</mxCell>
```

**Why:** When `parent` points to a container (not the default layer "1"), Draw.io adds the child's x/y to the parent's x/y. If the child already uses canvas-absolute values, the result is double-offset positioning.

---

## AP-04: Missing as="geometry" on mxGeometry

**Problem:** Shape has no position or size. Renders at (0,0) with 0x0 dimensions.

```xml
<!-- WRONG: missing as="geometry" -->
<mxCell id="2" value="Lost" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="150" width="120" height="60" />
</mxCell>
```

**Fix:** ALWAYS include `as="geometry"` on the mxGeometry element.

```xml
<!-- CORRECT -->
<mxCell id="2" value="Found" style="rounded=1;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="150" width="120" height="60" as="geometry" />
</mxCell>
```

**Why:** The `as="geometry"` attribute is the binding mechanism that tells mxGraph to use this element as the cell's geometry. Without it, the mxGeometry is ignored.

---

## AP-05: Width and Height on Edge Geometry

**Problem:** Unpredictable edge rendering and label sizing.

```xml
<!-- WRONG: width/height on edge geometry -->
<mxCell id="4" style="endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry width="50" height="50" relative="1" as="geometry" />
</mxCell>
```

**Fix:** NEVER set width or height on edge geometry. Edge dimensions are determined by source/target positions and waypoints.

```xml
<!-- CORRECT -->
<mxCell id="4" style="endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Why:** Width and height on edge geometry are used internally for label bounding box calculations. Setting them explicitly interferes with the automatic label sizing.

---

## AP-06: Waypoints with as="geometry" Instead of as="points"

**Problem:** Waypoints are ignored. Edge routes directly from source to target.

```xml
<!-- WRONG: as="geometry" on Array -->
<mxGeometry relative="1" as="geometry">
  <Array as="geometry">
    <mxPoint x="300" y="150" />
  </Array>
</mxGeometry>
```

**Fix:** ALWAYS use `as="points"` on the Array element.

```xml
<!-- CORRECT -->
<mxGeometry relative="1" as="geometry">
  <Array as="points">
    <mxPoint x="300" y="150" />
  </Array>
</mxGeometry>
```

**Why:** The `as` attribute acts as a key. mxGraph looks for `as="points"` to find waypoint data. Any other value is ignored for routing purposes.

---

## AP-07: Connection Points Outside 0.0-1.0 Range

**Problem:** Edge exits or enters at an unexpected location, potentially far from the shape.

```xml
<!-- WRONG: exitX=2 is outside the shape bounds -->
<mxCell id="4" style="exitX=2;exitY=0.5;entryX=0;entryY=0.5;endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Fix:** ALWAYS keep exitX, exitY, entryX, entryY in the 0.0-1.0 range.

```xml
<!-- CORRECT: exitX=1 is the right edge of the shape -->
<mxCell id="4" style="exitX=1;exitY=0.5;entryX=0;entryY=0.5;endArrow=classic;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Why:** These are relative coordinates where 0.0 = left/top edge and 1.0 = right/bottom edge of the shape's bounding box. Values outside this range project the connection point beyond the shape boundary.

---

## AP-08: Mismatched labelPosition and align

**Problem:** Label appears to float away from the shape instead of being visually attached.

```xml
<!-- WRONG: both push label to the right -->
style="labelPosition=right;align=right;"
```

**Fix:** ALWAYS set `align` to the OPPOSITE of `labelPosition`.

```xml
<!-- CORRECT: label right of shape, text aligned left toward shape -->
style="labelPosition=right;align=left;"
```

**Why:** `labelPosition` moves the label bounding box relative to the shape. `align` controls text alignment within that bounding box. When both point the same direction, the text drifts away from the shape.

---

## AP-09: Missing Perimeter on Non-Rectangular Shapes

**Problem:** Edges connect to the bounding rectangle instead of the actual shape outline.

```xml
<!-- WRONG: ellipse without perimeter -->
<mxCell id="2" value="Start" style="ellipse;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="80" height="80" as="geometry" />
</mxCell>
```

**Fix:** ALWAYS add the matching perimeter style for non-rectangular shapes.

```xml
<!-- CORRECT -->
<mxCell id="2" value="Start" style="ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="80" height="80" as="geometry" />
</mxCell>
```

**Why:** Without an explicit perimeter, mxGraph defaults to the rectangular perimeter. Edges will connect to the invisible bounding box corners instead of the ellipse outline, creating visually incorrect connections.

---

## AP-10: alternateBounds Position Mismatch

**Problem:** Container jumps to a different position when collapsed.

```xml
<!-- WRONG: alternateBounds at different position than parent geometry -->
<mxGeometry x="100" y="100" width="300" height="200" as="geometry">
  <mxRectangle x="50" y="50" width="160" height="30" as="alternateBounds" />
</mxGeometry>
```

**Fix:** ALWAYS set the alternateBounds x/y to match the parent geometry x/y.

```xml
<!-- CORRECT: same x/y as parent -->
<mxGeometry x="100" y="100" width="300" height="200" as="geometry">
  <mxRectangle x="100" y="100" width="160" height="30" as="alternateBounds" />
</mxGeometry>
```

**Why:** When Draw.io swaps between normal and alternate bounds, a position mismatch causes the container to visually jump to a different location on the canvas.

---

## AP-11: Relative Waypoints Inside Edge Geometry

**Problem:** Waypoints appear at wrong positions because they are treated as absolute despite being intended as relative.

```xml
<!-- WRONG thinking: "waypoints relative to source" -->
<!-- Waypoints are ALWAYS absolute canvas coordinates -->
<Array as="points">
  <mxPoint x="20" y="30" />  <!-- This is canvas (20, 30), not 20px from source -->
</Array>
```

**Fix:** ALWAYS use absolute canvas coordinates for waypoints, regardless of whether the edge's geometry is relative.

```xml
<!-- CORRECT: absolute canvas coordinates -->
<Array as="points">
  <mxPoint x="300" y="150" />
  <mxPoint x="300" y="250" />
</Array>
```

**Why:** The `relative="1"` on edge geometry ONLY affects the label positioning (x/y on mxGeometry). Waypoints in the `<Array as="points">` are ALWAYS absolute canvas coordinates. This is a common source of confusion.

---

## AP-12: Edges Between Container Children with Wrong Parent

**Problem:** Edge disappears or renders at the wrong position when connecting two shapes inside the same container.

```xml
<!-- Shapes inside container id="10" -->
<mxCell id="11" value="A" vertex="1" parent="10" ... />
<mxCell id="12" value="B" vertex="1" parent="10" ... />
<!-- WRONG: edge parent is default layer, but source/target are in container -->
<mxCell id="13" edge="1" source="11" target="12" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Fix:** When connecting cells within the same container, set the edge's parent to that container.

```xml
<!-- CORRECT: edge parent matches the container of its source/target -->
<mxCell id="13" edge="1" source="11" target="12" parent="10">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Why:** The edge's parent determines its coordinate space. If the edge parent differs from the shapes' parent, the edge coordinates and the shape coordinates are in different reference frames, causing misalignment.
