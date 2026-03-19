# Draw.io Core Styles — Property Reference

> Complete reference of all mxGraph style properties organized by category.
> Source: drawio.com/doc/faq/drawio-style-reference, mxConstants.js

---

## 1. Fill Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `fillColor` | `#RRGGBB`, `none`, `default` | `default` | Interior fill color |
| `gradientColor` | `#RRGGBB`, `none` | `none` | Gradient end color (start = `fillColor`) |
| `gradientDirection` | `north`, `south`, `east`, `west` | `south` | Gradient flow direction |
| `opacity` | 0–100 | `100` | Overall opacity (fill + stroke) |
| `fillOpacity` | 0–100 | `100` | Fill-only opacity |

When `fillColor=default`, the shape uses the theme's default fill (typically `#FFFFFF`).
Setting `fillColor=none` makes the shape transparent.

---

## 2. Stroke Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `strokeColor` | `#RRGGBB`, `none`, `default` | `default` | Border/outline color |
| `strokeWidth` | number | `1` | Border thickness in pixels |
| `strokeOpacity` | 0–100 | `100` | Stroke-only opacity |
| `dashed` | `0`, `1` | `0` | Enable dashed stroke |
| `dashPattern` | string | — | Space-separated dash/gap lengths (e.g., `"8 4"`) |
| `fixDash` | `0`, `1` | `0` | When `1`, dash pattern does NOT scale with strokeWidth |

ALWAYS set `dashed=1` alongside `dashPattern`. The `dashPattern` property alone does nothing.

---

## 3. Decorative Effects

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `shadow` | `0`, `1` | `0` | Drop shadow behind shape |
| `glass` | `0`, `1` | `0` | Glossy shine overlay |
| `rounded` | `0`, `1` | `0` | Rounded corners on rectangles |

The `shadow` property on individual cells ONLY works when the `<mxGraphModel>` element
also has `shadow="1"`. If model-level shadow is `0`, per-cell shadows are ignored.

---

## 4. Shape and Geometry Properties

### 4.1 Built-in Primitive Shapes

| Shape Value | Default Perimeter |
|-------------|-------------------|
| `rectangle` | `rectanglePerimeter` |
| `ellipse` | `ellipsePerimeter` |
| `doubleEllipse` | `ellipsePerimeter` |
| `rhombus` | `rhombusPerimeter` |
| `triangle` | `trianglePerimeter` |
| `hexagon` | `hexagonPerimeter` |
| `cylinder` | `rectanglePerimeter` |
| `cloud` | `ellipsePerimeter` |
| `actor` | `rectanglePerimeter` |
| `label` | `rectanglePerimeter` |
| `swimlane` | `rectanglePerimeter` |
| `line` | — |
| `image` | `rectanglePerimeter` |
| `arrow` | `rectanglePerimeter` |
| `arrowConnector` | — |
| `connector` | — |

### 4.2 Extended Shapes (Draw.io Additions)

| Shape Value | Description |
|-------------|-------------|
| `parallelogram` | Parallelogram / input-output |
| `trapezoid` | Trapezoid |
| `step` | Step / chevron |
| `process` | Process rectangle (double vertical borders) |
| `document` | Document with wavy bottom |
| `callout` | Speech bubble |
| `cube` | 3D cube |
| `folder` | Folder with tab |
| `card` | Card with clipped corner |
| `note` | Sticky note |
| `tape` | Tape / ribbon |
| `internalStorage` | Internal storage symbol |
| `or` | OR gate |
| `xor` | XOR gate |
| `dataStorage` | Data storage |
| `manualInput` | Manual input |
| `delay` | Delay shape |
| `display` | Display shape |
| `offPageConnector` | Off-page connector |

### 4.3 Stencil Library Shapes

Stencil shapes use the `shape=mxgraph.*` prefix:

```
shape=mxgraph.flowchart.decision;
shape=mxgraph.aws4.lambda_function;
shape=mxgraph.bpmn.shape;
shape=mxgraph.cisco.router;
shape=mxgraph.uml.component;
```

When using stencil shapes, ALWAYS set the perimeter based on the visual form of the
stencil (round stencils use `ellipsePerimeter`, rectangular stencils use `rectanglePerimeter`).

