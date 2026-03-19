# Draw.io Skill Package — Refined Masterplan

> Phase B3 output. Refined 2026-03-19 based on 4 vooronderzoek documents (3800+ lines of research).
> Supersedes raw-masterplan.md.

---

## 1. Refinement Decisions

| # | Decision | Rationale |
|---|----------|-----------|
| R-001 | Keep 22 skills unchanged | Research confirms all 22 skills have sufficient scope. No overlap warranting merges, no gaps requiring new skills. |
| R-002 | Cap batches at 3 parallel agents | WORKFLOW.md standard: "3 agents per batch (optimal for Claude Code Agent tool)". Raw masterplan had batches of 4 — adjusted. |
| R-003 | Clear scope boundary: core-styles vs syntax-styles | core-styles = understanding the system (format, inheritance, perimeters, color system). syntax-styles = complete property reference catalog (120+ properties). Different audiences, no duplication. |
| R-004 | Add license, compatibility, metadata fields to all skills | WORKFLOW template requires these frontmatter fields. Not in raw masterplan. |
| R-005 | Directory structure follows WORKFLOW standard | `skills/source/drawio-{category}/{skill-name}/SKILL.md` (not `skills/drawio/`). |
| R-006 | Topic research (B4) via inline WebFetch during skill creation | Each agent prompt includes specific source URLs. Separate topic-research docs not needed for this package — the 4 vooronderzoek documents are comprehensive enough. |
| R-007 | Batch plan: 8 batches (max 3 agents each) | Respects dependency graph and parallelism constraints. |

---

## 2. Final Skill Inventory (22 Skills)

### 2.1 Core Skills (3)

| # | Skill Name | Scope |
|---|-----------|-------|
| 1 | `drawio-core-xml-format` | mxfile/diagram/mxGraphModel/root hierarchy, required cells (id=0, id=1), mxCell attributes, simplified format, compression |
| 2 | `drawio-core-styles` | Style string format, property categories, color system, fontStyle bitfield, perimeter requirements, style inheritance |
| 3 | `drawio-core-geometry` | Coordinate system, vertex vs edge geometry, waypoints, container-relative coordinates, label positioning |

### 2.2 Syntax Skills (4)

| # | Skill Name | Scope |
|---|-----------|-------|
| 4 | `drawio-syntax-cells` | Vertex/edge creation, UserObject metadata, HTML labels, groups, containers |
| 5 | `drawio-syntax-connections` | Floating vs fixed connections, exit/entry points, custom connection points, waypoints, self-loops |
| 6 | `drawio-syntax-styles` | Complete style property reference (120+), shape catalog, stencil format, edge styles, arrow markers |
| 7 | `drawio-syntax-metadata` | Pages, layers, custom properties, file-level variables, placeholders, tooltips, links, MathJax |

### 2.3 Implementation Skills (11)

| # | Skill Name | Scope |
|---|-----------|-------|
| 8 | `drawio-impl-flowcharts` | Standard flowchart shapes, decision branching, directed flow |
| 9 | `drawio-impl-swimlanes` | Pool/lane container nesting, cross-functional layout, horizontal/vertical |
| 10 | `drawio-impl-architecture` | C4 model, cloud stencils (AWS4, Azure, GCP2), system context |
| 11 | `drawio-impl-er-diagrams` | Entity tables, crow's foot notation, FK relationships |
| 12 | `drawio-impl-bpmn` | BPMN 2.0: tasks, events, gateways, pools, message flows |
| 13 | `drawio-impl-uml` | Class diagrams, sequence diagrams, 6 UML connector types |
| 14 | `drawio-impl-mindmaps` | Central topic, branching, tree layout, organic connectors |
| 15 | `drawio-impl-network` | Cisco/generic shapes, rack diagrams, topology layouts |
| 16 | `drawio-impl-templates` | Template catalog, custom template creation, template XML format |
| 17 | `drawio-impl-csv-import` | CSV directives, column references, conditional styling, auto-layout |
| 18 | `drawio-impl-mermaid-conversion` | Supported types, conversion method, limitations (single compound shape) |

