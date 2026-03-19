# Vooronderzoek: Draw.io Style System — Complete Technical Reference

> Onderzocht op 2026-03-19. Bronnen: drawio.com/doc/faq/drawio-style-reference, jgraph.github.io/mxgraph/docs/js-api/files/util/mxConstants-js.html (mxConstants), drawio.com/doc/faq/ai-drawio-generation.
>
> **Verwerkt:** Nee

---

## 1. Style String Syntax

Every mxCell in a Draw.io diagram carries its visual appearance in a single `style` attribute. This attribute is a **semicolon-delimited string** of key=value pairs. Understanding this format is the foundation of all Draw.io styling.

### 1.1 Format Rules

The style string follows these rules:

1. Properties are separated by semicolons (`;`)
2. Each property is a `key=value` pair
3. A style string MAY start with a **shape identifier** (a bare word without `=`), which sets the base shape
4. A trailing semicolon is conventional but not strictly required
5. Boolean values use `0` (false) and `1` (true) — NEVER `true`/`false`
6. Color values use `#RRGGBB` hex notation, or the keywords `none` and `default`
7. Property names are camelCase

### 1.2 Style String Examples

**Simple rectangle:**
```
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;
```

**Ellipse with custom font:**
```
ellipse;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;fontSize=14;fontStyle=1;
```

**Edge with classic arrow:**
```
endArrow=classic;html=1;rounded=0;strokeColor=#000000;
```

**Swimlane container:**
```
swimlane;horizontal=1;startSize=30;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;
```

### 1.3 Leading Shape Identifier

When a style string starts with a bare word (no `=`), it sets the `shape` property. These two are equivalent:

```
ellipse;whiteSpace=wrap;html=1;
```
```
shape=ellipse;whiteSpace=wrap;html=1;
```

Common leading identifiers: `ellipse`, `rhombus`, `triangle`, `hexagon`, `swimlane`, `image`, `line`, `text`.

### 1.4 The html=1 Property

The `html=1` property is **ALWAYS required** for shapes and edges in modern Draw.io files. It enables HTML label rendering, which is necessary for:

- Rich text formatting within labels
- Line breaks (`<br>`)
- Mixed formatting (bold, italic, colors within one label)
- Proper tooltip rendering

Omitting `html=1` causes labels to render as plain text without formatting support. Every AI-generated cell MUST include this property.

---

## 2. Shape Properties

Draw.io supports a wide range of shape types through the `shape` style property. Shapes fall into three categories: built-in primitives, extended shapes, and stencil library shapes.

### 2.1 Built-in Primitive Shapes

These shapes are defined in the mxGraph core (`mxConstants.SHAPE_*`):

| Shape Value | mxConstant | Description | Default Perimeter |
|-------------|------------|-------------|-------------------|
| `rectangle` | SHAPE_RECTANGLE | Standard rectangle (default shape) | `rectanglePerimeter` |
| `ellipse` | SHAPE_ELLIPSE | Circle or oval | `ellipsePerimeter` |
| `doubleEllipse` | SHAPE_DOUBLE_ELLIPSE | Nested ellipse (BPMN events) | `ellipsePerimeter` |
| `rhombus` | SHAPE_RHOMBUS | Diamond / decision node | `rhombusPerimeter` |
| `triangle` | SHAPE_TRIANGLE | Triangle pointing right | `trianglePerimeter` |
| `hexagon` | SHAPE_HEXAGON | Regular hexagon | `hexagonPerimeter` |
| `cylinder` | SHAPE_CYLINDER | Database cylinder | `rectanglePerimeter` |
| `cloud` | SHAPE_CLOUD | Cloud shape | `ellipsePerimeter` |
| `actor` | SHAPE_ACTOR | Stick figure / actor | `rectanglePerimeter` |
| `label` | SHAPE_LABEL | Rectangle with image+label | `rectanglePerimeter` |
| `swimlane` | SHAPE_SWIMLANE | Swimlane with header bar | `rectanglePerimeter` |
| `line` | SHAPE_LINE | Horizontal/vertical line | — |
| `image` | SHAPE_IMAGE | Image-only shape | `rectanglePerimeter` |
| `arrow` | SHAPE_ARROW | Arrow block shape | `rectanglePerimeter` |
| `arrowConnector` | SHAPE_ARROW_CONNECTOR | Arrow as a connector | — |
| `connector` | SHAPE_CONNECTOR | Standard edge connector | — |

### 2.2 Extended Shapes (Draw.io Additions)

Draw.io extends the mxGraph primitives with additional shapes that are NOT in the base mxConstants but are widely available in the editor:

| Shape Value | Description |
|-------------|-------------|
| `parallelogram` | Parallelogram / input-output symbol |
| `trapezoid` | Trapezoid shape |
| `step` | Step / chevron shape |
| `process` | Process rectangle (double vertical borders) |
| `document` | Document with wavy bottom |
| `callout` | Speech bubble / callout |
| `cube` | 3D cube |
| `folder` | Folder with tab |
| `card` | Card with clipped corner |
| `note` | Sticky note shape |
| `tape` | Tape / ribbon shape |
| `internalStorage` | Internal storage symbol |
| `or` | OR gate |
| `xor` | XOR gate |
| `dataStorage` | Data storage symbol |
| `manualInput` | Manual input symbol |
| `delay` | Delay shape |
| `display` | Display shape |
| `offPageConnector` | Off-page connector |

### 2.3 Stencil Library Shapes

Draw.io includes thousands of additional shapes from stencil libraries. These use the `shape=mxgraph.*` prefix:

```
shape=mxgraph.flowchart.decision;
shape=mxgraph.aws4.lambda_function;
shape=mxgraph.bpmn.shape;
shape=mxgraph.cisco.router;
shape=mxgraph.uml.component;
```

Stencil shapes are loaded from external XML stencil files. When using stencil shapes, the perimeter MUST still be set appropriately based on the visual form of the stencil. For example, a circular stencil should use `perimeter=ellipsePerimeter`.

### 2.4 Shape Geometry Modifiers

These properties modify how a shape is rendered geometrically:

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `rounded` | `0`, `1` | `0` | Round rectangle corners |
| `arcSize` | number (0–50) | varies | Corner radius as percentage of shorter side |
| `absoluteArcSize` | `0`, `1` | `0` | When `1`, arcSize is in absolute pixels instead of percentage |
| `aspect` | `variable`, `fixed` | `variable` | `fixed` preserves width/height ratio on resize |
| `direction` | `north`, `south`, `east`, `west` | — | Rotates shape in 90-degree increments |
| `flipH` | `0`, `1` | `0` | Mirror horizontally |
| `flipV` | `0`, `1` | `0` | Mirror vertically |
| `rotation` | 0–360 | `0` | Free rotation angle in degrees |
| `fixedSize` | `0`, `1` | `0` | Shape size independent of label size |

---

## 3. Visual Properties

Visual properties control the fill, stroke, and decorative effects of shapes and edges.

### 3.1 Fill Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `fillColor` | `#RRGGBB`, `none`, `default` | `default` | Interior fill color |
| `gradientColor` | `#RRGGBB`, `none` | `none` | Gradient end color (start is `fillColor`) |
| `gradientDirection` | `north`, `south`, `east`, `west` | `south` | Direction of gradient flow |
| `opacity` | 0–100 | `100` | Overall opacity (affects both fill and stroke) |
| `fillOpacity` | 0–100 | `100` | Fill-only opacity |

When `fillColor=default`, the shape uses the theme's default fill color (typically white or `#FFFFFF`). Setting `fillColor=none` makes the shape transparent.

### 3.2 Stroke Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `strokeColor` | `#RRGGBB`, `none`, `default` | `default` | Border/outline color |
| `strokeWidth` | number | `1` | Border thickness in pixels |
| `strokeOpacity` | 0–100 | `100` | Stroke-only opacity |
| `dashed` | `0`, `1` | `0` | Enable dashed stroke |
| `dashPattern` | string | — | Custom dash pattern (e.g., `"8 4"` for 8px dash, 4px gap) |
| `fixDash` | `0`, `1` | `0` | When `1`, dash pattern does not scale with strokeWidth |

### 3.3 Decorative Effects

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `shadow` | `0`, `1` | `0` | Drop shadow behind shape |
| `glass` | `0`, `1` | `0` | Glossy shine overlay effect |
| `rounded` | `0`, `1` | `0` | Rounded corners on rectangles |

**Important:** The `shadow` style property on individual cells only works when the global `shadow` attribute on the `<mxGraphModel>` element is also enabled. If the model-level shadow is `0`, per-cell shadow settings are ignored.

### 3.4 Sketch / Hand-Drawn Mode

Draw.io supports a hand-drawn rendering mode (powered by rough.js). These properties control the sketch appearance:

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `sketch` | `0`, `1` | `0` | Enable hand-drawn / sketch style |
| `comic` | `0`, `1` | `0` | Comic book style variant |
| `fillStyle` | `solid`, `hachure`, `cross-hatch`, `dots` | — | Fill pattern in sketch mode |
| `fillWeight` | number | — | Weight of hatch lines |
| `hachureGap` | number | — | Gap between hatch lines in pixels |
| `hachureAngle` | number (degrees) | — | Angle of hatch lines |
| `jiggle` | number | — | Amount of randomness / wobble in lines |
| `curveFitting` | 0–1 | — | Quality of curve approximation |
| `simplification` | 0–1 | — | Path simplification level |
| `disableMultiStroke` | `0`, `1` | — | Disable double-stroke effect |
| `disableMultiStrokeFill` | `0`, `1` | — | Disable double-stroke on fill |

