# Anti-Patterns: Draw.io Syntax Metadata

What NOT to do when working with pages, layers, variables, placeholders, tooltips, links, and MathJax in Draw.io XML.

---

## AP-01: Nested diagram Elements

### WRONG

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Overview">
    <diagram id="page-2" name="Detail">
      <mxGraphModel>
        <root>
          <mxCell id="0" />
          <mxCell id="1" parent="0" />
        </root>
      </mxGraphModel>
    </diagram>
  </diagram>
</mxfile>
```

### RIGHT

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Detail">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Why It Fails

`<diagram>` elements MUST be direct children of `<mxfile>`, NEVER nested inside each other. Nested diagrams are silently ignored by Draw.io — the inner page will not appear.

---

## AP-02: Duplicate diagram IDs

### WRONG

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Overview">
    <!-- ... -->
  </diagram>
  <diagram id="page-1" name="Detail">
    <!-- ... -->
  </diagram>
</mxfile>
```

### RIGHT

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Overview">
    <!-- ... -->
  </diagram>
  <diagram id="page-2" name="Detail">
    <!-- ... -->
  </diagram>
</mxfile>
```

### Why It Fails

Duplicate `<diagram>` IDs corrupt the file. Draw.io uses the `id` to identify pages for internal links (`data:page/id,...`), page switching, and export. Duplicate IDs cause unpredictable behavior: the wrong page opens, or pages overwrite each other.

---

## AP-03: Missing Structural Cells on a Page

### WRONG

```xml
<diagram id="page-2" name="Detail">
  <mxGraphModel>
    <root>
      <mxCell id="10" value="Shape" style="rounded=1;whiteSpace=wrap;html=1;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
      </mxCell>
    </root>
  </mxGraphModel>
</diagram>
```

### RIGHT

```xml
<diagram id="page-2" name="Detail">
  <mxGraphModel>
    <root>
      <mxCell id="0" />
      <mxCell id="1" parent="0" />
      <mxCell id="10" value="Shape" style="rounded=1;whiteSpace=wrap;html=1;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
      </mxCell>
    </root>
  </mxGraphModel>
</diagram>
```

### Why It Fails

Every page MUST have `<mxCell id="0" />` (root container) and `<mxCell id="1" parent="0" />` (default layer). Without these, Draw.io cannot resolve the `parent="1"` reference on content cells, and the entire page fails to render.

---

## AP-04: Missing placeholders="1" on object

### WRONG

```xml
<object id="2" label="Server: %hostname%" hostname="web-01">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
  </mxCell>
</object>
```

Renders as: "Server: %hostname%" (literal text)

### RIGHT

```xml
<object id="2" label="Server: %hostname%" placeholders="1" hostname="web-01">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
  </mxCell>
</object>
```

Renders as: "Server: web-01"

### Why It Fails

Without `placeholders="1"`, Draw.io treats `%hostname%` as literal text. The substitution engine is opt-in per cell. ALWAYS set `placeholders="1"` on every `<object>` that uses `%variable%` tokens.

---

## AP-05: Double-Quoted vars Attribute

### WRONG

```xml
<mxfile vars="{"project":"Atlas","version":"2.1"}">
```

### RIGHT

```xml
<mxfile vars='{"project":"Atlas","version":"2.1"}'>
```

### Why It Fails

The `vars` value contains JSON with double quotes. If the XML attribute also uses double quotes as delimiters, the parser sees `vars="{"` and breaks. ALWAYS use single quotes around the `vars` attribute value to avoid this conflict.

---

## AP-06: Reusing Cell IDs Across Pages

### WRONG

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Page 1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Shape A" style="rounded=1;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Page 2">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Shape B" style="rounded=1;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### RIGHT

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Page 1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Shape A" style="rounded=1;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Page 2">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="10" value="Shape B" style="rounded=1;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Why It Fails

Cell IDs MUST be unique across the entire file, not just within a single page. The exception is `id="0"` and `id="1"` which are structural cells required on every page. Duplicate IDs on content cells cause clipboard, undo, and cross-page reference operations to break.

---

## AP-07: Putting id or value on Inner mxCell When Using object Wrapper

### WRONG

```xml
<object id="2" label="Web Server" ip="10.0.1.10">
  <mxCell id="2" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;"
          vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
  </mxCell>
</object>
```

### RIGHT

```xml
<object id="2" label="Web Server" ip="10.0.1.10">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
  </mxCell>
</object>
```

### Why It Fails

When using `<object>`, the `id` and `label`/`value` attributes belong ONLY on the wrapper element. Putting `id` on both creates a duplicate ID. Putting `value` on the inner `<mxCell>` conflicts with `label` on `<object>` and causes unpredictable label rendering.

---

## AP-08: Missing math="1" on mxGraphModel for LaTeX

### WRONG

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" math="0">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="$$E = mc^2$$"
            style="text;html=1;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="200" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Renders as literal text: "$$E = mc^2$$"

### RIGHT

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" math="1">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="$$E = mc^2$$"
            style="text;html=1;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="200" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

MathJax rendering is disabled by default (`math="0"`). Without `math="1"` on `<mxGraphModel>`, the `$$...$$` delimiters are treated as plain text. ALWAYS set `math="1"` when the diagram contains LaTeX formulas.

---

## AP-09: Layer Cell Without parent="0"

### WRONG

```xml
<mxCell id="layer-bg" value="Background" parent="1" />
```

### RIGHT

```xml
<mxCell id="layer-bg" value="Background" parent="0" />
```

### Why It Fails

A layer MUST have `parent="0"` (the root container). Setting `parent="1"` makes the cell a child of the default layer instead of a sibling layer. It will appear as a shape on the default layer, not as a separate layer in the Layers panel.

---

## AP-10: Using File-Level Variables Without mxfile Wrapper

### WRONG

```xml
<mxGraphModel vars='{"project":"Atlas"}'>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="2" label="%project%" placeholders="1">
      <mxCell style="text;html=1;whiteSpace=wrap;" vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="200" height="40" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

### RIGHT

```xml
<mxfile compressed="false" vars='{"project":"Atlas"}'>
  <diagram id="page-1" name="Page-1">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <object id="2" label="%project%" placeholders="1">
          <mxCell style="text;html=1;whiteSpace=wrap;" vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="200" height="40" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### Why It Fails

The `vars` attribute belongs on `<mxfile>`, NOT on `<mxGraphModel>`. The `<mxGraphModel>` element does not support `vars`. File-level variables are ONLY available when the full `<mxfile>` wrapper is used.

---

## AP-11: Wrong Internal Link Format

### WRONG

```xml
<object id="2" label="Go to Page 2" link="page-2">
```

### ALSO WRONG

```xml
<object id="2" label="Go to Page 2" link="#page-2">
```

### RIGHT

```xml
<object id="2" label="Go to Page 2" link="data:page/id,page-2">
```

### Why It Fails

Internal page links MUST use the exact format `data:page/id,<diagramId>`. Any other format is treated as an external URL, which either opens a broken page in the browser or does nothing. The `<diagramId>` MUST match the `id` attribute of the target `<diagram>` element.