### 2.4 Error Skills (2)

| # | Skill Name | Scope |
|---|-----------|-------|
| 19 | `drawio-errors-xml` | Validation errors, missing cells, duplicate IDs, broken refs, HTML escaping |
| 20 | `drawio-errors-rendering` | Visual issues, missing perimeters, routing problems, invisible elements |

### 2.5 Agent Skills (2)

| # | Skill Name | Scope |
|---|-----------|-------|
| 21 | `drawio-agents-diagram-generator` | Intent → type → skill → XML → validate pipeline |
| 22 | `drawio-agents-code-validator` | Multi-stage XML validation pipeline, error reporting, fix suggestions |

---

## 3. Batch Execution Plan

| Batch | Skills | Count | Dependencies |
|-------|--------|-------|-------------|
| **B5.1** | core-xml-format, core-styles, core-geometry | 3 | None (foundation) |
| **B5.2** | syntax-cells, syntax-connections, syntax-styles | 3 | B5.1 |
| **B5.3** | syntax-metadata, impl-flowcharts, impl-mindmaps | 3 | B5.1, B5.2 |
| **B5.4** | impl-templates, impl-csv-import, impl-mermaid-conversion | 3 | B5.2 |
| **B5.5** | impl-swimlanes, impl-er-diagrams, impl-network | 3 | B5.2 |
| **B5.6** | impl-architecture, impl-bpmn, impl-uml | 3 | B5.2 |
| **B5.7** | errors-xml, errors-rendering | 2 | B5.1, B5.2 |
| **B5.8** | agents-diagram-generator, agents-code-validator | 2 | ALL previous |

**Total: 22 skills in 8 batches. Quality gate between every batch.**

---

## 4. Agent Prompts

### Common Preamble (include in EVERY agent prompt)

```
You are creating a Draw.io skill for the Draw.io Claude Skill Package.

**Output location:** C:\Users\Freek Heijting\Documents\GitHub\Draw.io-Claude-Skill-Package\skills\source\drawio-{CATEGORY}\{SKILL-NAME}\

**Create these files:**
1. SKILL.md (< 500 lines, YAML frontmatter with folded block scalar description)
2. references/methods.md (complete attribute/property reference)
3. references/examples.md (working XML examples)
4. references/anti-patterns.md (what NOT to do, with explanations)

**YAML frontmatter format (MANDATORY):**
---
name: {SKILL-NAME}
description: >
  Use when [specific trigger scenario].
  Prevents the [common mistake this skill guards against].
  Covers [key topics].
  Keywords: [comma-separated terms].
license: MIT
compatibility: "Designed for Claude Code. Requires Draw.io / diagrams.net (current)."
metadata:
  author: OpenAEC-Foundation
  version: "1.0"
---

**Quality rules:**
- English ONLY
- Deterministic language: ALWAYS/NEVER (not "you might", "consider", "should")
- SKILL.md < 500 lines (put details in references/)
- All XML examples MUST be valid mxGraph XML
- Include decision trees for conditional logic
- Reference links to references/ files at the bottom of SKILL.md

**Research sources (use WebFetch to verify):**
- drawio.com/doc/faq/ai-drawio-generation
- drawio.com/doc/faq/drawio-style-reference
- jgraph.github.io/mxgraph/docs/js-api/
```

---

### Batch B5.1 — Core Skills

#### Agent 1: drawio-core-xml-format

```
{COMMON PREAMBLE with CATEGORY=core, SKILL-NAME=drawio-core-xml-format}

**Scope:**
- Complete mxfile/diagram/mxGraphModel/root XML hierarchy
- All mxCell attributes (id, parent, value, style, vertex, edge, source, target, connectable)
- mxGeometry basics (x, y, width, height, relative, as="geometry")
- Required structural cells (id=0 root, id=1 default layer)
- Simplified format (just <mxGraphModel> without wrappers — Draw.io auto-wraps)
- Compression format (deflate + base64) and why AI MUST use uncompressed
- Multi-page support (multiple <diagram> elements)

**Research document:** docs/research/vooronderzoek-drawio-xml.md (sections 1-4)

**Key rules to encode:**
- ALWAYS generate uncompressed XML (compressed="false")
- ALWAYS include id=0 and id=1 structural cells
- NEVER use duplicate cell IDs within a diagram
- ALWAYS use html=1 in style when labels contain HTML
```