Example of a sketch-style rectangle:
```
rounded=1;whiteSpace=wrap;html=1;sketch=1;jiggle=2;fillStyle=hachure;hachureGap=4;fillColor=#DAE8FC;strokeColor=#6C8EBF;
```

---

## 4. Font and Label Properties

Draw.io labels support rich text formatting through a combination of style properties and HTML content within the `value` attribute.

### 4.1 Core Font Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `fontSize` | number | `12` | Font size in pixels |
| `fontFamily` | string | `Helvetica` | Font family name |
| `fontColor` | `#RRGGBB`, `default` | `default` | Text color |
| `fontStyle` | bitmask integer | `0` | Combined font style flags |

### 4.2 fontStyle Bitflag System

The `fontStyle` property uses a **bitmask** to combine multiple text decorations in a single integer. The flags are defined in `mxConstants`:

| Flag | Value | Effect |
|------|-------|--------|
| `FONT_BOLD` | 1 | **Bold** text |
| `FONT_ITALIC` | 2 | *Italic* text |
| `FONT_UNDERLINE` | 4 | Underlined text |
| `FONT_STRIKETHROUGH` | 8 | ~~Strikethrough~~ text |

Combine flags with bitwise OR (addition for non-overlapping flags):

| fontStyle Value | Rendering |
|-----------------|-----------|
| `0` | Normal text |
| `1` | Bold |
| `2` | Italic |
| `3` | Bold + Italic |
| `4` | Underline |
| `5` | Bold + Underline |
| `6` | Italic + Underline |
| `7` | Bold + Italic + Underline |
| `8` | Strikethrough |
| `9` | Bold + Strikethrough |

### 4.3 Text Alignment

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `align` | `left`, `center`, `right` | `center` | Horizontal text alignment within the label bounds |
| `verticalAlign` | `top`, `middle`, `bottom` | `middle` | Vertical text alignment within the label bounds |

### 4.4 Label Positioning

Label positioning controls WHERE the label is placed relative to the shape. This is independent of text alignment (which controls how text is aligned WITHIN the label bounds).

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelPosition` | `left`, `center`, `right` | `center` | Horizontal position of the label relative to the shape |
| `verticalLabelPosition` | `top`, `middle`, `bottom` | `middle` | Vertical position of the label relative to the shape |

**Critical rule:** When `labelPosition` is not `center`, the `align` property MUST be set to the opposite direction to keep the label visually attached to the shape. For example:

```
labelPosition=left;align=right;    // Label to the left, text right-aligned toward shape
labelPosition=right;align=left;    // Label to the right, text left-aligned toward shape
verticalLabelPosition=top;verticalAlign=bottom;  // Label above, text bottom-aligned
verticalLabelPosition=bottom;verticalAlign=top;   // Label below, text top-aligned
```

### 4.5 Text Wrapping and Overflow

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `whiteSpace` | `wrap`, `nowrap` | — | `wrap` enables word wrapping to fit shape width |
| `overflow` | `visible`, `hidden`, `fill`, `width` | — | How text exceeding bounds is handled |
| `labelWidth` | number | — | Fixed label width in pixels |
| `horizontal` | `0`, `1` | `1` | `0` renders text vertically (rotated 90 degrees) |
| `textDirection` | `default`, `ltr`, `rtl` | `default` | Text direction for bidirectional text |

The `overflow` values:
- **`visible`** — Text extends beyond shape bounds (default for edges)
- **`hidden`** — Text is clipped at shape bounds
- **`fill`** — Label fills the entire shape
- **`width`** — Label has fixed width but variable height

### 4.6 Label Spacing (Padding)

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `spacing` | number | `2` | Padding on all sides in pixels |
| `spacingTop` | number | `0` | Additional top padding |
| `spacingBottom` | number | `0` | Additional bottom padding |
| `spacingLeft` | number | `0` | Additional left padding |
| `spacingRight` | number | `0` | Additional right padding |

Total top padding = `spacing` + `spacingTop`. The individual spacing values are added to the base `spacing` value.

### 4.7 Label Background and Border

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelBackgroundColor` | `#RRGGBB`, `none`, `default` | — | Background color behind the text label |
| `labelBorderColor` | `#RRGGBB`, `none` | — | Border color around the label |
| `textOpacity` | 0–100 | `100` | Opacity of the text only |
| `noLabel` | `0`, `1` | `0` | Hide the label entirely |

---

## 5. Edge / Connector Styles

Edges (connectors) in Draw.io have their own specialized style properties controlling routing, path shape, and endpoint behavior.

