# Draw.io Skill Package — Raw Masterplan

> Phase B1 output. Created 2026-03-19.
> Based on technology landscape research across XML format, style system, diagram types, and integration points.

---

## 1. Technology Landscape

### 1.1 Draw.io / diagrams.net

- **Open source** (Apache 2.0), maintained by JGraph Ltd
- **Web app:** app.diagrams.net — also available as desktop (Electron), VS Code extension, Confluence/Jira plugin
- **File format:** mxGraph XML (`.drawio` / `.xml`)
- **Rendering engine:** mxGraph 4.x (JavaScript client-side)
- **50+ shape libraries** (General, AWS, Azure, GCP, Cisco, UML, BPMN, etc.)
- **150+ built-in templates** across 15 categories

### 1.2 mxGraph XML Format

**File hierarchy:**
```
<mxfile>                          ← Root (host, modified, agent, version, type)
  <diagram id="..." name="...">  ← One per page/tab
    <mxGraphModel ...>            ← Graph settings (grid, page size, shadow, math)
      <root>
        <mxCell id="0"/>          ← REQUIRED: root container
        <mxCell id="1" parent="0"/> ← REQUIRED: default layer
        <!-- All diagram elements -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

**Two fundamental cell types:**
- **Vertex** (`vertex="1"`) — shapes, containers, swimlanes, groups
- **Edge** (`edge="1"`) — connectors between vertices

**Key XML constructs:**
- `<mxCell>` — Every element (id, parent, value, style, vertex/edge, source/target)
- `<mxGeometry>` — Positioning (x, y, width, height for vertices; relative=1 for edges)
- `<UserObject>` / `<object>` — Custom metadata wrapper around mxCell
- `<Array as="points">` — Edge waypoints
- `<mxPoint>` — Source/target points for unconnected edges

**Compression:** Files are stored as Base64(DEFLATE(URL-encode(XML))). For AI generation: ALWAYS use uncompressed XML.

### 1.3 Style System

Semicolon-separated `key=value;` pairs on the `style` attribute.

**Property categories:**
- Fill & stroke (fillColor, strokeColor, strokeWidth, dashed, opacity, gradient)
- Shape & geometry (shape, rounded, arcSize, rotation, direction, perimeter)
- Text & labels (fontSize, fontFamily, fontColor, fontStyle bitfield, align, whiteSpace, html)
- Edge routing (edgeStyle, curved, rounded, jettySize, elbow)
- Arrow markers (startArrow, endArrow, startFill, endFill, startSize, endSize)
- Connection points (exitX/Y, entryX/Y, exitPerimeter, entryPerimeter)
- Container/swimlane (container, collapsible, startSize, childLayout, swimlaneFillColor)
- Behavior (movable, resizable, editable, deletable, foldable)
- Sketch mode (sketch, comic, fillStyle, jiggle)
- Images (image, imageWidth, imageHeight)

**Built-in shapes:** rectangle, ellipse, rhombus, triangle, hexagon, cylinder, cloud, actor, swimlane, document, folder, card, note, process, callout, parallelogram, trapezoid, step, cube, datastore, table, plus

**Stencil shapes:** `shape=mxgraph.<library>.<shape>` (e.g., `mxgraph.aws4.lambda`)

**Edge styles:** orthogonalEdgeStyle, elbowEdgeStyle, entityRelationEdgeStyle, segmentEdgeStyle, loopEdgeStyle, sideToSideEdgeStyle, topToBottomEdgeStyle

**Font style bitfield:** 1=bold, 2=italic, 4=underline, 8=strikethrough (additive)

### 1.4 Connections

- **Floating:** Auto-routes along perimeter (no exit/entry specified)
- **Fixed:** Exact connection points via exitX/Y, entryX/Y (0.0–1.0 relative coordinates)
- **Custom points:** `points=[[x,y],[x,y],...]` on shapes
- **Self-loops:** loopEdgeStyle

### 1.5 Pages & Layers

- **Multi-page:** Multiple `<diagram>` elements in one `<mxfile>`
- **Layers:** Additional `<mxCell parent="0">` elements beyond id="1"; cells reference their layer as parent

### 1.6 Integration Points

- **CSV import:** Formatting directives (`# label`, `# style`, `# connect`) + CSV data → auto-generated diagrams
- **Mermaid conversion:** 15 diagram types supported; result is single compound shape (not individual cells)
- **SQL import:** DDL → ER diagrams
- **Export:** PNG, SVG, PDF, JPEG, WebP, HTML (all optionally with embedded XML for re-editing)
- **Visio import:** .vsdx files