#### Agent 2: drawio-core-styles

```
{COMMON PREAMBLE with CATEGORY=core, SKILL-NAME=drawio-core-styles}

**Scope:**
- Style string syntax (semicolon-separated key=value pairs)
- Leading shape identifier (e.g., "ellipse;" or "rhombus;" before properties)
- Property categories overview (fill, stroke, text, shape, edge, container, behavior)
- Color system (#RRGGBB hex, "none" for transparent, named colors)
- fontStyle bitfield (1=bold, 2=italic, 4=underline, 8=strikethrough, additive)
- Perimeter system (MUST match shape type)
- Style inheritance and defaults
- html=1 requirement

**Research document:** docs/research/vooronderzoek-drawio-styles.md (sections 1, 7, 10, 11)

**Key rules to encode:**
- ALWAYS include html=1 in every cell style
- ALWAYS set perimeter matching the shape (ellipse→ellipsePerimeter, rhombus→rhombusPerimeter)
- NEVER use invalid color values (must be #RRGGBB, "none", or valid CSS color)
- ALWAYS terminate style strings with semicolon
```

#### Agent 3: drawio-core-geometry

```
{COMMON PREAMBLE with CATEGORY=core, SKILL-NAME=drawio-core-geometry}

**Scope:**
- Coordinate system (origin = top-left, positive x=right, positive y=down)
- Vertex geometry (absolute x, y, width, height)
- Edge geometry (relative=1, source/target points)
- Waypoints (Array as="points" with mxPoint elements)
- Container-relative coordinates (children use relative coords to parent)
- Label positioning on edges (x=-1 to 1 along edge, y=offset in pixels)
- Label positioning on vertices (labelPosition, verticalLabelPosition)
- Connection point system (exitX/Y, entryX/Y, 0.0 to 1.0)

**Research document:** docs/research/vooronderzoek-drawio-xml.md (sections 3, 5)

**Key rules to encode:**
- ALWAYS use relative="1" on edge geometry
- NEVER use absolute coordinates for children inside containers
- ALWAYS specify width and height for vertices (no implicit sizing)
- Connection points use 0.0-1.0 relative coordinates (0,0=top-left, 1,1=bottom-right, 0.5,0.5=center)
```

---

### Batch B5.2 — Syntax Skills

#### Agent 4: drawio-syntax-cells

```
{COMMON PREAMBLE with CATEGORY=syntax, SKILL-NAME=drawio-syntax-cells}

**Scope:**
- Vertex cells (vertex="1") — shapes, images, containers
- Edge cells (edge="1") — connectors with source/target
- Cell attribute reference (all attributes with valid values)
- UserObject / <object> wrapper for custom metadata properties
- HTML labels (value attribute with HTML content, html=1 required)
- Placeholder syntax (%variable%) in labels
- Groups and containers (container=1, parent references)
- Layer cells (additional cells with parent="0")

**Research document:** docs/research/vooronderzoek-drawio-xml.md (sections 2, 4, 6)

**Key rules to encode:**
- ALWAYS set vertex="1" for shapes, edge="1" for connectors
- NEVER omit the parent attribute (default parent="1" for the default layer)
- ALWAYS use <object> wrapper when adding custom properties
- ALWAYS escape HTML entities in value attribute (&amp; &lt; &gt; &quot;)
```

#### Agent 5: drawio-syntax-connections

