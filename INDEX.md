# Draw.io Skill Package — Skill Index

> 22 deterministic skills for Draw.io / diagrams.net diagram generation with Claude.
> Each skill is self-contained, English-only, and follows ALWAYS/NEVER deterministic language.

---

## Skills by Category

### Core (3 skills) — Foundation knowledge

These skills define the fundamental concepts every other skill builds on: XML format, style system, and coordinate geometry.

| # | Skill | Path | Description | Lines |
|---|-------|------|-------------|-------|
| 1 | [drawio-core-xml-format](skills/source/drawio-core/drawio-core-xml-format/) | `core/` | mxGraph XML hierarchy (mxfile > diagram > mxGraphModel > root), required structural cells (id="0" and id="1"), vertex vs edge cells, mxGeometry basics, HTML labels, UserObject metadata, and compression rules. Prevents the #1 AI mistake: generating compressed XML. | 264 |
| 2 | [drawio-core-styles](skills/source/drawio-core/drawio-core-styles/) | `core/` | Style string syntax (semicolon-delimited key=value pairs), property categories (fill, stroke, text, shape, edge, container, behavior), color system (#RRGGBB hex only), fontStyle bitfield (1=bold, 2=italic, 4=underline, 8=strikethrough), perimeter-shape matching rules, and style inheritance/defaults. | 320 |
| 3 | [drawio-core-geometry](skills/source/drawio-core/drawio-core-geometry/) | `core/` | Screen coordinate system (origin top-left, Y increases downward), vertex geometry (absolute x/y/width/height), edge geometry (relative="1", label positioning with x=-1..1), waypoints, container-relative coordinates, collapsible containers with alternateBounds, connection points (exitX/Y, entryX/Y in 0-1 range), and label positioning rules. | 293 |

---

### Syntax (4 skills) — How to write mxGraph XML

These skills cover the mechanics of constructing cells, connections, style strings, and metadata in mxGraph XML.

| # | Skill | Path | Description | Lines |
|---|-------|------|-------------|-------|
| 4 | [drawio-syntax-cells](skills/source/drawio-syntax/drawio-syntax-cells/) | `syntax/` | mxCell creation for vertices (vertex="1") and edges (edge="1"), UserObject/object wrappers for custom metadata, HTML labels with XML escaping, placeholder variable substitution (%variable%), groups vs containers (container=1), collapsible swimlanes, layer cells (parent="0"), and coordinate rules for container children. | 491 |
| 5 | [drawio-syntax-connections](skills/source/drawio-syntax/drawio-syntax-connections/) | `syntax/` | Floating vs fixed connections (exitX/Y, entryX/Y), 8 edge routing algorithms (orthogonal, elbow, entityRelation, segment, sideToSide, topToBottom, loop, isometric), waypoint syntax, self-loops, custom connection points, edge label positioning, multiple labels per edge, 21 arrow types with fill behavior, and UML arrow patterns. | 344 |
| 6 | [drawio-syntax-styles](skills/source/drawio-syntax/drawio-syntax-styles/) | `syntax/` | Complete catalog of 120+ style properties organized by category, 16 built-in primitive shapes with perimeter requirements, 19 extended shapes, stencil library format (shape=mxgraph.*), 21 arrow types, 7 edge routing algorithms, sketch/hand-drawn mode properties (jiggle, fillStyle, hachureGap), and cross-reference decision tree for finding the right property. | 244 |
| 7 | [drawio-syntax-metadata](skills/source/drawio-syntax/drawio-syntax-metadata/) | `syntax/` | Multi-page diagrams (mxfile > multiple diagram elements), layer system (cells with parent="0"), custom properties via object wrapper, file-level variables (vars attribute with single-quoted JSON), placeholder resolution order (cell > parent > ancestor > layer > root > file), predefined placeholders (%date%, %page%, %filename%), tooltips, external and internal page links, and MathJax/LaTeX support (math="1", $$...$$ delimiters). | 447 |

---

### Implementation (11 skills) — Diagram type recipes

Each implementation skill provides complete, ready-to-use patterns for a specific diagram type: shapes, styles, connections, layout strategy, and a working XML example.

| # | Skill | Path | Description | Lines |
|---|-------|------|-------------|-------|
| 8 | [drawio-impl-flowcharts](skills/source/drawio-impl/drawio-impl-flowcharts/) | `impl/` | ISO 5807 flowchart shapes (process=rectangle, decision=rhombus, terminator=rounded arcSize=50, data=parallelogram, document, predefined process, manual input, preparation=hexagon, database=cylinder3), color conventions per shape type, decision branch labeling rules, top-to-bottom and left-to-right layout strategies, and a complete order processing example with 12 shapes. | 311 |
| 9 | [drawio-impl-swimlanes](skills/source/drawio-impl/drawio-impl-swimlanes/) | `impl/` | Pool/lane container hierarchy (pool > lane > shapes), container-relative coordinate system, pool style (shape=table with childLayout=tableLayout), lane style (swimlane with startSize), horizontal vs vertical orientation, header sizing, lane geometry calculation (width matches pool, heights sum to pool height minus startSize), cross-lane edge routing (parent=pool), nested lanes, and a 3-lane order processing example. | 327 |
| 10 | [drawio-impl-er-diagrams](skills/source/drawio-impl/drawio-impl-er-diagrams/) | `impl/` | Entity table shapes (shape=table with childLayout=tableLayout), attribute rows as child cells, PK notation (fontStyle=4 underline), FK notation (fontStyle=2 italic), all 6 crow's foot cardinality markers (ERone, ERmany, ERmandOne, ERzeroToOne, ERoneToMany, ERzeroToMany), entityRelationEdgeStyle, startFill=0/endFill=0 requirement, entity color conventions, and a 3-entity e-commerce example with relationships. | 274 |
| 11 | [drawio-impl-bpmn](skills/source/drawio-impl/drawio-impl-bpmn/) | `impl/` | BPMN 2.0 elements using shape=mxgraph.bpmn.shape: events (standard/catching/throwing/end with symbol variants), activities (tasks with type markers: user, service, script, send, receive), gateways (exclusive/parallel/inclusive/event-based), pools and lanes, sequence flows (solid) vs message flows (dashed) vs associations, data objects and stores, and an invoice processing example. | 260 |
| 12 | [drawio-impl-uml](skills/source/drawio-impl/drawio-impl-uml/) | `impl/` | Five UML diagram types: class diagrams (3-compartment swimlane with stackLayout, visibility prefixes, separator lines), sequence diagrams (umlLifeline with lifelinePerimeter, activation bars, message types), use case diagrams (umlActor, system boundary container), state machines (initial/final states, transitions), activity diagrams (fork/join bars). All 7 UML relationship arrow styles with exact style strings. | 399 |
| 13 | [drawio-impl-architecture](skills/source/drawio-impl/drawio-impl-architecture/) | `impl/` | C4 model diagrams (system context, container, component) with exact color conventions (Person=#08427b, System=#1168bd, External=#999999), three-line label format, cloud architecture stencils for AWS (mxgraph.aws4.* with resourceIcon/resIcon pattern), Azure (mxgraph.azure.*), and GCP (mxgraph.gcp2.*), AWS group containers (region/VPC/subnet), deployment diagram pattern with nested cube containers, and a complete C4 system context example. | 304 |
| 14 | [drawio-impl-network](skills/source/drawio-impl/drawio-impl-network/) | `impl/` | Network topology diagrams with Cisco cisco19 stencils (router, switch, firewall, server, AP, laptop), AWS/Azure/GCP cloud stencils, bidirectional physical links (endArrow=none), zone boundaries (DMZ=red, LAN=green, WAN=blue, Management=orange), topology patterns (star, ring, mesh, three-tier), rack diagrams (1U=20px), AWS architecture nesting (Region > VPC > Subnet), IP address labeling with object wrappers, and a complete LAN topology example. | 376 |
| 15 | [drawio-impl-mindmaps](skills/source/drawio-impl/drawio-impl-mindmaps/) | `impl/` | Mind map anatomy (central topic, main branches, sub-branches, leaf nodes), curved connectors (curved=1, endArrow=none), 3-level size hierarchy (largest center, medium branches, small leaves), color coding strategy (6 branch color families), radial layout pattern with positioning reference, concept map variant (labeled directed edges), Draw.io tree layout integration, and a complete 3-branch mind map example. | 405 |
| 16 | [drawio-impl-csv-import](skills/source/drawio-impl/drawio-impl-csv-import/) | `impl/` | Draw.io CSV import format: directive lines (# label, # style, # connect, # identity, # namespace, # layout, # ignore, # width/height, # padding/nodespacing/levelspacing), conditional styling with stylename/styles, column references (%columnName%), connect directive JSON format (from/to/invert/label/style), line continuation with backslash, 5 layout algorithms (auto, verticalTree, horizontalTree, organic, circle), and complete org chart, flowchart, and network examples. | 336 |
| 17 | [drawio-impl-mermaid-conversion](skills/source/drawio-impl/drawio-impl-mermaid-conversion/) | `impl/` | Mermaid-to-Draw.io conversion via open_drawio_mermaid MCP tool. Critical limitation: conversion produces a SINGLE compound shape (grouped SVG), NOT individual mxCells. Decision tree for Mermaid vs native XML, 13 supported Mermaid diagram types, syntax quick reference for flowchart/sequence/class/state/ER/gantt/mindmap, workarounds for the compound shape limitation, and conversion methods (MCP, URL parameter, UI, embed mode). | 260 |
| 18 | [drawio-impl-templates](skills/source/drawio-impl/drawio-impl-templates/) | `impl/` | Template XML structure (mxfile wrapper with diagram/mxGraphModel), 15 built-in template categories (150+ templates), template modification pattern (keep structure, swap content), custom template creation checklist, semantic cell IDs, placeholder text convention ([Placeholder]), page size reference (A4/Letter), color scheme reference, MCP integration via open_drawio_xml, and complete flowchart and org chart template examples. | 452 |

---

### Errors (2 skills) — Diagnosis and anti-patterns

These skills provide systematic diagnostic approaches for when diagrams fail to render or look wrong.

| # | Skill | Path | Description | Lines |
|---|-------|------|-------------|-------|
| 19 | [drawio-errors-xml](skills/source/drawio-errors/drawio-errors-xml/) | `errors/` | Symptom-to-root-cause decision tree for XML-level errors. 19 cataloged error types (E-001 through E-019): malformed XML, missing structural cells, duplicate IDs, compression issues, broken parent references, missing html=1, double escaping, missing XML escaping, perimeter mismatch, true/false instead of 1/0, missing whiteSpace=wrap, style syntax errors, missing relative="1", arrow configuration errors, vertex/edge style confusion, missing container=1, absolute vs relative coordinates, and nonexistent shape names. Top 5 AI generation mistakes ranked by frequency. | 434 |
| 20 | [drawio-errors-rendering](skills/source/drawio-errors/drawio-errors-rendering/) | `errors/` | Symptom-based diagnostic for visual rendering issues in 7 categories: invisible shapes (transparent fill/stroke, zero opacity/dimensions, off-canvas, collapsed parent), wrong connection routing (perimeter mismatch, exitX/Y values outside 0-1, stale waypoints), label problems (truncated, overlapping, missing, detached), container/child layout issues, font rendering (fontStyle bitmask, safe fonts), export-specific problems (SVG/PNG/PDF), and shape overlap/alignment. Quick fix reference table for 15 common symptoms. | 431 |

---

### Agents (2 skills) — Intelligent orchestration

These skills orchestrate the other skills, providing pipelines for diagram generation and validation.

| # | Skill | Path | Description | Lines |
|---|-------|------|-------------|-------|
| 21 | [drawio-agents-diagram-generator](skills/source/drawio-agents/drawio-agents-diagram-generator/) | `agents/` | Central orchestrator for natural language to Draw.io diagram generation. 5-step pipeline: parse intent, select diagram type (comprehensive decision tree), load implementation skill (routing table for all 11 impl skills), generate XML (mandatory structure, cell ID rules, style rules, geometry rules, label rules), and validate output. Handles ambiguity resolution, template selection, multi-page diagrams, mixed diagram types, and MCP tool integration (open_drawio_xml, open_drawio_mermaid, open_drawio_csv). | 402 |
| 22 | [drawio-agents-code-validator](skills/source/drawio-agents/drawio-agents-code-validator/) | `agents/` | 8-stage validation pipeline for mxGraph XML. Stages 1-4 are BLOCKING: XML well-formedness (tag closure, nesting, attribute quoting, special characters), structure check (root cell, default layer, document wrapper), ID uniqueness (cross-page, reserved IDs), parent-child integrity (parent exists, no circular refs). Stages 5-8 are WARNINGS: style validation (120+ known properties, valid shape names), geometry check (vertex dimensions, edge relative="1"), connection validation (source/target exist, valid arrow names), perimeter check. Auto-fix capabilities for each stage. Standardized error report format. | 408 |

---

## Totals

| Category | Skills | Total Lines |
|----------|--------|-------------|
| Core | 3 | 877 |
| Syntax | 4 | 1,526 |
| Implementation | 11 | 3,694 |
| Errors | 2 | 865 |
| Agents | 2 | 810 |
| **Total** | **22** | **7,772** |

---

## Skill Dependencies

```
agents/diagram-generator ──> ALL impl/* skills (routes by diagram type)
agents/diagram-generator ──> agents/code-validator (post-generation validation)
agents/code-validator    ──> errors/xml (references E-001..E-019 error codes)

impl/* skills            ──> core/xml-format (file structure)
impl/* skills            ──> core/styles (style string syntax)
impl/* skills            ──> core/geometry (coordinate system)
impl/* skills            ──> syntax/connections (edge routing)

syntax/cells             ──> core/xml-format (mxCell attributes)
syntax/connections       ──> core/geometry (waypoints, connection points)
syntax/styles            ──> core/styles (property reference)
syntax/metadata          ──> core/xml-format (multi-page structure)

errors/rendering         ──> core/styles (style diagnostics)
errors/rendering         ──> core/geometry (coordinate diagnostics)
errors/xml               ──> core/xml-format (structure validation)
```

---

## How to Use This Package

1. **Generating a diagram from a description:** Start with `drawio-agents-diagram-generator` (skill #21). It routes to the correct implementation skill automatically.

2. **Building a specific diagram type:** Go directly to the relevant `impl/` skill (skills #8-18). Each contains complete shape styles, connection patterns, and working examples.

3. **Looking up a style property or shape name:** Use `drawio-syntax-styles` (skill #6) for the complete 120+ property catalog, or `drawio-core-styles` (skill #2) for style string syntax rules.

4. **Debugging a broken diagram:** Start with `drawio-errors-xml` (skill #19) for XML-level errors, or `drawio-errors-rendering` (skill #20) for visual rendering issues.

5. **Validating generated XML:** Use `drawio-agents-code-validator` (skill #22) to run the 8-stage validation pipeline.

---

**Version:** 1.0 — All 22 skills complete and validated.
