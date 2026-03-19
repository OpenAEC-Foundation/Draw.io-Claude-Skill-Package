# Examples: BPMN 2.0 Implementation

Working XML examples for BPMN 2.0 patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal BPMN Process (Start, Task, End)

The simplest valid BPMN process: one start event, one task, one end event inside a pool.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Simple Process" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="460" height="150" as="geometry" />
    </mxCell>

    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="30" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="task1" value="Do Work" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="120" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="290" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task1" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Exclusive Gateway (XOR) Branching

A process that splits based on a condition and merges back.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Order Approval" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="780" height="250" as="geometry" />
    </mxCell>

    <!-- Start -->
    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="30" y="105" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Task: Review Order -->
    <mxCell id="task1" value="Review&#xa;Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="120" y="90" width="120" height="70" as="geometry" />
    </mxCell>

    <!-- Exclusive Gateway: Split -->
    <mxCell id="gw1" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="290" y="100" width="50" height="50" as="geometry" />
    </mxCell>

    <!-- Branch A: Approve -->
    <mxCell id="task2" value="Approve" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="400" y="30" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Branch B: Reject -->
    <mxCell id="task3" value="Reject" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="400" y="170" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Exclusive Gateway: Merge -->
    <mxCell id="gw2" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="570" y="100" width="50" height="50" as="geometry" />
    </mxCell>

    <!-- Task: Notify Customer -->
    <mxCell id="task4" value="Notify&#xa;Customer" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="660" y="90" width="120" height="70" as="geometry" />
    </mxCell>

    <!-- End -->
    <mxCell id="end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="730" y="105" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Flows -->
    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task1" target="gw1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f3" value="Approved" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw1" target="task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f4" value="Rejected" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw1" target="task3">
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

---

## 3. Two Pools with Message Flow (Inter-Organizational)

A customer sends an order to a supplier. The supplier processes it and sends a confirmation back.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool 1: Customer -->
    <mxCell id="pool_cust" value="Customer" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="600" height="150" as="geometry" />
    </mxCell>

    <mxCell id="c_start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool_cust">
      <mxGeometry x="30" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="c_task1" value="Place Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool_cust">
      <mxGeometry x="120" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="c_wait" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=message;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool_cust">
      <mxGeometry x="310" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="c_task2" value="Receive&#xa;Confirmation" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool_cust">
      <mxGeometry x="400" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="c_end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool_cust">
      <mxGeometry x="550" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Customer sequence flows -->
    <mxCell id="cf1" style="endArrow=classic;html=1;" edge="1" parent="pool_cust" source="c_start" target="c_task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="cf2" style="endArrow=classic;html=1;" edge="1" parent="pool_cust" source="c_task1" target="c_wait">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="cf3" style="endArrow=classic;html=1;" edge="1" parent="pool_cust" source="c_wait" target="c_task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="cf4" style="endArrow=classic;html=1;" edge="1" parent="pool_cust" source="c_task2" target="c_end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Pool 2: Supplier -->
    <mxCell id="pool_sup" value="Supplier" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="260" width="600" height="150" as="geometry" />
    </mxCell>

    <mxCell id="s_start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=message;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool_sup">
      <mxGeometry x="30" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="s_task1" value="Process&#xa;Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool_sup">
      <mxGeometry x="120" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="s_task2" value="Send&#xa;Confirmation" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool_sup">
      <mxGeometry x="300" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="s_end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool_sup">
      <mxGeometry x="470" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Supplier sequence flows -->
    <mxCell id="sf1" style="endArrow=classic;html=1;" edge="1" parent="pool_sup" source="s_start" target="s_task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="sf2" style="endArrow=classic;html=1;" edge="1" parent="pool_sup" source="s_task1" target="s_task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="sf3" style="endArrow=classic;html=1;" edge="1" parent="pool_sup" source="s_task2" target="s_end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Message Flows (between pools, parent="1") -->
    <mxCell id="mf1" value="Order" style="endArrow=open;endFill=0;startArrow=oval;startFill=0;dashed=1;strokeColor=#666666;html=1;" edge="1" parent="1" source="c_task1" target="s_start">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="mf2" value="Confirmation" style="endArrow=open;endFill=0;startArrow=oval;startFill=0;dashed=1;strokeColor=#666666;html=1;" edge="1" parent="1" source="s_task2" target="c_wait">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Key points demonstrated:
- Message flows use `parent="1"` (the page root), NOT a pool
- Message flows are dashed with open arrowhead and circle at source
- Sequence flows stay within their respective pools
- Each pool has its own start and end events

---

## 4. Parallel Gateway (Fork and Join)

A process that executes two tasks in parallel, then waits for both to complete.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Shipping Process" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="700" height="250" as="geometry" />
    </mxCell>

    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="30" y="105" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Parallel Gateway: Fork -->
    <mxCell id="fork" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=parallelGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="120" y="100" width="50" height="50" as="geometry" />
    </mxCell>

    <!-- Parallel branch A -->
    <mxCell id="taskA" value="Pack Items" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="230" y="30" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Parallel branch B -->
    <mxCell id="taskB" value="Print Label" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="230" y="170" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Parallel Gateway: Join -->
    <mxCell id="join" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=parallelGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="410" y="100" width="50" height="50" as="geometry" />
    </mxCell>

    <mxCell id="task_ship" value="Ship Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="520" y="90" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="660" y="105" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Flows (no condition labels on parallel gateway edges) -->
    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="fork">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="fork" target="taskA">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f3" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="fork" target="taskB">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f4" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="taskA" target="join">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f5" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="taskB" target="join">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f6" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="join" target="task_ship">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f7" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task_ship" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Timer and Error Events with Boundary Event