```
{COMMON PREAMBLE with CATEGORY=syntax, SKILL-NAME=drawio-syntax-connections}

**Scope:**
- Floating connections (no exit/entry specified — auto-routes along perimeter)
- Fixed connections (exitX/Y + entryX/Y at specific connection points)
- Edge routing styles (orthogonalEdgeStyle, elbowEdgeStyle, entityRelationEdgeStyle, segmentEdgeStyle, isometricEdgeStyle)
- Waypoints (Array as="points" with mxPoint elements for manual routing)
- Self-loops (loopEdgeStyle)
- Custom connection points on shapes (points=[[x,y],...])
- Connection constraints (portConstraint, perimeter spacing)
- Edge labels (label positioning with x, y offset on mxGeometry)

**Research documents:**
- docs/research/vooronderzoek-drawio-xml.md (section 5)
- docs/research/vooronderzoek-drawio-styles.md (section 5)

**WebFetch sources:**
- drawio.com/doc/faq/connectors
- drawio.com/doc/faq/shape-connection-points-customise

**Key rules to encode:**
- ALWAYS use source and target attributes to connect edges to cells
- NEVER hardcode waypoints when edgeStyle can auto-route
- ALWAYS use exitPerimeter=0 when using exitX/Y on non-standard points
- Edge labels: x ranges -1 (source end) to 1 (target end), 0 = center
```

#### Agent 6: drawio-syntax-styles

```
{COMMON PREAMBLE with CATEGORY=syntax, SKILL-NAME=drawio-syntax-styles}

**Scope:**
- Complete style property reference (120+ properties organized by category)
- Built-in shape catalog (22+ shapes with style strings)
- Stencil shape format (shape=mxgraph.<library>.<shape>)
- Edge style catalog (7 routing algorithms with visual examples described)
- Arrow marker catalog (21 types: classic, block, open, oval, diamond, etc.)
- Arrow fill behavior (startFill/endFill: 0=open, 1=filled)
- Sketch mode properties (sketch=1, comic=1, jiggle, fillStyle)
- Image shape properties (image=URL, imageWidth, imageHeight)

**Research document:** docs/research/vooronderzoek-drawio-styles.md (ALL sections)

**Key rules to encode:**
- ALWAYS use the complete property name (strokeColor, not stroke-color)
- NEVER mix shape identifier with shape= property (use "ellipse;" OR "shape=ellipse;", not both)
- Arrow types: classic (default), block, open, oval, diamond, diamondThin, dash, cross, circlePlus, circle, ERone, ERmany, ERmandOne, ERzeroToOne, ERoneToMany, ERzeroToMany
- Stencil shapes ALWAYS start with shape=mxgraph.
```

---

### Batch B5.3 — Syntax + Basic Impl

#### Agent 7: drawio-syntax-metadata

```
{COMMON PREAMBLE with CATEGORY=syntax, SKILL-NAME=drawio-syntax-metadata}

**Scope:**
- Multi-page diagrams (multiple <diagram> elements, unique IDs and names)
- Layer system (additional mxCell parent="0" elements, layer visibility)
- Custom properties via <object> element (label, placeholders="1")
- File-level variables (vars attribute on <mxfile> as JSON)
- Placeholder system (%variable%, predefined: %date%, %filename%, %page%, %pagenumber%)
- Placeholder scope resolution (cell → parent → file-level vars)
- Tooltips (tooltip attribute on <object>)
- Links (link attribute on <object>)
- MathJax/LaTeX support (math="1" on mxGraphModel, $$formula$$ in labels)

**Research documents:**
- docs/research/vooronderzoek-drawio-xml.md (sections 4, 6, 7)
- docs/research/vooronderzoek-drawio-integration.md (section 8)

**Key rules to encode:**
- ALWAYS use unique diagram IDs across pages
- ALWAYS set placeholders="1" on <object> to enable placeholder substitution
- File-level vars use single-quoted JSON: vars='{"key":"value"}'
- NEVER nest <diagram> elements (they are siblings under <mxfile>)
```

#### Agent 8: drawio-impl-flowcharts

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-flowcharts}

**Scope:**
- Standard flowchart shapes and their styles:
  - Process (rounded rectangle), Decision (rhombus), Terminator (ellipse/stadium)
  - Data (parallelogram), Document (shape=document), Predefined Process (shape=process)
  - Manual Input, Preparation (hexagon), Database (shape=cylinder3)
- Connection patterns (directed arrows, decision branching with Yes/No labels)
- Decision tree layout (diamond → left/right or top/bottom branching)
- Complete flowchart XML example (10+ shapes, realistic process)
- Auto-layout hints for tree structure

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 1)

