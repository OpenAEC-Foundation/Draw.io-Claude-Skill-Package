# Draw.io Style Properties — Complete Reference Catalog

> 120+ style properties organized by category. Every property includes its exact name,
> valid values, default value, and description.

---

## 1. Fill Properties

Properties controlling the interior fill of shapes (vertices only).

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `fillColor` | `#RRGGBB`, `none`, `default` | `default` | Interior fill color. `none` = transparent. `default` = theme color. |
| `gradientColor` | `#RRGGBB`, `none` | `none` | Gradient end color. Start color is `fillColor`. |
| `gradientDirection` | `north`, `south`, `east`, `west` | `south` | Direction of gradient flow. |
| `opacity` | 0–100 | `100` | Overall opacity. Affects BOTH fill and stroke. |
| `fillOpacity` | 0–100 | `100` | Fill-only opacity. Independent of `strokeOpacity`. |

### Fill Color Rules

- `fillColor=default` uses the active theme's default fill (Kennedy theme: `#FFFFFF`).
- `fillColor=none` makes the shape fully transparent.
- ALWAYS use `#RRGGBB` hex notation (6 digits). NEVER use 3-digit hex (`#FFF`), RGB functions, or color names.

---

## 2. Stroke Properties

Properties controlling borders, outlines, and line rendering.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `strokeColor` | `#RRGGBB`, `none`, `default` | `default` | Border/outline color. |
| `strokeWidth` | number | `1` | Border thickness in pixels. |
| `strokeOpacity` | 0–100 | `100` | Stroke-only opacity. |
| `dashed` | `0`, `1` | `0` | Enable dashed stroke rendering. |
| `dashPattern` | string | — | Custom dash pattern. Space-separated values (e.g., `8 4` = 8px dash, 4px gap). |
| `fixDash` | `0`, `1` | `0` | When `1`, dash pattern does NOT scale with `strokeWidth`. |

### Dash Pattern Rules

- ALWAYS set `dashed=1` when using `dashPattern`. The pattern is ignored without `dashed=1`.
- Format: space-separated list of alternating dash and gap lengths in pixels.
- Example: `dashed=1;dashPattern=8 4;` = 8px dash, 4px gap, repeating.
- Example: `dashed=1;dashPattern=12 4 4 4;` = long dash, gap, dot, gap (dash-dot pattern).

---

## 3. Decorative Effects

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `shadow` | `0`, `1` | `0` | Drop shadow behind shape. ONLY works when `<mxGraphModel shadow="1">`. |
| `glass` | `0`, `1` | `0` | Glossy shine overlay effect. |
| `rounded` | `0`, `1` | `0` | Rounded corners on rectangles and edge bends. |

---

## 4. Shape Geometry Modifiers

Properties controlling shape geometry, rotation, and sizing.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `shape` | shape name | `rectangle` | Base shape type. See Section 15 for complete catalog. |
| `perimeter` | perimeter name | `rectanglePerimeter` | Edge connection boundary calculator. MUST match shape. |
| `rounded` | `0`, `1` | `0` | Round rectangle corners. |
| `arcSize` | 0–50 | varies | Corner radius as percentage of shorter side. |
| `absoluteArcSize` | `0`, `1` | `0` | When `1`, `arcSize` is in absolute pixels instead of percentage. |
| `aspect` | `variable`, `fixed` | `variable` | `fixed` preserves width/height ratio on resize. |
| `direction` | `north`, `south`, `east`, `west` | — | Rotates shape in 90-degree increments. |
| `flipH` | `0`, `1` | `0` | Mirror shape horizontally. |
| `flipV` | `0`, `1` | `0` | Mirror shape vertically. |
| `rotation` | 0–360 | `0` | Free rotation angle in degrees. |
| `fixedSize` | `0`, `1` | `0` | Shape size independent of label size. |

### Perimeter-Shape Matching (MANDATORY)

ALWAYS set the correct perimeter for non-default shapes:

