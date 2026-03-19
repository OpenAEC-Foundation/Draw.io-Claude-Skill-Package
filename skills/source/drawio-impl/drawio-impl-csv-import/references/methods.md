# Methods Reference: CSV Import Implementation

Complete directive syntax and property reference for Draw.io CSV import.

---

## 1. Directive Syntax

ALL directives follow the pattern: `# directiveName: value`

### Comment Lines

```
## This is a comment — ignored by the parser
```

Lines starting with `##` are ALWAYS ignored. Use them to document the CSV import.

### Line Continuation

```
# connect: {"from": "manager", "to": "name", \
#   "invert": true, "style": "curved=1;"}
```

A backslash `\` at the end of a line continues the directive on the next line. The continuation line MUST start with `#`.

---

## 2. Label Directive

```
# label: %column1%
```

Template for shape labels. Supports HTML when shapes use `html=1;` in their style.

HTML formatting options in labels:

| HTML | Effect |
|------|--------|
| `<br>` | Line break |
| `<b>text</b>` | Bold |
| `<i>text</i>` | Italic |
| `<font color="#FF0000">text</font>` | Colored text |
| `<a href="mailto:%email%">Email</a>` | Hyperlink |
| `<small>text</small>` | Smaller text |
| `<sub>text</sub>` | Subscript |
| `<sup>text</sup>` | Superscript |

Multi-line label example:

```
# label: <b>%name%</b><br><i style="color:gray;">%role%</i><br><a href="mailto:%email%">%email%</a>
```

---

## 3. Style Directive

### Static Style (All Shapes Identical)

```
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

### Dynamic Style (Column-Driven Colors)

```
# style: rounded=1;whiteSpace=wrap;html=1;fillColor=%fill%;strokeColor=%stroke%;
```

Column references in styles are replaced per row. The column MUST contain valid mxGraph values (e.g., hex color codes).

### Image Style

```
# style: label;image=%image%;whiteSpace=wrap;html=1;rounded=1;
```

The `label` style type combined with `image=` displays an image with a text label below.

---

## 4. Conditional Style Directives

### stylename

```
# stylename: columnName
```

Names the column whose values select which style to apply. Each distinct value in this column maps to a style defined in `# styles:`.

### styles

```
# styles: {"value1": "style1;property=x;", "value2": "style2;property=y;"}
```

JSON object where:
- Keys = possible values in the `stylename` column
- Values = complete mxGraph style strings

EVERY distinct value in the `stylename` column MUST have a matching key. Missing keys produce shapes with no style.

### Combined Example

```
# stylename: priority
# styles: {"high": "rounded=1;fillColor=#f8cecc;strokeColor=#b85450;whiteSpace=wrap;html=1;", \
#   "medium": "rounded=1;fillColor=#fff2cc;strokeColor=#d6b656;whiteSpace=wrap;html=1;", \
#   "low": "rounded=1;fillColor=#d5e8d4;strokeColor=#82b366;whiteSpace=wrap;html=1;"}
```

---

## 5. Connect Directive

### Minimal Connection

```
# connect: {"from": "parent", "to": "id"}
```

### Full Connection

```
# connect: {"from": "manager", "to": "name", "invert": true, "label": "manages", "style": "curved=1;endArrow=blockThin;endFill=1;fontSize=11;"}
```

### Property Reference

| Property | Type | Required | Default | Description |
|----------|------|----------|---------|-------------|
| `from` | string | YES | — | Column in the current row containing the reference value |
| `to` | string | YES | — | Column in the target row to match against |
| `invert` | boolean | NO | `false` | Reverses arrow direction |
| `label` | string | NO | none | Edge label text |
| `style` | string | NO | default edge | mxGraph style for the edge |

### Connection Matching Logic

1. For each data row, read the value from the `from` column.
2. Find the row where the `to` column (or identity column) matches that value.
3. Create an edge from the current row's shape to the matched shape.
4. If `invert` is `true`, the edge direction is reversed.
5. Empty values in the `from` column produce no connection (root nodes).