**Key rules to encode:**
- ALWAYS use rhombus shape for decisions (not diamond — it's called rhombus in mxGraph)
- ALWAYS label decision branches (Yes/No or True/False)
- ALWAYS use consistent flow direction (top-to-bottom or left-to-right)
- NEVER mix flow directions within the same flowchart
```

#### Agent 9: drawio-impl-mindmaps

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-mindmaps}

**Scope:**
- Central topic shape (large rounded rectangle or ellipse)
- Branch shapes (smaller rounded rectangles with colored fills)
- Organic/curved connectors (curved=1, no arrows)
- Tree layout pattern (manual positioning for consistent spacing)
- Color coding by branch level
- Mind map vs concept map differences
- Complete mind map XML example (central topic + 3 levels of branches)

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 7)

**Key rules to encode:**
- ALWAYS use curved connectors without arrows for mind map branches
- ALWAYS center the root topic and spread branches radially
- NEVER use straight orthogonal connectors in mind maps
- Color each branch family with a consistent color for visual grouping
```

---

### Batch B5.4 — Integration Impl Skills

#### Agent 10: drawio-impl-templates

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-templates}

**Scope:**
- Built-in template catalog (150+ templates across 15 categories)
- Template XML structure (standard mxfile with pre-built content)
- Creating custom templates (save as .xml with descriptive page names)
- Template categories: Basic, Flowcharts, UML, ER, Network, Cloud, BPMN, etc.
- Using templates as starting points for AI generation
- Template modification patterns (swap content, keep structure)

**Research document:** docs/research/vooronderzoek-drawio-integration.md (section 3)

**Key rules to encode:**
- ALWAYS use an existing template shape as reference when creating similar diagrams
- NEVER create complex diagrams from scratch when a template exists
- Templates are standard mxGraph XML — modify cells, don't rebuild structure
```

#### Agent 11: drawio-impl-csv-import

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-csv-import}

**Scope:**
- CSV format specification: directive lines (# prefix) + CSV data
- All directives: # label, # style, # identity, # namespace, # connect, # layout, # width, # height, # padding, # ignore, # link, # parentstyle, # nodespacing, # levelspacing, # edgespacing
- Connection JSON format: {"from":"col", "to":"col", "invert":bool, "style":"..."}
- Column references in style (%column_name%)
- Conditional styling based on column values
- Auto-layout options (verticalTree, horizontalTree, organic, circle)
- Complete CSV examples (org chart, flowchart, network)

**Research document:** docs/research/vooronderzoek-drawio-integration.md (section 1)

**WebFetch source:** drawio.com/doc/faq/csv-import

**Key rules to encode:**
- ALWAYS start CSV with directive lines (# label is mandatory)
- ALWAYS specify # identity for unique cell IDs
- ALWAYS specify # connect for edge creation
- CSV columns become cell properties accessible via %column%
```

#### Agent 12: drawio-impl-mermaid-conversion

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-mermaid-conversion}

**Scope:**
- Supported Mermaid diagram types (flowchart, sequence, class, state, ER, gantt, pie, journey, quadrant, requirement, C4, mindmap)
- How to use @drawio/mcp open_drawio_mermaid tool
- CRITICAL limitation: Mermaid conversion produces a SINGLE compound shape, NOT individual mxCells
- Decision tree: When to use Mermaid vs native mxGraph XML
- Mermaid syntax quick reference for each supported type
- Workarounds for the compound shape limitation

**Research document:** docs/research/vooronderzoek-drawio-integration.md (section 2)

