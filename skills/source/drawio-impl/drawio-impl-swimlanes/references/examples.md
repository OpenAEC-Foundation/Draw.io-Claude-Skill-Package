# Examples: Swimlane Implementation

Working XML examples for swimlane patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal 2-Lane Swimlane

The simplest valid swimlane: one pool, two lanes, one shape per lane, one cross-lane edge.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool -->
    <mxCell id="pool1" value="Process" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="400" height="290" as="geometry" />
    </mxCell>

    <!-- Lane 1 -->
    <mxCell id="lane1" value="Team A" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="30" width="400" height="130" as="geometry" />
    </mxCell>

    <mxCell id="t1" value="Task A" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane1">
      <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Lane 2 -->
    <mxCell id="lane2" value="Team B" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="160" width="400" height="130" as="geometry" />
    </mxCell>

    <mxCell id="t2" value="Task B" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane2">
      <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Cross-lane edge -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="t1" target="t2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. 3-Lane Cross-Functional Flowchart with Decision

A business process across three departments with a decision point and labeled branches.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool -->
    <mxCell id="pool1" value="Order Processing" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="700" height="430" as="geometry" />
    </mxCell>

    <!-- Lane: Sales -->
    <mxCell id="lane_sales" value="Sales" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="30" width="700" height="130" as="geometry" />
    </mxCell>

    <mxCell id="t1" value="Receive&lt;br&gt;Order" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="lane_sales">
      <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="t2" value="Validate&lt;br&gt;Order" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_sales">
      <mxGeometry x="220" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="d1" value="Valid?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="lane_sales">
      <mxGeometry x="400" y="25" width="100" height="80" as="geometry" />
    </mxCell>

    <mxCell id="t_reject" value="Reject" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="lane_sales">
      <mxGeometry x="560" y="35" width="100" height="60" as="geometry" />
    </mxCell>

    <!-- Lane: Warehouse -->
    <mxCell id="lane_warehouse" value="Warehouse" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="160" width="700" height="130" as="geometry" />
    </mxCell>

    <mxCell id="t3" value="Pick Items" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_warehouse">
      <mxGeometry x="220" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="t4" value="Pack&lt;br&gt;Shipment" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_warehouse">
      <mxGeometry x="400" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Lane: Finance -->
    <mxCell id="lane_finance" value="Finance" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="290" width="700" height="140" as="geometry" />
    </mxCell>

    <mxCell id="t5" value="Generate&lt;br&gt;Invoice" style="shape=document;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="lane_finance">
      <mxGeometry x="400" y="40" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="t6" value="Complete" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="lane_finance">
      <mxGeometry x="560" y="40" width="100" height="60" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="t1" target="t2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="t2" target="d1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="d1" target="t3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="d1" target="t_reject">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="t3" target="t4">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e6" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="t4" target="t5">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e7" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="t5" target="t6">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Vertical Lanes (Top-to-Bottom Flow)

Lanes side by side with `horizontal=0` and process flowing top-to-bottom.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Pool with vertical lanes -->
    <mxCell id="pool1" value="Approval Workflow" style="swimlane;startSize=30;container=1;collapsible=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="520" height="400" as="geometry" />
    </mxCell>

    <!-- Lane: Requester (vertical, side-by-side) -->
    <mxCell id="lane_req" value="Requester" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=0;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry x="0" y="30" width="260" height="370" as="geometry" />
    </mxCell>

    <mxCell id="v1" value="Submit&lt;br&gt;Request" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="lane_req">
      <mxGeometry x="70" y="50" width="120" height="50" as="geometry" />
    </mxCell>

    <mxCell id="v4" value="Implement&lt;br&gt;Change" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_req">
      <mxGeometry x="70" y="280" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Lane: Approver (vertical, side-by-side) -->
    <mxCell id="lane_app" value="Approver" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=0;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry x="260" y="30" width="260" height="370" as="geometry" />
    </mxCell>

    <mxCell id="v2" value="Review&lt;br&gt;Request" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane_app">
      <mxGeometry x="70" y="50" width="120" height="50" as="geometry" />
    </mxCell>

    <mxCell id="v3" value="Approved?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="lane_app">
      <mxGeometry x="60" y="150" width="100" height="80" as="geometry" />
    </mxCell>

    <mxCell id="v_reject" value="Rejected" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="lane_app">
      <mxGeometry x="70" y="280" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="v1" target="v2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="v2" target="v3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="v3" target="v4">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="v3" target="v_reject">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Key differences for vertical lanes:
- `horizontal=0` on each lane style.
- Lanes use x-coordinates to stack side by side instead of y-coordinates.
- Lane heights equal the pool's content height (pool height minus pool startSize).
- Lane widths divide the pool width evenly.

---

## 4. Nested Lanes (Sub-Lanes)

A pool with a parent lane containing two sub-lanes.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Software Development" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="600" height="360" as="geometry" />
    </mxCell>

    <!-- Parent lane: Engineering -->
    <mxCell id="lane_eng" value="Engineering" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="30" width="600" height="200" as="geometry" />
    </mxCell>

    <!-- Sub-lane: Frontend -->
    <mxCell id="sub_fe" value="Frontend" style="swimlane;startSize=25;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="lane_eng">
      <mxGeometry y="30" width="600" height="85" as="geometry" />
    </mxCell>

    <mxCell id="fe_task" value="Build UI" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sub_fe">
      <mxGeometry x="40" y="28" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Sub-lane: Backend -->
    <mxCell id="sub_be" value="Backend" style="swimlane;startSize=25;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="lane_eng">
      <mxGeometry y="115" width="600" height="85" as="geometry" />
    </mxCell>

    <mxCell id="be_task" value="Build API" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sub_be">
      <mxGeometry x="40" y="28" width="120" height="50" as="geometry" />
    </mxCell>

    <!-- Lane: QA -->
    <mxCell id="lane_qa" value="QA" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#fff2cc;strokeColor=#d6b656;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="230" width="600" height="130" as="geometry" />
    </mxCell>

    <mxCell id="qa_task" value="Integration&lt;br&gt;Testing" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="lane_qa">
      <mxGeometry x="220" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="fe_task" target="qa_task">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="be_task" target="qa_task">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Key points for nested lanes:
- Sub-lanes have `parent` set to the parent lane (NOT the pool).
- Sub-lane y-coordinates are relative to the parent lane.
- Sub-lane widths MUST equal the parent lane width.
- Cross-lane edges connecting shapes in sub-lanes to shapes in other lanes MUST use the pool as parent.

---

## 5. Simple Pool Without Table Layout

Using a plain `swimlane` style for the pool instead of `shape=table`.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="pool1" value="Support Ticket Flow" style="swimlane;startSize=30;container=1;collapsible=0;fontStyle=1;strokeColor=#6c8ebf;fillColor=#dae8fc;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="500" height="290" as="geometry" />
    </mxCell>

    <mxCell id="lane1" value="Customer" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#d5e8d4;strokeColor=#82b366;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="30" width="500" height="130" as="geometry" />
    </mxCell>

    <mxCell id="s1" value="Submit&lt;br&gt;Ticket" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="lane1">
      <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="lane2" value="Support Agent" style="swimlane;startSize=30;container=1;collapsible=0;horizontal=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;" vertex="1" parent="pool1">
      <mxGeometry y="160" width="500" height="130" as="geometry" />
    </mxCell>

    <mxCell id="s2" value="Resolve&lt;br&gt;Issue" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="lane2">
      <mxGeometry x="40" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <mxCell id="s3" value="Close&lt;br&gt;Ticket" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="lane2">
      <mxGeometry x="220" y="35" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="s1" target="s2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="pool1" source="s2" target="s3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

This simpler pool style works when you do not need table row enforcement. The visual result is similar but without automatic row alignment.