### Multiple Connections

Each `# connect:` line creates one type of connection. Use multiple lines for different relationship types:

```
# connect: {"from": "manager", "to": "name", "invert": true, "label": "reports to"}
# connect: {"from": "mentor", "to": "name", "style": "dashed=1;endArrow=open;"}
```

### Common Edge Styles

| Style String | Effect |
|-------------|--------|
| `endArrow=classic;html=1;` | Standard arrow |
| `endArrow=blockThin;endFill=1;` | Thin filled arrow |
| `endArrow=open;` | Open arrowhead |
| `endArrow=none;` | No arrowhead (undirected) |
| `dashed=1;` | Dashed line |
| `curved=1;` | Curved routing |
| `strokeWidth=2;` | Thicker line |
| `strokeColor=#FF0000;` | Colored line |

---

## 6. Identity Directive

```
# identity: columnName
```

- Designates the column used for connection target matching.
- If omitted, the FIRST column is used as identity.
- Values in the identity column MUST be unique across all rows.

---

## 7. Namespace Directive

```
# namespace: prefix-
```

- Prepends `prefix-` to all generated cell IDs.
- ALWAYS use when importing multiple CSVs into the same diagram.
- ALWAYS use a trailing hyphen or underscore for readability.

---

## 8. Layout Directive

```
# layout: algorithmName
```

### Available Algorithms

| Algorithm | Description | Best For |
|-----------|-------------|----------|
| `auto` | Draw.io selects the best layout | General purpose |
| `verticalTree` | Top-to-bottom tree | Org charts, hierarchies |
| `horizontalTree` | Left-to-right tree | Process flows, timelines |
| `organic` | Force-directed layout | Network diagrams, unstructured |
| `circle` | Circular arrangement | Peer groups, ring topologies |

---

## 9. Dimension Directives

```
# width: auto
# width: 120
# height: auto
# height: 60
```

- `auto` — shape sizes to fit label content.
- Numeric — fixed pixel dimension for ALL shapes.
- ALWAYS use `auto` when labels vary significantly in length.

---

## 10. Spacing Directives

```
# padding: -12
# nodespacing: 40
# levelspacing: 100
# edgespacing: 40
```

| Directive | Unit | Description |
|-----------|------|-------------|
| `padding` | pixels | Label padding inside shapes (negative reduces it) |
| `nodespacing` | pixels | Horizontal gap between sibling nodes |
| `levelspacing` | pixels | Vertical gap between hierarchy levels |
| `edgespacing` | pixels | Gap between parallel edges |

---

## 11. Ignore Directive

```
# ignore: col1,col2,col3
```

- Comma-separated list of column names.
- Ignored columns do NOT appear in shape metadata/tooltips.
- ALWAYS ignore: ID columns, color columns, connection reference columns, image URL columns.

---

## 12. Link Directive

```
# link: urlColumn
```

- The named column's values become clickable hyperlinks on shapes.
- Values MUST be valid URLs (e.g., `https://example.com`).

---

## 13. Parent Style Directive

```
# parentstyle: swimlane;whiteSpace=wrap;html=1;childLayout=stackLayout;horizontal=1;horizontalStack=0;resizeParent=1;resizeLast=0;collapsible=1;
```

- Defines the style for auto-created container/parent shapes.
- Used when the layout algorithm groups nodes into containers.
- The `swimlane` style is the most common parent style.

---

## 14. CSV Data Format Rules

1. The header row MUST be the first line after all directive lines.
2. Column names are case-sensitive and MUST exactly match `%placeholder%` references.
3. Empty cells are valid — they produce no connection when used in `from` columns.
4. Values containing commas MUST be quoted: `"value, with comma"`.
5. Every data row MUST have the same number of fields as the header.
6. Each data row produces exactly one shape in the diagram.
