# Anti-Patterns: BPMN 2.0 Implementation

What NOT to do when generating BPMN 2.0 diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Using Generic Ellipse for Events

### WRONG

```xml
<mxCell id="start" value="Start" style="ellipse;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;"
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;"
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

A generic `ellipse` has no BPMN semantic meaning. It cannot display event type icons (message, timer, error, signal) and does not render the correct border weight for start vs. intermediate vs. end events. ALWAYS use `shape=mxgraph.bpmn.shape` with `outline` and `symbol` properties.

---

## AP-02: Using Generic Rhombus for Gateways

### WRONG

```xml
<mxCell id="gw1" value="X" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;"
        vertex="1" parent="pool1">
  <mxGeometry x="270" y="85" width="50" height="50" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="gw1" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;"
        vertex="1" parent="pool1">
  <mxGeometry x="270" y="85" width="50" height="50" as="geometry" />
</mxCell>
```

### Why It Fails

A generic `rhombus` does not render BPMN gateway markers (X, +, O, pentagon). Placing text like "X" inside a diamond is a visual hack that breaks when the diagram is validated or exported. ALWAYS use `shape=mxgraph.bpmn.shape` with the correct `symbol` property (`exclusiveGw`, `parallelGw`, `inclusiveGw`, `eventGw`).

---

## AP-03: Using Solid Lines for Message Flows

### WRONG

```xml
<mxCell id="mf1" style="endArrow=classic;html=1;"
        edge="1" parent="1" source="task_pool1" target="task_pool2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="mf1" style="endArrow=open;endFill=0;startArrow=oval;startFill=0;dashed=1;strokeColor=#666666;html=1;"
        edge="1" parent="1" source="task_pool1" target="task_pool2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

BPMN 2.0 specification requires message flows to be dashed lines with an open arrowhead and a small circle at the source. Using solid lines makes message flows visually identical to sequence flows, which creates ambiguity about whether the communication crosses organizational boundaries. ALWAYS use `dashed=1;endArrow=open;endFill=0;startArrow=oval;startFill=0;` for message flows.

---

## AP-04: Using Sequence Flows Between Pools

### WRONG

```xml
<!-- Sequence flow connecting elements in different pools -->
<mxCell id="f1" style="endArrow=classic;html=1;"
        edge="1" parent="pool1" source="task_in_pool1" target="task_in_pool2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Message flow between pools, parent="1" (page root) -->
<mxCell id="mf1" style="endArrow=open;endFill=0;startArrow=oval;startFill=0;dashed=1;strokeColor=#666666;html=1;"
        edge="1" parent="1" source="task_in_pool1" target="task_in_pool2">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Sequence flows are ONLY valid within a single pool. They represent the order of activities within one participant's process. Cross-pool communication ALWAYS uses message flows. Additionally, the edge `parent` MUST be `"1"` (the page root) for message flows, NOT a pool ID, because the edge spans two separate containers.

---

## AP-05: Omitting Pool Containers for Multi-Participant Processes

### WRONG

```xml
<!-- Elements placed directly on canvas without pools -->
<mxCell id="task1" value="Send Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="70" as="geometry" />
</mxCell>
<mxCell id="task2" value="Receive Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="300" width="120" height="70" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- Each participant gets its own pool -->
<mxCell id="pool_buyer" value="Buyer" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;..."
        vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="500" height="150" as="geometry" />
</mxCell>
<mxCell id="task1" value="Send Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;"
        vertex="1" parent="pool_buyer">
  <mxGeometry x="100" y="40" width="120" height="70" as="geometry" />
</mxCell>

<mxCell id="pool_seller" value="Seller" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;..."
        vertex="1" parent="1">
  <mxGeometry x="40" y="260" width="500" height="150" as="geometry" />
</mxCell>
<mxCell id="task2" value="Receive Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;"
        vertex="1" parent="pool_seller">
  <mxGeometry x="100" y="40" width="120" height="70" as="geometry" />
</mxCell>
```

### Why It Fails

Without pools, there is no visual boundary showing which participant owns which activities. This violates BPMN 2.0 which requires pools for inter-organizational processes. Without pools, you also cannot use message flows (which require source and target in different pools). ALWAYS use pools when modelling processes with multiple participants.

---

## AP-06: Missing Gateway Condition Labels

### WRONG

```xml
<!-- Exclusive gateway outgoing edges without condition labels -->
<mxCell id="f1" style="endArrow=classic;html=1;"
        edge="1" parent="pool1" source="gw1" target="task_approve">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="f2" style="endArrow=classic;html=1;"
        edge="1" parent="pool1" source="gw1" target="task_reject">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="f1" value="Approved" style="endArrow=classic;html=1;"
        edge="1" parent="pool1" source="gw1" target="task_approve">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
<mxCell id="f2" value="Rejected" style="endArrow=classic;html=1;"
        edge="1" parent="pool1" source="gw1" target="task_reject">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Unlabeled exclusive/inclusive gateway branches make it impossible for readers to understand the routing logic. Every outgoing edge from an exclusive or inclusive gateway MUST have a `value` describing the condition. The only exception is parallel gateways, where all paths execute simultaneously and condition labels are unnecessary.

---

## AP-07: Using Text Labels on BPMN Events

### WRONG

```xml
<mxCell id="start" value="Start" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;..."
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;..."
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

BPMN events are 40 x 40 circles. Placing text like "Start" or "End" inside them clutters the shape and makes it unreadable. The event type is communicated through the visual shape (thin/double/thick circle and icon). ALWAYS leave the `value` attribute empty for BPMN events. If a label is needed for documentation, use an annotation connected with an association flow.

---

## AP-08: Mixing BPMN and Flowchart Shapes

### WRONG

```xml
<!-- Start as BPMN event, but decision as generic rhombus -->
<mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;..."
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
<mxCell id="gw1" value="Check?" style="rhombus;whiteSpace=wrap;html=1;"
        vertex="1" parent="pool1">
  <mxGeometry x="270" y="85" width="120" height="80" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;..."
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
<mxCell id="gw1" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;"
        vertex="1" parent="pool1">
  <mxGeometry x="270" y="85" width="50" height="50" as="geometry" />
</mxCell>
```

### Why It Fails

BPMN and ISO 5807 flowcharts are different notations with different shape semantics. Mixing them in a single diagram creates confusion. A BPMN diagram MUST use BPMN shapes exclusively. NEVER combine BPMN events with flowchart diamonds, rectangles, or stadiums. ALWAYS use the BPMN shape library consistently throughout the entire diagram.

---

## AP-09: Wrong Event Dimensions

### WRONG

```xml
<!-- Event at 80x80 instead of standard 40x40 -->
<mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;..."
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="75" width="80" height="80" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;..."
        vertex="1" parent="pool1">
  <mxGeometry x="30" y="95" width="40" height="40" as="geometry" />
</mxCell>
```

### Why It Fails

BPMN events are standardized at 40 x 40 pixels. Oversized events disrupt the visual hierarchy where activities (120 x 70) are the dominant shapes and events are small markers. Undersized events make the type icon unreadable. ALWAYS use 40 x 40 for events and 50 x 50 for gateways.