| Shape | Required Perimeter |
|-------|-------------------|
| `rectangle` (default) | `rectanglePerimeter` (default — no need to specify) |
| Rounded rectangle | `rectanglePerimeter` (default) |
| `ellipse` | `ellipsePerimeter` |
| `doubleEllipse` | `ellipsePerimeter` |
| `rhombus` | `rhombusPerimeter` |
| `triangle` | `trianglePerimeter` |
| `hexagon` | `hexagonPerimeter` |
| `cloud` | `ellipsePerimeter` |
| `cylinder` / `cylinder3` | `rectanglePerimeter` |
| `swimlane` | `rectanglePerimeter` |
| `parallelogram` | `rectanglePerimeter` |
| Stencil (round visual) | `ellipsePerimeter` |
| Stencil (rectangular visual) | `rectanglePerimeter` |

---

## 5. Font Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `fontSize` | number | `12` | Font size in pixels. |
| `fontFamily` | string | `Helvetica` | Font family name. |
| `fontColor` | `#RRGGBB`, `default` | `default` | Text color. |
| `fontStyle` | bitmask integer | `0` | Combined font style flags. See bitfield table below. |

### fontStyle Bitfield

Combine flags by adding their values:

| Flag | Value | Effect |
|------|-------|--------|
| Normal | `0` | No decoration |
| Bold | `1` | **Bold** text |
| Italic | `2` | *Italic* text |
| Underline | `4` | Underlined text |
| Strikethrough | `8` | ~~Strikethrough~~ text |

Common combinations:

| fontStyle | Result |
|-----------|--------|
| `0` | Normal |
| `1` | Bold |
| `2` | Italic |
| `3` | Bold + Italic |
| `4` | Underline |
| `5` | Bold + Underline |
| `7` | Bold + Italic + Underline |
| `9` | Bold + Strikethrough |

---

## 6. Text Alignment

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `align` | `left`, `center`, `right` | `center` | Horizontal text alignment within label bounds. |
| `verticalAlign` | `top`, `middle`, `bottom` | `middle` | Vertical text alignment within label bounds. |

---

## 7. Label Positioning

Controls WHERE the label is placed relative to the shape. Independent of text alignment.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelPosition` | `left`, `center`, `right` | `center` | Horizontal label position relative to shape. |
| `verticalLabelPosition` | `top`, `middle`, `bottom` | `middle` | Vertical label position relative to shape. |

### Label Position Alignment Rule (MANDATORY)

When `labelPosition` is NOT `center`, ALWAYS set `align` to the OPPOSITE value:

| labelPosition | Required align |
|---------------|---------------|
| `left` | `right` |
| `right` | `left` |
| `center` | any (default: `center`) |

When `verticalLabelPosition` is NOT `middle`, ALWAYS set `verticalAlign` to the OPPOSITE value:

| verticalLabelPosition | Required verticalAlign |
|-----------------------|----------------------|
| `top` | `bottom` |
| `bottom` | `top` |
| `middle` | any (default: `middle`) |

---

## 8. Text Wrapping and Overflow

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `whiteSpace` | `wrap`, `nowrap` | — | `wrap` enables word wrapping to fit shape width. |
| `overflow` | `visible`, `hidden`, `fill`, `width` | — | How text exceeding bounds is handled. |
| `labelWidth` | number | — | Fixed label width in pixels. |
| `horizontal` | `0`, `1` | `1` | `0` renders text vertically (rotated 90 degrees). |
| `textDirection` | `default`, `ltr`, `rtl` | `default` | Text direction for bidirectional text. |

### Overflow Values

| Value | Behavior |
|-------|----------|
| `visible` | Text extends beyond shape bounds (default for edges). |
| `hidden` | Text is clipped at shape bounds. |
| `fill` | Label fills the entire shape. |
| `width` | Label has fixed width but variable height. |

---

## 9. Label Spacing (Padding)

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `spacing` | number | `2` | Base padding on ALL sides in pixels. |
| `spacingTop` | number | `0` | Additional top padding. Added to `spacing`. |
| `spacingBottom` | number | `0` | Additional bottom padding. Added to `spacing`. |
| `spacingLeft` | number | `0` | Additional left padding. Added to `spacing`. |
| `spacingRight` | number | `0` | Additional right padding. Added to `spacing`. |

Total top padding = `spacing` + `spacingTop`. Each directional spacing is ADDED to the base `spacing` value.

---

## 10. Label Background and Visibility

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelBackgroundColor` | `#RRGGBB`, `none`, `default` | — | Background color behind the text label. |
| `labelBorderColor` | `#RRGGBB`, `none` | — | Border color around the label. |
| `textOpacity` | 0–100 | `100` | Opacity of the text only. |
| `noLabel` | `0`, `1` | `0` | Hide the label entirely. Shape still visible. |

