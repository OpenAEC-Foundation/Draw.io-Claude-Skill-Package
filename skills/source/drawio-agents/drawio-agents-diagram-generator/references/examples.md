# Examples: Diagram Generator Agent

Working examples showing the complete generation pipeline from user request to validated XML output.

---

## 1. Simple Flowchart Generation

### User Request

"Create a diagram showing a user login process"

### Pipeline Execution

```
Step 1 — PARSE INTENT:
  Subject: login process
  Relationships: sequential (process implies steps)
  Hierarchy: none
  Flow direction: sequential
  Explicit type: none
  Keywords matched: "process" -> FLOWCHART

Step 2 — SELECT TYPE:
  Flowchart score: 2 (process + sequential)
  No ambiguity. Selected: flowchart

Step 3 — LOAD SKILL:
  Primary: drawio-impl-flowcharts
  Shapes: terminator, process, decision, data I/O
  Layout: top-to-bottom

Step 4 — GENERATE XML:
  (see output below)

Step 5 — VALIDATE:
  All checks passed.
```

### Generated XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="start" value="Start" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
    </mxCell>

    <mxCell id="enter_creds" value="Enter Username&lt;br&gt;&amp; Password" style="shape=parallelogram;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;" vertex="1" parent="1">
      <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="validate" value="Validate&lt;br&gt;Credentials" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="220" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="valid_check" value="Valid?" style="rhombus;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="200" y="320" width="120" height="80" as="geometry" />
    </mxCell>

    <mxCell id="dashboard" value="Show Dashboard" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="190" y="440" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="error_msg" value="Show Error&lt;br&gt;Message" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="400" y="340" width="140" height="60" as="geometry" />
    </mxCell>

    <mxCell id="end" value="End" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
      <mxGeometry x="200" y="540" width="120" height="40" as="geometry" />
    </mxCell>

    <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="start" target="enter_creds">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="enter_creds" target="validate">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="validate" target="valid_check">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" value="Yes" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="valid_check" target="dashboard">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" value="No" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="valid_check" target="error_msg">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e6" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="error_msg" target="enter_creds">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e7" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="dashboard" target="end">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Ambiguous Request — Disambiguation Required

### User Request

"Visualize our system"

### Pipeline Execution

```
Step 1 — PARSE INTENT:
  Subject: "our system"
  Relationships: unclear
  Hierarchy: unclear
  Explicit type: none
  Keywords matched: "system" -> ARCHITECTURE (weak)

Step 2 — SELECT TYPE:
  Architecture score: 1 (weak — "system" alone is insufficient)
  Network score: 0
  UML score: 0
  Result: AMBIGUOUS — must ask user.
```

### Agent Response

```
Your request could be represented as:
1. **Architecture diagram** — Best for showing cloud services, APIs, and system components.
2. **Network diagram** — Best for showing physical/logical network topology and devices.
3. **UML component diagram** — Best for showing software modules and their interfaces.

Which type fits your needs? (Or describe what you want in more detail.)
```

### After User Clarifies: "It's a cloud architecture with AWS services"

```
Step 2 (resumed) — SELECT TYPE:
  Architecture score: 3 (explicit "cloud architecture" + "AWS")
  Selected: architecture

Step 3 — LOAD SKILL:
  Primary: drawio-impl-architecture
  Proceed with generation...
```

---

## 3. ER Diagram Generation

### User Request

"Create an ER diagram for a blog system with users, posts, and comments"

### Pipeline Execution

```
Step 1 — PARSE INTENT:
  Subject: blog system database
  Relationships: users have posts, posts have comments
  Explicit type: "ER diagram"
  Keywords matched: "ER diagram" -> ER DIAGRAM (strong)

Step 2 — SELECT TYPE:
  ER diagram score: 3 (explicit mention)
  Selected: ER diagram

Step 3 — LOAD SKILL:
  Primary: drawio-impl-er-diagrams
```