### 4.4 Geometry Modifiers

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `rounded` | `0`, `1` | `0` | Round rectangle corners |
| `arcSize` | 0–50 | varies | Corner radius as percentage of shorter side |
| `absoluteArcSize` | `0`, `1` | `0` | When `1`, arcSize is in absolute pixels |
| `aspect` | `variable`, `fixed` | `variable` | `fixed` preserves ratio on resize |
| `direction` | `north`, `south`, `east`, `west` | — | Rotates shape in 90-degree increments |
| `flipH` | `0`, `1` | `0` | Mirror horizontally |
| `flipV` | `0`, `1` | `0` | Mirror vertically |
| `rotation` | 0–360 | `0` | Free rotation in degrees |
| `fixedSize` | `0`, `1` | `0` | Shape size independent of label size |

---

## 5. Perimeter Types

| Perimeter Value | Used For |
|-----------------|----------|
| `rectanglePerimeter` | Rectangles, labels, images, cylinders, swimlanes, parallelograms |
| `ellipsePerimeter` | Ellipses, circles, clouds, double ellipses, round stencils |
| `rhombusPerimeter` | Rhombus / diamond shapes |
| `trianglePerimeter` | Triangle shapes |
| `hexagonPerimeter` | Hexagon shapes |

---

## 6. Font and Label Properties

### 6.1 Core Font Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `fontSize` | number | `12` | Font size in pixels |
| `fontFamily` | string | `Helvetica` | Font family name |
| `fontColor` | `#RRGGBB`, `default` | `default` | Text color |
| `fontStyle` | bitmask integer | `0` | Combined font style flags |

### 6.2 fontStyle Bitmask

| Flag | Value |
|------|-------|
| Bold | `1` |
| Italic | `2` |
| Underline | `4` |
| Strikethrough | `8` |

Combine by addition: bold + italic = `3`, bold + underline = `5`.

### 6.3 Text Alignment

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `align` | `left`, `center`, `right` | `center` | Horizontal text alignment within label bounds |
| `verticalAlign` | `top`, `middle`, `bottom` | `middle` | Vertical text alignment within label bounds |

### 6.4 Label Positioning

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelPosition` | `left`, `center`, `right` | `center` | Horizontal position of label relative to shape |
| `verticalLabelPosition` | `top`, `middle`, `bottom` | `middle` | Vertical position of label relative to shape |

When `labelPosition` is NOT `center`, `align` MUST be the opposite value:

| labelPosition | Required align |
|---------------|---------------|
| `left` | `right` |
| `right` | `left` |

When `verticalLabelPosition` is NOT `middle`:

| verticalLabelPosition | Required verticalAlign |
|-----------------------|-----------------------|
| `top` | `bottom` |
| `bottom` | `top` |

### 6.5 Text Wrapping and Overflow

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `whiteSpace` | `wrap`, `nowrap` | — | `wrap` enables word wrapping |
| `overflow` | `visible`, `hidden`, `fill`, `width` | — | Text overflow handling |
| `labelWidth` | number | — | Fixed label width in pixels |
| `horizontal` | `0`, `1` | `1` | `0` renders text vertically (90-degree rotation) |
| `textDirection` | `default`, `ltr`, `rtl` | `default` | Text direction |

Overflow values:
- `visible` — Text extends beyond shape bounds (default for edges)
- `hidden` — Text clipped at shape bounds
- `fill` — Label fills the entire shape
- `width` — Fixed width, variable height

### 6.6 Label Spacing (Padding)

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `spacing` | number | `2` | Padding on all sides in pixels |
| `spacingTop` | number | `0` | Additional top padding |
| `spacingBottom` | number | `0` | Additional bottom padding |
| `spacingLeft` | number | `0` | Additional left padding |
| `spacingRight` | number | `0` | Additional right padding |

Total top padding = `spacing` + `spacingTop`. Individual values are ADDED to the base `spacing`.

### 6.7 Label Background and Border

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `labelBackgroundColor` | `#RRGGBB`, `none`, `default` | — | Background color behind text |
| `labelBorderColor` | `#RRGGBB`, `none` | — | Border around label |
| `textOpacity` | 0–100 | `100` | Text-only opacity |
| `noLabel` | `0`, `1` | `0` | Hide label entirely |

---

## 7. Edge / Connector Properties

### 7.1 Edge Style (Routing Algorithm)

| edgeStyle Value | Description |
|-----------------|-------------|
| `orthogonalEdgeStyle` | Rectilinear routing with right-angle bends (most common) |
| `elbowEdgeStyle` | Single elbow (L-shaped or Z-shaped) |
| `entityRelationEdgeStyle` | ER diagram style with fixed-length stubs |
| `segmentEdgeStyle` | User-defined segments (manual waypoints) |
| `sideToSideEdgeStyle` | Horizontal routing side to side |
| `topToBottomEdgeStyle` | Vertical routing top to bottom |
| `loopEdgeStyle` | Self-referencing loop |
| `isometricEdgeStyle` | Isometric (30-degree angle) routing |