### 5.1 Edge Style (Routing Algorithm)

The `edgeStyle` property determines how an edge is routed between its source and target shapes:

| edgeStyle Value | mxConstant | Description |
|-----------------|------------|-------------|
| `orthogonalEdgeStyle` | EDGESTYLE_ORTHOGONAL | Rectilinear routing with right-angle bends (most common) |
| `elbowEdgeStyle` | EDGESTYLE_ELBOW | Single elbow (L-shaped or Z-shaped) routing |
| `entityRelationEdgeStyle` | EDGESTYLE_ENTITY_RELATION | ER diagram style with fixed-length stubs |
| `segmentEdgeStyle` | EDGESTYLE_SEGMENT | User-defined segments (manual waypoints) |
| `sideToSideEdgeStyle` | EDGESTYLE_SIDETOSIDE | Horizontal routing from side to side |
| `topToBottomEdgeStyle` | EDGESTYLE_TOPTOBOTTOM | Vertical routing from top to bottom |
| `loopEdgeStyle` | EDGESTYLE_LOOP | Self-referencing loop routing |
| `isometricEdgeStyle` | — | Isometric (30-degree angle) routing |

When NO `edgeStyle` is set, the edge uses a direct straight line between source and target.

### 5.2 Edge Path Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `curved` | `0`, `1` | `0` | Smooth curved path instead of sharp corners |
| `rounded` | `0`, `1` | `1` | Round edge corners (for orthogonal edges) |
| `elbow` | `horizontal`, `vertical` | — | Preferred direction for elbow edges |
| `orthogonalLoop` | `0`, `1` | `1` | Routing style for self-referencing loops |
| `noEdgeStyle` | `0`, `1` | `0` | Disable edge style application entirely |

### 5.3 Connection Point Properties (Entry/Exit)

Connection points define WHERE on a shape an edge attaches. Values are relative coordinates where `(0,0)` is the top-left corner and `(1,1)` is the bottom-right corner of the shape.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `exitX` | 0.0–1.0 | — | Relative X of exit point on source shape |
| `exitY` | 0.0–1.0 | — | Relative Y of exit point on source shape |
| `exitDx` | number | — | Absolute X offset from the exit point |
| `exitDy` | number | — | Absolute Y offset from the exit point |
| `exitPerimeter` | `0`, `1` | `1` | Project exit point onto perimeter |
| `entryX` | 0.0–1.0 | — | Relative X of entry point on target shape |
| `entryY` | 0.0–1.0 | — | Relative Y of entry point on target shape |
| `entryDx` | number | — | Absolute X offset from the entry point |
| `entryDy` | number | — | Absolute Y offset from the entry point |
| `entryPerimeter` | `0`, `1` | `1` | Project entry point onto perimeter |

Common connection point patterns:

```
exitX=1;exitY=0.5;    // Right center of source
entryX=0;entryY=0.5;  // Left center of target

exitX=0.5;exitY=1;    // Bottom center of source
entryX=0.5;entryY=0;  // Top center of target
```

Reference grid for common positions:

| Position | X | Y |
|----------|---|---|
| Top-left | 0 | 0 |
| Top-center | 0.5 | 0 |
| Top-right | 1 | 0 |
| Middle-left | 0 | 0.5 |
| Center | 0.5 | 0.5 |
| Middle-right | 1 | 0.5 |
| Bottom-left | 0 | 1 |
| Bottom-center | 0.5 | 1 |
| Bottom-right | 1 | 1 |

### 5.4 Edge Spacing and Jetty

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jettySize` | `auto`, number | `auto` | Minimum length of the first/last segment for orthogonal edges |
| `sourceJettySize` | number | — | Override jetty size at source end only |
| `targetJettySize` | number | — | Override jetty size at target end only |
| `sourcePerimeterSpacing` | number | — | Gap between edge endpoint and source perimeter |
| `targetPerimeterSpacing` | number | — | Gap between edge endpoint and target perimeter |
| `perimeterSpacing` | number | — | Gap between edge endpoint and perimeter (both ends) |

### 5.5 Line Crossing Visualization

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jumpStyle` | `arc`, `gap`, `sharp` | — | How crossing lines are visualized |
| `jumpSize` | number | `6` | Size of the jump/gap at crossings |

---

## 6. Arrow Types — Complete Catalog

Arrow markers are set via `startArrow` and `endArrow`. The `startFill` and `endFill` properties control whether the arrow marker is filled (solid) or hollow (outline only).

### 6.1 All Arrow Types

