# Anti-Patterns: Mermaid Conversion

What NOT to do when using Mermaid conversion in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Expecting Individual Cell Access After Mermaid Conversion

### WRONG

```
// Generate diagram via Mermaid
open_drawio_mermaid(content: "graph TD\n  A[Start] --> B[Process] --> C[End]")

// Then attempt to edit individual nodes via drawio-mcp-server
edit_cell(id: "A", value: "New Start")  // FAILS — "A" does not exist as an mxCell
delete_cell(id: "B")                     // FAILS — "B" is not a separate cell
restyle(id: "C", style: "fillColor=#ff0000;")  // FAILS — "C" is not addressable
```

### RIGHT

Generate the diagram as native mxGraph XML from the start:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="A" value="Start" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="140" height="60" as="geometry" />
    </mxCell>
    <mxCell id="B" value="Process" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="200" y="140" width="140" height="60" as="geometry" />
    </mxCell>
    <mxCell id="C" value="End" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="200" y="240" width="140" height="60" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="A" target="B">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="B" target="C">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

Mermaid conversion produces a SINGLE compound shape — the entire diagram is one grouped SVG object. Individual node IDs from the Mermaid source (A, B, C) do NOT become mxCell IDs. There are NO individual cells to select, edit, or delete.

---

## AP-02: Mixing Mermaid Compound Shapes with Native Cells

### WRONG

```
// Insert a Mermaid diagram
open_drawio_mermaid(content: "graph TD\n  A[Service A] --> B[Service B]")

// Then try to connect a native mxCell to a Mermaid node
add_cell(id: "ext1", value: "External System", ...)
add_connection(source: "ext1", target: "A")  // FAILS — "A" is not an addressable cell
```

### RIGHT

Generate ALL shapes as native mxGraph XML so they can be connected:

```xml
<mxCell id="svcA" value="Service A" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="200" y="40" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="svcB" value="Service B" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="200" y="140" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="ext1" value="External System" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="400" y="40" width="140" height="60" as="geometry" />
</mxCell>
<!-- Connections work because all cells are native mxCells -->
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="svcA" target="svcB">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="ext1" target="svcA">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

A Mermaid compound shape is opaque to the mxGraph model. Native cells CANNOT reference nodes inside the compound shape because those nodes do NOT exist as separate mxCell elements. The Mermaid shape is one monolithic object.

---

## AP-03: Using Mermaid for Production Diagrams That Need Updates

### WRONG

Using Mermaid for a diagram that will be iteratively updated by an AI agent:

```
// Sprint 1: Generate initial architecture
open_drawio_mermaid(content: "graph TD\n  A[API] --> B[DB]")

// Sprint 2: Add a cache layer — IMPOSSIBLE without regenerating everything
// Must replace the ENTIRE Mermaid source, losing any manual positioning adjustments
```

### RIGHT

Use native mxGraph XML from the start so individual cells can be added incrementally:

```
// Sprint 1: Generate initial architecture
add_cell(id: "api", value: "API", ...)
add_cell(id: "db", value: "DB", ...)
add_connection(source: "api", target: "db")

// Sprint 2: Add cache — works because cells are individually addressable
add_cell(id: "cache", value: "Cache", ...)
add_connection(source: "api", target: "cache")
add_connection(source: "cache", target: "db")
```

### Why It Fails

Mermaid diagrams are all-or-nothing. You CANNOT add a single node — you must replace the entire Mermaid source text. This means every update regenerates the full diagram, losing any manual layout adjustments the user made (repositioning, resizing).

---

## AP-04: Invalid Mermaid Syntax Without Validation

### WRONG

```
open_drawio_mermaid(
  content: "graph TD\n  A[Start] --> B(Process\n  B --> C[End]"
)
// Missing closing parenthesis on node B — produces blank diagram with no error
```

### RIGHT

ALWAYS validate syntax before sending:

```
open_drawio_mermaid(
  content: "graph TD\n  A[Start] --> B(Process)\n  B --> C[End]"
)
```

### Validation Checklist

1. Every node shape bracket is properly closed: `[]`, `()`, `{}`, `(())`, `[[]]`, `[()]`
2. Arrow syntax is valid: `-->`, `--->`, `-.->`, `==>`, `-->`
3. Labels use correct syntax: `-->|label|` or `--label-->`
4. Diagram starts with a valid keyword: `graph`, `flowchart`, `sequenceDiagram`, etc.
5. Indentation is consistent (spaces, not tabs)
6. Special characters in labels are quoted: `"label with spaces"`

### Why It Fails

The `open_drawio_mermaid` tool does NOT return syntax errors. Invalid Mermaid text produces a blank or broken diagram with no indication of what went wrong. ALWAYS verify syntax correctness before making the tool call.

---

## AP-05: Using Wrong Parameter Name

### WRONG

```
open_drawio_mermaid(
  data: "graph TD\n  A --> B"     // WRONG — parameter is "content", not "data"
)

open_drawio_mermaid(
  xml: "graph TD\n  A --> B"      // WRONG — parameter is "content", not "xml"
)

open_drawio_mermaid(
  mermaid: "graph TD\n  A --> B"  // WRONG — parameter is "content", not "mermaid"
)
```

### RIGHT

```
open_drawio_mermaid(
  content: "graph TD\n  A --> B"  // CORRECT — always use "content"
)
```

### Why It Fails

The `open_drawio_mermaid` tool has exactly one required parameter: `content`. Using any other parameter name results in the Mermaid text not being received by the tool, producing a blank result.

---

## AP-06: Attempting to Ungroup a Mermaid Compound Shape

### WRONG

Selecting the Mermaid shape and using Edit > Ungroup (or Ctrl+Shift+U) to split it into individual cells.

### What Actually Happens

The ungroup operation either:
- Does nothing (the shape remains a single compound object)
- Produces broken SVG fragments that are NOT valid mxCells
- Loses all text labels and connection information

### RIGHT

If you need individual cells, generate native mxGraph XML from the start. Use the Mermaid source text as a specification document, then translate it to XML manually.

### Why It Fails

The Mermaid compound shape is a rendered SVG image wrapped in a single mxCell container. It is NOT a group of mxCells. The "ungroup" operation is designed for mxCell groups, not for SVG containers. There is NO supported way to decompose a Mermaid shape into individual editable cells.