### Generated XML

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Users Entity -->
    <mxCell id="users_header" value="users" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="users_r1" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="users_header">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r1_k" value="PK" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;fontStyle=1;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r1">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r1_v" value="id INT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r1">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r2" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="users_header">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r2_k" value="" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r2">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r2_v" value="username VARCHAR" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r2">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r3" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="users_header">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r3_k" value="" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r3">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r3_v" value="email VARCHAR" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r3">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r4" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="users_header">
      <mxGeometry y="120" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r4_k" value="" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r4">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="users_r4_v" value="created_at DATETIME" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="users_r4">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>

    <!-- Posts Entity -->
    <mxCell id="posts_header" value="posts" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#d5e8d4;strokeColor=#82b366;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="340" y="40" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="posts_r1" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="posts_header">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r1_k" value="PK" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;fontStyle=1;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r1">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r1_v" value="id INT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r1">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r2" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="posts_header">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r2_k" value="FK" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;fontStyle=2;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r2">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r2_v" value="user_id INT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r2">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r3" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="posts_header">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r3_k" value="" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r3">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r3_v" value="title VARCHAR" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r3">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r4" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="posts_header">
      <mxGeometry y="120" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r4_k" value="" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r4">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="posts_r4_v" value="body TEXT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="posts_r4">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>

    <!-- Comments Entity -->
    <mxCell id="comments_header" value="comments" style="shape=table;startSize=30;container=1;collapsible=0;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#fff2cc;strokeColor=#d6b656;whiteSpace=wrap;html=1;" vertex="1" parent="1">
      <mxGeometry x="640" y="40" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="comments_r1" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="comments_header">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r1_k" value="PK" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;fontStyle=1;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r1">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r1_v" value="id INT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r1">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r2" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="comments_header">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r2_k" value="FK" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;fontStyle=2;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r2">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r2_v" value="post_id INT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r2">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r3" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="comments_header">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r3_k" value="FK" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;fontStyle=2;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r3">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r3_v" value="user_id INT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r3">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r4" value="" style="shape=tableRow;horizontal=0;startSize=0;swimlaneHead=0;swimlaneBody=0;fillColor=none;collapsible=0;dropTarget=0;points=[[0,0.5],[1,0.5]];portConstraint=eastwest;fontSize=12;whiteSpace=wrap;html=1;" vertex="1" parent="comments_header">
      <mxGeometry y="120" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r4_k" value="" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r4">
      <mxGeometry width="40" height="30" as="geometry" />
    </mxCell>
    <mxCell id="comments_r4_v" value="body TEXT" style="shape=partialRectangle;connectable=0;fillColor=none;top=0;left=0;bottom=0;right=0;overflow=hidden;whiteSpace=wrap;html=1;" vertex="1" parent="comments_r4">
      <mxGeometry x="40" width="160" height="30" as="geometry" />
    </mxCell>

    <!-- Relationships -->
    <mxCell id="rel_user_post" style="edgeStyle=orthogonalEdgeStyle;endArrow=ERmany;startArrow=ERone;endFill=0;startFill=0;html=1;" edge="1" parent="1" source="users_r1" target="posts_r2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="rel_post_comment" style="edgeStyle=orthogonalEdgeStyle;endArrow=ERmany;startArrow=ERone;endFill=0;startFill=0;html=1;" edge="1" parent="1" source="posts_r1" target="comments_r2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="rel_user_comment" style="edgeStyle=orthogonalEdgeStyle;endArrow=ERmany;startArrow=ERone;endFill=0;startFill=0;html=1;" edge="1" parent="1" source="users_r1" target="comments_r3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. Multi-Page Diagram Generation

### User Request

"Create a diagram with the system architecture on page 1 and the deployment flow on page 2"

### Pipeline Execution

```
Step 1 — PARSE INTENT:
  Multi-page request detected.
  Page 1: architecture diagram
  Page 2: flowchart (deployment flow)

Step 2 — SELECT TYPE:
  Page 1: architecture (explicit)
  Page 2: flowchart (explicit "flow")

Step 3 — LOAD SKILLS:
  Page 1: drawio-impl-architecture
  Page 2: drawio-impl-flowcharts
```

### Generated XML (Multi-Page Structure)

```xml
<mxfile>
  <diagram name="System Architecture" id="arch_page">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Architecture cells here -->
        <mxCell id="frontend" value="Frontend&lt;br&gt;(React)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
          <mxGeometry x="40" y="200" width="140" height="60" as="geometry" />
        </mxCell>
        <mxCell id="api" value="API Gateway" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
          <mxGeometry x="260" y="200" width="140" height="60" as="geometry" />
        </mxCell>
        <mxCell id="db" value="PostgreSQL" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;" vertex="1" parent="1">
          <mxGeometry x="480" y="190" width="120" height="80" as="geometry" />
        </mxCell>
        <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="frontend" target="api">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="api" target="db">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram name="Deployment Flow" id="deploy_page">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <!-- Deployment flowchart cells here -->
        <mxCell id="start" value="Start Deploy" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
          <mxGeometry x="200" y="40" width="120" height="40" as="geometry" />
        </mxCell>
        <mxCell id="build" value="Build Docker&lt;br&gt;Image" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
          <mxGeometry x="190" y="120" width="140" height="60" as="geometry" />
        </mxCell>
        <mxCell id="test" value="Run Tests" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
          <mxGeometry x="190" y="220" width="140" height="60" as="geometry" />
        </mxCell>
        <mxCell id="deploy_end" value="Deploy to&lt;br&gt;Production" style="rounded=1;whiteSpace=wrap;html=1;arcSize=50;fillColor=#f8cecc;strokeColor=#b85450;" vertex="1" parent="1">
          <mxGeometry x="200" y="320" width="120" height="40" as="geometry" />
        </mxCell>
        <mxCell id="e1" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="start" target="build">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e2" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="build" target="test">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        <mxCell id="e3" style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;" edge="1" parent="1" source="test" target="deploy_end">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 5. Mermaid Conversion Request

### User Request

"Convert this Mermaid diagram to Draw.io:
```
graph TD
    A[Start] --> B{Is it raining?}
    B -->|Yes| C[Take umbrella]
    B -->|No| D[Go outside]
    C --> D
```
"

### Pipeline Execution

```
Step 1 — PARSE INTENT:
  Source format: Mermaid syntax
  Keywords matched: "Convert", "Mermaid" -> MERMAID CONVERSION (strong)

Step 2 — SELECT TYPE:
  Mermaid conversion score: 3 (explicit)
  Selected: Mermaid conversion

Step 3 — LOAD SKILL:
  Primary: drawio-impl-mermaid-conversion

Step 4 — GENERATE:
  Use MCP tool open_drawio_mermaid with the Mermaid syntax.
  The MCP server handles the conversion and opens the result.
```

### Agent Response

```
This is a Mermaid flowchart. I will use the open_drawio_mermaid MCP tool
to convert and open it directly in Draw.io.

[Calls open_drawio_mermaid with the Mermaid syntax]

The diagram has been opened in Draw.io. It contains:
- 4 shapes: Start, decision (Is it raining?), Take umbrella, Go outside
- 4 connections with Yes/No labels on the decision branches
```