| Arrow Value | Visual Description | Typical Use |
|-------------|-------------------|-------------|
| `none` | No arrow marker | Undirected connections |
| `classic` | Traditional triangular arrowhead | Standard directed flow (default for endArrow) |
| `classicThin` | Slender classic variant | Lighter visual weight |
| `block` | Solid rectangular/filled triangle | Strong directional indicator |
| `blockThin` | Narrow block variant | UML generalization (with endFill=0) |
| `open` | Open (unfilled) chevron | Lightweight direction indicator |
| `openThin` | Thin open chevron | Subtle direction |
| `oval` | Circular marker | Composition endpoints |
| `diamond` | Diamond-shaped marker | UML aggregation / composition |
| `diamondThin` | Narrow diamond variant | Lighter aggregation |
| `box` | Square marker | Terminal / endpoint marker |
| `halfCircle` | Semicircle | Interface notation |
| `circle` | Full circle | State machine notation |
| `circlePlus` | Circle with plus sign | Required interface (UML) |
| `cross` | X-shaped cross | Deletion / cancellation |
| `baseDash` | Horizontal dash at base | Base indicator |
| `doubleBlock` | Double triangular arrowhead | Double direction emphasis |
| `dash` | Short dash line | Simple terminator |
| `async` | Open arrow (async message) | UML sequence diagrams |
| `openAsync` | Open async arrow | Asynchronous messaging |
| `manyOptional` | Crow's foot many-optional | ER diagrams: zero or many |

### 6.2 Fill Behavior

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `startFill` | `0`, `1` | `1` | `1` = filled/solid start marker, `0` = hollow/outline |
| `endFill` | `0`, `1` | `1` | `1` = filled/solid end marker, `0` = hollow/outline |
| `startSize` | number | — | Size of start arrow marker in pixels |
| `endSize` | number | — | Size of end arrow marker in pixels |

**UML convention examples:**

```
// Inheritance (hollow triangle)
endArrow=block;endFill=0;

// Composition (filled diamond)
startArrow=diamond;startFill=1;

// Aggregation (hollow diamond)
startArrow=diamond;startFill=0;

// Dependency (open arrow, dashed)
endArrow=open;dashed=1;

// Implementation (hollow triangle, dashed)
endArrow=block;endFill=0;dashed=1;
```

---

## 7. Perimeter System

The perimeter system is one of the most critical and most frequently misunderstood aspects of Draw.io styling. The perimeter determines how edge connection points are calculated on the boundary of a shape.

### 7.1 Available Perimeter Types

| Perimeter Value | mxConstant | Used For |
|-----------------|------------|----------|
| `rectanglePerimeter` | PERIMETER_RECTANGLE | Rectangles, labels, images, cylinders, swimlanes |
| `ellipsePerimeter` | PERIMETER_ELLIPSE | Ellipses, circles, clouds, double ellipses |
| `rhombusPerimeter` | PERIMETER_RHOMBUS | Rhombus / diamond shapes |
| `trianglePerimeter` | PERIMETER_TRIANGLE | Triangle shapes |
| `hexagonPerimeter` | PERIMETER_HEXAGON | Hexagon shapes |

### 7.2 How Perimeters Work

When an edge connects to a shape, the edge routing algorithm needs to calculate the exact point on the shape's boundary where the edge should terminate. The perimeter function takes:

1. The center point of the shape's bounding box
2. The direction from which the edge approaches
3. The shape's dimensions

It then returns the precise intersection point on the shape's mathematical boundary.

### 7.3 Perimeter-Shape Matching Rules

**ALWAYS match the perimeter to the visual shape.** This is a hard requirement. Mismatched perimeters cause edges to connect at visually incorrect positions.

| Shape | REQUIRED Perimeter |
|-------|-------------------|
| Rectangle (default) | `rectanglePerimeter` (default) |
| Rounded rectangle | `rectanglePerimeter` |
| Ellipse / Circle | `ellipsePerimeter` |
| Double Ellipse | `ellipsePerimeter` |
| Rhombus / Diamond | `rhombusPerimeter` |
| Triangle | `trianglePerimeter` |
| Hexagon | `hexagonPerimeter` |
| Cloud | `ellipsePerimeter` |
| Cylinder | `rectanglePerimeter` |
| Swimlane | `rectanglePerimeter` |
| Parallelogram | `rectanglePerimeter` |
| Custom stencil (round) | `ellipsePerimeter` |
| Custom stencil (rectangular) | `rectanglePerimeter` |

### 7.4 What Happens With Wrong Perimeters

When a perimeter does not match the shape:

- **Ellipse with rectanglePerimeter:** Edges connect at the bounding box corners/sides instead of the curved boundary. This creates visible gaps between the edge endpoint and the ellipse outline.
- **Rectangle with ellipsePerimeter:** Edges connect at positions calculated for a curved boundary, causing endpoints to float outside or inside the rectangle.
- **Rhombus with rectanglePerimeter:** Edges connect to the bounding box instead of the diamond's diagonal edges, creating gaps at the diamond's sides.

