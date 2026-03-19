# Examples Reference: Draw.io Code Validator

Concrete validation examples showing pipeline input, detected errors, and corrected output.

---

## Example 1: Clean Pass — All 8 Stages Pass

### Input XML

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="40" as="geometry" />
        </mxCell>
        <mxCell id="3" value="Process" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="200" width="120" height="60" as="geometry" />
        </mxCell>
        <mxCell id="4" style="endArrow=classic;html=1;" edge="1" source="2" target="3" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Validation Report

```
VALIDATION RESULT: PASS

BLOCKING ERRORS (must fix): None
WARNINGS (should fix): None

SUMMARY: 0 blocking errors, 0 warnings
```

---

## Example 2: Stage 1 Failure — Malformed XML

### Input XML

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="R&D Department" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
        </mxCell>
        <mxCell id="3" value="<b>Important</b>" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="200" width="140" height="60" as="geometry">
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Detected Errors

```
VALIDATION RESULT: FAIL

BLOCKING ERRORS (must fix):
  [S1-E1] Stage 1 — XML Well-Formedness
    Severity: BLOCKING
    Location: <mxCell id="2" value="R&D Department" ...>
    Error: Unescaped ampersand in value attribute — "R&D" contains raw "&"
    Fix: Change value="R&D Department" to value="R&amp;D Department"

  [S1-E2] Stage 1 — XML Well-Formedness
    Severity: BLOCKING
    Location: <mxCell id="3" value="<b>Important</b>" ...>
    Error: Unescaped angle brackets in value attribute
    Fix: Change value="<b>Important</b>" to value="&lt;b&gt;Important&lt;/b&gt;"

  [S1-E3] Stage 1 — XML Well-Formedness
    Severity: BLOCKING
    Location: <mxGeometry ... as="geometry"> (inside cell id="3")
    Error: Unclosed <mxGeometry> tag — missing self-close or close tag
    Fix: Change <mxGeometry x="100" y="200" width="140" height="60" as="geometry">
         to <mxGeometry x="100" y="200" width="140" height="60" as="geometry" />

SUMMARY: 3 blocking errors, 0 warnings
```

### Corrected XML

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="R&amp;D Department" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
        </mxCell>
        <mxCell id="3" value="&lt;b&gt;Important&lt;/b&gt;" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="200" width="140" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## Example 3: Stage 2 and 3 Failures — Missing Structure + Duplicate IDs

### Input XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="1" value="Box A" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="1" value="Box B" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Detected Errors

```
VALIDATION RESULT: FAIL

BLOCKING ERRORS (must fix):
  [S2-E1] Stage 2 — Structure Check
    Severity: BLOCKING
    Location: <root> element
    Error: Missing root cell <mxCell id="0"/>
    Fix: Insert <mxCell id="0"/> as the first child of <root>

  [S2-E2] Stage 2 — Structure Check
    Severity: BLOCKING
    Location: <mxCell id="1" value="Box A" ...>
    Error: Cell id="1" has vertex="1" and style attributes — the default layer cell MUST be pure
    Fix: Create a clean <mxCell id="1" parent="0"/> and reassign content to new IDs

  [S3-E1] Stage 3 — ID Uniqueness
    Severity: BLOCKING
    Location: Two cells with id="1" (value="Box A" and value="Box B")
    Error: Duplicate ID "1" used by 2 cells
    Fix: Reassign second occurrence to id="3", update parent references

SUMMARY: 3 blocking errors, 0 warnings
AUTO-FIXED: Inserted id="0", cleaned id="1" as default layer, reassigned "Box A" to id="2", "Box B" to id="3"
```

### Corrected XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Box A" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Box B" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## Example 4: Stage 4 Failure — Broken Parent References

### Input XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Item" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="99">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Other" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="3">
      <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Detected Errors

```
VALIDATION RESULT: FAIL

BLOCKING ERRORS (must fix):
  [S4-E1] Stage 4 — Parent-Child Integrity
    Severity: BLOCKING
    Location: <mxCell id="2" parent="99" ...>
    Error: Parent "99" does not exist in the document
    Fix: Change parent="99" to parent="1" (default layer)

  [S4-E2] Stage 4 — Parent-Child Integrity
    Severity: BLOCKING
    Location: <mxCell id="3" parent="3" ...>
    Error: Cell is its own parent (circular reference)
    Fix: Change parent="3" to parent="1" (default layer)

SUMMARY: 2 blocking errors, 0 warnings
```

---

## Example 5: Warning Stages — Style, Geometry, Connection, and Perimeter Issues