---

## 11. Edge Style (Routing Algorithm)

The `edgeStyle` property determines how an edge is routed between source and target.

| edgeStyle Value | Description | Typical Use |
|-----------------|-------------|-------------|
| (omitted) | Straight line, no routing | Simple direct connections |
| `orthogonalEdgeStyle` | Right-angle bends (rectilinear) | Flowcharts, most diagrams |
| `elbowEdgeStyle` | Single L-shaped or Z-shaped elbow | Simple orthogonal layouts |
| `entityRelationEdgeStyle` | Fixed-length stubs at both ends | ER diagrams |
| `segmentEdgeStyle` | User-defined segments via waypoints | Manual custom routing |
| `sideToSideEdgeStyle` | Horizontal routing, side to side | Left-right flow layouts |
| `topToBottomEdgeStyle` | Vertical routing, top to bottom | Top-down hierarchies |
| `loopEdgeStyle` | Self-referencing loop | Self-connections |
| `isometricEdgeStyle` | 30-degree angle routing | Isometric diagrams |

---

## 12. Edge Path Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `curved` | `0`, `1` | `0` | Smooth curved path instead of sharp corners. |
| `rounded` | `0`, `1` | `1` | Round edge corners (for orthogonal edges). |
| `elbow` | `horizontal`, `vertical` | — | Preferred direction for elbow edges. |
| `orthogonalLoop` | `0`, `1` | `1` | Routing style for self-referencing loops. |
| `noEdgeStyle` | `0`, `1` | `0` | Disable edge style application entirely (straight line). |

---

## 13. Connection Points (Entry/Exit)

Relative coordinates where `(0,0)` = top-left and `(1,1)` = bottom-right of the shape.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `exitX` | 0.0–1.0 | — | Relative X of exit point on source shape. |
| `exitY` | 0.0–1.0 | — | Relative Y of exit point on source shape. |
| `exitDx` | number | — | Absolute X offset from the exit point (pixels). |
| `exitDy` | number | — | Absolute Y offset from the exit point (pixels). |
| `exitPerimeter` | `0`, `1` | `1` | Project exit point onto shape perimeter. |
| `entryX` | 0.0–1.0 | — | Relative X of entry point on target shape. |
| `entryY` | 0.0–1.0 | — | Relative Y of entry point on target shape. |
| `entryDx` | number | — | Absolute X offset from the entry point (pixels). |
| `entryDy` | number | — | Absolute Y offset from the entry point (pixels). |
| `entryPerimeter` | `0`, `1` | `1` | Project entry point onto shape perimeter. |

### Common Connection Points

| Position | X | Y |
|----------|---|---|
| Top-left | `0` | `0` |
| Top-center | `0.5` | `0` |
| Top-right | `1` | `0` |
| Middle-left | `0` | `0.5` |
| Center | `0.5` | `0.5` |
| Middle-right | `1` | `0.5` |
| Bottom-left | `0` | `1` |
| Bottom-center | `0.5` | `1` |
| Bottom-right | `1` | `1` |

---

