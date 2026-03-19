# Examples: Template Implementation

Working XML examples for template patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal Empty Template

The simplest valid template: just the structural cells and page settings.

```xml
<mxfile host="app.diagrams.net" type="device">
  <diagram id="blank" name="Blank Diagram">
    <mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="1169" pageHeight="827">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 2. SWOT Analysis Template

A 2x2 grid template for SWOT analysis with labeled quadrants.

```xml
<mxfile host="app.diagrams.net" type="device">
  <diagram id="swot-template" name="SWOT Analysis">
    <mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="1169" pageHeight="827">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Title -->
        <mxCell id="title" value="SWOT Analysis: [Subject]"
                style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=18;fontStyle=1;"
                vertex="1" parent="1">
          <mxGeometry x="300" y="20" width="280" height="40" as="geometry" />
        </mxCell>

        <!-- Strengths (top-left) -->
        <mxCell id="strengths" value="&lt;b&gt;Strengths&lt;/b&gt;&lt;br&gt;&lt;br&gt;- [Strength 1]&lt;br&gt;- [Strength 2]&lt;br&gt;- [Strength 3]"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;verticalAlign=top;align=left;spacingLeft=10;spacingTop=5;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="80" width="240" height="180" as="geometry" />
        </mxCell>

        <!-- Weaknesses (top-right) -->
        <mxCell id="weaknesses" value="&lt;b&gt;Weaknesses&lt;/b&gt;&lt;br&gt;&lt;br&gt;- [Weakness 1]&lt;br&gt;- [Weakness 2]&lt;br&gt;- [Weakness 3]"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;verticalAlign=top;align=left;spacingLeft=10;spacingTop=5;"
                vertex="1" parent="1">
          <mxGeometry x="360" y="80" width="240" height="180" as="geometry" />
        </mxCell>

        <!-- Opportunities (bottom-left) -->
        <mxCell id="opportunities" value="&lt;b&gt;Opportunities&lt;/b&gt;&lt;br&gt;&lt;br&gt;- [Opportunity 1]&lt;br&gt;- [Opportunity 2]&lt;br&gt;- [Opportunity 3]"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;verticalAlign=top;align=left;spacingLeft=10;spacingTop=5;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="280" width="240" height="180" as="geometry" />
        </mxCell>

        <!-- Threats (bottom-right) -->
        <mxCell id="threats" value="&lt;b&gt;Threats&lt;/b&gt;&lt;br&gt;&lt;br&gt;- [Threat 1]&lt;br&gt;- [Threat 2]&lt;br&gt;- [Threat 3]"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;verticalAlign=top;align=left;spacingLeft=10;spacingTop=5;"
                vertex="1" parent="1">
          <mxGeometry x="360" y="280" width="240" height="180" as="geometry" />
        </mxCell>

        <!-- Labels: Internal/External -->
        <mxCell id="label_internal" value="&lt;b&gt;INTERNAL&lt;/b&gt;"
                style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=11;fontColor=#999999;"
                vertex="1" parent="1">
          <mxGeometry x="20" y="160" width="70" height="30" as="geometry" />
        </mxCell>
        <mxCell id="label_external" value="&lt;b&gt;EXTERNAL&lt;/b&gt;"
                style="text;html=1;align=center;verticalAlign=middle;resizable=0;points=[];autosize=1;strokeColor=none;fillColor=none;fontSize=11;fontColor=#999999;"
                vertex="1" parent="1">
          <mxGeometry x="20" y="360" width="70" height="30" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 3. Swimlane Process Template

A 3-lane horizontal swimlane template for cross-functional process flows.

