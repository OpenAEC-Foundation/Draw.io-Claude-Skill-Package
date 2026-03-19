# Draw.io Style Properties — Anti-Patterns

> Common mistakes when working with Draw.io style properties.
> Each anti-pattern shows the WRONG approach, explains WHY it fails, and provides
> the CORRECT solution.

---

## AP-01: Missing html=1

**Severity:** Critical — labels lose ALL formatting.

```
// WRONG
rounded=1;whiteSpace=wrap;fillColor=#DAE8FC;

// CORRECT
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;
```

**Why it fails:** Without `html=1`, labels render as plain text. Line breaks (`<br>`), bold/italic formatting, and mixed styles inside labels are ignored.

**Rule:** ALWAYS include `html=1` on every vertex and every edge.

---

## AP-02: Missing whiteSpace=wrap

**Severity:** High — long labels overflow shape bounds.

```
// WRONG
html=1;fillColor=#DAE8FC;

// CORRECT
whiteSpace=wrap;html=1;fillColor=#DAE8FC;
```

**Why it fails:** Without `whiteSpace=wrap`, text renders in a single line extending beyond the shape boundary. The shape does NOT auto-resize to fit.

**Rule:** ALWAYS include `whiteSpace=wrap` on vertices with text labels.

---

## AP-03: Wrong Perimeter for Shape

**Severity:** Critical — edges connect at visually incorrect positions.

```
// WRONG — rectangle perimeter on an ellipse
ellipse;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;

// CORRECT
ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;
```

**Why it fails:** The perimeter calculates where edges attach to the shape boundary. A rectangle perimeter on an ellipse calculates attachment points on the bounding box, NOT on the curved ellipse boundary. Edges appear to float away from the shape.

**Rule:** ALWAYS match the perimeter to the shape type:
- `ellipse` → `ellipsePerimeter`
- `rhombus` → `rhombusPerimeter`
- `triangle` → `trianglePerimeter`
- `hexagon` → `hexagonPerimeter`
- All others → `rectanglePerimeter` (default)

---

## AP-04: Using true/false Instead of 0/1

**Severity:** Critical — boolean properties silently ignored.

```
// WRONG
rounded=true;dashed=true;shadow=true;

// CORRECT
rounded=1;dashed=1;shadow=1;
```

**Why it fails:** Draw.io boolean properties expect `0` and `1` as integer values. String values `"true"` and `"false"` are NOT parsed as booleans — they are silently ignored, and the default value is used instead.

**Rule:** ALWAYS use `0` and `1` for boolean properties. NEVER use `true`, `false`, `yes`, `no`.

---

## AP-05: Conflicting Label Position and Alignment

**Severity:** High — label appears in wrong position.

```
// WRONG — both push label right
labelPosition=right;align=right;

// CORRECT — align opposes labelPosition
labelPosition=right;align=left;
```

**Why it fails:** When `labelPosition=right`, the label box is placed to the right of the shape. If `align=right` too, the text inside the label box is right-aligned, pushing it further away from the shape. The label appears disconnected.

**Rule:** When `labelPosition` is NOT `center`, ALWAYS set `align` to the OPPOSITE value. Same for `verticalLabelPosition` and `verticalAlign`.

---

## AP-06: Shadow Without Global Shadow

**Severity:** Medium — shadow property has no visible effect.

```xml
<!-- WRONG — cell shadow=1 but model shadow not set -->
<mxGraphModel>
  <root>
    <mxCell id="2" style="rounded=1;html=1;shadow=1;" vertex="1" parent="1">
```

```xml
<!-- CORRECT — model-level shadow enabled -->
<mxGraphModel shadow="1">
  <root>
    <mxCell id="2" style="rounded=1;html=1;shadow=1;" vertex="1" parent="1">
```

**Why it fails:** The cell-level `shadow=1` style property is ONLY respected when the `<mxGraphModel>` element also has `shadow="1"`. If the model-level shadow is `0` or absent, ALL cell shadows are suppressed.

**Rule:** When using `shadow=1` on cells, ALWAYS set `shadow="1"` on the `<mxGraphModel>` element.

---

## AP-07: Applying Vertex Properties to Edges

**Severity:** Medium — properties silently ignored.

```
// WRONG — fillColor has no effect on edges
edgeStyle=orthogonalEdgeStyle;html=1;endArrow=classic;fillColor=#FF0000;

// CORRECT — use strokeColor for edge color
edgeStyle=orthogonalEdgeStyle;html=1;endArrow=classic;strokeColor=#FF0000;
```

**Why it fails:** Vertex-only properties (`fillColor`, `shape`, `container`, `collapsible`, `glass`) are silently ignored on edges. No error is thrown.

**Rule:** NEVER apply vertex-only properties to edges. Use `strokeColor` for edge color, NOT `fillColor`.

---

## AP-08: Applying Edge Properties to Vertices

**Severity:** Medium — properties silently ignored.

```
// WRONG — edgeStyle on a vertex
rounded=1;whiteSpace=wrap;html=1;edgeStyle=orthogonalEdgeStyle;endArrow=classic;

// CORRECT — vertex without edge properties
rounded=1;whiteSpace=wrap;html=1;
```

**Why it fails:** Edge-only properties (`edgeStyle`, `startArrow`, `endArrow`, `curved`, `jettySize`, `exitX/Y`, `entryX/Y`) are silently ignored on vertices.

**Rule:** NEVER apply edge-only properties to vertices.

---

## AP-09: Incorrect Dash Pattern Format

**Severity:** Medium — dash pattern not rendering as expected.