## 14. Edge Spacing and Jetty

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jettySize` | `auto`, number | `auto` | Minimum length of first/last segment for orthogonal edges. |
| `sourceJettySize` | number | — | Override jetty size at source end only. |
| `targetJettySize` | number | — | Override jetty size at target end only. |
| `perimeterSpacing` | number | — | Gap between edge endpoint and perimeter (both ends). |
| `sourcePerimeterSpacing` | number | — | Gap between edge endpoint and source perimeter. |
| `targetPerimeterSpacing` | number | — | Gap between edge endpoint and target perimeter. |

---

## 15. Line Crossing Visualization

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jumpStyle` | `arc`, `gap`, `sharp` | — | How crossing lines are visualized. |
| `jumpSize` | number | `6` | Size of the jump/gap at crossings in pixels. |

---

## 16. Arrow Properties

### Arrow Type Values

Set via `startArrow` and `endArrow`.

| Arrow Value | Visual Description | Typical Use |
|-------------|-------------------|-------------|
| `none` | No arrow marker | Undirected connections, associations |
| `classic` | Traditional triangular arrowhead | Standard directed flow |
| `classicThin` | Slender classic variant | Lighter visual weight |
| `block` | Solid filled triangle | Strong directional indicator |
| `blockThin` | Narrow block variant | UML generalization (with `endFill=0`) |
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

### Arrow Fill and Size

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `startFill` | `0`, `1` | `1` | `1` = filled/solid start marker, `0` = hollow/outline. |
| `endFill` | `0`, `1` | `1` | `1` = filled/solid end marker, `0` = hollow/outline. |
| `startSize` | number | — | Size of start arrow marker in pixels. |
| `endSize` | number | — | Size of end arrow marker in pixels. |

### UML Arrow Conventions

| Relationship | Style Properties |
|-------------|-----------------|
| Inheritance | `endArrow=block;endFill=0;` |
| Composition | `startArrow=diamond;startFill=1;` |
| Aggregation | `startArrow=diamond;startFill=0;` |
| Dependency | `endArrow=open;dashed=1;` |
| Implementation | `endArrow=block;endFill=0;dashed=1;` |
| Association | `endArrow=open;` |
| Bidirectional | `startArrow=classic;endArrow=classic;` |
| No direction | `endArrow=none;startArrow=none;` |

---

## 17. Built-in Shape Catalog

### Primitive Shapes (mxGraph core)

| Shape Value | mxConstant | Default Perimeter |
|-------------|------------|-------------------|
| `rectangle` | `SHAPE_RECTANGLE` | `rectanglePerimeter` |
| `ellipse` | `SHAPE_ELLIPSE` | `ellipsePerimeter` |
| `doubleEllipse` | `SHAPE_DOUBLE_ELLIPSE` | `ellipsePerimeter` |
| `rhombus` | `SHAPE_RHOMBUS` | `rhombusPerimeter` |
| `triangle` | `SHAPE_TRIANGLE` | `trianglePerimeter` |
| `hexagon` | `SHAPE_HEXAGON` | `hexagonPerimeter` |
| `cylinder` | `SHAPE_CYLINDER` | `rectanglePerimeter` |
| `cloud` | `SHAPE_CLOUD` | `ellipsePerimeter` |
| `actor` | `SHAPE_ACTOR` | `rectanglePerimeter` |
| `label` | `SHAPE_LABEL` | `rectanglePerimeter` |
| `swimlane` | `SHAPE_SWIMLANE` | `rectanglePerimeter` |
| `line` | `SHAPE_LINE` | — |
| `image` | `SHAPE_IMAGE` | `rectanglePerimeter` |
| `arrow` | `SHAPE_ARROW` | `rectanglePerimeter` |
| `arrowConnector` | `SHAPE_ARROW_CONNECTOR` | — |
| `connector` | `SHAPE_CONNECTOR` | — |

### Extended Shapes (Draw.io additions)

| Shape Value | Description |
|-------------|-------------|
| `parallelogram` | Parallelogram / input-output symbol |
| `trapezoid` | Trapezoid shape |
| `step` | Step / chevron shape |
| `process` | Process rectangle (double vertical borders) |
| `document` | Document with wavy bottom edge |
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