---

## 8. Container and Group Styles

Containers (groups) allow shapes to hold child shapes. Children use coordinates relative to their parent container.

### 8.1 Container Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `container` | `0`, `1` | `0` | Marks cell as a container that can hold children |
| `collapsible` | `0`, `1` | `1` | Shows collapse/expand button on container |
| `recursiveResize` | `0`, `1` | `1` | Resize children proportionally when container resizes |
| `foldable` | `0`, `1` | — | Allow fold/collapse capability |

### 8.2 Swimlane Properties

Swimlanes are a specialized container type with a header bar:

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `swimlane` | (leading identifier) | — | Marks shape as a swimlane |
| `startSize` | number | `23` | Height of the swimlane header in pixels |
| `horizontal` | `0`, `1` | `1` | `1` = horizontal swimlane (header on top), `0` = vertical (header on left) |
| `swimlaneFillColor` | `#RRGGBB` | — | Fill color of the swimlane body (below header) |
| `swimlaneLine` | `0`, `1` | — | Show/hide the line between header and body |
| `separatorColor` | `#RRGGBB` | — | Color of the header/body separator line |

### 8.3 Child Layout Properties

Containers can automatically arrange their children using layout properties:

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `childLayout` | `stackLayout`, `treeLayout`, `flowLayout` | — | Automatic layout algorithm for children |
| `resizeParent` | `0`, `1` | — | Parent container resizes to fit children |
| `resizeParentMax` | `0`, `1` | — | Limit parent auto-resize |
| `resizeLast` | `0`, `1` | — | Last child fills remaining space in stack |
| `horizontalStack` | `0`, `1` | — | Stack direction: `1` = horizontal, `0` = vertical |
| `marginBottom` | number | — | Bottom margin for stack layout |

### 8.4 Container Example

```xml
<!-- Parent container -->
<mxCell id="group1" value="My Group" style="swimlane;horizontal=1;startSize=30;
  fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;
  html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="400" height="300" as="geometry" />
</mxCell>

<!-- Child shape (coordinates relative to parent) -->
<mxCell id="child1" value="Step 1" style="rounded=1;whiteSpace=wrap;html=1;
  fillColor=#DAE8FC;strokeColor=#6C8EBF;" vertex="1" parent="group1">
  <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
</mxCell>
```

Note that `child1` has `parent="group1"` and its coordinates `(20, 40)` are relative to the group's top-left corner, not the canvas origin.

---

## 9. Special Styles

### 9.1 Image Shapes

Image shapes display an external image:

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `image` | URL string | — | Image URL (supports `data:` URIs, HTTP URLs, and built-in images) |
| `imageWidth` | number | `42` | Image display width |
| `imageHeight` | number | `42` | Image display height |
| `imageAlign` | `left`, `center`, `right` | — | Horizontal alignment of image within shape |
| `imageVerticalAlign` | `top`, `middle`, `bottom` | — | Vertical alignment of image within shape |
| `imageAspect` | `0`, `1` | `1` | Preserve image aspect ratio |
| `imageBackground` | `#RRGGBB` | — | Background color behind image |
| `imageBorder` | `#RRGGBB` | — | Border color around image |

Example of an image shape:
```
shape=image;image=https://example.com/icon.png;imageWidth=48;imageHeight=48;html=1;
```

### 9.2 Behavior / Lock Properties

These properties control user interaction permissions on individual cells:

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `movable` | `0`, `1` | `1` | Allow the user to drag/move the cell |
| `resizable` | `0`, `1` | `1` | Allow the user to resize the cell |
| `rotatable` | `0`, `1` | `1` | Allow rotation via the rotation handle |
| `bendable` | `0`, `1` | `1` | Allow adding/moving edge bend points |
| `editable` | `0`, `1` | `1` | Allow double-click label editing |
| `deletable` | `0`, `1` | `1` | Allow deletion via keyboard |
| `cloneable` | `0`, `1` | `1` | Allow cloning via Ctrl+drag |
| `connectable` | `0`, `1` | `1` | Allow creating new connections from this cell |
| `pointerEvents` | `0`, `1` | `1` | Enable mouse event handling (transparent shapes) |
| `autosize` | `0`, `1` | `0` | Automatically resize shape to fit label content |

Setting `movable=0;resizable=0;editable=0;deletable=0;` creates a locked, read-only shape.

### 9.3 Indicator Properties

Indicators are small markers that appear on a shape (like status icons):

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `indicatorShape` | shape name | — | Shape type for the indicator |
| `indicatorImage` | URL | — | Image for the indicator |
| `indicatorColor` | `#RRGGBB` | — | Indicator fill color |
| `indicatorStrokeColor` | `#RRGGBB` | — | Indicator border color |
| `indicatorGradientColor` | `#RRGGBB` | — | Indicator gradient end color |
| `indicatorSpacing` | number | — | Gap between label and indicator |
| `indicatorWidth` | number | — | Indicator width |
| `indicatorHeight` | number | — | Indicator height |
| `indicatorDirection` | direction | — | Indicator placement direction |