```
// WRONG — no space, concatenated digits
dashed=1;dashPattern=84;

// CORRECT — space-separated values
dashed=1;dashPattern=8 4;
```

**Why it fails:** `dashPattern` expects a space-separated list of alternating dash and gap lengths. Without spaces, the entire string is parsed as a single number.

**Rule:** ALWAYS use space-separated values in `dashPattern`. ALWAYS set `dashed=1` alongside `dashPattern`.

---

## AP-10: Missing container=1 for Groups

**Severity:** Critical — children do NOT move with parent.

```
// WRONG — swimlane without container flag
swimlane;html=1;startSize=30;

// CORRECT
swimlane;html=1;startSize=30;container=1;
```

**Why it fails:** Without `container=1`, child shapes that reference this cell as `parent` still use absolute coordinates instead of coordinates relative to the container. Moving the "parent" does NOT move the children.

**Rule:** ALWAYS include `container=1` on any shape intended to hold children.

---

## AP-11: Edge Missing relative="1" on Geometry

**Severity:** Critical — edge labels and waypoints positioned incorrectly.

```xml
<!-- WRONG — missing relative="1" -->
<mxCell id="e1" edge="1" source="a" target="b" style="endArrow=classic;html=1;">
  <mxGeometry as="geometry" />
</mxCell>

<!-- CORRECT -->
<mxCell id="e1" edge="1" source="a" target="b" style="endArrow=classic;html=1;">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

**Why it fails:** Edge geometry uses relative coordinates (0.0 to 1.0 along the edge path) for label positioning. Without `relative="1"`, coordinates are treated as absolute pixel values, causing labels to appear far from the edge.

**Rule:** Edge `<mxGeometry>` MUST ALWAYS include `relative="1"`.

---

## AP-12: Using CSS Property Names Instead of camelCase

**Severity:** Critical — properties not recognized.

```
// WRONG — CSS naming conventions
fill-color=#DAE8FC;stroke-color=#6C8EBF;font-size=14;stroke-width=2;

// CORRECT — Draw.io camelCase names
fillColor=#DAE8FC;strokeColor=#6C8EBF;fontSize=14;strokeWidth=2;
```

**Why it fails:** Draw.io style properties use camelCase naming, NOT CSS kebab-case. Unrecognized property names are silently ignored.

**Rule:** ALWAYS use exact camelCase property names: `fillColor`, `strokeColor`, `fontSize`, `strokeWidth`, `fontFamily`, `fontColor`, `fontStyle`, `edgeStyle`, `startArrow`, `endArrow`.

---

## AP-13: Stencil Shape Without mxgraph. Prefix

**Severity:** Critical — shape not rendered.

```
// WRONG — bare stencil name
shape=aws4.lambda_function;

// CORRECT — full mxgraph prefix
shape=mxgraph.aws4.lambda_function;
```

**Why it fails:** Stencil shapes are loaded from external stencil XML files via the `mxgraph.` prefix. Without this prefix, Draw.io cannot locate the stencil definition and falls back to a default rectangle.

**Rule:** Stencil shapes ALWAYS use `shape=mxgraph.<library>.<shape>;` format.

---

## AP-14: Using 3-Digit Hex Colors

**Severity:** Medium — color not applied correctly.

```
// WRONG — 3-digit hex
fillColor=#FFF;strokeColor=#000;

// CORRECT — 6-digit hex
fillColor=#FFFFFF;strokeColor=#000000;
```

**Why it fails:** Draw.io expects 6-digit `#RRGGBB` hex notation. 3-digit shorthand is NOT reliably expanded.

**Rule:** ALWAYS use full 6-digit `#RRGGBB` hex colors.

---

## AP-15: Confusing shape Identifier with shape= Property

**Severity:** Medium — unexpected rendering.

```
// WRONG — leading identifier AND shape= property conflict
ellipse;shape=rectangle;whiteSpace=wrap;html=1;

// CORRECT — use one or the other
ellipse;whiteSpace=wrap;html=1;
// OR
shape=ellipse;whiteSpace=wrap;html=1;
```

**Why it fails:** A leading bare word (e.g., `ellipse;`) sets the shape implicitly. Adding `shape=rectangle;` after it creates a conflict. The last `shape=` value wins, overriding the leading identifier.

**Rule:** NEVER mix a leading shape identifier with an explicit `shape=` property. Use one method consistently.

---

## AP-16: Missing Semicolon Between Properties

**Severity:** Critical — properties merged into one invalid value.

```
// WRONG — missing semicolon between fillColor and strokeColor
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FCstrokeColor=#6C8EBF;

// CORRECT
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;
```

**Why it fails:** Without the semicolon separator, `fillColor=#DAE8FCstrokeColor=#6C8EBF` is parsed as a single property with an invalid color value. Both properties are lost.

**Rule:** ALWAYS terminate every property with a semicolon. ALWAYS verify semicolons between all key=value pairs.

---

## AP-17: Forgetting endFill=0 for Hollow Arrows

**Severity:** Medium — arrow appears filled instead of hollow.

```
// WRONG — block arrow is filled by default
endArrow=block;

// CORRECT — hollow triangle for UML inheritance
endArrow=block;endFill=0;
```

**Why it fails:** Arrow markers default to `endFill=1` (filled/solid). For UML inheritance (hollow triangle), UML aggregation (hollow diamond), and similar notations, you MUST explicitly set `endFill=0` or `startFill=0`.

**Rule:** ALWAYS explicitly set `startFill` and `endFill` when the fill state matters semantically (e.g., UML relationships).
