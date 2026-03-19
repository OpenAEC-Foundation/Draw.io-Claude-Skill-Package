# Vooronderzoek: Draw.io Diagram Types — Complete Technical Reference

> Onderzocht op 2026-03-19. Bronnen: drawio.com/doc/faq/ai-drawio-generation, drawio.com/doc/faq/drawio-style-reference, drawio.com/blog (crows-foot-notation, uml-overview, process-map-flowchart), jgraph/drawio GitHub repository.
>
> **Verwerkt:** Nee

---

## Table of Contents

1. [Flowcharts](#1-flowcharts)
2. [Swimlane / Lane Diagrams](#2-swimlane--lane-diagrams)
3. [Software Architecture (C4, Component, Deployment)](#3-software-architecture)
4. [ER Diagrams](#4-er-diagrams)
5. [BPMN 2.0](#5-bpmn-20)
6. [UML Diagrams](#6-uml-diagrams)
7. [Mind Maps](#7-mind-maps)
8. [Network Diagrams](#8-network-diagrams)
9. [Org Charts](#9-org-charts)
10. [Venn Diagrams](#10-venn-diagrams)
11. [Infographics / Timelines](#11-infographics--timelines)
12. [Common Patterns Across Diagram Types](#12-common-patterns-across-diagram-types)
13. [Shape Libraries and Stencils](#13-shape-libraries-and-stencils)

---

## 1. Flowcharts

Flowcharts follow ISO 5807 standards. Draw.io provides all standard flowchart shapes in the General and Flowchart shape libraries.

### Standard Shapes

| Shape | Style Key | Purpose |
|-------|-----------|---------|
| Process | `rounded=0;whiteSpace=wrap;html=1;` | Standard task/step (rectangle) |
| Decision | `rhombus;whiteSpace=wrap;html=1;` | Yes/No branch (diamond) |
| Terminator | `rounded=1;whiteSpace=wrap;html=1;arcSize=50;` | Start/End (stadium shape) |
| Data (I/O) | `shape=parallelogram;whiteSpace=wrap;html=1;` | Input/output (rhomboid) |
| Document | `shape=document;whiteSpace=wrap;html=1;` | Document output (wavy bottom) |
| Predefined Process | `shape=process;whiteSpace=wrap;html=1;` | Subprocess reference (double-barred rectangle) |
| Manual Input | `shape=manualInput;whiteSpace=wrap;html=1;` | User input (sloped top) |
| Preparation | `shape=hexagon;whiteSpace=wrap;html=1;` | Setup step |
| Database | `shape=cylinder3;whiteSpace=wrap;html=1;` | Data store |

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Start -->
    <mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Process step -->
    <mxCell id="step1" value="Process Order" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- Decision -->
    <mxCell id="dec1" value="Valid?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="200" y="220" width="120" height="80" as="geometry" />
    </mxCell>

    <!-- Data I/O -->
    <mxCell id="data1" value="Read Input" style="shape=parallelogram;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;" vertex="1" parent="1">
      <mxGeometry x="380" y="240" width="140" height="60" as="geometry" />
    </mxCell>

    <!-- End -->
    <mxCell id="end" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="200" y="340" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="endArrow=classic;html=1;" edge="1" parent="1" source="start" target="step1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=classic;html=1;" edge="1" parent="1" source="step1" target="dec1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" value="Yes" style="endArrow=classic;html=1;" edge="1" parent="1" source="dec1" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="No" style="endArrow=classic;html=1;" edge="1" parent="1" source="dec1" target="data1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Key Style Properties

- Decision branches ALWAYS use edge labels (`value="Yes"` / `value="No"`) on the connector `mxCell`.
- Terminators use `arcSize=50` to produce the stadium/pill shape.
- Edge routing defaults to `edgeStyle=orthogonalEdgeStyle` for clean right-angle connectors.

### Anti-Patterns

- NEVER use `ellipse` for start/end; use `rounded=1;arcSize=50` for ISO-compliant terminators.
- NEVER omit `whiteSpace=wrap;html=1;` — text will overflow and not wrap.
- NEVER hard-code waypoints on edges when orthogonal routing suffices; use `edgeStyle=orthogonalEdgeStyle` instead.

---

## 2. Swimlane / Lane Diagrams

Swimlanes use the `container=1` pattern where child cells have coordinates relative to the parent container.

### Horizontal vs. Vertical

| Orientation | Key Style Difference |
|-------------|---------------------|
| Horizontal lanes | `swimlane;horizontal=1;startSize=30;` (header on left, flow left-to-right) |
| Vertical lanes | `swimlane;horizontal=0;startSize=30;` (header on top, flow top-to-bottom) |

Note: `horizontal=0` on a swimlane means the **label** is horizontal but the lane stacks **vertically** — this is a common source of confusion. The `startSize` property controls the header band height/width.

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool (outer container) -->
    <mxCell id="pool1" value="Order Process" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="600" height="300" as="geometry" />
    </mxCell>

    <!-- Lane 1: Sales -->
    <mxCell id="lane1" value="Sales" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="30" width="600" height="130" as="geometry" />
    </mxCell>

    <!-- Task inside lane1 — coordinates relative to lane1 -->
    <mxCell id="task1" value="Receive Order" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="lane1">
      <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="task2" value="Validate Order" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane1">
      <mxGeometry x="220" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Lane 2: Warehouse -->
    <mxCell id="lane2" value="Warehouse" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="160" width="600" height="140" as="geometry" />
    </mxCell>

    <mxCell id="task3" value="Pick Items" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="lane2">
      <mxGeometry x="220" y="40" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Cross-lane connection -->
    <mxCell id="e1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task1" target="task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task2" target="task3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Critical Rules for Containers

- Child cells MUST set `parent="<container_id>"` — NEVER `parent="1"` when inside a swimlane.
- Child coordinates are ALWAYS relative to the container's top-left corner (after the header).
- Cross-lane edges MUST set `parent` to the common ancestor (the pool), NOT to one of the lanes.
- `container=1` MUST be present in the style for drag-and-drop children to work.
- `collapsible=0` prevents accidental lane collapse in the editor.
- `recursiveResize=0` on the pool prevents child lanes from auto-resizing when the pool resizes.

### Anti-Patterns

- NEVER place child elements with absolute page coordinates when they belong inside a container — they will render in the wrong position.
- NEVER set edge `parent` to a lane when the edge crosses lane boundaries.
- NEVER omit `container=1` from swimlane styles; without it, children will not move with the lane.

---

## 3. Software Architecture

### 3.1 C4 Model

Draw.io supports C4 diagrams through the `c4` shape library. The four levels are: System Context, Container, Component, and Code.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Person -->
    <mxCell id="person1" value="&lt;b&gt;Customer&lt;/b&gt;&lt;br&gt;[Person]&lt;br&gt;&lt;br&gt;Uses the web app to place orders" style="shape=mxgraph.c4.person2;whiteSpace=wrap;html=1;align=center;metaEdit=1;points=[[0.5,0,0],[1,0.5,0],[1,0.75,0],[0.75,1,0],[0.5,1,0],[0.25,1,0],[0,0.75,0],[0,0.5,0]];fillColor=#08427b;fontColor=#ffffff;strokeColor=#073763;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="200" y="20" width="200" height="180" as="geometry" />
    </mxCell>

    <!-- Software System -->
    <mxCell id="sys1" value="&lt;b&gt;E-Commerce System&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Handles orders, payments, inventory" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="150" y="280" width="300" height="150" as="geometry" />
    </mxCell>

    <!-- External System -->
    <mxCell id="ext1" value="&lt;b&gt;Payment Gateway&lt;/b&gt;&lt;br&gt;[External System]&lt;br&gt;&lt;br&gt;Processes credit card payments" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#999999;fontColor=#ffffff;strokeColor=#8A8A8A;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="520" y="280" width="240" height="150" as="geometry" />
    </mxCell>

    <!-- Relationships -->
    <mxCell id="r1" value="Places orders using" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="person1" target="sys1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r2" value="Sends payment requests to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="sys1" target="ext1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

**C4 Color Conventions:**
| Element | fillColor | fontColor |
|---------|-----------|-----------|
| Person | `#08427b` | `#ffffff` |
| Software System | `#1168bd` | `#ffffff` |
| External System | `#999999` | `#ffffff` |
| Container | `#438dd5` | `#ffffff` |
| Component | `#85bbf0` | `#000000` |

### 3.2 Component Diagram

```xml
<!-- Component with provided/required interfaces -->
<mxCell id="comp1" value="&lt;b&gt;Auth Service&lt;/b&gt;" style="shape=component;whiteSpace=wrap;html=1;align=center;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="160" height="80" as="geometry" />
</mxCell>

<!-- Provided interface (lollipop) -->
<mxCell id="iface1" value="IAuth" style="shape=lollipop;whiteSpace=wrap;html=1;direction=south;" vertex="1" parent="1">
  <mxGeometry x="160" y="70" width="40" height="30" as="geometry" />
</mxCell>
```

### 3.3 Deployment Diagram

```xml
<!-- Deployment node (nested containers) -->
<mxCell id="node1" value="&lt;b&gt;Production Server&lt;/b&gt;&lt;br&gt;Ubuntu 22.04" style="shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;verticalAlign=top;" vertex="1" parent="1">
  <mxGeometry x="80" y="60" width="300" height="200" as="geometry" />
</mxCell>

<!-- Artifact inside node -->
<mxCell id="art1" value="api-server.jar" style="shape=note;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="node1">
  <mxGeometry x="30" y="50" width="120" height="60" as="geometry" />
</mxCell>

<mxCell id="art2" value="PostgreSQL 15" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;size=10;" vertex="1" parent="node1">
  <mxGeometry x="170" y="40" width="100" height="80" as="geometry" />
</mxCell>
```

### Anti-Patterns

- NEVER mix C4 abstraction levels in a single diagram — each page MUST represent one level.
- NEVER omit the descriptive text in C4 elements; the format is ALWAYS: Name, [Type], Description.
- NEVER use arbitrary colors for C4 — follow the standard color conventions above.

---

## 4. ER Diagrams

Draw.io supports entity-relationship diagrams with crow's foot notation through the Entity Relation shape library.

### Cardinality Markers (Crow's Foot)

| Relationship | Source Arrow | Target Arrow | Meaning |
|-------------|-------------|--------------|---------|
| One-to-one (mandatory) | `ERone` | `ERone` | Exactly one on each side |
| One-to-many | `ERone` | `ERmany` | One source, many targets |
| Many-to-many | `ERmany` | `ERmany` | Many on both sides |
| Zero-or-one | `ERzeroToOne` | — | Optional single |
| Zero-or-many | `ERzeroToMany` | — | Optional multiple |
| One-or-many (mandatory) | `ERoneToMany` | — | At least one, possibly many |

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Entity: Customer -->
    <mxCell id="ent1" value="Customer" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="ent1_pk" value="customer_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent1">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="ent1_f1" value="name  VARCHAR(100)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent1">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="ent1_f2" value="email  VARCHAR(255)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent1">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Entity: Order -->
    <mxCell id="ent2" value="Order" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="380" y="80" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="ent2_pk" value="order_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent2">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="ent2_fk" value="customer_id  FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=2;" vertex="1" parent="ent2">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="ent2_f1" value="order_date  DATE" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent2">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="ent2_f2" value="total  DECIMAL(10,2)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent2">
      <mxGeometry y="120" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Relationship: Customer 1:N Order (crow's foot) -->
    <mxCell id="rel1" value="" style="edgeStyle=orthogonalEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent1" target="ent2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Key Style Properties for ER

- `startArrow=ERone;startFill=0;` — single line (one) at source.
- `endArrow=ERmany;endFill=0;` — crow's foot (many) at target.
- `endArrow=ERzeroToMany;endFill=0;` — circle + crow's foot (zero-to-many).
- `endArrow=ERoneToMany;endFill=0;` — line + crow's foot (one-to-many).
- Entity tables use `shape=table;startSize=30;container=1;childLayout=tableLayout;`.
- Primary keys use `fontStyle=4` (underline); foreign keys use `fontStyle=2` (italic).
- `edgeStyle=entityRelationEdgeStyle` provides the classic ER curved connector (alternative to orthogonal).

### Anti-Patterns

- NEVER use generic arrows (`endArrow=classic`) for ER diagrams — ALWAYS use `ER*` arrow types.
- NEVER place attribute rows outside the entity container — they MUST be children with `parent="<entity_id>"`.
- NEVER use `startFill=1` or `endFill=1` with ER arrows — crow's foot markers MUST use `Fill=0`.

---

## 5. BPMN 2.0

BPMN (Business Process Model and Notation) 2.0 is supported through the BPMN shape library. Draw.io implements the full BPMN 2.0 specification.

### BPMN Element Categories

| Category | Elements | Shape Prefix |
|----------|----------|-------------|
| Events | Start, Intermediate, End | `mxgraph.bpmn.shape` with `outline=` |
| Activities | Task, Subprocess | `mxgraph.bpmn.task` or rounded rectangle |
| Gateways | Exclusive, Parallel, Inclusive, Event-based | `mxgraph.bpmn.shape` with `outline=catching` |
| Flows | Sequence, Message, Association | Edge styles |
| Swimlanes | Pool, Lane | `swimlane` with BPMN styling |

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool -->
    <mxCell id="pool1" value="Invoice Processing" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="760" height="250" as="geometry" />
    </mxCell>

    <!-- Start Event (thin circle) -->
    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;symbol=general;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Task: Receive Invoice -->
    <mxCell id="task1" value="Receive&#xa;Invoice" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;" vertex="1" parent="pool1">
      <mxGeometry x="110" y="80" width="120" height="70" as="geometry" />
    </mxCell>

    <!-- Exclusive Gateway (X diamond) -->
    <mxCell id="gw1" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="270" y="85" width="50" height="50" as="geometry" />
    </mxCell>

    <!-- Task: Auto-Approve -->
    <mxCell id="task2" value="Auto-Approve" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;" vertex="1" parent="pool1">
      <mxGeometry x="370" y="30" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Task: Manual Review -->
    <mxCell id="task3" value="Manual Review" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;" vertex="1" parent="pool1">
      <mxGeometry x="370" y="140" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Parallel Gateway (+ diamond) -->
    <mxCell id="gw2" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=parallelGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="530" y="85" width="50" height="50" as="geometry" />
    </mxCell>

    <!-- Task: Process Payment -->
    <mxCell id="task4" value="Process&#xa;Payment" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;" vertex="1" parent="pool1">
      <mxGeometry x="620" y="80" width="100" height="70" as="geometry" />
    </mxCell>

    <!-- End Event (thick circle) -->
    <mxCell id="end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;symbol=terminate;outline=end;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="730" y="95" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Sequence Flows -->
    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task1" target="gw1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f3" value="≤ $1000" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw1" target="task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f4" value="&gt; $1000" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw1" target="task3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f5" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task2" target="gw2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f6" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task3" target="gw2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f7" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw2" target="task4">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f8" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task4" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### BPMN Gateway Symbols

| Gateway Type | Symbol Value | Meaning |
|-------------|-------------|---------|
| Exclusive (XOR) | `symbol=exclusiveGw` | One path only |
| Parallel (AND) | `symbol=parallelGw` | All paths simultaneously |
| Inclusive (OR) | `symbol=inclusiveGw` | One or more paths |
| Event-based | `symbol=eventGw` | Triggered by events |

### BPMN Event Types

| Event | outline | symbol | Visual |
|-------|---------|--------|--------|
| Start | `standard` | `general` | Thin circle |
| Intermediate catch | `catching` | `message`/`timer`/`signal` | Double thin circle |
| Intermediate throw | `throwing` | `message`/`signal` | Double thin circle, filled icon |
| End | `end` | `terminate`/`message`/`error` | Thick circle |

### Message Flow (between pools)

```xml
<mxCell id="mf1" value="" style="endArrow=open;endFill=0;startArrow=oval;startFill=0;dashed=1;html=1;strokeColor=#666666;" edge="1" parent="1" source="task_pool1" target="task_pool2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Anti-Patterns

- NEVER use solid lines for message flows — message flows MUST be dashed (`dashed=1`).
- NEVER connect elements across pools with sequence flows — use message flows instead.
- NEVER omit the pool container when modelling inter-organizational processes.
- NEVER use a generic diamond for gateways — ALWAYS use the correct BPMN gateway symbol.

---

## 6. UML Diagrams

Draw.io supports all 14 UML 2.5 diagram types through the UML and UML 2.5 shape libraries. Below are the most commonly generated types.

### 6.1 Class Diagram

Class diagrams use a three-compartment table structure: class name, attributes, operations.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Class: User -->
    <mxCell id="cls1" value="&lt;b&gt;User&lt;/b&gt;" style="swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="100" y="60" width="200" height="160" as="geometry" />
    </mxCell>
    <!-- Attributes compartment -->
    <mxCell id="cls1_attr" value="- id: int&#xa;- username: String&#xa;- email: String&#xa;- passwordHash: String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls1">
      <mxGeometry y="26" width="200" height="70" as="geometry" />
    </mxCell>
    <!-- Separator line -->
    <mxCell id="cls1_sep" value="" style="line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;strokeColor=#6c8ebf;" vertex="1" parent="cls1">
      <mxGeometry y="96" width="200" height="8" as="geometry" />
    </mxCell>
    <!-- Operations compartment -->
    <mxCell id="cls1_ops" value="+ login(password: String): bool&#xa;+ logout(): void&#xa;+ getProfile(): Profile" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls1">
      <mxGeometry y="104" width="200" height="56" as="geometry" />
    </mxCell>

    <!-- Class: Profile -->
    <mxCell id="cls2" value="&lt;b&gt;Profile&lt;/b&gt;" style="swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="400" y="60" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="cls2_attr" value="- bio: String&#xa;- avatar: URL" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls2">
      <mxGeometry y="26" width="200" height="40" as="geometry" />
    </mxCell>
    <mxCell id="cls2_sep" value="" style="line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;strokeColor=#82b366;" vertex="1" parent="cls2">
      <mxGeometry y="66" width="200" height="8" as="geometry" />
    </mxCell>
    <mxCell id="cls2_ops" value="+ updateBio(text: String): void" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls2">
      <mxGeometry y="74" width="200" height="46" as="geometry" />
    </mxCell>

    <!-- Association: User -> Profile (1:1) -->
    <mxCell id="assoc1" value="1                           1" style="endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="cls1" target="cls2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### UML Relationship Arrow Styles

| Relationship | startArrow | endArrow | dashed | endFill |
|-------------|-----------|----------|--------|---------|
| Association | none | none | 0 | — |
| Directed Association | none | open | 0 | 1 |
| Inheritance | none | block | 0 | 0 |
| Realization | none | block | 1 | 0 |
| Dependency | none | open | 1 | 1 |
| Aggregation | diamond | none | 0 | 0 |
| Composition | diamond | none | 0 | 1 |

### 6.2 Sequence Diagram

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Lifeline: Client -->
    <mxCell id="ll1" value="Client" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=#dae8fc;strokeColor=#6c8ebf;size=40;" vertex="1" parent="1">
      <mxGeometry x="80" y="40" width="100" height="300" as="geometry" />
    </mxCell>

    <!-- Lifeline: Server -->
    <mxCell id="ll2" value="Server" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=#d5e8d4;strokeColor=#82b366;size=40;" vertex="1" parent="1">
      <mxGeometry x="280" y="40" width="100" height="300" as="geometry" />
    </mxCell>

    <!-- Lifeline: Database -->
    <mxCell id="ll3" value="Database" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=#fff2cc;strokeColor=#d6b656;size=40;" vertex="1" parent="1">
      <mxGeometry x="480" y="40" width="100" height="300" as="geometry" />
    </mxCell>

    <!-- Sync message: Client -> Server -->
    <mxCell id="msg1" value="POST /login" style="html=1;verticalAlign=bottom;endArrow=block;endFill=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="130" y="120" as="sourcePoint" />
        <mxPoint x="330" y="120" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Sync message: Server -> Database -->
    <mxCell id="msg2" value="SELECT user" style="html=1;verticalAlign=bottom;endArrow=block;endFill=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="330" y="160" as="sourcePoint" />
        <mxPoint x="530" y="160" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Return message: Database -> Server -->
    <mxCell id="msg3" value="user record" style="html=1;verticalAlign=bottom;endArrow=open;endFill=0;dashed=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="530" y="200" as="sourcePoint" />
        <mxPoint x="330" y="200" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Return message: Server -> Client -->
    <mxCell id="msg4" value="200 OK + token" style="html=1;verticalAlign=bottom;endArrow=open;endFill=0;dashed=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="330" y="240" as="sourcePoint" />
        <mxPoint x="130" y="240" as="targetPoint" />
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

### 6.3 Use Case Diagram

```xml
<!-- Actor -->
<mxCell id="actor1" value="Customer" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
  <mxGeometry x="60" y="120" width="30" height="55" as="geometry" />
</mxCell>

<!-- System boundary -->
<mxCell id="sys" value="E-Commerce System" style="rounded=1;whiteSpace=wrap;html=1;container=1;collapsible=0;fillColor=none;strokeColor=#666666;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=14;" vertex="1" parent="1">
  <mxGeometry x="160" y="40" width="300" height="280" as="geometry" />
</mxCell>

<!-- Use cases (ellipses inside system) -->
<mxCell id="uc1" value="Browse Products" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sys">
  <mxGeometry x="50" y="30" width="180" height="60" as="geometry" />
</mxCell>
<mxCell id="uc2" value="Place Order" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sys">
  <mxGeometry x="50" y="110" width="180" height="60" as="geometry" />
</mxCell>
<mxCell id="uc3" value="Make Payment" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sys">
  <mxGeometry x="50" y="190" width="180" height="60" as="geometry" />
</mxCell>

<!-- Association lines (no arrows for use case associations) -->
<mxCell id="a1" style="endArrow=none;html=1;" edge="1" parent="1" source="actor1" target="uc1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### 6.4 State Machine Diagram

```xml
<!-- Start state -->
<mxCell id="s0" value="" style="ellipse;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="100" y="40" width="30" height="30" as="geometry" />
</mxCell>

<!-- State with entry/exit actions -->
<mxCell id="s1" value="&lt;b&gt;Idle&lt;/b&gt;&lt;hr&gt;entry / resetTimer()&lt;br&gt;exit / saveState()" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;align=center;verticalAlign=top;arcSize=15;" vertex="1" parent="1">
  <mxGeometry x="60" y="110" width="160" height="80" as="geometry" />
</mxCell>

<!-- End state -->
<mxCell id="sf" value="" style="ellipse;html=1;shape=doubleCircle;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
  <mxGeometry x="120" y="340" width="30" height="30" as="geometry" />
</mxCell>
```

### Anti-Patterns (UML)

- NEVER use filled arrowheads (`endFill=1`) for inheritance — ALWAYS use `endArrow=block;endFill=0` (hollow triangle).
- NEVER use solid lines for return messages in sequence diagrams — ALWAYS use `dashed=1;endArrow=open;endFill=0`.
- NEVER place use cases outside the system boundary container.
- NEVER use `shape=ellipse` for the UML actor — ALWAYS use `shape=umlActor`.

---

## 7. Mind Maps

Draw.io supports mind maps with automatic tree layout and the dedicated `mindmap` shape.

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Central topic -->
    <mxCell id="center" value="Project Plan" style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=16;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="300" y="200" width="160" height="80" as="geometry" />
    </mxCell>

    <!-- Branch 1: Design -->
    <mxCell id="b1" value="Design" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="80" y="60" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="b1_1" value="Wireframes" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="1">
      <mxGeometry x="10" y="120" width="100" height="30" as="geometry" />
    </mxCell>
    <mxCell id="b1_2" value="Mockups" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="1">
      <mxGeometry x="130" y="120" width="100" height="30" as="geometry" />
    </mxCell>

    <!-- Branch 2: Development -->
    <mxCell id="b2" value="Development" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=13;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="540" y="60" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Branch 3: Testing -->
    <mxCell id="b3" value="Testing" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=13;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="540" y="320" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Connections (curved, no arrows for mind maps) -->
    <mxCell id="ec1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;" edge="1" parent="1" source="center" target="b1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec1a" style="endArrow=none;html=1;curved=1;strokeColor=#999999;" edge="1" parent="1" source="b1" target="b1_1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec1b" style="endArrow=none;html=1;curved=1;strokeColor=#999999;" edge="1" parent="1" source="b1" target="b1_2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec2" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#82b366;" edge="1" parent="1" source="center" target="b2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec3" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#d6b656;" edge="1" parent="1" source="center" target="b3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Key Properties

- Mind map branches use `endArrow=none` — there are NO directional arrows.
- `curved=1` produces organic-looking connections suitable for mind maps.
- Hierarchical color coding: central topic is darkest, child branches progressively lighter.
- Draw.io also supports automatic mind map layout via `Edit > Layout > Tree > Mindmap`.

### Anti-Patterns

- NEVER use directed arrows in mind maps — ALWAYS use `endArrow=none`.
- NEVER use orthogonal edge routing — ALWAYS use `curved=1` for the organic mind map look.

---

## 8. Network Diagrams

Network diagrams use specialized shape libraries: Networking (general), Cisco, AWS, Azure, and GCP.

### Complete XML Example (Generic Network)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Internet Cloud -->
    <mxCell id="cloud" value="Internet" style="shape=cloud;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=14;" vertex="1" parent="1">
      <mxGeometry x="250" y="20" width="200" height="100" as="geometry" />
    </mxCell>

    <!-- Firewall -->
    <mxCell id="fw" value="Firewall" style="shape=mxgraph.cisco.firewalls.firewall;whiteSpace=wrap;html=1;fillColor=#FF6666;sketch=0;" vertex="1" parent="1">
      <mxGeometry x="310" y="160" width="80" height="60" as="geometry" />
    </mxCell>

    <!-- Router -->
    <mxCell id="router" value="Core Router" style="shape=mxgraph.cisco.routers.router;whiteSpace=wrap;html=1;fillColor=#00979D;sketch=0;" vertex="1" parent="1">
      <mxGeometry x="310" y="270" width="80" height="60" as="geometry" />
    </mxCell>

    <!-- Switch -->
    <mxCell id="sw1" value="Switch L3" style="shape=mxgraph.cisco.switches.workgroup_switch;whiteSpace=wrap;html=1;fillColor=#00BCD4;sketch=0;" vertex="1" parent="1">
      <mxGeometry x="130" y="380" width="80" height="50" as="geometry" />
    </mxCell>

    <!-- Servers -->
    <mxCell id="srv1" value="Web Server" style="shape=mxgraph.cisco.servers.standard_server;whiteSpace=wrap;html=1;fillColor=#4D9900;sketch=0;" vertex="1" parent="1">
      <mxGeometry x="60" y="480" width="50" height="65" as="geometry" />
    </mxCell>
    <mxCell id="srv2" value="DB Server" style="shape=mxgraph.cisco.servers.standard_server;whiteSpace=wrap;html=1;fillColor=#4D9900;sketch=0;" vertex="1" parent="1">
      <mxGeometry x="180" y="480" width="50" height="65" as="geometry" />
    </mxCell>

    <!-- Network segments (labeled zones) -->
    <mxCell id="dmz" value="DMZ" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF0000;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF0000;container=1;collapsible=0;" vertex="1" parent="1">
      <mxGeometry x="30" y="460" width="230" height="110" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="n1" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="cloud" target="fw">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="n2" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="fw" target="router">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="n3" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="router" target="sw1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="n4" style="endArrow=none;html=1;" edge="1" parent="1" source="sw1" target="srv1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="n5" style="endArrow=none;html=1;" edge="1" parent="1" source="sw1" target="srv2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Network Shape Libraries

| Library | Shape Prefix | Example Shapes |
|---------|-------------|----------------|
| Cisco | `shape=mxgraph.cisco.*` | `routers.router`, `switches.workgroup_switch`, `firewalls.firewall`, `servers.standard_server` |
| AWS | `shape=mxgraph.aws4.*` | `compute.EC2`, `database.RDS`, `networkingAndContentDelivery.VPC` |
| Azure | `shape=mxgraph.azure.*` | `compute.VirtualMachine`, `databases.SQLDatabase`, `networking.VirtualNetwork` |
| GCP | `shape=mxgraph.gcp2.*` | `compute.ComputeEngine`, `databases.CloudSQL` |

### Key Style Properties

- Network links use `endArrow=none` (bidirectional connectivity).
- Segment labels use the `<object>` wrapper for metadata (IP addresses, VLANs).
- Zone boundaries use `dashed=1;container=1;fillColor=none;` for visual grouping.

### Anti-Patterns

- NEVER use generic rectangles for network devices — ALWAYS use the appropriate stencil shapes.
- NEVER use directed arrows for physical network links — ALWAYS use `endArrow=none`.
- NEVER place cloud provider shapes from different vendors in the same diagram without clear zone separation.

---

## 9. Org Charts

Org charts use tree layout with person-shaped containers and hierarchical connectors.

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- CEO -->
    <mxCell id="ceo" value="&lt;b&gt;Jane Smith&lt;/b&gt;&lt;br&gt;CEO" style="shape=image;verticalLabelPosition=bottom;labelBackgroundColor=#ffffff;verticalAlign=top;imageAspect=0;image=https://cdn.example.com/avatar.png;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="280" y="40" width="80" height="80" as="geometry" />
    </mxCell>

    <!-- Alternative: text-only person shape -->
    <mxCell id="cto" value="&lt;b&gt;Bob Lee&lt;/b&gt;&lt;br&gt;CTO" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="120" y="180" width="120" height="50" as="geometry" />
    </mxCell>

    <mxCell id="cfo" value="&lt;b&gt;Alice Wong&lt;/b&gt;&lt;br&gt;CFO" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;arcSize=20;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="400" y="180" width="120" height="50" as="geometry" />
    </mxCell>

    <mxCell id="dev_lead" value="&lt;b&gt;Charlie Brown&lt;/b&gt;&lt;br&gt;Dev Lead" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="60" y="290" width="120" height="50" as="geometry" />
    </mxCell>

    <mxCell id="qa_lead" value="&lt;b&gt;Diana Prince&lt;/b&gt;&lt;br&gt;QA Lead" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;arcSize=20;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="200" y="290" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Hierarchy connectors (no arrows, orthogonal) -->
    <mxCell id="h1" style="endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;strokeColor=#999999;" edge="1" parent="1" source="ceo" target="cto">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="h2" style="endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;strokeColor=#999999;" edge="1" parent="1" source="ceo" target="cfo">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="h3" style="endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;strokeColor=#999999;" edge="1" parent="1" source="cto" target="dev_lead">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="h4" style="endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;strokeColor=#999999;" edge="1" parent="1" source="cto" target="qa_lead">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Key Properties

- Hierarchy connectors use `endArrow=none;edgeStyle=orthogonalEdgeStyle;` for clean vertical/horizontal lines.
- Person cards use HTML labels with `<b>Name</b><br>Title` format.
- Color coding by department is a common convention.
- Draw.io supports automatic tree layout: `Edit > Layout > Tree > Vertical Tree`.

### Anti-Patterns

- NEVER use directed arrows for org chart hierarchy lines — ALWAYS use `endArrow=none`.
- NEVER use curved edges for org charts — ALWAYS use `edgeStyle=orthogonalEdgeStyle`.
- NEVER mix horizontal and vertical tree directions within the same org chart.

---

## 10. Venn Diagrams

Venn diagrams use overlapping ellipses with transparency to visualize set intersections.

### Complete XML Example

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Circle A -->
    <mxCell id="circA" value="&lt;b&gt;Design&lt;/b&gt;" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;opacity=50;fontSize=14;verticalAlign=top;" vertex="1" parent="1">
      <mxGeometry x="80" y="80" width="250" height="250" as="geometry" />
    </mxCell>

    <!-- Circle B -->
    <mxCell id="circB" value="&lt;b&gt;Development&lt;/b&gt;" style="ellipse;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;opacity=50;fontSize=14;verticalAlign=top;" vertex="1" parent="1">
      <mxGeometry x="230" y="80" width="250" height="250" as="geometry" />
    </mxCell>

    <!-- Circle C (three-set Venn) -->
    <mxCell id="circC" value="&lt;b&gt;Business&lt;/b&gt;" style="ellipse;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;opacity=50;fontSize=14;verticalAlign=bottom;" vertex="1" parent="1">
      <mxGeometry x="155" y="200" width="250" height="250" as="geometry" />
    </mxCell>

    <!-- Intersection label (center) -->
    <mxCell id="center_label" value="&lt;b&gt;Product&lt;br&gt;Excellence&lt;/b&gt;" style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=11;fontColor=#333333;" vertex="1" parent="1">
      <mxGeometry x="240" y="240" width="90" height="40" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Key Properties

- `opacity=50` (or `fillOpacity=50`) is CRITICAL for making overlapping regions visible through transparency.
- Circles MUST physically overlap in their geometry coordinates to create visual intersections.
- Intersection labels are placed as separate text cells positioned over the overlap area.
- `strokeWidth=2` helps distinguish circle boundaries in the overlap zone.

### Anti-Patterns

- NEVER use `opacity=100` (the default) — overlapping circles will completely obscure each other.
- NEVER use rectangles for Venn diagrams — ALWAYS use `ellipse`.
- NEVER rely on automatic layout for Venn diagrams — overlap positions MUST be calculated manually.

---

## 11. Infographics / Timelines

### Timeline Pattern

Timelines typically use a horizontal or vertical spine with numbered milestone markers.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Timeline spine -->
    <mxCell id="spine" value="" style="endArrow=classic;html=1;strokeWidth=3;strokeColor=#333333;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="60" y="200" as="sourcePoint" />
        <mxPoint x="740" y="200" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Milestone 1 -->
    <mxCell id="m1_dot" value="" style="ellipse;fillColor=#1168bd;strokeColor=#0b4884;aspect=fixed;" vertex="1" parent="1">
      <mxGeometry x="110" y="190" width="20" height="20" as="geometry" />
    </mxCell>
    <mxCell id="m1_label" value="&lt;b&gt;Q1 2026&lt;/b&gt;&lt;br&gt;Research Phase" style="text;html=1;align=center;verticalAlign=top;whiteSpace=wrap;fontSize=10;" vertex="1" parent="1">
      <mxGeometry x="70" y="220" width="100" height="50" as="geometry" />
    </mxCell>

    <!-- Milestone 2 -->
    <mxCell id="m2_dot" value="" style="ellipse;fillColor=#d5e8d4;strokeColor=#82b366;aspect=fixed;" vertex="1" parent="1">
      <mxGeometry x="260" y="190" width="20" height="20" as="geometry" />
    </mxCell>
    <mxCell id="m2_label" value="&lt;b&gt;Q2 2026&lt;/b&gt;&lt;br&gt;Development" style="text;html=1;align=center;verticalAlign=bottom;whiteSpace=wrap;fontSize=10;" vertex="1" parent="1">
      <mxGeometry x="220" y="140" width="100" height="50" as="geometry" />
    </mxCell>

    <!-- Milestone 3 -->
    <mxCell id="m3_dot" value="" style="ellipse;fillColor=#fff2cc;strokeColor=#d6b656;aspect=fixed;" vertex="1" parent="1">
      <mxGeometry x="410" y="190" width="20" height="20" as="geometry" />
    </mxCell>
    <mxCell id="m3_label" value="&lt;b&gt;Q3 2026&lt;/b&gt;&lt;br&gt;Testing" style="text;html=1;align=center;verticalAlign=top;whiteSpace=wrap;fontSize=10;" vertex="1" parent="1">
      <mxGeometry x="370" y="220" width="100" height="50" as="geometry" />
    </mxCell>

    <!-- Milestone 4 -->
    <mxCell id="m4_dot" value="" style="ellipse;fillColor=#f8cecc;strokeColor=#b85450;aspect=fixed;" vertex="1" parent="1">
      <mxGeometry x="560" y="190" width="20" height="20" as="geometry" />
    </mxCell>
    <mxCell id="m4_label" value="&lt;b&gt;Q4 2026&lt;/b&gt;&lt;br&gt;Launch" style="text;html=1;align=center;verticalAlign=bottom;whiteSpace=wrap;fontSize=10;" vertex="1" parent="1">
      <mxGeometry x="520" y="140" width="100" height="50" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

### Numbered Steps Pattern

```xml
<!-- Step indicator (circle with number) -->
<mxCell id="step1" value="1" style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=16;fontStyle=1;aspect=fixed;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="40" height="40" as="geometry" />
</mxCell>
<mxCell id="step1_text" value="&lt;b&gt;Define Requirements&lt;/b&gt;&lt;br&gt;Gather stakeholder input and document needs" style="text;html=1;align=left;verticalAlign=middle;whiteSpace=wrap;" vertex="1" parent="1">
  <mxGeometry x="160" y="95" width="200" height="50" as="geometry" />
</mxCell>
```

### Key Properties

- Timeline spines use `strokeWidth=3` for visual prominence.
- Milestone labels alternate above and below the spine for readability (zigzag pattern).
- `aspect=fixed` on milestone dots ensures they remain circular regardless of resizing.
- Step numbers use `ellipse;aspect=fixed;` with a contrasting color scheme.

### Anti-Patterns

- NEVER align all milestone labels on the same side — ALWAYS alternate above/below for readability.
- NEVER use thin lines (`strokeWidth=1`) for the timeline spine — it will be visually lost.

---

## 12. Common Patterns Across Diagram Types

### 12.1 Containers and Grouping

Containers are shapes that hold child elements. Children move, resize, and collapse with their parent.

```xml
<!-- Group container -->
<mxCell id="group1" value="Authentication Module" style="rounded=1;whiteSpace=wrap;html=1;container=1;collapsible=1;fillColor=none;strokeColor=#6c8ebf;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;" vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="300" height="200" as="geometry" />
</mxCell>

<!-- Child elements (relative coordinates) -->
<mxCell id="child1" value="Login Form" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="group1">
  <mxGeometry x="20" y="40" width="120" height="50" as="geometry" />
</mxCell>
```

**Container style keys:**
- `container=1` — enables child containment (MANDATORY).
- `collapsible=1` — adds expand/collapse toggle.
- `childLayout=stackLayout` — auto-stacks children vertically.
- `recursiveResize=0` — prevents cascading resize to children.

### 12.2 Layers

Layers allow visibility toggling and organization of diagram elements.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <!-- Default layer -->
    <mxCell id="1" value="Infrastructure" parent="0" />
    <!-- Additional layer -->
    <mxCell id="layer2" value="Application" parent="0" />

    <!-- Elements on default layer -->
    <mxCell id="srv" value="Server" style="..." vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="100" height="60" as="geometry" />
    </mxCell>

    <!-- Elements on application layer -->
    <mxCell id="app" value="API" style="..." vertex="1" parent="layer2">
      <mxGeometry x="100" y="100" width="100" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Layers are `mxCell` elements with `parent="0"`. The first layer (`id="1"`) is the default. Additional layers use unique IDs and MUST also have `parent="0"`.

### 12.3 Multi-Page Diagrams

Each page is a separate `<diagram>` element within `<mxfile>`.

```xml
<mxfile>
  <diagram id="page-1" name="System Context">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Page 1 content -->
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-2" name="Container View">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Page 2 content -->
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Each page MUST have its own `<root>` with independent `id="0"` and `id="1"` cells. Cell IDs are scoped per page and do NOT need to be globally unique across pages.

### 12.4 Metadata with `<object>` Wrapper

For cells that need custom properties beyond `value` and `style`, use the `<object>` wrapper:

```xml
<object id="srv1" label="Web Server" ip="10.0.1.10" environment="production" owner="ops-team">
  <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="140" height="70" as="geometry" />
  </mxCell>
</object>
```

When using `placeholders="1"` in the style, `%ip%` and `%environment%` resolve from the `<object>` attributes.

---

## 13. Shape Libraries and Stencils

Draw.io ships with 40+ shape libraries. Custom shapes are accessed via the `shape=mxgraph.*` namespace.

### Built-in Library Namespaces

| Namespace | Purpose | Example Shape |
|-----------|---------|---------------|
| `mxgraph.flowchart.*` | ISO 5807 flowchart shapes | `mxgraph.flowchart.process` |
| `mxgraph.bpmn.*` | BPMN 2.0 elements | `mxgraph.bpmn.shape` |
| `mxgraph.cisco.*` | Cisco network icons | `mxgraph.cisco.routers.router` |
| `mxgraph.aws4.*` | AWS Architecture icons (v4) | `mxgraph.aws4.compute.EC2` |
| `mxgraph.azure.*` | Microsoft Azure icons | `mxgraph.azure.compute.VirtualMachine` |
| `mxgraph.gcp2.*` | Google Cloud Platform icons | `mxgraph.gcp2.compute.ComputeEngine` |
| `mxgraph.c4.*` | C4 architecture model | `mxgraph.c4.person2` |
| `mxgraph.er.*` | Entity Relationship | `mxgraph.er.entity` |
| `mxgraph.ios.*` | iOS mockup elements | `mxgraph.ios.iButton` |
| `mxgraph.android.*` | Android mockup elements | `mxgraph.android.phone` |
| `mxgraph.mockup.*` | Generic wireframe shapes | `mxgraph.mockup.buttons.button` |
| `mxgraph.sysml.*` | SysML elements | `mxgraph.sysml.requirements.requirement` |
| `mxgraph.archimate3.*` | ArchiMate notation | `mxgraph.archimate3.application` |
| `mxgraph.electrical.*` | Electrical engineering | `mxgraph.electrical.resistor` |
| `mxgraph.pid.*` | Piping & Instrumentation | `mxgraph.pid.valves.valve` |
| `mxgraph.floorplan.*` | Floor plan / office layout | `mxgraph.floorplan.room` |
| `mxgraph.lean_mapping.*` | Lean / Value Stream Mapping | `mxgraph.lean_mapping.process_box` |

### How to Use Custom Shapes

To use any stencil shape, set the `shape` style property to the full namespace path:

```xml
<!-- AWS EC2 Instance -->
<mxCell id="ec2" value="Web Server" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;fillColor=#ED7100;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>

<!-- Azure Virtual Machine -->
<mxCell id="vm" value="App VM" style="shape=mxgraph.azure.virtual_machine;fillColor=#0078D4;strokeColor=#ffffff;fontColor=#ffffff;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;" vertex="1" parent="1">
  <mxGeometry x="250" y="100" width="60" height="60" as="geometry" />
</mxCell>

<!-- Cisco Router -->
<mxCell id="rtr" value="Edge Router" style="shape=mxgraph.cisco.routers.router;fillColor=#00979D;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;" vertex="1" parent="1">
  <mxGeometry x="400" y="100" width="78" height="53" as="geometry" />
</mxCell>
```

### AWS Architecture Diagram Pattern

AWS diagrams use nested containers for regions, VPCs, and availability zones:

```xml
<!-- AWS Region container -->
<mxCell id="region" value="eu-west-1" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_region;strokeColor=#00A4A6;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=1;" vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="500" height="350" as="geometry" />
</mxCell>

<!-- VPC inside region -->
<mxCell id="vpc" value="VPC 10.0.0.0/16" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_vpc;strokeColor=#8C4FFF;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#AAB7B8;dashed=0;" vertex="1" parent="region">
  <mxGeometry x="20" y="40" width="460" height="280" as="geometry" />
</mxCell>
```

### Enabling Shape Libraries

In the Draw.io editor, users enable libraries via `View > More Shapes`. When generating XML programmatically, any `shape=mxgraph.*` reference works automatically — the shapes are bundled with Draw.io and do NOT require separate installation.

### Anti-Patterns

- NEVER invent shape namespaces — ALWAYS verify the exact `mxgraph.*` path exists in Draw.io's stencil library.
- NEVER use generic rectangles when a dedicated stencil exists — it breaks visual convention and reduces diagram clarity.
- NEVER mix cloud provider stencils (e.g., AWS icons inside an Azure diagram) unless explicitly depicting a multi-cloud architecture.
- NEVER omit `verticalLabelPosition=bottom;verticalAlign=top;` on icon-style shapes — the label will overlap the icon.

---

## Summary Table: Diagram Type Quick Reference

| Diagram Type | Primary Shape Library | Key Style Property | Typical Edge Style |
|-------------|----------------------|-------------------|-------------------|
| Flowchart | General, Flowchart | `rounded=0/1;arcSize=50` | `endArrow=classic` |
| Swimlane | General | `swimlane;container=1;startSize=30` | `endArrow=classic` |
| C4 Architecture | C4 | `shape=mxgraph.c4.person2` | `endArrow=classic;dashed=0` |
| ER Diagram | Entity Relation | `shape=table;childLayout=tableLayout` | `endArrow=ERmany;startArrow=ERone` |
| BPMN 2.0 | BPMN | `shape=mxgraph.bpmn.shape;symbol=*` | `endArrow=classic` (sequence) |
| UML Class | UML 2.5 | `swimlane;fontStyle=1;startSize=26` | `endArrow=block;endFill=0` (inherit) |
| UML Sequence | UML 2.5 | `shape=umlLifeline` | `endArrow=block;endFill=1` (sync) |
| Mind Map | General | `ellipse;rounded=1` | `endArrow=none;curved=1` |
| Network | Cisco, AWS, Azure | `shape=mxgraph.cisco.*` | `endArrow=none` |
| Org Chart | General | `rounded=1;arcSize=20` | `endArrow=none;edgeStyle=orthogonal` |
| Venn | General | `ellipse;opacity=50` | N/A (no edges) |
| Timeline | General | `ellipse;aspect=fixed` | Spine arrow only |

---

## References

1. Draw.io AI Generation Guide — https://drawio.com/doc/faq/ai-drawio-generation
2. Draw.io Style Reference — https://drawio.com/doc/faq/drawio-style-reference
3. Draw.io Blog — https://drawio.com/blog
4. mxGraph XML Schema (mxfile.xsd) — bundled with Draw.io source
5. jgraph/drawio GitHub Repository — https://github.com/jgraph/drawio
