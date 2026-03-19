# Anti-Patterns: ER Diagram Implementation

What NOT to do when generating ER diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Using Generic Arrows Instead of ER Markers

### WRONG

```xml
<mxCell id="rel1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="ent_customer" target="ent_order">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="rel1" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;strokeColor=#666666;"
        edge="1" parent="1" source="ent_customer" target="ent_order">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`endArrow=classic` produces a generic arrowhead that conveys no cardinality information. ER diagrams MUST use crow's foot notation (`ERone`, `ERmany`, `ERzeroToOne`, `ERzeroToMany`, `ERmandOne`, `ERoneToMany`) to communicate relationship cardinality. Without ER markers, the diagram is semantically meaningless as a data model.

---

## AP-02: Using startFill=1 or endFill=1 with ER Arrows

### WRONG

```xml
<mxCell id="rel1" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=1;startArrow=ERone;startFill=1;"
        edge="1" parent="1" source="ent_a" target="ent_b">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="rel1" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;"
        edge="1" parent="1" source="ent_a" target="ent_b">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Setting `Fill=1` on ER markers produces filled (solid) versions of the crow's foot symbols. Standard crow's foot notation uses unfilled (outline) markers. Filled markers are visually ambiguous and do not conform to any recognized ER notation standard. ALWAYS use `startFill=0` and `endFill=0`.

---

## AP-03: Placing Attribute Rows Outside the Entity Container

### WRONG

```xml
<!-- Entity container -->
<mxCell id="ent1" value="Customer" style="shape=table;startSize=30;container=1;childLayout=tableLayout;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
</mxCell>

<!-- Attribute placed as sibling instead of child -->
<mxCell id="ent1_pk" value="customer_id  PK  INT" style="text;align=left;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="110" width="200" height="30" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="ent1" value="Customer" style="shape=table;startSize=30;container=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
</mxCell>

<!-- Attribute as child of entity -->
<mxCell id="ent1_pk" value="customer_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;"
        vertex="1" parent="ent1">
  <mxGeometry y="30" width="200" height="30" as="geometry" />
</mxCell>
```

### Why It Fails

When `parent="1"` is used instead of `parent="ent1"`, the attribute row is placed on the root canvas — not inside the entity. This means:
- The attribute will NOT move when the entity is dragged.
- The attribute will NOT be hidden when the entity is collapsed.
- The `childLayout=tableLayout` auto-stacking will NOT apply.
- The attribute will overlap other diagram elements.

ALWAYS set `parent` to the entity container's ID for every attribute row.

---

## AP-04: Using orthogonalEdgeStyle Instead of entityRelationEdgeStyle

### WRONG

```xml
<mxCell id="rel1" style="edgeStyle=orthogonalEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;"
        edge="1" parent="1" source="ent_a" target="ent_b">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="rel1" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;"
        edge="1" parent="1" source="ent_a" target="ent_b">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

`orthogonalEdgeStyle` produces right-angle connectors designed for flowcharts and block diagrams. In ER diagrams, `entityRelationEdgeStyle` provides the classic curved ER connector that:
- Routes cleanly between table shapes.
- Avoids overlapping with entity borders.
- Produces the expected visual appearance for database professionals.

While `orthogonalEdgeStyle` technically works, it produces a non-standard ER diagram appearance.

---

## AP-05: Missing container=1 on Entity Shape

### WRONG

```xml
<mxCell id="ent1" value="Customer" style="shape=table;startSize=30;childLayout=tableLayout;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="ent1" value="Customer" style="shape=table;startSize=30;container=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
</mxCell>
```

### Why It Fails

Without `container=1`, the entity shape does not accept child cells. Attribute rows with `parent="ent1"` will render incorrectly or not at all. The `childLayout=tableLayout` property has no effect without `container=1`. ALWAYS include `container=1` in entity styles.

---

## AP-06: Incorrect Entity Height Calculation

### WRONG

```xml
<!-- Entity with 4 attributes but height only 90 (should be 150) -->
<mxCell id="ent1" value="Order" style="shape=table;startSize=30;container=1;childLayout=tableLayout;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="90" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Height = startSize(30) + attributes(4) * rowHeight(30) = 150 -->
<mxCell id="ent1" value="Order" style="shape=table;startSize=30;container=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="150" as="geometry" />
</mxCell>
```

### Why It Fails

When entity height is too small, attribute rows overflow the container boundary. They render outside the visible table area, overlapping other elements. The formula is: `height = startSize + (attribute_count * row_height)`. With `startSize=30` and `row_height=30`, a 4-attribute entity MUST be 150px tall.

---

## AP-07: Mismatched Attribute Row Width

### WRONG

```xml
<mxCell id="ent1" value="Customer" style="shape=table;startSize=30;container=1;childLayout=tableLayout;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
</mxCell>
<!-- Row width (150) does not match entity width (200) -->
<mxCell id="ent1_pk" value="customer_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;"
        vertex="1" parent="ent1">
  <mxGeometry y="30" width="150" height="30" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="ent1" value="Customer" style="shape=table;startSize=30;container=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;"
        vertex="1" parent="1">
  <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
</mxCell>
<!-- Row width matches entity width -->
<mxCell id="ent1_pk" value="customer_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;"
        vertex="1" parent="ent1">
  <mxGeometry y="30" width="200" height="30" as="geometry" />
</mxCell>
```

### Why It Fails

When attribute row width does not match the entity container width, the row either falls short (leaving a visual gap on the right) or extends beyond the container boundary. ALWAYS ensure every attribute row `width` equals the parent entity `width`.

---

## AP-08: Missing PK/FK Visual Indicators

### WRONG

```xml
<!-- PK field with no fontStyle — indistinguishable from regular fields -->
<mxCell id="pk" value="customer_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;"
        vertex="1" parent="ent1">
  <mxGeometry y="30" width="200" height="30" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- PK field with fontStyle=4 (underline) -->
<mxCell id="pk" value="customer_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;"
        vertex="1" parent="ent1">
  <mxGeometry y="30" width="200" height="30" as="geometry" />
</mxCell>
```

### Why It Fails

Without `fontStyle=4` (underline) on PK fields and `fontStyle=2` (italic) on FK fields, all attributes look identical. Readers cannot distinguish keys from regular attributes. The text labels "PK" and "FK" in the value help, but the visual formatting (underline/italic) is the standard ER convention that database professionals expect.