### Input XML

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Decision" style="rhombus;rounded=true;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="80" as="geometry" />
        </mxCell>
        <mxCell id="3" value="Result" style="ellipse;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="300" width="120" height="80" as="geometry" />
        </mxCell>
        <mxCell id="4" style="endArrow=fancy;fillColor=#FF0000;" edge="1"
                source="2" target="88" parent="1">
          <mxGeometry as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Detected Errors

```
VALIDATION RESULT: PASS (with warnings)

BLOCKING ERRORS (must fix): None

WARNINGS (should fix):
  [S5-W1] Stage 5 — Style Validation
    Severity: WARNING
    Location: <mxCell id="2" style="rhombus;rounded=true;" ...>
    Error: Boolean value "true" used instead of "1" for property "rounded"
    Fix: Change rounded=true to rounded=1

  [S5-W2] Stage 5 — Style Validation
    Severity: WARNING
    Location: <mxCell id="2" style="rhombus;rounded=true;" ...>
    Error: Missing html=1 in style
    Fix: Add html=1; to style string

  [S5-W3] Stage 5 — Style Validation
    Severity: WARNING
    Location: <mxCell id="2" style="rhombus;rounded=true;" ...>
    Error: Missing whiteSpace=wrap in style (cell has a label)
    Fix: Add whiteSpace=wrap; to style string

  [S5-W4] Stage 5 — Style Validation
    Severity: WARNING
    Location: <mxCell id="4" style="endArrow=fancy;fillColor=#FF0000;" ...>
    Error: fillColor is a vertex-only property applied to an edge
    Fix: Remove fillColor=#FF0000 from edge style

  [S6-W1] Stage 6 — Geometry Check
    Severity: WARNING
    Location: <mxCell id="4" ...> (edge)
    Error: Edge geometry missing relative="1"
    Fix: Change <mxGeometry as="geometry" /> to <mxGeometry relative="1" as="geometry" />

  [S7-W1] Stage 7 — Connection Validation
    Severity: WARNING
    Location: <mxCell id="4" target="88" ...>
    Error: Target cell "88" does not exist
    Fix: Change target to reference an existing vertex, or remove the target attribute

  [S7-W2] Stage 7 — Connection Validation
    Severity: WARNING
    Location: <mxCell id="4" style="endArrow=fancy;" ...>
    Error: "fancy" is not a valid arrow name
    Fix: Change endArrow=fancy to endArrow=classic (or another valid name)

  [S8-W1] Stage 8 — Perimeter Check
    Severity: WARNING
    Location: <mxCell id="2" style="rhombus;..." ...>
    Error: Rhombus shape missing rhombusPerimeter
    Fix: Add perimeter=rhombusPerimeter; to style

  [S8-W2] Stage 8 — Perimeter Check
    Severity: WARNING
    Location: <mxCell id="3" style="ellipse;..." ...>
    Error: Ellipse shape missing ellipsePerimeter
    Fix: Add perimeter=ellipsePerimeter; to style

SUMMARY: 0 blocking errors, 9 warnings
```

---

## Example 6: Multi-Page Validation with Cross-Page Duplicate

### Input XML

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Server" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Detail">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="80" height="100" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Detected Errors

```
VALIDATION RESULT: FAIL

BLOCKING ERRORS (must fix):
  [S3-E1] Stage 3 — ID Uniqueness
    Severity: BLOCKING
    Location: Page "Overview" cell id="2" (value="Server") and Page "Detail" cell id="2" (value="Database")
    Error: Duplicate ID "2" across pages
    Fix: Reassign the second occurrence (page "Detail") to id="3"

SUMMARY: 1 blocking error, 0 warnings
NOTE: IDs "0" and "1" are structural and appear once per page — this is the expected pattern.
      Content IDs (2+) MUST be unique across ALL pages.
```

---

## Example 7: Container with Absolute Child Coordinates (Stage 6)

### Input XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Group" style="rounded=1;whiteSpace=wrap;html=1;container=1;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="200" width="300" height="200" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Child" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="2">
      <mxGeometry x="500" y="500" width="100" height="40" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Detected Errors

```
VALIDATION RESULT: PASS (with warnings)

BLOCKING ERRORS (must fix): None

WARNINGS (should fix):
  [S6-W1] Stage 6 — Geometry Check
    Severity: WARNING
    Location: <mxCell id="3" parent="2" ...>
    Error: Child coordinates (500, 500) exceed parent dimensions (300x200) —
           likely using absolute canvas coordinates instead of parent-relative coordinates
    Fix: Change to relative coordinates, e.g., x="20" y="30" (offset from parent's top-left)

SUMMARY: 0 blocking errors, 1 warning
```