**Key rules to encode:**
- NEVER use Mermaid conversion when individual cell editability is required
- ALWAYS use native mxGraph XML for diagrams that need per-element styling or connections
- Mermaid conversion is ONLY suitable for quick visualization, not production diagrams
- Use open_drawio_mermaid MCP tool for conversion (NOT manual XML manipulation)
```

---

### Batch B5.5 — Complex Impl Skills (Part 1)

#### Agent 13: drawio-impl-swimlanes

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-swimlanes}

**Scope:**
- Swimlane pools (container=1, style includes "swimlane;")
- Horizontal vs vertical orientation (horizontal=0 for vertical)
- Nested lanes (child swimlanes inside a pool)
- Header sizing (startSize property)
- Cross-functional flowchart pattern (shapes inside lanes, edges crossing lanes)
- Child coordinates are RELATIVE to the parent container
- Auto-expand behavior (swimlane auto-resizes to fit children)
- Complete swimlane XML example (2-3 lanes with process flow)

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 2)

**Key rules to encode:**
- ALWAYS set container=1 on swimlane parent cells
- ALWAYS use relative coordinates for children inside swimlanes
- NEVER use absolute canvas coordinates for shapes inside containers
- Swimlane header height = startSize value in pixels
```

#### Agent 14: drawio-impl-er-diagrams

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-er-diagrams}

**Scope:**
- Entity shapes (table-like containers with rows for attributes)
- Primary key (PK) and foreign key (FK) notation
- Crow's foot notation in Draw.io:
  - ERone, ERmany, ERmandOne, ERzeroToOne, ERoneToMany, ERzeroToMany arrows
- entityRelationEdgeStyle for ER connections
- Relationship labels (1:1, 1:N, M:N)
- Table shape pattern (swimlane with header + attribute rows)
- Complete ER diagram XML example (3+ entities with relationships)

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 4)

**Key rules to encode:**
- ALWAYS use entityRelationEdgeStyle for ER connections
- ALWAYS use ER-specific arrow types (ERone, ERmany, etc.) not generic arrows
- Entity tables use swimlane style with childLayout=stackLayout
- PK fields: mark with bold or underline in the label
```

#### Agent 15: drawio-impl-network

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-network}

**Scope:**
- Cisco network shapes (shape=mxgraph.cisco.*, shape=mxgraph.cisco19.*)
- Generic network shapes (server, router, switch, firewall, cloud, database)
- AWS/Azure/GCP cloud architecture shapes (shape=mxgraph.aws4.*, mxgraph.azure.*, mxgraph.gcp2.*)
- Network topology patterns (star, ring, mesh, bus)
- Zone/segment boundaries (dashed containers)
- Rack diagram patterns
- IP addressing labels on connections
- Complete network diagram XML example (LAN topology with router, switch, servers)

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 8)

**Key rules to encode:**
- ALWAYS use the correct stencil namespace (mxgraph.cisco19 for modern Cisco icons)
- ALWAYS use containers for network zones/segments
- Network connections typically use straight lines (no edgeStyle) or orthogonal
- Label connections with protocol/port info where relevant
```

---

### Batch B5.6 — Complex Impl Skills (Part 2)

#### Agent 16: drawio-impl-architecture

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-architecture}

**Scope:**
- C4 model implementation:
  - System Context (person, system, external system)
  - Container diagram (web app, API, database, message bus)
  - Component diagram
  - Color conventions (blue=#438DD5 for internal, gray=#999999 for external)
- Cloud architecture with stencils:
  - AWS (shape=mxgraph.aws4.*): compute, storage, database, networking
  - Azure (shape=mxgraph.azure.*): app services, VMs, databases
  - GCP (shape=mxgraph.gcp2.*): compute engine, cloud functions
- Deployment diagrams (nested containers for environments)
- Complete C4 system context XML example

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 3)

**Key rules to encode:**
- C4 diagrams: ALWAYS use the blue/gray color convention
- Cloud stencils: ALWAYS verify the exact shape name exists in the stencil library
- NEVER mix cloud provider stencils in the same architecture view
- Use containers for architectural boundaries (system boundary, deployment zone)
```

#### Agent 17: drawio-impl-bpmn

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-bpmn}

**Scope:**
- BPMN 2.0 elements:
  - Events: start (circle), intermediate (double circle), end (bold circle)
  - Event types: none, message, timer, error, signal, conditional, terminate
  - Activities: task (rounded rect), subprocess (rounded rect + marker)
  - Gateways: exclusive (X), parallel (+), inclusive (O), event-based (pentagon)
- Pools and lanes (swimlane containers for participants)
- Sequence flows (solid arrows) vs message flows (dashed arrows)
- Data objects and data stores
- BPMN shape styles in Draw.io (shape=mxgraph.bpmn.*)
- Complete BPMN process XML example (start → tasks → gateway → end)

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 5)

**Key rules to encode:**
- ALWAYS use the correct BPMN shape for each element type
- ALWAYS use solid lines for sequence flows, dashed for message flows
- Gateway shapes: exclusive=X marker, parallel=+ marker, inclusive=O marker
- Pools MUST contain at least one lane
```

