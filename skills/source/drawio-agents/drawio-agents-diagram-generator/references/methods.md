# Methods Reference: Diagram Generator Agent

Complete reference for the generation pipeline methods, decision algorithms, and orchestration patterns.

---

## 1. Intent Parsing Method

### Input Analysis

Extract these properties from the user's natural language description:

| Property | How to Extract | Example |
|----------|---------------|---------|
| Subject matter | The primary noun or domain | "login process" -> process |
| Relationships | Verbs connecting subjects | "connects to", "reports to", "flows into" |
| Hierarchy | Parent-child or containment language | "under", "within", "part of" |
| Flow direction | Sequential or temporal language | "then", "next", "after", "first" |
| Explicit type | Direct diagram type mention | "flowchart", "ER diagram", "network map" |
| Actor count | Number of distinct roles or departments | "sales team and engineering" -> 2 actors |
| Formality level | Business process vs informal sketch | "BPMN compliant" vs "quick sketch" |

### Keyword-to-Type Mapping

These keywords provide strong signals for diagram type:

```
FLOWCHART signals:
  flow, process, steps, algorithm, decision, if/then, workflow,
  procedure, sequence of steps, logic

SWIMLANE signals:
  lanes, departments, roles, responsibilities, handoff, cross-functional,
  who does what, multi-team, approval chain

BPMN signals:
  business process, BPMN, events, gateways, pools, message flow,
  timer event, exclusive gateway, parallel gateway

ARCHITECTURE signals:
  system, service, microservice, API, cloud, AWS, Azure, GCP,
  infrastructure, deployment, container, server, load balancer

UML signals:
  class, object, sequence, use case, activity, state machine, component,
  interface, inheritance, abstract, method, attribute

ER DIAGRAM signals:
  entity, relationship, table, column, primary key, foreign key,
  one-to-many, many-to-many, database schema, cardinality

MINDMAP / ORG CHART signals:
  org chart, hierarchy, team structure, reporting, mindmap, brainstorm,
  central topic, branches, tree, organization

NETWORK signals:
  network, topology, router, switch, firewall, server rack, VLAN,
  subnet, IP, LAN, WAN, devices

CSV IMPORT signals:
  CSV, spreadsheet, table data, bulk, import from file, tabular

MERMAID CONVERSION signals:
  Mermaid, convert from Mermaid, mermaid syntax, mermaid code

TEMPLATE signals:
  template, starting point, predefined, standard layout
```

---

## 2. Type Selection Method

### Confidence Scoring

For each candidate diagram type, assign a confidence score:

```
STRONG match (score: 3):
  User explicitly names the diagram type.
  Example: "Create a BPMN diagram" --> BPMN = 3

MEDIUM match (score: 2):
  User's description contains 2+ keywords for a type.
  Example: "Show the approval across departments" --> swimlanes = 2

WEAK match (score: 1):
  User's description contains 1 keyword for a type.
  Example: "Visualize the system" --> architecture = 1, network = 1

SELECTION RULE:
  If highest score >= 3 --> Select that type immediately.
  If highest score == 2 AND only one type scores 2 --> Select that type.
  If highest score == 2 AND multiple types score 2 --> ASK the user.
  If highest score <= 1 --> ASK the user.
```

### Disambiguation Prompt Template

When asking the user to clarify, use this format:

```
Your request could be represented as:
1. **[Type A]** — Best for [use case description].
2. **[Type B]** — Best for [use case description].
3. **[Type C]** — Best for [use case description].

Which type fits your needs? (Or describe what you want in more detail.)
```

---

## 3. Skill Loading Method

### Loading Sequence

When the diagram type is confirmed:

1. Load the primary implementation skill (from the Skill Routing Table).
2. ALWAYS also have `drawio-core-xml-format` rules in mind for structural validity.
3. Load supporting skills only when specific features are needed.

### Implementation Skill Interface

Every implementation skill provides:

| Component | Purpose |
|-----------|---------|
| Shape Reference Table | Style strings for all shapes in this diagram type |
| Color Conventions | Standard fill/stroke colors for shape categories |
| Connection Patterns | Edge styles and routing for this diagram type |
| Layout Strategy | Coordinate calculation method for positioning shapes |
| Complete Example | Full XML example demonstrating all features |
| Validation Checklist | Type-specific validation rules |

---

## 4. XML Generation Method

### Step-by-Step Construction

Build the XML in this order:

```
1. Write the <mxGraphModel> opening tag.
2. Write <root>.
3. Write <mxCell id="0" /> (root cell).
4. Write <mxCell id="1" parent="0" /> (default layer).
5. For each shape in the diagram:
   a. Assign a unique, descriptive ID.
   b. Look up the style string from the implementation skill.
   c. Calculate x, y position using the layout strategy.
   d. Set width and height from the skill's dimension recommendations.
   e. Write the <mxCell> element with <mxGeometry>.
6. For each connection:
   a. Assign a unique edge ID (e.g., e1, e2).
   b. Set source and target to valid cell IDs.
   c. Apply the skill's edge style.
   d. Add labels where required (decision branches).
   e. Write the edge <mxCell> with <mxGeometry relative="1">.
7. Close </root> and </mxGraphModel>.
```

### Position Calculation Algorithm

For top-to-bottom layout (most common):

```
Constants:
  GRID_SIZE = 10
  VERTICAL_SPACING = 40
  HORIZONTAL_CENTER = 260  (for shapes ~120px wide)
  BRANCH_OFFSET = 200      (horizontal distance for alternate branches)

For each shape in sequence:
  x = HORIZONTAL_CENTER - (shape_width / 2)
  y = previous_shape_y + previous_shape_height + VERTICAL_SPACING
  Snap to grid: x = round(x / GRID_SIZE) * GRID_SIZE
                 y = round(y / GRID_SIZE) * GRID_SIZE

For branch shapes (e.g., "No" path from a decision):
  x = HORIZONTAL_CENTER + BRANCH_OFFSET
  y = decision_y  (same vertical level as the decision)
```

For left-to-right layout:

```
Constants:
  HORIZONTAL_SPACING = 60
  VERTICAL_CENTER = 200

For each shape in sequence:
  x = previous_shape_x + previous_shape_width + HORIZONTAL_SPACING
  y = VERTICAL_CENTER - (shape_height / 2)

For branch shapes:
  x = decision_x  (same horizontal level)
  y = VERTICAL_CENTER + BRANCH_OFFSET
```

---

## 5. Validation Method

### Programmatic Validation Steps

For each generated diagram, execute these checks in order:

```
CHECK 1: XML Well-Formedness
  Parse the XML string. If parsing fails --> FIX malformed tags.

CHECK 2: Structural Cells
  Verify <mxCell id="0" /> exists.
  Verify <mxCell id="1" parent="0" /> exists.
  If missing --> ADD the missing cell(s).

CHECK 3: ID Uniqueness
  Collect all id attributes into a set.
  If set size < total count --> FIND and RENAME duplicate IDs.

CHECK 4: Reference Integrity
  For each edge cell, verify source ID exists in the cell set.
  For each edge cell, verify target ID exists in the cell set.
  For each cell with parent != "0" and parent != "1", verify parent ID exists.
  If broken reference --> FIX the reference or REMOVE the orphaned edge.

CHECK 5: Style Completeness
  For each vertex cell, verify style contains "whiteSpace=wrap;html=1;".
  For each style string, verify it ends with ";".
  If incomplete --> ADD missing style properties.

CHECK 6: Geometry Validity
  For each vertex, verify x >= 0 and y >= 0.
  For each pair of vertices, verify no overlap.
  For each edge, verify mxGeometry has relative="1".
  If invalid --> ADJUST coordinates.
```

---

## 6. MCP Integration Method

### Using open_drawio_xml

After validation, call the MCP tool with the complete XML string:

```
1. Take the final validated XML output.
2. Call the open_drawio_xml tool with the XML as input.
3. The diagram opens in the user's default Draw.io editor.
4. Report success or handle errors.
```

### Using drawio-mcp-server for Editing

For iterative editing after generation:

```
1. Generate the initial diagram via the pipeline.
2. Use drawio-mcp-server CRUD operations to modify individual cells.
3. Available operations: create, read, update, delete shapes and edges.
4. Access the visual editor at http://localhost:3000/.
```

### Using Mermaid/CSV Conversion

For non-XML source formats:

```
Mermaid input:
  1. Take the Mermaid syntax from the user.
  2. Call open_drawio_mermaid with the Mermaid string.
  3. The MCP server converts and opens the diagram.

CSV input:
  1. Take the CSV data from the user.
  2. Call open_drawio_csv with the CSV string.
  3. The MCP server converts and opens the diagram.
```
