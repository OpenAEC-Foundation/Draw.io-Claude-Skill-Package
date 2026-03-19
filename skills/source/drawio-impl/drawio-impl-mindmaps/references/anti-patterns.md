# Anti-Patterns: Draw.io Mind Maps

What NOT to do when creating mind maps, with explanations of why each pattern fails.

---

## AP-01: Using Orthogonal Connectors Instead of Curved

### WRONG

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=none;html=1;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Orthogonal (right-angle) connectors produce rigid, blocky lines that destroy the organic, radial appearance of a mind map. Mind maps rely on flowing curved lines to convey hierarchy visually. ALWAYS use `curved=1` and NEVER use `edgeStyle=orthogonalEdgeStyle` in mind maps.

---

## AP-02: Using Directed Arrows on Mind Map Branches

### WRONG

```xml
<mxCell id="e1" style="endArrow=classic;html=1;curved=1;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Mind map branches represent hierarchical association, NOT directional flow. Adding arrows (`endArrow=classic`) implies causality or sequence, which is semantically wrong for mind maps. ALWAYS use `endArrow=none`. If you need directed relationships, use a concept map instead.

---

## AP-03: All Branches the Same Color

### WRONG

```xml
<mxCell id="b1" value="Design"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="60" width="120" height="40" as="geometry" />
</mxCell>
<mxCell id="b2" value="Development"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="540" y="60" width="120" height="40" as="geometry" />
</mxCell>
<mxCell id="b3" value="Testing"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="320" y="360" width="120" height="40" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="b1" value="Design"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="60" width="120" height="40" as="geometry" />
</mxCell>
<mxCell id="b2" value="Development"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=13;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="540" y="60" width="120" height="40" as="geometry" />
</mxCell>
<mxCell id="b3" value="Testing"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=13;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="320" y="360" width="120" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

Color coding is a core feature of mind maps. Each main branch family MUST have a distinct color to help viewers quickly identify which branch a sub-topic belongs to. Using the same color for all branches eliminates this visual grouping and makes the mind map harder to read.

---

## AP-04: Central Topic Same Size as Branches

### WRONG

```xml
<!-- Central topic same size as branches — no visual hierarchy -->
<mxCell id="center" value="Main Topic"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=12;"
        vertex="1" parent="1">
  <mxGeometry x="300" y="200" width="120" height="40" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Central topic is larger, bolder, darker -->
<mxCell id="center" value="Main Topic"
        style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=16;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="300" y="200" width="160" height="80" as="geometry" />
</mxCell>
```

### Why It Fails

The central topic MUST be visually dominant. If it is the same size, font, and color as the branches, viewers cannot identify the root of the hierarchy. ALWAYS make the central topic larger (160-200px wide), use bold text (`fontStyle=1`), use a dark fill color, and use a larger font size (14-18).

---

## AP-05: Missing relative="1" on Edge Geometry

### WRONG

```xml
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Edge geometry without `relative="1"` causes Draw.io to interpret the geometry as absolute coordinates instead of relative to the source and target. This results in incorrectly positioned or invisible edges. ALWAYS include `relative="1"` on edge `<mxGeometry>`.

---

## AP-06: Placing All Branches on One Side

### WRONG

```
[Branch 1]
[Branch 2]      [CENTRAL TOPIC]
[Branch 3]
[Branch 4]
```

All branches clustered to the left with empty space on the right.

### RIGHT

```
        [Branch 1]        [Branch 2]
               \           /
                [CENTRAL TOPIC]
               /           \
        [Branch 3]        [Branch 4]
```

Branches distributed radially around the center.

### Why It Fails

Mind maps are radial diagrams. Placing all branches on one side wastes canvas space, creates visual imbalance, and makes the diagram look like a list rather than a mind map. ALWAYS distribute branches around the central topic: top-left, top-right, left, right, bottom-left, bottom-right.

---

## AP-07: Using Straight Lines (No curved=1)

### WRONG

```xml
<mxCell id="e1" style="endArrow=none;html=1;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Omitting `curved=1` produces rigid straight lines between nodes. While technically functional, straight lines make the diagram look like a tree chart or org chart rather than a mind map. The organic curved style is a defining visual characteristic of mind maps. ALWAYS set `curved=1` on every mind map connector.

---

## AP-08: Mixing Mind Map and Concept Map Styles

### WRONG

```xml
<!-- Some edges with arrows, some without — inconsistent -->
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" value="causes"
        style="endArrow=classic;html=1;curved=1;strokeColor=#82b366;"
        edge="1" source="center" target="b2" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT — Mind Map (all undirected)

```xml
<mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
        edge="1" source="center" target="b1" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#82b366;"
        edge="1" source="center" target="b2" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT — Concept Map (all directed with labels)

```xml
<mxCell id="e1" value="includes"
        style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
        edge="1" source="c1" target="c2" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" value="causes"
        style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
        edge="1" source="c1" target="c3" parent="1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Mixing directed and undirected edges in the same diagram creates visual confusion. Pick ONE style: either a mind map (all `endArrow=none`, no labels) or a concept map (all `endArrow=classic`, with relationship labels). NEVER mix them in a single diagram.