A process with a timer start event and an error boundary event on a subprocess.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Scheduled Report" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="700" height="280" as="geometry" />
    </mxCell>

    <!-- Timer Start Event -->
    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=timer;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="30" y="80" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Task: Generate Report -->
    <mxCell id="task1" value="Generate&#xa;Report" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="120" y="65" width="120" height="70" as="geometry" />
    </mxCell>

    <!-- Boundary Error Event on task1 (overlaps bottom edge) -->
    <mxCell id="err_boundary" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=catching;symbol=error;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="pool1">
      <mxGeometry x="160" y="115" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Normal path -->
    <mxCell id="task2" value="Send&#xa;Report" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="300" y="65" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="end_ok" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="470" y="80" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Error path -->
    <mxCell id="task_err" value="Log Error" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="300" y="200" width="120" height="50" as="geometry" />
    </mxCell>

    <mxCell id="end_err" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=error;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="470" y="205" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Sequence flows -->
    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task1" target="task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f3" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task2" target="end_ok">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f4" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="err_boundary" target="task_err">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f5" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task_err" target="end_err">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 6. Pool with Lanes (Roles within an Organization)

A hiring process with HR and Manager lanes inside one pool.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool with lanes -->
    <mxCell id="pool1" value="Hiring Process" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="760" height="330" as="geometry" />
    </mxCell>

    <!-- Lane: HR -->
    <mxCell id="lane_hr" value="HR" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="30" width="760" height="150" as="geometry" />
    </mxCell>

    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="lane_hr">
      <mxGeometry x="30" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="t1" value="Screen&#xa;Resumes" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_hr">
      <mxGeometry x="120" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="t3" value="Send Offer" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_hr">
      <mxGeometry x="520" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="lane_hr">
      <mxGeometry x="690" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Lane: Manager -->
    <mxCell id="lane_mgr" value="Hiring Manager" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="180" width="760" height="150" as="geometry" />
    </mxCell>

    <mxCell id="t2" value="Interview&#xa;Candidate" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_mgr">
      <mxGeometry x="220" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="gw1" value="" style="shape=mxgraph.bpmn.shape;perimeter=rhombusPerimeter;outline=standard;symbol=exclusiveGw;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="lane_mgr">
      <mxGeometry x="400" y="50" width="50" height="50" as="geometry" />
    </mxCell>

    <!-- Cross-lane edges use pool as parent -->
    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="t1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="t1" target="t2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f3" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="t2" target="gw1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f4" value="Hire" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw1" target="t3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f5" value="Reject" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="gw1" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f6" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="t3" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Key points demonstrated:
- Lanes are children of the pool (`parent="pool1"`)
- Shapes inside lanes use `parent="lane_hr"` or `parent="lane_mgr"`
- Cross-lane edges use `parent="pool1"` (the common ancestor)
- Lane widths equal pool width (760)
- Pool height = startSize (30) + lane_hr height (150) + lane_mgr height (150) = 330

---

## 7. Data Objects and Data Store

A process that reads from a data store and produces a data object.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Report Generation" style="shape=pool;startSize=30;horizontal=1;container=1;collapsible=0;swimlaneLine=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="560" height="220" as="geometry" />
    </mxCell>

    <mxCell id="start" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=standard;symbol=general;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="pool1">
      <mxGeometry x="30" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <mxCell id="task1" value="Query&#xa;Database" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="120" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="task2" value="Generate&#xa;Report" style="rounded=1;whiteSpace=wrap;html=1;arcSize=20;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="pool1">
      <mxGeometry x="300" y="40" width="120" height="70" as="geometry" />
    </mxCell>

    <mxCell id="end" value="" style="shape=mxgraph.bpmn.shape;perimeter=ellipsePerimeter;outline=end;symbol=terminate;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="pool1">
      <mxGeometry x="470" y="55" width="40" height="40" as="geometry" />
    </mxCell>

    <!-- Data Store -->
    <mxCell id="ds1" value="Customer DB" style="shape=datastore;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#666666;" vertex="1" parent="pool1">
      <mxGeometry x="150" y="150" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- Data Object -->
    <mxCell id="do1" value="Report" style="shape=mxgraph.bpmn.data;labelPosition=center;verticalLabelPosition=bottom;verticalAlign=top;fillColor=#FFFFFF;strokeColor=#666666;" vertex="1" parent="pool1">
      <mxGeometry x="342" y="150" width="35" height="50" as="geometry" />
    </mxCell>

    <!-- Sequence flows -->
    <mxCell id="f1" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="start" target="task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f2" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task1" target="task2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="f3" style="endArrow=classic;html=1;" edge="1" parent="pool1" source="task2" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Associations (dashed, no arrowhead for data store; directed for data object) -->
    <mxCell id="a1" style="endArrow=none;dashed=1;strokeColor=#999999;html=1;" edge="1" parent="pool1" source="ds1" target="task1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="a2" style="endArrow=open;endFill=0;dashed=1;strokeColor=#999999;html=1;" edge="1" parent="pool1" source="task2" target="do1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