---

## 18. Stencil Library Shapes

Stencil shapes use the `shape=mxgraph.<library>.<shape>` format.

### Format

```
shape=mxgraph.<library>.<shape>;
```

ALWAYS include the full `mxgraph.` prefix. NEVER use a bare stencil name.

### Common Stencil Libraries

| Library Prefix | Domain | Example |
|---------------|--------|---------|
| `mxgraph.flowchart` | Flowchart | `shape=mxgraph.flowchart.decision;` |
| `mxgraph.bpmn` | Business Process | `shape=mxgraph.bpmn.shape;` |
| `mxgraph.uml` | UML | `shape=mxgraph.uml.component;` |
| `mxgraph.er` | Entity-Relationship | `shape=mxgraph.er.entity;` |
| `mxgraph.aws4` | AWS Architecture | `shape=mxgraph.aws4.lambda_function;` |
| `mxgraph.azure` | Azure Architecture | `shape=mxgraph.azure.virtual_machine;` |
| `mxgraph.gcp2` | Google Cloud | `shape=mxgraph.gcp2.compute_engine;` |
| `mxgraph.cisco` | Cisco Network | `shape=mxgraph.cisco.router;` |
| `mxgraph.network` | General Network | `shape=mxgraph.network.server;` |
| `mxgraph.ios` | iOS Mockup | `shape=mxgraph.ios.iPhone;` |
| `mxgraph.android` | Android Mockup | `shape=mxgraph.android.phone;` |
| `mxgraph.mockup` | General Mockup | `shape=mxgraph.mockup.buttons.button;` |
| `mxgraph.electrical` | Electrical | `shape=mxgraph.electrical.resistor;` |
| `mxgraph.floorplan` | Floor Plans | `shape=mxgraph.floorplan.wall;` |

### Stencil Perimeter Rules

Stencil shapes do NOT automatically set their perimeter. ALWAYS set the perimeter based on the stencil's visual form:

- Round stencils → `perimeter=ellipsePerimeter;`
- Rectangular stencils → `perimeter=rectanglePerimeter;`
- Diamond stencils → `perimeter=rhombusPerimeter;`

---

## 19. Perimeter Types

| Perimeter Value | Used For |
|-----------------|----------|
| `rectanglePerimeter` | Rectangles, labels, images, cylinders, swimlanes, parallelograms |
| `ellipsePerimeter` | Ellipses, circles, clouds, double ellipses, round stencils |
| `rhombusPerimeter` | Rhombus / diamond shapes |
| `trianglePerimeter` | Triangle shapes |
| `hexagonPerimeter` | Hexagon shapes |

---

## 20. Container Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `container` | `0`, `1` | `0` | Marks cell as a container that holds children. |
| `collapsible` | `0`, `1` | `1` | Shows collapse/expand button on container. |
| `recursiveResize` | `0`, `1` | `1` | Resize children proportionally when container resizes. |
| `foldable` | `0`, `1` | — | Allow fold/collapse capability. |

---

## 21. Swimlane Properties

Swimlanes are specialized containers with a header bar.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `startSize` | number | `23` | Height of the swimlane header in pixels. |
| `horizontal` | `0`, `1` | `1` | `1` = horizontal (header on top), `0` = vertical (header on left). |
| `swimlaneFillColor` | `#RRGGBB` | — | Fill color of the swimlane body (below header). |
| `swimlaneLine` | `0`, `1` | — | Show/hide the line between header and body. |
| `separatorColor` | `#RRGGBB` | — | Color of the header/body separator line. |

---

## 22. Child Layout Properties

Containers can automatically arrange their children.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `childLayout` | `stackLayout`, `treeLayout`, `flowLayout` | — | Automatic layout algorithm for children. |
| `resizeParent` | `0`, `1` | — | Parent container resizes to fit children. |
| `resizeParentMax` | `0`, `1` | — | Limit parent auto-resize. |
| `resizeLast` | `0`, `1` | — | Last child fills remaining space in stack. |
| `horizontalStack` | `0`, `1` | — | Stack direction: `1` = horizontal, `0` = vertical. |
| `marginBottom` | number | — | Bottom margin for stack layout. |

