# Anti-Patterns: Swimlane Implementation

What NOT to do when generating swimlane diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Absolute Coordinates for Children Inside Containers

### WRONG

```xml
<!-- Pool is at x=40, y=40. Lane starts at y=70 (pool y + startSize). -->
<!-- Shape uses absolute page coordinates instead of container-relative -->
<mxCell id="t1" value="Task" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="lane1">
  <mxGeometry x="280" y="105" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Shape uses coordinates relative to lane1's top-left corner -->
<mxCell id="t1" value="Task" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="lane1">
  <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

When `parent` is set to a container, Draw.io interprets coordinates relative to the container's top-left corner. Using absolute page coordinates causes the shape to render at a completely wrong position — offset by the pool's and lane's own position. This is the #1 swimlane mistake. ALWAYS use container-relative coordinates for all child shapes.

---

## AP-02: Missing container=1 on Swimlane Style

### WRONG

```xml
<mxCell id="lane1" value="Sales" style="swimlane;startSize=30;collapsible=0;horizontal=1;"
        vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="lane1" value="Sales" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;"
        vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
```

### Why It Fails

Without `container=1`, the lane renders as a visual shape but does NOT function as a container. Child shapes with `parent="lane1"` will NOT move when the lane is repositioned. Drag-and-drop into the lane will NOT work in the editor. ALWAYS include `container=1` in every pool and lane style.

---

## AP-03: Cross-Lane Edge with Lane as Parent

### WRONG

```xml
<!-- task1 is in lane1, task2 is in lane2 — but edge parent is lane1 -->
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="lane1" source="task1" target="task2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Edge parent is the pool (common ancestor of both lanes) -->
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="pool1" source="task1" target="task2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

When an edge's parent is set to one lane but its source or target is in a different lane, Draw.io cannot correctly calculate the edge's coordinate system. The edge renders at a wrong position or disappears entirely. ALWAYS set cross-lane edge `parent` to the nearest common ancestor (the pool).

---

## AP-04: Child Shape with parent="1" Inside a Swimlane

### WRONG

```xml
<!-- Shape is visually positioned inside lane1 but uses parent="1" (root) -->
<mxCell id="t1" value="Task" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="280" y="145" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Shape correctly belongs to lane1 -->
<mxCell id="t1" value="Task" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="lane1">
  <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

A shape with `parent="1"` is a top-level shape. Even if its absolute coordinates place it visually inside a lane, it will NOT move when the lane is repositioned. It will NOT be included when the lane is collapsed, exported, or selected as a group. ALWAYS set `parent` to the containing lane's ID for shapes that belong inside a lane.

---

## AP-05: Lane Width Not Matching Pool Width

### WRONG

```xml
<mxCell id="pool1" value="Process" style="shape=table;startSize=30;container=1;..."
        vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="700" height="300" as="geometry" />
</mxCell>

<!-- Lane width (500) does not match pool width (700) -->
<mxCell id="lane1" value="Team A" style="swimlane;startSize=30;container=1;..."
        vertex="1" parent="pool1">
  <mxGeometry y="30" width="500" height="130" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="pool1" value="Process" style="shape=table;startSize=30;container=1;..."
        vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="700" height="300" as="geometry" />
</mxCell>

<!-- Lane width matches pool width -->
<mxCell id="lane1" value="Team A" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;"
        vertex="1" parent="pool1">
  <mxGeometry y="30" width="700" height="130" as="geometry" />
</mxCell>
```

### Why It Fails

When lane width is smaller than pool width, the lane does not span the full pool area. This creates visual gaps, misaligned lane borders, and child shapes that appear to float outside their lane. ALWAYS set lane width equal to pool width.

---

## AP-06: Missing collapsible=0 on Lanes

### WRONG

```xml
<mxCell id="lane1" value="Sales" style="swimlane;startSize=30;container=1;horizontal=1;"
        vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="lane1" value="Sales" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;"
        vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
```

### Why It Fails

Without `collapsible=0`, Draw.io displays a collapse/expand toggle on the lane header. Users can accidentally click it, collapsing the lane and hiding all its contents. This is confusing in cross-functional diagrams where lane visibility is expected. ALWAYS include `collapsible=0` on every lane.

---

## AP-07: Pool Height Does Not Match Lane Heights

### WRONG

```xml
<!-- Pool height (300) is less than startSize (30) + lane1 (130) + lane2 (200) = 360 -->
<mxCell id="pool1" value="Process" style="shape=table;startSize=30;container=1;..."
        vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="600" height="300" as="geometry" />
</mxCell>

<mxCell id="lane1" value="A" style="swimlane;..." vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
<mxCell id="lane2" value="B" style="swimlane;..." vertex="1" parent="pool1">
  <mxGeometry y="160" width="600" height="200" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Pool height (360) = startSize (30) + lane1 (130) + lane2 (200) -->
<mxCell id="pool1" value="Process" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;"
        vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="600" height="360" as="geometry" />
</mxCell>

<mxCell id="lane1" value="A" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
<mxCell id="lane2" value="B" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
  <mxGeometry y="160" width="600" height="200" as="geometry" />
</mxCell>
```

### Why It Fails

When pool height is too small, lanes extend beyond the pool boundary, creating visual clipping and broken lane borders. When pool height is too large, empty space appears below the last lane. ALWAYS ensure pool height equals `startSize + sum(all lane heights)`.

---

## AP-08: Child Shape Overlapping Lane Header

### WRONG

```xml
<!-- Lane startSize is 30, but child y=10 overlaps the header -->
<mxCell id="lane1" value="Sales" style="swimlane;startSize=30;container=1;..." vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
<mxCell id="t1" value="Task" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="lane1">
  <mxGeometry x="40" y="10" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="lane1" value="Sales" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
  <mxGeometry y="30" width="600" height="130" as="geometry" />
</mxCell>
<mxCell id="t1" value="Task" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="lane1">
  <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

The lane header occupies the top `startSize` pixels. Placing a child shape with y less than startSize causes it to overlap the header text, making both the header and the shape unreadable. ALWAYS position child shapes with `y >= startSize` of their parent lane.