When NO `edgeStyle` is set, the edge uses a direct straight line.

### 7.2 Edge Path Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `curved` | `0`, `1` | `0` | Smooth curved path |
| `rounded` | `0`, `1` | `1` | Round edge corners (for orthogonal edges) |
| `elbow` | `horizontal`, `vertical` | — | Preferred elbow direction |
| `orthogonalLoop` | `0`, `1` | `1` | Routing style for self-referencing loops |
| `noEdgeStyle` | `0`, `1` | `0` | Disable edge style entirely |

### 7.3 Connection Points (Entry/Exit)

Values are relative coordinates: `(0,0)` = top-left, `(1,1)` = bottom-right.

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `exitX` | 0.0–1.0 | — | Relative X of exit point on source |
| `exitY` | 0.0–1.0 | — | Relative Y of exit point on source |
| `exitDx` | number | — | Absolute X offset from exit point |
| `exitDy` | number | — | Absolute Y offset from exit point |
| `exitPerimeter` | `0`, `1` | `1` | Project exit point onto perimeter |
| `entryX` | 0.0–1.0 | — | Relative X of entry point on target |
| `entryY` | 0.0–1.0 | — | Relative Y of entry point on target |
| `entryDx` | number | — | Absolute X offset from entry point |
| `entryDy` | number | — | Absolute Y offset from entry point |
| `entryPerimeter` | `0`, `1` | `1` | Project entry point onto perimeter |

Common connection point grid:

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

### 7.4 Edge Spacing and Jetty

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jettySize` | `auto`, number | `auto` | Min length of first/last segment |
| `sourceJettySize` | number | — | Override jetty at source end |
| `targetJettySize` | number | — | Override jetty at target end |
| `perimeterSpacing` | number | — | Gap between endpoint and perimeter (both ends) |
| `sourcePerimeterSpacing` | number | — | Gap at source end only |
| `targetPerimeterSpacing` | number | — | Gap at target end only |

### 7.5 Line Crossing Visualization

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `jumpStyle` | `arc`, `gap`, `sharp` | — | How crossing lines are visualized |
| `jumpSize` | number | `6` | Size of the jump/gap |

---

## 8. Arrow Types

Set via `startArrow` and `endArrow`. Control fill with `startFill` / `endFill`.

### 8.1 All Arrow Values

| Arrow Value | Description | Typical Use |
|-------------|-------------|-------------|
| `none` | No arrow | Undirected connections |
| `classic` | Traditional triangular arrowhead | Standard directed flow |
| `classicThin` | Slender classic variant | Lighter visual weight |
| `block` | Solid filled triangle | Strong directional indicator |
| `blockThin` | Narrow block variant | UML generalization (with endFill=0) |
| `open` | Open (unfilled) chevron | Lightweight direction |
| `openThin` | Thin open chevron | Subtle direction |
| `oval` | Circular marker | Composition endpoints |
| `diamond` | Diamond marker | UML aggregation / composition |
| `diamondThin` | Narrow diamond | Lighter aggregation |
| `box` | Square marker | Terminal / endpoint |
| `halfCircle` | Semicircle | Interface notation |
| `circle` | Full circle | State machine notation |
| `circlePlus` | Circle with plus | Required interface (UML) |
| `cross` | X-shaped cross | Deletion / cancellation |
| `baseDash` | Horizontal dash at base | Base indicator |
| `doubleBlock` | Double triangular arrowhead | Double direction emphasis |
| `dash` | Short dash line | Simple terminator |
| `async` | Open arrow (async) | UML sequence diagrams |
| `openAsync` | Open async arrow | Asynchronous messaging |
| `manyOptional` | Crow's foot many-optional | ER diagrams |

### 8.2 Arrow Fill and Size

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `startFill` | `0`, `1` | `1` | `1` = filled/solid, `0` = hollow/outline |
| `endFill` | `0`, `1` | `1` | `1` = filled/solid, `0` = hollow/outline |
| `startSize` | number | — | Size of start arrow in pixels |
| `endSize` | number | — | Size of end arrow in pixels |

---

## 9. Container and Swimlane Properties

### 9.1 Container Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `container` | `0`, `1` | `0` | Marks cell as container for children |
| `collapsible` | `0`, `1` | `1` | Shows collapse/expand button |
| `recursiveResize` | `0`, `1` | `1` | Resize children proportionally |
| `foldable` | `0`, `1` | — | Allow fold/collapse |

### 9.2 Swimlane Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `startSize` | number | `23` | Header bar height in pixels |
| `horizontal` | `0`, `1` | `1` | `1` = header on top, `0` = header on left |
| `swimlaneFillColor` | `#RRGGBB` | — | Body fill color (below header) |
| `swimlaneLine` | `0`, `1` | — | Show/hide header-body separator |
| `separatorColor` | `#RRGGBB` | — | Separator line color |