---

## 23. Sketch / Hand-Drawn Mode

Powered by rough.js. These properties control hand-drawn appearance.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `sketch` | `0`, `1` | `0` | Enable hand-drawn / sketch style rendering. |
| `comic` | `0`, `1` | `0` | Comic book style variant. |
| `fillStyle` | `solid`, `hachure`, `cross-hatch`, `dots` | — | Fill pattern in sketch mode. |
| `fillWeight` | number | — | Weight of hatch lines. |
| `hachureGap` | number | — | Gap between hatch lines in pixels. |
| `hachureAngle` | number (degrees) | — | Angle of hatch lines. |
| `jiggle` | number | — | Amount of randomness / wobble in lines. Higher = more wobbly. |
| `curveFitting` | 0–1 | — | Quality of curve approximation. |
| `simplification` | 0–1 | — | Path simplification level. |
| `disableMultiStroke` | `0`, `1` | — | Disable double-stroke effect. |
| `disableMultiStrokeFill` | `0`, `1` | — | Disable double-stroke on fill. |

---

## 24. Image Shape Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `image` | URL string | — | Image URL. Supports `data:` URIs, HTTP URLs, and built-in images. |
| `imageWidth` | number | `42` | Image display width in pixels. |
| `imageHeight` | number | `42` | Image display height in pixels. |
| `imageAlign` | `left`, `center`, `right` | — | Horizontal alignment of image within shape. |
| `imageVerticalAlign` | `top`, `middle`, `bottom` | — | Vertical alignment of image within shape. |
| `imageAspect` | `0`, `1` | `1` | Preserve image aspect ratio. |
| `imageBackground` | `#RRGGBB` | — | Background color behind image. |
| `imageBorder` | `#RRGGBB` | — | Border color around image. |

Image shape usage:
```
shape=image;image=https://example.com/icon.png;imageWidth=48;imageHeight=48;html=1;
```

---

## 25. Behavior / Lock Properties

Control user interaction permissions on individual cells.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `movable` | `0`, `1` | `1` | Allow the user to drag/move the cell. |
| `resizable` | `0`, `1` | `1` | Allow the user to resize the cell. |
| `rotatable` | `0`, `1` | `1` | Allow rotation via the rotation handle. |
| `bendable` | `0`, `1` | `1` | Allow adding/moving edge bend points. |
| `editable` | `0`, `1` | `1` | Allow double-click label editing. |
| `deletable` | `0`, `1` | `1` | Allow deletion via keyboard. |
| `cloneable` | `0`, `1` | `1` | Allow cloning via Ctrl+drag. |
| `connectable` | `0`, `1` | `1` | Allow creating new connections from this cell. |
| `pointerEvents` | `0`, `1` | `1` | Enable mouse event handling. Set `0` for click-through shapes. |
| `autosize` | `0`, `1` | `0` | Automatically resize shape to fit label content. |

### Locked Shape Pattern

To create a fully locked, read-only shape:
```
movable=0;resizable=0;editable=0;deletable=0;rotatable=0;connectable=0;
```

---

## 26. Indicator Properties

Small markers that appear on a shape (e.g., status icons).

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `indicatorShape` | shape name | — | Shape type for the indicator. |
| `indicatorImage` | URL | — | Image for the indicator. |
| `indicatorColor` | `#RRGGBB` | — | Indicator fill color. |
| `indicatorStrokeColor` | `#RRGGBB` | — | Indicator border color. |
| `indicatorGradientColor` | `#RRGGBB` | — | Indicator gradient end color. |
| `indicatorSpacing` | number | — | Gap between label and indicator in pixels. |
| `indicatorWidth` | number | — | Indicator width in pixels. |
| `indicatorHeight` | number | — | Indicator height in pixels. |
| `indicatorDirection` | direction | — | Indicator placement direction. |

