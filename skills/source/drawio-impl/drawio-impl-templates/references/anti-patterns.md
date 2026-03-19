# Anti-Patterns: Template Implementation

What NOT to do when creating or using Draw.io templates, with explanations of why each pattern fails.

---

## AP-01: Missing mxfile Wrapper for Reusable Templates

### WRONG

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="step1" value="[Step 1]" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### RIGHT

```xml
<mxfile host="app.diagrams.net" type="device">
  <diagram id="template-1" name="Process Template">
    <mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="1169" pageHeight="827">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="step1" value="[Step 1]" style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Why It Fails

A bare `<mxGraphModel>` loses the diagram name, page tab information, and file metadata. When saved as a `.drawio` file, Draw.io expects the `<mxfile>` wrapper. Without it, the file opens but the diagram tab shows "Untitled" and multi-page support is broken. ALWAYS use `<mxfile>` for reusable templates.

---

## AP-02: Numeric-Only Cell IDs in Templates

### WRONG

```xml
<mxCell id="2" value="[Step 1]" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="3" value="[Step 2]" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="step_1" value="[Step 1]" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="step_2" value="[Step 2]" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Numeric IDs give no indication of what each shape represents. When modifying a template (adding shapes, removing shapes, updating edges), semantic IDs make it immediately clear which cell is being referenced. Numeric IDs also collide easily when merging templates or adding shapes. ALWAYS use descriptive IDs like `step_1`, `decision_auth`, `server_web`.

---

## AP-03: Hard-Coded Content in Templates

### WRONG

```xml
<mxCell id="title" value="Q3 2024 Sales Pipeline Review"
        style="text;html=1;align=center;verticalAlign=middle;fontSize=18;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="20" width="300" height="40" as="geometry" />
</mxCell>
<mxCell id="step_1" value="Contact John Smith at Acme Corp"
        style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="title" value="[Project Title]"
        style="text;html=1;align=center;verticalAlign=middle;fontSize=18;fontStyle=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="20" width="300" height="40" as="geometry" />
</mxCell>
<mxCell id="step_1" value="[First Action Item]"
        style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Templates with specific content are not reusable. The next user MUST read through every shape to identify which text needs changing, and risks leaving stale data from the original use case. ALWAYS use bracket-notation placeholders (`[Description]`) to signal which values require replacement.

---

## AP-04: Missing Grid and Guides in Template Settings

### WRONG

```xml
<mxGraphModel dx="1000" dy="600">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- shapes -->
  </root>
</mxGraphModel>
```

### RIGHT

```xml
<mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
              tooltips="1" connect="1" arrows="1" fold="1"
              page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- shapes -->
  </root>
</mxGraphModel>
```

### Why It Fails

Without `grid="1"` and `guides="1"`, shapes added by the user in the editor do not snap to the grid, resulting in misaligned diagrams. Templates set the editor defaults, so omitting these attributes forces users to manually enable grid/guides every time. ALWAYS include full `mxGraphModel` attributes.

---

## AP-05: Orphaned Edges After Shape Removal

### WRONG

Removing a shape but leaving its edges:

```xml
<!-- step_2 was removed, but its edges remain -->
<mxCell id="e_s1_s2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="step_1" target="step_2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e_s2_s3" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="step_2" target="step_3">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

Remove edges together with the shape, then reconnect:

```xml
<!-- step_2 removed; step_1 now connects directly to step_3 -->
<mxCell id="e_s1_s3" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="step_1" target="step_3">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Edges referencing a non-existent cell ID produce rendering errors in Draw.io. The edge either disappears or renders as a broken line pointing to coordinates (0,0). ALWAYS remove all edges that reference a deleted shape AND create new edges to maintain flow continuity.

---

## AP-06: Inconsistent Styling Across Template Shapes

### WRONG

```xml
<mxCell id="step_1" value="[Step 1]"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="step_2" value="[Step 2]"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#FF6347;strokeColor=#000000;fontSize=18;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="160" height="80" as="geometry" />
</mxCell>
<mxCell id="step_3" value="[Step 3]"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#90EE90;strokeColor=#228B22;shadow=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="320" width="120" height="50" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="step_1" value="[Step 1]"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="step_2" value="[Step 2]"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="step_3" value="[Step 3]"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="300" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Shapes of the same type MUST have identical styles in a template. Mixed colors, sizes, and fonts make the template look unprofessional and confuse users about whether different styling implies different semantics. ALWAYS use one consistent style per shape type (process, decision, terminator, etc.).

---

## AP-07: Generating Compressed Template XML

### WRONG

```xml
<mxfile host="app.diagrams.net">
  <diagram id="d1" name="Page-1">
    jZLBbsMgDIafJtcKktFeTbtu0i7dObLgJmgEIsxKs6ef...
  </diagram>
</mxfile>
```

### RIGHT

```xml
<mxfile host="app.diagrams.net">
  <diagram id="d1" name="Page-1">
    <mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="1169" pageHeight="827">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- shapes -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Why It Fails

Draw.io supports compressed (deflate + base64) diagram content, but compressed XML is unreadable and uneditable by humans or LLMs. Templates MUST use uncompressed XML so they can be reviewed, modified, and validated. Draw.io accepts both formats, so there is no benefit to compression for templates. NEVER generate compressed XML.

---

## AP-08: Duplicate Cell IDs Across Template Pages

### WRONG

```xml
<mxfile host="app.diagrams.net">
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="step_1" value="Overview Step" ... />
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Detail">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="step_1" value="Detail Step" ... />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### RIGHT

```xml
<mxfile host="app.diagrams.net">
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="overview_step_1" value="Overview Step" ... />
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Detail">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="detail_step_1" value="Detail Step" ... />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Why It Fails

While Draw.io technically allows duplicate IDs across separate `<diagram>` elements (each page has its own ID namespace), it causes confusion when programmatically manipulating templates. Cross-page links and references break when IDs collide. ALWAYS prefix cell IDs with the page context (e.g., `overview_`, `detail_`) in multi-page templates. The only exceptions are the structural cells `id="0"` and `id="1"`, which MUST exist in every page.