#### Agent 18: drawio-impl-uml

```
{COMMON PREAMBLE with CATEGORY=impl, SKILL-NAME=drawio-impl-uml}

**Scope:**
- Class diagrams:
  - 3-compartment class shape (name, attributes, methods)
  - Swimlane with childLayout=stackLayout for compartments
  - 6 connector types: association, aggregation, composition, dependency, realization, generalization
  - Arrow styles for each (open, diamond, diamondThin, block, dash)
- Sequence diagrams:
  - Lifelines (dashed vertical lines)
  - Synchronous messages (solid arrow), asynchronous (open arrow), return (dashed)
  - Activation bars (thin rectangles on lifelines)
- Use case diagrams (actor + ellipse use cases + system boundary)
- State machine diagrams (rounded rectangles, start/end markers)
- Activity diagrams (similar to flowcharts but with fork/join bars)

**Research document:** docs/research/vooronderzoek-drawio-diagrams.md (section 6)

**Key rules to encode:**
- Class diagrams: ALWAYS use swimlane+stackLayout for 3-compartment shapes
- UML associations: aggregation=open diamond (endFill=0), composition=filled diamond (endFill=1)
- Generalization arrow: block arrow with endFill=0 (open triangle)
- NEVER use generic arrows for UML relationships — each has a specific style
```

---

### Batch B5.7 — Error Skills

#### Agent 19: drawio-errors-xml

```
{COMMON PREAMBLE with CATEGORY=errors, SKILL-NAME=drawio-errors-xml}

**Scope:**
- XML structure errors:
  - Missing required cells (id=0, id=1)
  - Duplicate cell IDs
  - Broken parent references (parent="nonexistent")
  - Invalid nesting (edge inside edge, diagram inside diagram)
- Style string errors:
  - Invalid property names (stroke-color vs strokeColor)
  - Invalid property values (color names vs hex)
  - Missing semicolons
  - Missing html=1
- HTML escaping errors in labels (&, <, > not escaped)
- Compression/encoding issues (trying to edit compressed XML)
- Common AI generation errors (inventing non-existent shapes, wrong attribute names)
- Diagnostic decision tree (symptom → likely cause → fix)

**Research documents:**
- docs/research/vooronderzoek-drawio-xml.md (all sections)
- docs/research/vooronderzoek-drawio-styles.md (section 11)

**Key rules to encode:**
- Error: "Diagram doesn't render" → CHECK: id=0 and id=1 cells exist
- Error: "Shape looks wrong" → CHECK: perimeter matches shape type
- Error: "Labels don't show HTML" → CHECK: html=1 in style
- Error: "Connection routes incorrectly" → CHECK: edgeStyle value is valid
```

#### Agent 20: drawio-errors-rendering

```
{COMMON PREAMBLE with CATEGORY=errors, SKILL-NAME=drawio-errors-rendering}

**Scope:**
- Visual rendering issues:
  - Shapes invisible (fillColor=none + strokeColor=none, opacity=0)
  - Wrong connection routing (missing/wrong perimeter, incorrect edgeStyle)
  - Labels truncated or overlapping (overflow, whiteSpace, width issues)
  - Container resize issues (children outside bounds, negative coordinates)
  - Font rendering (fontFamily not available, fontStyle bitfield wrong)
- Layout issues:
  - Overlapping shapes (same coordinates)
  - Edges crossing unnecessarily (wrong edgeStyle choice)
  - Swimlane children misaligned (absolute vs relative coordinates)
- Export-specific issues:
  - SVG rendering differences from editor
  - PNG resolution and background color
- Diagnostic decision tree for each issue type

**Research documents:**
- docs/research/vooronderzoek-drawio-styles.md (sections 3, 4, 7, 11)
- docs/research/vooronderzoek-drawio-diagrams.md (anti-patterns from all sections)

**Key rules to encode:**
- Invisible shape → CHECK: fillColor, strokeColor, opacity values
- Connection misrouting → CHECK: perimeter matches shape, edgeStyle is valid
- Children outside container → CHECK: using relative coordinates, not absolute
- Label overflow → CHECK: whiteSpace=wrap, overflow settings
```