### 9.4 Port Constraints

Port constraints limit where edges can connect to a shape:

| Property | Values | Description |
|----------|--------|-------------|
| `portConstraint` | `eastwest`, `northsouth`, `perimeter`, `fixed` | General connection direction constraint |
| `sourcePortConstraint` | direction | Constraint on source side only |
| `targetPortConstraint` | direction | Constraint on target side only |

---

## 10. Style Inheritance and Defaults

### 10.1 Default Style Registry

mxGraph maintains a registry of default styles for vertices and edges. When a cell is created, its effective style is computed by:

1. **Base default** — The built-in default style for vertex or edge
2. **Named style** — If the style string starts with a registered style name
3. **Inline overrides** — Properties in the cell's `style` attribute override defaults

### 10.2 Vertex Defaults

The default vertex style includes:
```
shape=rectangle;perimeter=rectanglePerimeter;whiteSpace=wrap;html=1;
overflow=hidden;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;
fontSize=12;fontFamily=Helvetica;align=center;verticalAlign=middle;
```

### 10.3 Edge Defaults

The default edge style includes:
```
shape=connector;endArrow=classic;html=1;strokeColor=#000000;fontColor=#000000;
fontSize=12;fontFamily=Helvetica;align=center;verticalAlign=middle;
rounded=1;
```

### 10.4 Style Resolution Order

When rendering, properties are resolved in this order (later overrides earlier):

1. **Built-in defaults** (hardcoded in mxGraph)
2. **Theme defaults** (from the stylesheet registered in the graph)
3. **Named style** (if the style string references a registered name)
4. **Inline properties** (explicit key=value pairs in the style string)

This means you only need to specify properties that DIFFER from the defaults. For example, a rectangle only needs:
```
whiteSpace=wrap;html=1;
```
because `shape=rectangle` and `perimeter=rectanglePerimeter` are already defaults.

### 10.5 Theme Colors

Draw.io supports multiple themes. The `default` keyword for colors refers to the theme's default:

- **Kennedy theme** (default): white fill, black stroke
- **Dark theme**: dark fill, light stroke
- **Sketch theme**: hand-drawn style with muted colors
- **Simple theme**: minimal styling
- **Atlas theme**: blue-accented professional look

Using `fillColor=default` and `strokeColor=default` makes shapes adapt to whatever theme the user has selected.

---

## 11. Common Anti-Patterns and Mistakes

### 11.1 Missing html=1

**Problem:** Labels render as plain text, losing all formatting.

```
// WRONG — no html=1
rounded=1;whiteSpace=wrap;fillColor=#DAE8FC;

// CORRECT
rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;
```

Every vertex and edge MUST include `html=1`.

### 11.2 Wrong Perimeter for Shape

**Problem:** Edges connect at incorrect positions, floating away from the shape boundary.

```
// WRONG — rectangle perimeter on an ellipse
ellipse;whiteSpace=wrap;html=1;perimeter=rectanglePerimeter;

// CORRECT
ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;
```

ALWAYS match the perimeter to the shape type. See Section 7.3 for the complete mapping.

### 11.3 Using true/false Instead of 1/0

**Problem:** Boolean properties are silently ignored.

```
// WRONG — uses boolean strings
rounded=true;dashed=true;shadow=true;

// CORRECT — uses 0/1
rounded=1;dashed=1;shadow=1;
```

Draw.io boolean properties ALWAYS use `0` and `1`, NEVER `true` and `false`.

### 11.4 Conflicting Label Positioning

**Problem:** Label appears in unexpected position when `labelPosition` and `align` are not coordinated.

```
// WRONG — both push label to the right
labelPosition=right;align=right;

// CORRECT — align opposes labelPosition
labelPosition=right;align=left;
```

When `labelPosition` is not `center`, `align` MUST be set to the opposite value.

### 11.5 Missing whiteSpace=wrap

**Problem:** Long labels extend beyond shape bounds in a single line instead of wrapping.

```
// WRONG — no wrapping
html=1;fillColor=#DAE8FC;

// CORRECT
whiteSpace=wrap;html=1;fillColor=#DAE8FC;
```

ALWAYS include `whiteSpace=wrap` for shapes with text labels.

### 11.6 Edge Missing relative Geometry

**Problem:** Edge labels and waypoints positioned incorrectly.

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

Edge geometry MUST include `relative="1"` for correct coordinate calculation.

### 11.7 Applying Vertex Styles to Edges (and Vice Versa)

