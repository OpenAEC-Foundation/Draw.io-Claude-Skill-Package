# Anti-Patterns: Diagram Generator Agent

What NOT to do when orchestrating diagram generation, with explanations of why each pattern fails and the correct approach.

---

## AP-01: Guessing the Diagram Type

### WRONG

User says: "Visualize our system"

Agent immediately generates a network diagram without asking.

### RIGHT

Agent responds:

```
Your request could be represented as:
1. **Architecture diagram** — Best for showing cloud services, APIs, and system components.
2. **Network diagram** — Best for showing physical/logical network topology and devices.
3. **UML component diagram** — Best for showing software modules and their interfaces.

Which type fits your needs?
```

### Why It Fails

"Visualize our system" maps to at least three diagram types with equal probability. Generating the wrong type wastes the user's time and produces a diagram that does not match their mental model. ALWAYS ask when ambiguous.

---

## AP-02: Skipping Structural Cells

### WRONG

```xml
<mxGraphModel>
  <root>
    <mxCell id="step1" value="Do Thing" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="140" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### RIGHT

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="step1" value="Do Thing" style="rounded=0;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="140" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Why It Fails

Draw.io requires `<mxCell id="0" />` (root cell) and `<mxCell id="1" parent="0" />` (default layer). Without them, the diagram fails to load or renders an empty canvas. ALWAYS include both structural cells.

---

## AP-03: Generating Compressed XML

### WRONG

```xml
<mxfile>
  <diagram name="Page-1">
    7V1bc6M4Fv41rup9SBckce1jnKR7Z3a6u6q7Z2dfKIxtEhuzyHGS...
  </diagram>
</mxfile>
```

### RIGHT

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- Human-readable cells -->
  </root>
</mxGraphModel>
```

### Why It Fails

Compressed (Base64 + deflate) XML is unreadable, uneditable, and impossible to validate by inspection. The user cannot verify the diagram content, and errors are hidden inside the encoding. ALWAYS output uncompressed, human-readable mxGraph XML.

---

## AP-04: Skipping Validation

### WRONG

Agent generates XML and immediately presents it without checking.

Result: Edge `source="step3"` references a cell that does not exist, causing a broken connection in Draw.io.

### RIGHT

Agent generates XML, runs the validation checklist, finds the broken reference, fixes it, then presents the corrected diagram.

### Why It Fails

Generated XML frequently contains reference errors (typos in source/target IDs), duplicate IDs, or missing style properties. These errors produce silent failures in Draw.io — connections vanish, shapes render without labels, or the entire diagram fails to load. ALWAYS validate before presenting.

---

## AP-05: Using Wrong Shapes for the Diagram Type

### WRONG

User asks for an ER diagram. Agent generates rectangles with text labels instead of proper entity table shapes.

```xml
<mxCell id="users" value="Users: id, name, email"
        style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="200" height="60" as="geometry" />
</mxCell>
```

### RIGHT

Agent loads `drawio-impl-er-diagrams` skill and uses the correct table/entity shapes with PK/FK column indicators.

### Why It Fails

Each diagram type has specific shape conventions that convey semantic meaning. Using generic rectangles for ER entities loses the column structure, primary key indicators, and foreign key relationships. ALWAYS load the correct implementation skill and use its shape reference.

---

## AP-06: Overlapping Shapes

### WRONG

```xml
<mxCell id="step1" value="Step 1" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="step2" value="Step 2" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="220" y="120" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="step1" value="Step 1" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="190" y="100" width="140" height="60" as="geometry" />
</mxCell>
<mxCell id="step2" value="Step 2" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="190" y="200" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Overlapping shapes make the diagram unreadable. Labels become obscured, and users cannot distinguish between elements. ALWAYS calculate positions to prevent overlap, using at least 40px spacing between shapes.

---

## AP-07: Missing Edge Labels on Decisions

### WRONG

```xml
<mxCell id="dec1" value="Approved?" style="rhombus;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="80" as="geometry" />
</mxCell>
<mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_yes">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_no">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="dec1" value="Approved?" style="rhombus;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="80" as="geometry" />
</mxCell>
<mxCell id="e1" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_yes">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="e2" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
        edge="1" parent="1" source="dec1" target="step_no">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Unlabeled decision branches force the reader to guess which path is "Yes" and which is "No". This defeats the purpose of a decision point. ALWAYS label every edge leaving a decision shape.

---

## AP-08: Mixing Diagram Types Without Clarification

### WRONG

User says: "Show the architecture and the deployment process."

Agent generates a single diagram combining cloud service boxes with flowchart decision diamonds, creating an unreadable hybrid.

### RIGHT

Agent asks:

```
You mentioned both architecture and deployment process.
1. **Combined diagram** — Architecture boxes with deployment flow arrows between them.
2. **Two separate pages** — Architecture on page 1, deployment flowchart on page 2.

Which approach do you prefer?
```

### Why It Fails

Combining multiple diagram types without a clear visual strategy produces confusion. Architecture diagrams use spatial grouping; flowcharts use sequential flow. Mixing them without structure violates both conventions. ALWAYS clarify the user's intent for mixed requests.

---

## AP-09: Forgetting whiteSpace=wrap;html=1;

### WRONG

```xml
<mxCell id="step1" value="This is a long label that will overflow"
        style="rounded=0;" vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="step1" value="This is a long label that will overflow"
        style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `whiteSpace=wrap;`, text overflows outside the shape boundary and overlaps neighboring elements. Without `html=1;`, HTML entities like `<br>` render as literal text instead of line breaks. ALWAYS include both properties in every vertex style.

---

## AP-10: Not Offering to Open in Draw.io

### WRONG

Agent generates the XML and says "Here is your diagram" without offering any next steps.

### RIGHT

Agent generates the XML and says:

```
Here is your flowchart. I can:
1. Open it in Draw.io for you (using the MCP tool).
2. Save it as a .drawio file.
3. Modify specific elements.

What would you like to do?
```

### Why It Fails

Raw XML is not useful to most users without a way to view it visually. The MCP tools (`open_drawio_xml`, `drawio-mcp-server`) exist specifically to bridge XML generation and visual editing. ALWAYS offer to open the diagram after generating it.

---

## AP-11: Using Newlines Instead of HTML Breaks in Labels

### WRONG

```xml
<mxCell id="step1" value="Line 1
Line 2" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

### RIGHT

```xml
<mxCell id="step1" value="Line 1&lt;br&gt;Line 2" style="rounded=0;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

### Why It Fails

mxGraph renders labels as HTML when `html=1;` is set. Raw newlines in the `value` attribute are treated as whitespace (collapsed to a single space). ALWAYS use `<br>` for line breaks in labels. When the `<br>` appears inside an XML attribute, it MUST be escaped as `&lt;br&gt;` only if it would break the XML parser — in practice, `<br>` inside a `value` attribute is valid because Draw.io's parser handles it correctly.

---

## AP-12: Generating Excessively Large Single-Page Diagrams

### WRONG

Agent generates a single page with 50+ shapes spanning 5000 x 3000 pixels, requiring extensive scrolling and zooming.

### RIGHT

Agent asks:

```
This diagram has 50+ elements. For readability, I recommend:
1. **Split into pages** — Group related elements on separate pages.
2. **Use collapsible groups** — Nest detail inside expandable containers.
3. **Proceed as single page** — Generate everything on one canvas.

Which approach do you prefer?
```

### Why It Fails

Large single-page diagrams are difficult to navigate, print, and present. Elements at the edges require excessive zooming and scrolling. NEVER generate diagrams exceeding 2000px in any dimension without discussing alternatives with the user.