---

### Batch B5.8 — Agent Skills

#### Agent 21: drawio-agents-diagram-generator

```
{COMMON PREAMBLE with CATEGORY=agents, SKILL-NAME=drawio-agents-diagram-generator}

**Scope:**
- Decision tree: User request → Diagram type selection
  - Process/workflow → flowchart or BPMN
  - Organization/hierarchy → org chart or mind map
  - Software design → architecture, UML, or ER
  - Network/infrastructure → network diagram
  - Lanes/departments → swimlanes
- Skill routing: Diagram type → Which skill to load
- XML generation pipeline:
  1. Parse user intent
  2. Select diagram type
  3. Load appropriate impl skill
  4. Generate mxGraph XML
  5. Validate with drawio-agents-code-validator
- MCP tool integration:
  - Use open_drawio_xml to preview generated diagrams
  - Use drawio-mcp-server for iterative editing
- Template selection guidance (when to start from template vs from scratch)

**Key rules to encode:**
- ALWAYS ask clarifying questions if diagram type is ambiguous
- ALWAYS validate generated XML before presenting to user
- ALWAYS generate uncompressed XML
- ALWAYS offer to open the diagram in Draw.io editor after generation
- Decision tree MUST cover all 11 diagram types
```

#### Agent 22: drawio-agents-code-validator

```
{COMMON PREAMBLE with CATEGORY=agents, SKILL-NAME=drawio-agents-code-validator}

**Scope:**
- Multi-stage validation pipeline:
  1. **XML Well-formedness**: Valid XML, proper nesting
  2. **Structure Check**: Required cells (id=0, id=1), valid hierarchy
  3. **ID Uniqueness**: No duplicate IDs across entire diagram
  4. **Parent-Child Integrity**: All parent references resolve, no orphans
  5. **Style Validation**: Known property names, valid values, html=1 present
  6. **Geometry Check**: Vertices have width/height, edges have relative=1
  7. **Connection Validation**: source/target reference existing cells, edge routing valid
  8. **Perimeter Check**: Shape-perimeter consistency
- Error reporting format (severity, location, description, fix suggestion)
- Auto-fix capabilities (what can be corrected automatically)
- Integration with drawio-errors-xml and drawio-errors-rendering skills

**Key rules to encode:**
- ALWAYS run ALL 8 validation stages (never skip)
- Report errors in order of severity (structural → style → cosmetic)
- For each error: provide the fix, not just the diagnosis
- NEVER accept XML that fails stages 1-4 (structural errors are blocking)
- Stages 5-8 produce warnings, not blocking errors
```

---

## 5. Post-Refinement Notes

### What Changed from Raw Masterplan
1. Batch size capped at 3 (was 3-4 in raw plan)
2. 8 batches instead of 6 (more granular quality gates)
3. Added YAML frontmatter fields (license, compatibility, metadata)
4. Directory structure aligned with WORKFLOW standard (skills/source/)
5. Complete agent prompts for all 22 skills
6. Decision R-006: topic research via inline WebFetch (no separate B4 phase)

### Quality Gate Checklist (apply after EVERY batch)
1. [ ] All files exist (SKILL.md + references/)
2. [ ] YAML frontmatter valid (name, description with `>`, license, compatibility, metadata)
3. [ ] SKILL.md < 500 lines
4. [ ] English-only content
5. [ ] Deterministic language (grep for "might", "consider", "should", "often", "usually")
6. [ ] All XML examples are well-formed
7. [ ] References linked from SKILL.md
8. [ ] Sources traceable to SOURCES.md