**Problem:** Some properties only apply to vertices or only to edges.

Vertex-only properties (ignored on edges): `fillColor`, `shape` (except `connector`), `container`, `collapsible`, `swimlane`.

Edge-only properties (ignored on vertices): `edgeStyle`, `startArrow`, `endArrow`, `curved`, `jettySize`, `exitX/Y`, `entryX/Y`.

### 11.8 Shadow Without Global Shadow

**Problem:** Per-cell `shadow=1` has no effect.

The cell-level `shadow=1` property only works when the `<mxGraphModel>` element also has `shadow="1"`. If the model-level shadow is disabled, individual cell shadows are not rendered.

### 11.9 Incorrect Dash Pattern Format

**Problem:** Dash pattern not rendering as expected.

```
// WRONG — no spaces, wrong format
dashed=1;dashPattern=84;

// CORRECT — space-separated values
dashed=1;dashPattern=8 4;
```

The `dashPattern` value is a space-separated list of dash and gap lengths. ALWAYS set `dashed=1` alongside `dashPattern`.

### 11.10 Forgetting container=1 for Groups

**Problem:** Child shapes do not move with the parent, coordinates are not relative.

```
// WRONG — no container flag
swimlane;html=1;startSize=30;

// CORRECT
swimlane;html=1;startSize=30;container=1;
```

Any shape intended to hold children MUST include `container=1`.

---

## 12. Quick Reference: Complete Style String Templates

### 12.1 Common Shape Templates

```
// Rectangle
rounded=0;whiteSpace=wrap;html=1;

// Rounded Rectangle
rounded=1;whiteSpace=wrap;html=1;arcSize=10;

// Ellipse
ellipse;whiteSpace=wrap;html=1;perimeter=ellipsePerimeter;

// Diamond (Decision)
rhombus;whiteSpace=wrap;html=1;perimeter=rhombusPerimeter;

// Triangle
triangle;whiteSpace=wrap;html=1;perimeter=trianglePerimeter;

// Hexagon
shape=hexagon;whiteSpace=wrap;html=1;perimeter=hexagonPerimeter;

// Cylinder (Database)
shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;size=15;

// Cloud
ellipse;shape=cloud;whiteSpace=wrap;html=1;

// Document
shape=document;whiteSpace=wrap;html=1;boundedLbl=1;size=0.27;

// Parallelogram
shape=parallelogram;whiteSpace=wrap;html=1;perimeter=parallelogramPerimeter;
```

### 12.2 Common Edge Templates

```
// Standard arrow
endArrow=classic;html=1;

// Orthogonal connector
edgeStyle=orthogonalEdgeStyle;rounded=1;orthogonalLoop=1;jettySize=auto;html=1;endArrow=classic;

// Dashed dependency
endArrow=open;dashed=1;html=1;

// Bidirectional
startArrow=classic;endArrow=classic;html=1;

// No arrows (association)
endArrow=none;startArrow=none;html=1;

// UML inheritance
endArrow=block;endFill=0;html=1;edgeStyle=orthogonalEdgeStyle;

// UML composition
startArrow=diamond;startFill=1;endArrow=open;html=1;

// Curved connector
curved=1;endArrow=classic;html=1;
```

### 12.3 Swimlane Template

```
// Horizontal swimlane
swimlane;horizontal=1;startSize=30;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;container=1;collapsible=0;html=1;whiteSpace=wrap;
```

---

## 13. Property Reference Summary Table

Total unique style properties documented in this reference: **120+**

| Category | Count | Key Properties |
|----------|-------|---------------|
| Fill & Stroke | 12 | fillColor, strokeColor, strokeWidth, opacity, dashed |
| Shape Geometry | 10 | shape, perimeter, rounded, arcSize, rotation, direction |
| Font & Label | 18 | fontSize, fontFamily, fontStyle, fontColor, align, whiteSpace |
| Edge Routing | 10 | edgeStyle, curved, rounded, jettySize, elbow |
| Connection Points | 12 | exitX/Y, entryX/Y, exitDx/Dy, entryDx/Dy, exitPerimeter, entryPerimeter |
| Arrows | 6 | startArrow, endArrow, startFill, endFill, startSize, endSize |
| Container | 10 | container, collapsible, childLayout, startSize, swimlaneFillColor |
| Image | 8 | image, imageWidth, imageHeight, imageAlign, imageAspect |
| Sketch Mode | 11 | sketch, comic, fillStyle, jiggle, curveFitting |
| Behavior | 11 | movable, resizable, editable, deletable, connectable, autosize |
| Indicator | 9 | indicatorShape, indicatorColor, indicatorSpacing |
| Label Position | 6 | labelPosition, verticalLabelPosition, spacing, labelWidth |
