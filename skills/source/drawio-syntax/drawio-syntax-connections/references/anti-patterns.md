# Anti-Patterns: Draw.io Syntax Connections

What NOT to do when creating edges and connections, with explanations of why each pattern fails.

---

## AP-01: Missing source or target Attribute

### WRONG

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

An edge without `source` and `target` creates a floating line that is disconnected from all shapes. When shapes are moved, the edge stays in place. ALWAYS set both `source` and `target` to valid vertex IDs.

---

## AP-02: Referencing Non-Existent Cell IDs

### WRONG

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="99" target="100" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Ensure vertices with id="2" and id="3" exist in the same diagram -->
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Draw.io silently ignores edges that reference non-existent source or target IDs. The edge becomes invisible with no error message. ALWAYS verify that referenced IDs exist as vertex cells in the same diagram.

---

## AP-03: Missing relative="1" on Edge Geometry

### WRONG

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry x="300" y="200" width="100" height="50" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Edge geometry MUST use `relative="1"`. Without it, the `x` and `y` values are interpreted as absolute canvas coordinates instead of relative label positioning. The edge renders incorrectly and labels appear in wrong positions.

---

## AP-04: Hardcoding Waypoints When Edge Style Can Auto-Route

### WRONG

```xml
<!-- Manually routing a simple left-to-right connection -->
<mxCell id="4" style="html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry">
    <Array as="points">
      <mxPoint x="220" y="130" />
      <mxPoint x="280" y="130" />
      <mxPoint x="280" y="130" />
      <mxPoint x="350" y="130" />
    </Array>
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Hardcoded waypoints create rigid edges that break when shapes are moved. The routing algorithm (`edgeStyle`) automatically calculates optimal paths and adapts when the diagram layout changes. NEVER add waypoints for paths that an edgeStyle can handle automatically.

---

## AP-05: exitX/exitY Without exitDx/exitDy

### WRONG

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=1;exitY=0.5;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

When `exitX` and `exitY` are set without explicit `exitDx=0;exitDy=0`, the offset values default to undefined. This causes unpredictable edge endpoint positioning in some Draw.io versions. ALWAYS include `exitDx=0;exitDy=0` when using fixed exit points. The same applies to `entryDx=0;entryDy=0` with entry points.

---

## AP-06: Using exitX/exitY Values Outside 0-1 Range

### WRONG

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=150;exitY=75;exitDx=0;exitDy=0;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;exitX=1;exitY=0.5;exitDx=0;exitDy=0;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

The `exitX`, `exitY`, `entryX`, and `entryY` values are RELATIVE coordinates in the range 0.0 to 1.0, where `(0,0)` is the top-left and `(1,1)` is the bottom-right of the shape. Using absolute pixel values places the connection point far outside the shape boundary.

---

## AP-07: Self-Loop Without loopEdgeStyle

### WRONG

```xml
<mxCell id="4" value="retry" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="2" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" value="retry" style="edgeStyle=loopEdgeStyle;html=1;"
        edge="1" source="2" target="2" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

When `source` equals `target`, the orthogonal router cannot compute a valid path between two identical points. The edge renders as invisible or a zero-length line. ALWAYS use `edgeStyle=loopEdgeStyle` for self-referencing edges.

---

## AP-08: Edge Label x Value Outside -1 to 1 Range

### WRONG

```xml
<mxCell id="4" value="label" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry x="50" y="10" relative="1" as="geometry">
    <mxPoint as="offset" />
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" value="label" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry x="0.5" y="10" relative="1" as="geometry">
    <mxPoint as="offset" />
  </mxGeometry>
</mxCell>
```

### Why It Fails

With `relative="1"`, the `x` value on edge geometry ranges from `-1` (source end) to `1` (target end), with `0` being the center. Using pixel values like `50` places the label far beyond the target end. The `y` value IS in pixels (perpendicular offset).

---

## AP-09: Setting Both vertex="1" and edge="1"

### WRONG

```xml
<mxCell id="4" value="connector" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        vertex="1" edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" value="connector" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

A cell is EITHER a vertex (shape) OR an edge (connector). Setting both produces undefined behavior — the cell may render as a shape, an edge, or not at all. NEVER combine `vertex="1"` and `edge="1"` on the same cell.

---

## AP-10: Edge Label Child Without connectable="0"

### WRONG

```xml
<mxCell id="5" value="source label" style="edgeLabel;html=1;"
        vertex="1" parent="4">
  <mxGeometry x="-0.8" y="0" relative="1" as="geometry">
    <mxPoint as="offset" />
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="5" value="source label" style="edgeLabel;html=1;"
        vertex="1" connectable="0" parent="4">
  <mxGeometry x="-0.8" y="0" relative="1" as="geometry">
    <mxPoint as="offset" />
  </mxGeometry>
</mxCell>
```

### Why It Fails

Without `connectable="0"`, the edge label becomes a valid connection target. Other edges can accidentally attach to the label instead of the intended shape. ALWAYS set `connectable="0"` on edge label children.

---

## AP-11: Using sourcePoint/targetPoint Instead of source/target Attributes

### WRONG

```xml
<!-- Shapes exist at these coordinates, but edge uses absolute points instead of IDs -->
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" parent="1">
  <mxGeometry relative="1" as="geometry">
    <mxPoint x="220" y="130" as="sourcePoint" />
    <mxPoint x="400" y="130" as="targetPoint" />
  </mxGeometry>
</mxCell>
```

### RIGHT

```xml
<mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
        edge="1" source="2" target="3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`sourcePoint` and `targetPoint` are absolute canvas coordinates that do NOT track shape movement. When the user moves a shape, the edge endpoint stays at its original position. ALWAYS use `source` and `target` attributes with cell IDs to create edges that stay connected when shapes move.