```xml
<mxfile host="app.diagrams.net" type="device">
  <diagram id="swimlane-template" name="Swimlane Process">
    <mxGraphModel dx="1200" dy="800" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="1169" pageHeight="827">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Lane 1 -->
        <mxCell id="lane_1" value="[Role 1]"
                style="swimlane;startSize=30;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
                vertex="1" parent="1">
          <mxGeometry x="40" y="40" width="700" height="160" as="geometry" />
        </mxCell>
        <mxCell id="start" value="Start"
                style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;"
                vertex="1" parent="lane_1">
          <mxGeometry x="30" y="55" width="100" height="35" as="geometry" />
        </mxCell>
        <mxCell id="task_1" value="[Task 1]"
                style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="lane_1">
          <mxGeometry x="180" y="45" width="120" height="50" as="geometry" />
        </mxCell>

        <!-- Lane 2 -->
        <mxCell id="lane_2" value="[Role 2]"
                style="swimlane;startSize=30;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;"
                vertex="1" parent="1">
          <mxGeometry x="40" y="200" width="700" height="160" as="geometry" />
        </mxCell>
        <mxCell id="task_2" value="[Task 2]"
                style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="lane_2">
          <mxGeometry x="180" y="45" width="120" height="50" as="geometry" />
        </mxCell>
        <mxCell id="decision_1" value="[Check?]"
                style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;"
                vertex="1" parent="lane_2">
          <mxGeometry x="370" y="35" width="100" height="70" as="geometry" />
        </mxCell>

        <!-- Lane 3 -->
        <mxCell id="lane_3" value="[Role 3]"
                style="swimlane;startSize=30;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;"
                vertex="1" parent="1">
          <mxGeometry x="40" y="360" width="700" height="160" as="geometry" />
        </mxCell>
        <mxCell id="task_3" value="[Task 3]"
                style="rounded=0;whiteSpace=wrap;html=1;"
                vertex="1" parent="lane_3">
          <mxGeometry x="370" y="45" width="120" height="50" as="geometry" />
        </mxCell>
        <mxCell id="end" value="End"
                style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;"
                vertex="1" parent="lane_3">
          <mxGeometry x="570" y="52" width="100" height="35" as="geometry" />
        </mxCell>

        <!-- Cross-lane connections -->
        <mxCell id="e_start_t1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
                edge="1" parent="1" source="start" target="task_1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_t1_t2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
                edge="1" parent="1" source="task_1" target="task_2">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_t2_d1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
                edge="1" parent="1" source="task_2" target="decision_1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_d1_t3" value="Yes"
                style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
                edge="1" parent="1" source="decision_1" target="task_3">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_d1_t1" value="No"
                style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
                edge="1" parent="1" source="decision_1" target="task_1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_t3_end" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;"
                edge="1" parent="1" source="task_3" target="end">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Key points for swimlane templates:
- Each lane is a `swimlane` container with `startSize=30` for the header.
- Shapes inside a lane use `parent="lane_id"` and coordinates relative to the lane.
- Cross-lane edges use `parent="1"` (the root container) so they route across lane boundaries.

---

## 4. Network Topology Template

A basic network diagram template with cloud, server, and client nodes.

```xml
<mxfile host="app.diagrams.net" type="device">
  <diagram id="network-template" name="Network Topology">
    <mxGraphModel dx="1000" dy="600" grid="1" gridSize="10" guides="1"
                  tooltips="1" connect="1" arrows="1" fold="1"
                  page="1" pageScale="1" pageWidth="1169" pageHeight="827">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />

        <!-- Internet Cloud -->
        <mxCell id="cloud" value="Internet"
                style="ellipse;shape=cloud;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=14;"
                vertex="1" parent="1">
          <mxGeometry x="320" y="40" width="200" height="100" as="geometry" />
        </mxCell>

        <!-- Firewall -->
        <mxCell id="firewall" value="[Firewall]"
                style="shape=mxgraph.cisco.firewalls.firewall;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="385" y="190" width="70" height="55" as="geometry" />
        </mxCell>

        <!-- Switch -->
        <mxCell id="switch" value="[Core Switch]"
                style="shape=mxgraph.cisco.switches.workgroup_switch;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="380" y="310" width="80" height="50" as="geometry" />
        </mxCell>

        <!-- Servers -->
        <mxCell id="server_1" value="[Web Server]"
                style="shape=mxgraph.cisco.servers.standard_server;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="160" y="420" width="60" height="70" as="geometry" />
        </mxCell>
        <mxCell id="server_2" value="[App Server]"
                style="shape=mxgraph.cisco.servers.standard_server;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="390" y="420" width="60" height="70" as="geometry" />
        </mxCell>
        <mxCell id="server_3" value="[DB Server]"
                style="shape=mxgraph.cisco.servers.standard_server;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="620" y="420" width="60" height="70" as="geometry" />
        </mxCell>

        <!-- Connections -->
        <mxCell id="e_cloud_fw" style="endArrow=none;html=1;strokeWidth=2;"
                edge="1" parent="1" source="cloud" target="firewall">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_fw_sw" style="endArrow=none;html=1;strokeWidth=2;"
                edge="1" parent="1" source="firewall" target="switch">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_sw_s1" style="endArrow=none;html=1;strokeWidth=1;"
                edge="1" parent="1" source="switch" target="server_1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_sw_s2" style="endArrow=none;html=1;strokeWidth=1;"
                edge="1" parent="1" source="switch" target="server_2">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e_sw_s3" style="endArrow=none;html=1;strokeWidth=1;"
                edge="1" parent="1" source="switch" target="server_3">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 5. Template Modification: Swapping Content

Starting from the flowchart template in SKILL.md, replace placeholders for a real use case.

### Before (Template)

```xml
<mxCell id="step_1" value="[Step 1]"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
</mxCell>

<mxCell id="decision_1" value="[Condition?]"
        style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="220" width="120" height="80" as="geometry" />
</mxCell>
```

### After (Filled In)

```xml
<mxCell id="step_1" value="Validate User Input"
        style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="1">
  <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
</mxCell>

<mxCell id="decision_1" value="Input&lt;br&gt;Valid?"
        style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="220" width="120" height="80" as="geometry" />
</mxCell>
```

Only the `value` attributes changed. Style, geometry, and IDs remain identical.
