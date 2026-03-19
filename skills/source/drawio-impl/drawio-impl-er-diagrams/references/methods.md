# Methods Reference: ER Diagram Implementation

Complete style strings and attribute reference for all ER diagram shapes and connections.

---

## 1. Entity Container Styles

### Standard Entity (Table Shape)

```
shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;
```

With colors (primary entity):

```
shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

### Style Property Breakdown

| Property | Value | Purpose |
|----------|-------|---------|
| `shape=table` | Required | Renders as table with header band |
| `startSize=30` | 30px | Height of the header/title band |
| `container=1` | Required | Enables child cell attachment |
| `collapsible=1` | Optional | Allows collapse in editor |
| `childLayout=tableLayout` | Required | Auto-stacks rows vertically |
| `fixedRows=1` | Recommended | Prevents row reordering |
| `rowLines=0` | 0 or 1 | 0 = no separators, 1 = row lines |
| `fontStyle=1` | Bold | Bold entity name in header |
| `align=center` | Center | Centers entity name |
| `resizeLast=1` | Recommended | Last row stretches to fill |

---

## 2. Attribute Row Styles

### Primary Key (PK) Row

```
text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;
```

`fontStyle=4` = underline. This is the universal ER convention for primary keys.

### Foreign Key (FK) Row

```
text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=2;
```

`fontStyle=2` = italic. Distinguishes foreign keys from regular attributes.

### Composite Key (PK + FK) Row

```
text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=6;
```

`fontStyle=6` = underline + italic (4 + 2). Used when a field is both PK and FK.

### Regular Attribute Row

```
text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;
```

No `fontStyle` — renders as plain text.

### Attribute Row Property Breakdown

| Property | Value | Purpose |
|----------|-------|---------|
| `text` | Required | Renders as text-only cell |
| `strokeColor=none` | Required | No border around rows |
| `fillColor=none` | Required | Transparent background |
| `align=left` | Required | Left-aligns attribute text |
| `verticalAlign=middle` | Required | Centers text vertically in row |
| `spacingLeft=4` | 4px | Left padding for readability |
| `spacingRight=4` | 4px | Right padding |
| `overflow=hidden` | Required | Clips text that exceeds width |
| `rotatable=0` | Required | Prevents rotation in editor |
| `whiteSpace=wrap` | Required | Enables text wrapping |
| `html=1` | Required | Enables HTML rendering |

---

## 3. Attribute Row Geometry

Every attribute row MUST follow this geometry pattern:

```xml
<mxGeometry y="OFFSET" width="ENTITY_WIDTH" height="30" as="geometry" />
```

- `x` is OMITTED (defaults to 0, relative to parent).
- `y` = `startSize + (row_index * 30)` where row_index starts at 0.
- `width` MUST match the parent entity width.
- `height` = 30px per row (standard).

Example for an entity with `startSize=30` and 3 attributes:

| Row | y offset | Calculation |
|-----|----------|-------------|
| PK row (index 0) | 30 | 30 + (0 * 30) |
| FK row (index 1) | 60 | 30 + (1 * 30) |
| Regular (index 2) | 90 | 30 + (2 * 30) |

---

## 4. Crow's Foot Arrow Markers

### All ER Arrow Types

| Marker Name | Draw.io Value | Symbol Description |
|-------------|--------------|-------------------|
| One | `ERone` | Single vertical line |
| Many | `ERmany` | Three-pronged fork (crow's foot) |
| Mandatory One | `ERmandOne` | Two vertical lines (must be exactly one) |
| Zero-or-One | `ERzeroToOne` | Circle + single vertical line |
| One-or-Many | `ERoneToMany` | Vertical line + crow's foot |
| Zero-or-Many | `ERzeroToMany` | Circle + crow's foot |

### Edge Style Template

```
edgeStyle=entityRelationEdgeStyle;html=1;startArrow={SOURCE_MARKER};startFill=0;endArrow={TARGET_MARKER};endFill=0;strokeColor=#666666;
```

Replace `{SOURCE_MARKER}` and `{TARGET_MARKER}` with the appropriate `ER*` value.

---

## 5. Relationship Edge Styles

### One-to-One (Mandatory)

```
edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERone;startFill=0;endArrow=ERone;endFill=0;strokeColor=#666666;
```

### One-to-Many

```
edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERone;startFill=0;endArrow=ERmany;endFill=0;strokeColor=#666666;
```

### One-to-Many (Mandatory Both Sides)

```
edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERmandOne;startFill=0;endArrow=ERoneToMany;endFill=0;strokeColor=#666666;
```

### Zero-or-One to Zero-or-Many

```
edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERzeroToOne;startFill=0;endArrow=ERzeroToMany;endFill=0;strokeColor=#666666;
```

### Many-to-Many

```
edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERmany;startFill=0;endArrow=ERmany;endFill=0;strokeColor=#666666;
```

---

## 6. Entity Color Palette

| Role | fillColor | strokeColor |
|------|----------|-------------|
| Primary entity | `#dae8fc` | `#6c8ebf` |
| Secondary entity | `#d5e8d4` | `#82b366` |
| Junction table | `#fff2cc` | `#d6b656` |
| Lookup table | `#e1d5e7` | `#9673a6` |
| Audit/log table | `#f5f5f5` | `#666666` |

---

## 7. fontStyle Values

| Value | Rendering | Use Case |
|-------|-----------|----------|
| `0` | Normal | Regular attributes |
| `1` | Bold | Entity name (header) |
| `2` | Italic | Foreign key fields |
| `4` | Underline | Primary key fields |
| `5` | Bold + Underline | (rarely used) |
| `6` | Italic + Underline | Composite PK+FK fields |
| `7` | Bold + Italic + Underline | (rarely used) |

fontStyle values are additive bitmasks: Bold=1, Italic=2, Underline=4.

---

## 8. Attribute Value Format

ALWAYS use this format for attribute display text:

```
field_name  TYPE
```

Or with key indicators:

```
field_name  PK  TYPE
field_name  FK  TYPE
```

Examples:
- `customer_id  PK  INT`
- `order_id  FK  INT`
- `name  VARCHAR(100)`
- `created_at  TIMESTAMP`
- `total  DECIMAL(10,2)`
