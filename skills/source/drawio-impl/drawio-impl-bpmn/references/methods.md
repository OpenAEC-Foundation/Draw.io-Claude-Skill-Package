# Methods Reference: BPMN 2.0 Implementation

Complete style strings and attribute reference for all BPMN 2.0 elements in Draw.io.

---

## 1. Event Styles

### Start Event (None)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;
```

Thin single circle, empty interior. Represents the beginning of a process.

### Start Event (Message)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=message;fillColor=#d5e8d4;strokeColor=#82b366;
```

Thin circle with envelope icon. Process starts when a message is received.

### Start Event (Timer)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=timer;fillColor=#d5e8d4;strokeColor=#82b366;
```

Thin circle with clock icon. Process starts at a scheduled time.

### Start Event (Signal)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=signal;fillColor=#d5e8d4;strokeColor=#82b366;
```

Thin circle with triangle icon. Process starts when a signal is broadcast.

### Intermediate Catch Event (Message)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=message;fillColor=#fff2cc;strokeColor=#d6b656;
```

Double thin circle with unfilled envelope. Waits for a message to arrive.

### Intermediate Catch Event (Timer)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=timer;fillColor=#fff2cc;strokeColor=#d6b656;
```

Double thin circle with clock. Waits for a time duration or date.

### Intermediate Catch Event (Signal)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=signal;fillColor=#fff2cc;strokeColor=#d6b656;
```

Double thin circle with unfilled triangle. Waits for a signal.

### Intermediate Catch Event (Error)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=error;fillColor=#fff2cc;strokeColor=#d6b656;
```

Double thin circle with lightning bolt. Catches an error from a subprocess. ONLY valid as a boundary event attached to an activity.

### Intermediate Throw Event (Message)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=throwing;symbol=message;fillColor=#fff2cc;strokeColor=#d6b656;
```

Double thin circle with filled envelope. Sends a message.

### Intermediate Throw Event (Signal)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=throwing;symbol=signal;fillColor=#fff2cc;strokeColor=#d6b656;
```

Double thin circle with filled triangle. Broadcasts a signal.

### End Event (None / Terminate)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;
```

Thick circle with filled interior. Terminates the process.

### End Event (Message)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=message;fillColor=#f8cecc;strokeColor=#b85450;
```

Thick circle with filled envelope. Sends a message at process end.

### End Event (Error)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=error;fillColor=#f8cecc;strokeColor=#b85450;
```

Thick circle with lightning bolt. Process ends with an error thrown to parent.

### End Event (Signal)

```
shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=signal;fillColor=#f8cecc;strokeColor=#b85450;
```

Thick circle with filled triangle. Broadcasts signal at process end.

**Event dimensions:** ALWAYS 40 x 40 px.

---

## 2. Activity Styles

### Task (Generic)

```
rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Standard rounded rectangle for a single unit of work. Dimensions: 120 x 70.

### User Task

```
shape=mxgraph.bpmn.task;taskMarker=user;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task performed by a human with UI assistance.

### Service Task

```
shape=mxgraph.bpmn.task;taskMarker=service;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task performed by an automated service or application.

### Script Task

```
shape=mxgraph.bpmn.task;taskMarker=script;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task executed by a script engine.

### Send Task

```
shape=mxgraph.bpmn.task;taskMarker=send;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task that sends a message to an external participant.

### Receive Task

```
shape=mxgraph.bpmn.task;taskMarker=receive;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task that waits for a message from an external participant.

### Manual Task

```
shape=mxgraph.bpmn.task;taskMarker=manual;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task performed by a person without system assistance.

### Business Rule Task

```
shape=mxgraph.bpmn.task;taskMarker=businessRule;rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Task that evaluates a business rule engine.

### Collapsed Subprocess

```
rounded=1;whiteSpace=wrap;html=1;arcSize=20;strokeWidth=2;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Double-bordered rounded rectangle. `strokeWidth=2` creates the BPMN double border. Dimensions: 120 x 70.

