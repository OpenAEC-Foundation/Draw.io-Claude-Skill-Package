# Methods Reference: Draw.io Mind Maps

Complete property reference for mind map shapes, connectors, and layout in mxGraph XML.

---

## 1. Central Topic Shape Properties

Properties for the root node of a mind map (Level 0).

| Property | Values | Default | Description |
|----------|--------|---------|-------------|
| `ellipse` | *(shape keyword)* | — | Ellipse shape for organic central topic. |
| `rounded` | `0`, `1` | `0` | Set to `1` with `arcSize=40` for rounded rectangle alternative. |
| `fillColor` | Hex color | — | ALWAYS use a dark saturated color (e.g., `#1168bd`). |
| `fontColor` | Hex color | `#000000` | ALWAYS use `#ffffff` on dark backgrounds. |
| `strokeColor` | Hex color | — | Slightly darker than fillColor (e.g., `#0b4884`). |
| `fontSize` | Number | `12` | ALWAYS use 14–18 for central topic. |
| `fontStyle` | `0`, `1`, `2`, `3` | `0` | ALWAYS use `1` (bold) for central topic. |
| `whiteSpace` | `wrap` | — | ALWAYS include. Enables text wrapping. |
| `html` | `1` | — | ALWAYS include. Enables HTML label rendering. |

### Recommended Central Topic Dimensions

| Diagram Size | Width | Height |
|-------------|-------|--------|
| Small (3–4 branches) | 140–160 px | 70–80 px |
| Medium (5–6 branches) | 160–180 px | 80–90 px |
| Large (7+ branches) | 180–200 px | 90–100 px |

---

## 2. Branch Shape Properties

Properties for Level 1 (main branches) and Level 2+ (sub-branches).

| Property | Level 1 Value | Level 2+ Value | Description |
|----------|--------------|----------------|-------------|
| `rounded` | `1` | `1` | ALWAYS rounded rectangles for branches. |
| `fillColor` | Branch family color | `#f5f5f5` or lighter tint | Color coding per branch. |
| `strokeColor` | Matching dark accent | `#666666` or `#999999` | Border color. |
| `fontSize` | 12–14 | 10–12 | Progressively smaller. |
| `fontStyle` | `1` (bold) | `0` (normal) | Bold for main branches only. |
| `whiteSpace` | `wrap` | `wrap` | ALWAYS include. |
| `html` | `1` | `1` | ALWAYS include. |

### Recommended Branch Dimensions

| Level | Width | Height |
|-------|-------|--------|
| Level 1 (Main Branch) | 110–140 px | 35–50 px |
| Level 2 (Sub-Branch) | 80–110 px | 28–35 px |
| Level 3+ (Leaf Node) | 70–100 px | 25–30 px |

---

## 3. Connector (Edge) Properties

Properties for curved mind map branch connectors.

### 3.1 Required Edge Attributes

| Attribute | Value | Description |
|-----------|-------|-------------|
| `edge` | `"1"` | ALWAYS set. Marks cell as an edge. |
| `source` | Cell ID | ALWAYS set. ID of the parent node. |
| `target` | Cell ID | ALWAYS set. ID of the child node. |
| `parent` | `"1"` | ALWAYS set. Default layer. |

### 3.2 Edge Style Properties

| Property | Value | NEVER Use | Description |
|----------|-------|-----------|-------------|
| `endArrow` | `none` | `classic`, `block`, `open`, `diamond` | Mind maps have NO directional arrows. |
| `curved` | `1` | `0` | ALWAYS curved for organic look. |
| `html` | `1` | — | ALWAYS include. |
| `strokeWidth` | `1`–`3` | `0` | Thicker for higher-level connections. |
| `strokeColor` | Hex color | — | Match branch family color or use gray. |

### 3.3 Connector Stroke Width by Level

| Connection Level | strokeWidth | strokeColor Strategy |
|-----------------|-------------|---------------------|
| Center to Level 1 | 2–3 | Match the target branch's `strokeColor` |
| Level 1 to Level 2 | 1–2 | `#999999` or lighter branch color |
| Level 2 to Level 3+ | 1 | `#BBBBBB` or `#CCCCCC` |

### 3.4 Edge Geometry

ALWAYS include this exact geometry element inside every edge cell:

```xml
<mxGeometry relative="1" as="geometry" />
```

NEVER omit `relative="1"`. NEVER add `x`, `y`, `width`, or `height` to edge geometry.

---

## 4. Color Family Reference

### 4.1 Standard Branch Colors (Draw.io Default Palette)

| Family | fillColor (Level 1) | strokeColor (Level 1) | Connector strokeColor |
|--------|--------------------|-----------------------|----------------------|
| Blue | `#dae8fc` | `#6c8ebf` | `#6c8ebf` |
| Green | `#d5e8d4` | `#82b366` | `#82b366` |
| Yellow | `#fff2cc` | `#d6b656` | `#d6b656` |
| Purple | `#e1d5e7` | `#9673a6` | `#9673a6` |
| Red/Orange | `#f8cecc` | `#b85450` | `#b85450` |
| Teal | `#d4e1f5` | `#4a86c8` | `#4a86c8` |
| Gray | `#f5f5f5` | `#666666` | `#999999` |

### 4.2 Central Topic Colors

| Style | fillColor | strokeColor | fontColor |
|-------|-----------|-------------|-----------|
| Dark Blue (recommended) | `#1168bd` | `#0b4884` | `#ffffff` |
| Dark Green | `#2d7600` | `#1a4500` | `#ffffff` |
| Dark Purple | `#6c3082` | `#4a1d5e` | `#ffffff` |
| Dark Red | `#a61c00` | `#6e1200` | `#ffffff` |

---

## 5. Layout Properties

### 5.1 Radial Positioning

ALWAYS position the central topic near the geometric center of the canvas. Recommended canvas center coordinates:

| Canvas Size | Center X | Center Y |
|-------------|----------|----------|
| Small (800x600) | 300–350 | 230–270 |
| Medium (1200x800) | 500–550 | 330–370 |
| Large (1600x1000) | 700–750 | 430–470 |

### 5.2 Branch Spacing

| Relationship | Minimum Distance |
|-------------|-----------------|
| Central topic to Level 1 branch | 120–180 px (center-to-center) |
| Level 1 to Level 2 branch | 80–120 px (center-to-center) |
| Sibling branches (same level) | 20+ px vertical gap |
| Adjacent branch families | 40+ px gap to prevent overlap |

### 5.3 mxCompactTreeLayout Properties (Programmatic Layout)

| Property | Mind Map Value | Description |
|----------|---------------|-------------|
| `horizontal` | `false` | Radial spread |
| `levelDistance` | `60` | Pixels between hierarchy levels |
| `nodeDistance` | `20` | Pixels between sibling nodes |
| `resizeParent` | `true` | Auto-resize container to fit children |
| `edgeRouting` | `curved` | ALWAYS curved for mind maps |

---

## 6. Concept Map Differences

Properties that differ when creating concept maps instead of mind maps.

| Property | Mind Map | Concept Map |
|----------|----------|-------------|
| `endArrow` | `none` | `classic` |
| `value` (on edge) | *(empty)* | Relationship label (e.g., `"causes"`, `"requires"`) |
| `fontSize` (on edge) | — | `9`–`11` |
| `fontColor` (on edge) | — | `#666666` or `#999999` |
| Cross-links allowed | No | Yes — edges between any two nodes |
| Structure | Strict tree | Arbitrary graph |