---

## 27. Port Constraints

Limit where edges can connect to a shape.

| Property | Values | Description |
|----------|--------|-------------|
| `portConstraint` | `eastwest`, `northsouth`, `perimeter`, `fixed` | General connection direction constraint. |
| `sourcePortConstraint` | direction value | Constraint on source side only. |
| `targetPortConstraint` | direction value | Constraint on target side only. |

---

## 28. Style Inheritance and Defaults

### Resolution Order (later overrides earlier)

1. **Built-in defaults** — hardcoded in mxGraph
2. **Theme defaults** — from the stylesheet registered in the graph
3. **Named style** — if the style string references a registered name
4. **Inline properties** — explicit `key=value` pairs in the style string

### Default Vertex Style

```
shape=rectangle;perimeter=rectanglePerimeter;whiteSpace=wrap;html=1;
overflow=hidden;fillColor=#ffffff;strokeColor=#000000;fontColor=#000000;
fontSize=12;fontFamily=Helvetica;align=center;verticalAlign=middle;
```

### Default Edge Style

```
shape=connector;endArrow=classic;html=1;strokeColor=#000000;fontColor=#000000;
fontSize=12;fontFamily=Helvetica;align=center;verticalAlign=middle;rounded=1;
```

You only need to specify properties that DIFFER from these defaults. A rectangle only needs:
```
whiteSpace=wrap;html=1;
```

### Theme Colors

The `default` keyword adapts to the active theme:

| Theme | Default Fill | Default Stroke |
|-------|-------------|----------------|
| Kennedy (default) | White | Black |
| Dark | Dark fill | Light stroke |
| Sketch | Muted colors | Muted stroke |
| Simple | Minimal | Minimal |
| Atlas | Blue-accented | Professional |

Using `fillColor=default;strokeColor=default;` makes shapes adapt to any theme.

---

## 29. Property Applicability Summary

### Vertex-Only Properties (ignored on edges)

`fillColor`, `gradientColor`, `gradientDirection`, `fillOpacity`, `shape` (except `connector`),
`perimeter`, `arcSize`, `absoluteArcSize`, `aspect`, `container`, `collapsible`, `foldable`,
`recursiveResize`, `swimlaneFillColor`, `swimlaneLine`, `separatorColor`, `startSize`,
`childLayout`, `glass`, `shadow`, `imageWidth`, `imageHeight`, `imageAlign`, `imageVerticalAlign`,
`imageAspect`, `imageBackground`, `imageBorder`.

### Edge-Only Properties (ignored on vertices)

`edgeStyle`, `startArrow`, `endArrow`, `startFill`, `endFill`, `startSize`, `endSize`,
`curved`, `jettySize`, `sourceJettySize`, `targetJettySize`, `exitX`, `exitY`, `exitDx`,
`exitDy`, `exitPerimeter`, `entryX`, `entryY`, `entryDx`, `entryDy`, `entryPerimeter`,
`orthogonalLoop`, `noEdgeStyle`, `jumpStyle`, `jumpSize`, `perimeterSpacing`,
`sourcePerimeterSpacing`, `targetPerimeterSpacing`.

### Properties That Apply to Both

`strokeColor`, `strokeWidth`, `strokeOpacity`, `dashed`, `dashPattern`, `fixDash`,
`opacity`, `fontSize`, `fontFamily`, `fontColor`, `fontStyle`, `align`, `verticalAlign`,
`labelPosition`, `verticalLabelPosition`, `whiteSpace`, `overflow`, `labelWidth`,
`horizontal`, `textDirection`, `spacing`, `spacingTop`, `spacingBottom`, `spacingLeft`,
`spacingRight`, `labelBackgroundColor`, `labelBorderColor`, `textOpacity`, `noLabel`,
`rounded`, `rotation`, `flipH`, `flipV`, `movable`, `resizable`, `rotatable`,
`editable`, `deletable`, `cloneable`, `connectable`, `pointerEvents`, `html`.