---

## 2. Skill Inventory (22 Skills)

### 2.1 Core Skills (3) — Foundation knowledge

| # | Skill Name | Scope | Complexity |
|---|-----------|-------|------------|
| 1 | `drawio-core-xml-format` | mxfile/diagram/mxGraphModel/root hierarchy, mxCell attributes, mxGeometry, compression format, required cells (id=0, id=1), simplified format | Medium |
| 2 | `drawio-core-styles` | Style string format, property categories (fill, stroke, text, shape, behavior), color system (#RRGGBB, none, default), fontStyle bitfield, perimeter requirements | High |
| 3 | `drawio-core-geometry` | Coordinate system (origin top-left), absolute vs relative positioning, edge geometry (relative=1), waypoints, source/target points, container-relative coordinates, label positioning on edges | Medium |

### 2.2 Syntax Skills (4) — How to write XML

| # | Skill Name | Scope | Complexity |
|---|-----------|-------|------------|
| 4 | `drawio-syntax-cells` | Vertex vs edge cells, cell attributes (id, parent, value, style), UserObject/object wrapper for metadata, placeholders (%var%), HTML labels, groups, containers | Medium |
| 5 | `drawio-syntax-connections` | Floating vs fixed connections, exitX/Y + entryX/Y, custom connection points, edge waypoints (Array/mxPoint), self-loops, connection constraints (portConstraint) | Medium |
| 6 | `drawio-syntax-styles` | Complete style property reference, built-in shapes catalog, stencil shape format, edge styles catalog, arrow markers catalog, sketch mode properties | High |
| 7 | `drawio-syntax-metadata` | Pages (multi-diagram), layers, custom properties, file-level variables, placeholders, tooltips, links, MathJax/LaTeX support | Low |

### 2.3 Implementation Skills (11) — Diagram type recipes

| # | Skill Name | Scope | Complexity |
|---|-----------|-------|------------|
| 8 | `drawio-impl-flowcharts` | Basic flowcharts, process flows, decision trees; shapes: rectangle, diamond, oval, parallelogram; directed arrows | Medium |
| 9 | `drawio-impl-swimlanes` | Swimlane pools, cross-functional flowcharts; container nesting, startSize, horizontal/vertical orientation, auto-expand | High |
| 10 | `drawio-impl-architecture` | C4 model, cloud architecture (AWS/Azure/GCP shapes), system context diagrams; stencil library usage (mxgraph.aws4.*, mxgraph.azure.*, mxgraph.gcp2.*) | High |
| 11 | `drawio-impl-er-diagrams` | Entity-relationship diagrams, crow's foot notation, table shapes with PK/FK rows, SQL import patterns | Medium |
| 12 | `drawio-impl-bpmn` | BPMN 2.0 compliance: tasks, events (start/intermediate/end with types), gateways (exclusive/inclusive/parallel/event-based), pools, message flows, data objects | High |
| 13 | `drawio-impl-uml` | UML 2.5: class diagrams (3-section shapes, 6 connector types), sequence diagrams (lifelines, messages, activation bars), activity/state/use case/component/deployment | High |
| 14 | `drawio-impl-mindmaps` | Mind maps, concept maps; central topic + branching, tree layout, organic connectors | Low |
| 15 | `drawio-impl-network` | Network topology diagrams; Cisco/generic network shapes, rack diagrams, LAN/WAN layouts | Medium |
| 16 | `drawio-impl-templates` | Using and creating diagram templates; template XML structure, built-in template catalog (150+), custom template creation | Low |
| 17 | `drawio-impl-csv-import` | CSV-to-diagram: formatting directives (# label, # style, # connect, # layout), column references (%col%), conditional styling, auto-layout | Medium |
| 18 | `drawio-impl-mermaid-conversion` | Mermaid-to-Draw.io: supported types (15), conversion patterns, limitations (single compound shape), when to use Mermaid vs native XML | Low |

### 2.4 Error Skills (2) — Diagnosis and anti-patterns

| # | Skill Name | Scope | Complexity |
|---|-----------|-------|------------|
| 19 | `drawio-errors-xml` | XML validation errors, missing required cells, duplicate IDs, broken parent-child refs, invalid style strings, HTML escaping errors, compression issues | Medium |
| 20 | `drawio-errors-rendering` | Visual rendering issues: missing perimeters, wrong connection routing, overlapping shapes, invisible elements (opacity/fillColor=none), font rendering, container resize issues | Medium |

### 2.5 Agent Skills (2) — Intelligent orchestration

| # | Skill Name | Scope | Complexity |
|---|-----------|-------|------------|
| 21 | `drawio-agents-diagram-generator` | Decision tree: user intent → diagram type → skill selection → XML generation → validation. Orchestrates other skills based on natural language requests | High |
| 22 | `drawio-agents-code-validator` | XML validation pipeline: structure check → ID uniqueness → parent-child integrity → style validation → geometry check → connection validation | High |

---

## 3. Dependency Graph

```
Layer 0 (Foundation):
  drawio-core-xml-format
  drawio-core-styles
  drawio-core-geometry

Layer 1 (Syntax — depends on Layer 0):
  drawio-syntax-cells        → core-xml-format, core-geometry
  drawio-syntax-connections  → core-xml-format, core-geometry, core-styles
  drawio-syntax-styles       → core-styles
  drawio-syntax-metadata     → core-xml-format

Layer 2 (Basic Impl — depends on Layer 1):
  drawio-impl-flowcharts     → syntax-cells, syntax-connections, syntax-styles
  drawio-impl-mindmaps       → syntax-cells, syntax-connections, syntax-styles
  drawio-impl-templates      → syntax-cells
  drawio-impl-csv-import     → syntax-cells, syntax-connections
  drawio-impl-mermaid-conversion → (minimal dependencies)

Layer 3 (Complex Impl — depends on Layer 1):
  drawio-impl-swimlanes      → syntax-cells, syntax-connections, syntax-styles
  drawio-impl-er-diagrams    → syntax-cells, syntax-connections, syntax-styles
  drawio-impl-network        → syntax-cells, syntax-connections, syntax-styles
  drawio-impl-architecture   → syntax-cells, syntax-connections, syntax-styles
  drawio-impl-bpmn           → syntax-cells, syntax-connections, syntax-styles, syntax-metadata
  drawio-impl-uml            → syntax-cells, syntax-connections, syntax-styles

Layer 4 (Errors — depends on Layer 0-1):
  drawio-errors-xml          → core-xml-format, syntax-cells
  drawio-errors-rendering    → core-styles, core-geometry, syntax-styles

Layer 5 (Agents — depends on ALL):
  drawio-agents-diagram-generator → ALL impl skills
  drawio-agents-code-validator    → ALL core + syntax + error skills
```

---

## 4. Batch Execution Order (Phase B5)

| Batch | Skills | Count | Parallel Agents |
|-------|--------|-------|-----------------|
| **B5.1** | core-xml-format, core-styles, core-geometry | 3 | 3 |
| **B5.2** | syntax-cells, syntax-connections, syntax-styles, syntax-metadata | 4 | 4 |
| **B5.3** | impl-flowcharts, impl-mindmaps, impl-templates | 3 | 3 |
| **B5.4** | impl-swimlanes, impl-er-diagrams, impl-csv-import, impl-mermaid-conversion | 4 | 4 |
| **B5.5** | impl-architecture, impl-bpmn, impl-uml, impl-network | 4 | 4 |
| **B5.6** | errors-xml, errors-rendering, agents-diagram-generator, agents-code-validator | 4 | 4 |

**Quality gate between every batch.** Total: 22 skills in 6 batches.

---

## 5. Per-Skill Specification Summary

### Core Skills

**drawio-core-xml-format**
- Category: Document & Asset Creation
- Key content: mxfile hierarchy, required cells (id=0, id=1), mxCell attributes, simplified format (mxGraphModel only), compression format
- Sources: drawio.com/doc/faq/drawio-style-reference, drawio.com/doc/faq/ai-drawio-generation
- Scripts: xml_structure_validator.py

**drawio-core-styles**
- Category: Document & Asset Creation
- Key content: Style string format, property catalog (80+ properties), color system, fontStyle bitfield, perimeter requirements
- Sources: mxConstants JS API, drawio.com/doc/faq/drawio-style-reference
- Scripts: style_validator.py

**drawio-core-geometry**
- Category: Document & Asset Creation
- Key content: Coordinate system, vertex vs edge geometry, waypoints, container-relative coordinates, label positioning
- Sources: mxGeometry JS API, mxGraph tutorial

### Syntax Skills

**drawio-syntax-cells**
- Category: Document & Asset Creation
- Key content: Vertex/edge creation, UserObject metadata, HTML labels, groups, containers
- Sources: mxCell JS API

**drawio-syntax-connections**
- Category: Document & Asset Creation
- Key content: Floating vs fixed, exit/entry points, custom connection points, waypoints, self-loops
- Sources: drawio.com/doc/faq/connectors, drawio.com/doc/faq/shape-connection-points-customise

**drawio-syntax-styles**
- Category: Document & Asset Creation
- Key content: Complete property reference, shape catalog, stencil format, edge styles, arrow markers
- Sources: mxConstants, drawio.com/doc/faq/drawio-style-reference

**drawio-syntax-metadata**
- Category: Document & Asset Creation
- Key content: Pages, layers, custom properties, variables, placeholders, MathJax
- Sources: drawio.com/doc

### Implementation Skills

**drawio-impl-flowcharts**
- Category: Workflow Automation
- Key content: Standard flowchart shapes, decision branching, directed flow
- Assets: flowchart-basic.xml template

**drawio-impl-swimlanes**
- Category: Workflow Automation
- Key content: Pool/lane container nesting, cross-functional layout, auto-expand
- Assets: swimlane-horizontal.xml, swimlane-vertical.xml templates

**drawio-impl-architecture**
- Category: MCP Enhancement
- Key content: C4 model, cloud stencils (AWS4, Azure, GCP2), system context
- Assets: c4-template.xml, aws-architecture.xml templates

**drawio-impl-er-diagrams**
- Category: Document & Asset Creation
- Key content: Entity tables, crow's foot notation, FK relationships, SQL import
- Assets: er-basic.xml template

**drawio-impl-bpmn**
- Category: Workflow Automation
- Key content: BPMN 2.0 elements (tasks, events, gateways), pools, message flows
- Assets: bpmn-process.xml template

**drawio-impl-uml**
- Category: Document & Asset Creation
- Key content: Class diagrams (3-section), sequence diagrams, 6 connector types
- Assets: uml-class.xml, uml-sequence.xml templates

**drawio-impl-mindmaps**
- Category: Document & Asset Creation
- Key content: Central topic, branching, tree layout, organic connectors
- Assets: mindmap-basic.xml template

**drawio-impl-network**
- Category: MCP Enhancement
- Key content: Cisco/generic shapes, rack diagrams, topology layouts
- Assets: network-lan.xml template

**drawio-impl-templates**
- Category: Document & Asset Creation
- Key content: Template catalog (150+), custom template creation, template XML format

**drawio-impl-csv-import**
- Category: Workflow Automation
- Key content: CSV directives, column references, conditional styling, auto-layout

**drawio-impl-mermaid-conversion**
- Category: Document & Asset Creation
- Key content: 15 supported types, conversion method, limitations

### Error Skills

**drawio-errors-xml**
- Category: Domain-Specific Intelligence
- Key content: Validation errors, missing cells, duplicate IDs, broken refs, HTML escaping
- Scripts: xml_error_checker.py

**drawio-errors-rendering**
- Category: Domain-Specific Intelligence
- Key content: Visual issues, missing perimeters, routing problems, invisible elements

### Agent Skills

**drawio-agents-diagram-generator**
- Category: Workflow Automation + Context-Aware Tool Selection
- Key content: Intent → type → skill → XML → validate pipeline, decision tree
- allowed-tools: Bash(python:*), MCP tools (drawio-editor, drawio-official)

**drawio-agents-code-validator**
- Category: Domain-Specific Intelligence + Iterative Refinement
- Key content: Multi-stage validation pipeline, error reporting, fix suggestions
- Scripts: validate_diagram.py
- allowed-tools: Bash(python:*)

---

## 6. Key Research Sources Used

| Source | URL | Used For |
|--------|-----|----------|
| Draw.io AI Generation Guide | drawio.com/doc/faq/ai-drawio-generation | AI-specific XML generation rules |
| Draw.io Style Reference | drawio.com/doc/faq/drawio-style-reference | Complete style property catalog |
| mxConstants JS API | jgraph.github.io/mxgraph/docs/js-api/files/util/mxConstants-js.html | Authoritative style/shape constants |
| mxCell JS API | jgraph.github.io/mxgraph/docs/js-api/files/model/mxCell-js.html | Cell attributes |
| mxGeometry JS API | jgraph.github.io/mxgraph/docs/js-api/files/model/mxGeometry-js.html | Geometry system |
| mxEdgeStyle JS API | jgraph.github.io/mxgraph/docs/js-api/files/view/mxEdgeStyle-js.html | Edge routing algorithms |
| Draw.io Connectors | drawio.com/doc/faq/connectors | Connection patterns |
| Draw.io Connection Points | drawio.com/doc/faq/shape-connection-points-customise | Custom connection points |
| Draw.io Tools | jgraph.github.io/drawio-tools/ | CSV tool, compression converter |
| DeepWiki File Format | deepwiki.com/jgraph/drawio-diagrams/10-file-format-reference | File format deep dive |

---

## 7. Open Items for Phase B2 (Deep Research)

These topics need deep research (minimum 2000 words each) before skill creation:

1. **vooronderzoek-drawio-xml.md** — Deep dive into XML format edge cases, version differences, simplified vs full format, round-trip fidelity
2. **vooronderzoek-drawio-styles.md** — Complete style property catalog with valid values, stencil library enumeration, theme system
3. **vooronderzoek-drawio-diagrams.md** — Per-diagram-type shape catalogs, connection patterns, layout algorithms
4. **vooronderzoek-drawio-integration.md** — CSV directive specification, Mermaid conversion internals, SQL import, export formats, MCP server capabilities

---

## 8. Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| Style property catalog incomplete | Skills produce invalid styles | Verify against mxConstants source code in B2 |
| Stencil shapes change between versions | Architecture skill breaks | Pin to current stencil library versions |
| Mermaid conversion is limited (single shape) | Users expect editable output | Document limitation clearly, recommend native XML |
| 22 skills may need adjustment | Some too broad, some too narrow | Refine in B3 after deep research |
| CSV import directives underdocumented | csv-import skill incomplete | Reverse-engineer from drawio-tools source |
