# Methods Reference: Swimlane Implementation

Complete style strings and attribute reference for all swimlane components.

---

## 1. Pool Styles

### Table-Based Pool (Recommended)

```
shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;
```

Use this style for structured pool layouts where lanes are arranged as table rows. The `childLayout=tableLayout` property ensures consistent lane alignment.

### Simple Pool (Alternative)

```
swimlane;startSize=30;container=1;collapsible=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;
```

Use this for simpler layouts without table row enforcement. Lanes are manually positioned using y-coordinates.

### Pool with Resize Control

```
shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;recursiveResize=0;strokeColor=#6c8ebf;fillColor=#dae8fc;
```

Adding `recursiveResize=0` prevents child lanes from auto-resizing when the pool is resized in the editor.

---

## 2. Lane Styles

### Horizontal Lane (Vertical Stacking, Left-to-Right Flow)

```
swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;
```

The header renders on the LEFT side with rotated text. The lane content area extends to the right. Lanes stack vertically within the pool.

### Vertical Lane (Horizontal Stacking, Top-to-Bottom Flow)

```
swimlane;startSize=30;container=1;collapsible=0;horizontal=0;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;
```

The header renders on the TOP with horizontal text. The lane content area extends downward. Lanes stack side by side within the pool.

### Lane with Custom Header Size

```
swimlane;startSize=50;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;
```

Increase `startSize` for multi-line header labels or larger fonts. ALWAYS ensure child shapes are positioned below the startSize boundary.

### Color-Coded Lanes

| Department | Fill Color | Stroke Color |
|------------|-----------|-------------|
| Sales / Business | `fillColor=#d5e8d4` | `strokeColor=#82b366` |
| Engineering / IT | `fillColor=#dae8fc` | `strokeColor=#6c8ebf` |
| Finance | `fillColor=#fff2cc` | `strokeColor=#d6b656` |
| Operations / Warehouse | `fillColor=#f5f5f5` | `strokeColor=#666666` |
| Management | `fillColor=#e1d5e7` | `strokeColor=#9673a6` |
| Error / Reject | `fillColor=#f8cecc` | `strokeColor=#b85450` |

---

## 3. Container Attributes

### Required Attributes

| Attribute | Value | Purpose |
|-----------|-------|---------|
| `container` | `1` | REQUIRED on every pool and lane — enables parent-child hierarchy |
| `collapsible` | `0` | Prevents accidental collapse in the editor |
| `startSize` | Number (px) | Header band height/width |

### Optional Attributes

| Attribute | Value | Purpose |
|-----------|-------|---------|
| `recursiveResize` | `0` | Prevents child auto-resize on pool resize |
| `resizable` | `1` | Allows manual resizing in editor |
| `childLayout` | `tableLayout` | Enforces table row layout for children |
| `fixedRows` | `1` | Locks row structure |
| `rowLines` | `0` | Hides row separator lines |
| `swimlaneLine` | `0` | Hides the line between header and content |

---

## 4. Geometry Calculations

### Pool Dimensions

```
Pool x, y = absolute page coordinates
Pool width = desired total width (MUST accommodate all lane content)
Pool height = startSize + sum(lane heights)
```

### Lane Dimensions

```
Lane x = 0 (ALWAYS, lanes span full pool width)
Lane y = pool.startSize + sum(previous lane heights)
Lane width = pool width
Lane height = startSize + max(child content height) + padding
```

### Child Dimensions

```
Child x = horizontal offset from lane left edge
Child y = value >= lane.startSize (to avoid header overlap)
```

### Worked Example: 3 Lanes

```
Pool: startSize=30, width=700
  Lane 1: y=30,  height=130  (content area: 100px)
  Lane 2: y=160, height=130  (content area: 100px)
  Lane 3: y=290, height=140  (content area: 110px)
Pool height = 30 + 130 + 130 + 140 = 430
```

---

## 5. Edge Styles for Cross-Lane Connections

### Standard Cross-Lane Edge

```xml
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="pool1" source="task_in_lane1" target="task_in_lane2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

ALWAYS use `parent="pool1"` (the common ancestor) for cross-lane edges.

### Labeled Cross-Lane Edge

```xml
<mxCell id="e1" value="Approved" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="pool1" source="decision1" target="next_step">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Curved Cross-Lane Edge

```
edgeStyle=orthogonalEdgeStyle;curved=1;endArrow=classic;html=1;
```

Use `curved=1` when multiple edges cross lane boundaries to reduce visual clutter.

---

## 6. mxGraphModel Settings for Swimlanes

| Attribute | Recommended Value | Purpose |
|-----------|------------------|---------|
| `grid` | `1` | Enable grid for alignment |
| `gridSize` | `10` | 10px grid spacing |
| `guides` | `1` | Enable alignment guides |
| `connect` | `1` | Enable connection handling |
| `arrows` | `1` | Show connection arrows |
| `pageWidth` | `1169` | A4 landscape width |
| `pageHeight` | `827` | A4 landscape height |

---

## 7. Text Formatting in Lane Headers

### Simple Header

```xml
<mxCell id="lane1" value="Sales" style="swimlane;..." />
```

### HTML Header (Multi-Line)

```xml
<mxCell id="lane1" value="&lt;b&gt;Sales&lt;/b&gt;&lt;br&gt;Department" style="swimlane;startSize=50;..." />
```

Increase `startSize` to accommodate multi-line headers. ALWAYS use `&lt;` and `&gt;` for HTML entities in XML attributes.

### Font Properties in Lane Styles

| Property | Values | Example |
|----------|--------|---------|
| `fontSize` | Number | `fontSize=14;` |
| `fontStyle` | Bitmask: 1=bold, 2=italic, 4=underline | `fontStyle=1;` (bold) |
| `fontColor` | Hex color | `fontColor=#333333;` |