### 9.3 Child Layout Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `childLayout` | `stackLayout`, `treeLayout`, `flowLayout` | — | Auto-layout for children |
| `resizeParent` | `0`, `1` | — | Parent resizes to fit children |
| `resizeParentMax` | `0`, `1` | — | Limit parent auto-resize |
| `resizeLast` | `0`, `1` | — | Last child fills remaining space |
| `horizontalStack` | `0`, `1` | — | `1` = horizontal stack, `0` = vertical |
| `marginBottom` | number | — | Bottom margin for stack layout |

---

## 10. Image Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `image` | URL string | — | Image URL (HTTP, data: URI, built-in) |
| `imageWidth` | number | `42` | Display width |
| `imageHeight` | number | `42` | Display height |
| `imageAlign` | `left`, `center`, `right` | — | Horizontal image alignment |
| `imageVerticalAlign` | `top`, `middle`, `bottom` | — | Vertical image alignment |
| `imageAspect` | `0`, `1` | `1` | Preserve aspect ratio |
| `imageBackground` | `#RRGGBB` | — | Background behind image |
| `imageBorder` | `#RRGGBB` | — | Border around image |

---

## 11. Sketch / Hand-Drawn Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `sketch` | `0`, `1` | `0` | Enable hand-drawn style |
| `comic` | `0`, `1` | `0` | Comic book variant |
| `fillStyle` | `solid`, `hachure`, `cross-hatch`, `dots` | — | Fill pattern in sketch mode |
| `fillWeight` | number | — | Weight of hatch lines |
| `hachureGap` | number | — | Gap between hatch lines |
| `hachureAngle` | number (degrees) | — | Angle of hatch lines |
| `jiggle` | number | — | Randomness / wobble amount |
| `curveFitting` | 0–1 | — | Curve approximation quality |
| `simplification` | 0–1 | — | Path simplification level |
| `disableMultiStroke` | `0`, `1` | — | Disable double-stroke effect |
| `disableMultiStrokeFill` | `0`, `1` | — | Disable double-stroke on fill |

---

## 12. Behavior / Lock Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `movable` | `0`, `1` | `1` | Allow drag/move |
| `resizable` | `0`, `1` | `1` | Allow resize |
| `rotatable` | `0`, `1` | `1` | Allow rotation |
| `bendable` | `0`, `1` | `1` | Allow adding/moving bend points |
| `editable` | `0`, `1` | `1` | Allow label editing |
| `deletable` | `0`, `1` | `1` | Allow deletion |
| `cloneable` | `0`, `1` | `1` | Allow Ctrl+drag cloning |
| `connectable` | `0`, `1` | `1` | Allow creating connections from cell |
| `pointerEvents` | `0`, `1` | `1` | Enable mouse events |
| `autosize` | `0`, `1` | `0` | Auto-resize to fit label |

Locked read-only shape: `movable=0;resizable=0;editable=0;deletable=0;`

---

## 13. Indicator Properties

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `indicatorShape` | shape name | — | Shape type for indicator |
| `indicatorImage` | URL | — | Image for indicator |
| `indicatorColor` | `#RRGGBB` | — | Indicator fill color |
| `indicatorStrokeColor` | `#RRGGBB` | — | Indicator border color |
| `indicatorGradientColor` | `#RRGGBB` | — | Indicator gradient end color |
| `indicatorSpacing` | number | — | Gap between label and indicator |
| `indicatorWidth` | number | — | Indicator width |
| `indicatorHeight` | number | — | Indicator height |
| `indicatorDirection` | direction | — | Indicator placement |

---

## 14. Port Constraints

| Property | Values | Description |
|----------|--------|-------------|
| `portConstraint` | `eastwest`, `northsouth`, `perimeter`, `fixed` | Connection direction constraint |
| `sourcePortConstraint` | direction | Source side constraint |
| `targetPortConstraint` | direction | Target side constraint |