### Expanded Subprocess

```
rounded=1;whiteSpace=wrap;html=1;arcSize=10;container=1;collapsible=0;startSize=25;strokeWidth=2;fillColor=#f5f5f5;strokeColor=#666666;
```

Container that holds nested BPMN elements. Set `container=1` so children use relative coordinates. Dimensions: 300 x 200 (minimum).

---

## 3. Gateway Styles

### Exclusive Gateway (XOR)

```
shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;
```

Diamond with X marker. Exactly one outgoing path is taken. ALWAYS label outgoing edges with conditions.

### Parallel Gateway (AND)

```
shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=parallelGw;fillColor=#fff2cc;strokeColor=#d6b656;
```

Diamond with + marker. ALL outgoing paths execute simultaneously. Outgoing edges do NOT need condition labels.

### Inclusive Gateway (OR)

```
shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=inclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;
```

Diamond with O marker. One or more outgoing paths are taken based on conditions. ALWAYS label outgoing edges with conditions.

### Event-Based Gateway

```
shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=eventGw;fillColor=#fff2cc;strokeColor=#d6b656;
```

Diamond with pentagon marker. The path is determined by which event occurs first. Outgoing edges connect to intermediate catch events ONLY.

**Gateway dimensions:** ALWAYS 50 x 50 px.

---

## 4. Pool and Lane Styles

### Pool

```
shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;
```

Outermost container for a BPMN participant. `startSize=30` controls the header height. `horizontal=1` renders the header on the left side.

### Lane

```
swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;
```

Subdivision within a pool. Lanes are children of the pool and use container-relative coordinates.

---

## 5. Flow Styles

### Sequence Flow (Standard)

```
endArrow=classic;html=1;
```

Solid line with filled arrowhead. Connects elements within the SAME pool.

### Conditional Sequence Flow

```
endArrow=classic;html=1;startArrow=diamond;startFill=0;startSize=14;
```

Solid line with small diamond at the source end. Indicates a condition on the flow.

### Message Flow

```
endArrow=open;endFill=0;startArrow=oval;startFill=0;dashed=1;strokeColor=#666666;html=1;
```

Dashed line with open arrowhead and small circle at source. Connects elements in DIFFERENT pools. `parent` MUST be `"1"` (the page root), NOT a pool.

### Association (Undirected)

```
endArrow=none;dashed=1;strokeColor=#999999;html=1;
```

Dashed line without arrowheads. Links data objects or text annotations to activities.

### Association (Directed)

```
endArrow=open;endFill=0;dashed=1;strokeColor=#999999;html=1;
```

Dashed line with open arrowhead. Shows directional data flow to/from activities.

---

## 6. Data Element Styles

### Data Object

```
shape=mxgraph.bpmn.data;labelPosition=center;verticalLabelPosition=bottom;verticalAlign=top;fillColor=#FFFFFF;strokeColor=#666666;
```

Page-with-folded-corner shape. Represents data required or produced by an activity. Dimensions: 35 x 50.

### Data Store

```
shape=datastore;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#666666;
```

Cylinder shape. Represents a persistent data repository. Dimensions: 60 x 60.

---

## 7. Boundary Event Attachment

To attach an intermediate event to the boundary of an activity, position the event so it overlaps the activity border. Set the event's `parent` to the same container as the activity (the pool or lane), NOT to the activity itself.

**Positioning rule:** Place the boundary event at the bottom edge of the activity. For an activity at `y=90, height=70`, place the boundary event at `y=140` (activity y + height - half event height).

```xml
<!-- Activity -->
<mxCell id="task1" value="Process Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
  <mxGeometry x="200" y="90" width="120" height="70" as="geometry" />
</mxCell>

<!-- Boundary Error Event (overlaps bottom edge of task1) -->
<mxCell id="boundary_err" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=error;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
  <mxGeometry x="240" y="140" width="40" height="40" as="geometry" />
</mxCell>
```
