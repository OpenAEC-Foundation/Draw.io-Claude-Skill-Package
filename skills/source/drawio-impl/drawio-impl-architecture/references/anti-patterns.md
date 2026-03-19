# Anti-Patterns: Architecture Diagram Implementation

What NOT to do when generating architecture diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Wrong C4 Colors

### WRONG

```xml
<mxCell id="sys1" value="&lt;b&gt;Order System&lt;/b&gt;&lt;br&gt;[Software System]"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=11;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="150" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="sys1" value="&lt;b&gt;Order System&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Handles order processing and fulfillment"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="150" as="geometry" />
</mxCell>
```

### Why It Fails

C4 diagrams rely on a strict color scheme to communicate meaning at a glance. Using `#dae8fc` (light blue, a Draw.io default) instead of `#1168bd` (C4 internal system blue) breaks the visual language. Readers cannot distinguish internal systems from external systems or containers. ALWAYS use the exact C4 color codes.

---

## AP-02: Missing C4 Label Description

### WRONG

```xml
<mxCell id="sys1" value="Order System"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="150" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="sys1" value="&lt;b&gt;Order System&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Handles order processing and fulfillment"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="150" as="geometry" />
</mxCell>
```

### Why It Fails

C4 model elements ALWAYS require three lines: bold name, type tag in brackets, and a description. Omitting the `[Software System]` type tag and description violates the C4 specification. Without the type tag, readers cannot determine the abstraction level. Without the description, the diagram loses its self-documenting purpose.

---

## AP-03: Mixing C4 Abstraction Levels

### WRONG

Placing a Person, Software System, AND Container on the same page:

```xml
<!-- Person on same page as containers — WRONG -->
<mxCell id="person1" value="Customer" style="shape=mxgraph.c4.person2;..." vertex="1" parent="1">
  <mxGeometry x="350" y="20" width="200" height="180" as="geometry" />
</mxCell>
<mxCell id="sys1" value="E-Commerce [Software System]" style="rounded=1;fillColor=#1168bd;..." vertex="1" parent="1">
  <mxGeometry x="200" y="250" width="300" height="150" as="geometry" />
</mxCell>
<mxCell id="web" value="Web App [Container: React]" style="rounded=1;fillColor=#438dd5;..." vertex="1" parent="1">
  <mxGeometry x="600" y="250" width="240" height="150" as="geometry" />
</mxCell>
```

### RIGHT

System context page shows ONLY persons and software systems. Container page shows a system boundary with containers inside. Use separate `<diagram>` pages for each level.

### Why It Fails

C4 diagrams are designed to zoom in progressively: System Context -> Container -> Component -> Code. Mixing levels on one page creates confusion about the scope being depicted. A system context diagram shows the forest; a container diagram shows the trees. Combining both loses the clarity of each view.

---

## AP-04: Using endArrow=none for C4 Relationships

### WRONG

```xml
<mxCell id="r1" value="Uses" style="endArrow=none;html=1;strokeColor=#707070;"
        edge="1" parent="1" source="person1" target="sys1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="r1" value="Uses" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;"
        edge="1" parent="1" source="person1" target="sys1">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

C4 relationships are directional — they describe who initiates the interaction. "Customer uses E-Commerce System" is different from "E-Commerce System serves Customer." Using `endArrow=none` removes this directionality and makes the diagram ambiguous.

---

## AP-05: Mixing Cloud Provider Stencils in the Same View

### WRONG

```xml
<!-- AWS and Azure icons side by side without separation — WRONG -->
<mxCell id="ec2" value="Web Server" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;..."
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
<mxCell id="sql_db" value="Database" style="shape=mxgraph.azure.sql_database;..."
        vertex="1" parent="1">
  <mxGeometry x="300" y="100" width="50" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- AWS zone -->
<mxCell id="aws_zone" value="AWS" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF9900;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF9900;container=1;collapsible=0;"
        vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="ec2" value="Web Server" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;outlineConnect=0;"
        vertex="1" parent="aws_zone">
  <mxGeometry x="120" y="60" width="60" height="60" as="geometry" />
</mxCell>

<!-- Azure zone -->
<mxCell id="azure_zone" value="Azure" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#0078D4;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#0078D4;container=1;collapsible=0;"
        vertex="1" parent="1">
  <mxGeometry x="400" y="40" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="sql_db" value="Database" style="shape=mxgraph.azure.sql_database;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;"
        vertex="1" parent="azure_zone">
  <mxGeometry x="120" y="60" width="50" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Mixing AWS and Azure stencils without visual separation confuses readers about which cloud provider hosts which resource. In multi-cloud diagrams, ALWAYS place each provider's resources inside a labeled zone container with a provider-specific border color. This makes the cloud boundary explicit.

---

## AP-06: Deployment Nodes Without container=1

### WRONG

```xml
<mxCell id="server" value="Production Server" style="shape=cube;whiteSpace=wrap;html=1;size=10;fillColor=#f5f5f5;strokeColor=#666666;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="60" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="app" value="api-server.jar" style="shape=note;whiteSpace=wrap;html=1;"
        vertex="1" parent="server">
  <mxGeometry x="30" y="50" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="server" value="Production Server" style="shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;verticalAlign=top;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="60" width="300" height="200" as="geometry" />
</mxCell>
<mxCell id="app" value="api-server.jar" style="shape=note;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;"
        vertex="1" parent="server">
  <mxGeometry x="30" y="50" width="120" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Without `container=1`, the cube shape does not function as a container in Draw.io. Child elements with `parent="server"` will render but will NOT move with the server when dragged. The visual containment is fake — it breaks as soon as the user interacts with the diagram.

---

## AP-07: Using Legacy GCP Namespace

### WRONG

```xml
<mxCell id="gce" value="VM Instance" style="shape=mxgraph.gcp.compute_engine;..."
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="gce" value="VM Instance" style="shape=mxgraph.gcp2.compute_engine;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

The `mxgraph.gcp.*` namespace is the legacy GCP stencil set with outdated iconography. The `mxgraph.gcp2.*` namespace contains the current Google Cloud icons. ALWAYS use `gcp2` for new diagrams.

---

## AP-08: Missing fontColor on Dark C4 Backgrounds

### WRONG

```xml
<mxCell id="sys1" value="&lt;b&gt;Order System&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Handles orders"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;strokeColor=#0b4884;fontSize=11;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="150" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="sys1" value="&lt;b&gt;Order System&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Handles orders"
        style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="300" height="150" as="geometry" />
</mxCell>
```

### Why It Fails

Draw.io defaults `fontColor` to black (`#000000`). On a dark blue background (`#1168bd`), black text is nearly invisible. ALWAYS set `fontColor=#ffffff` on Person, Software System, External System, and Container shapes. Component shapes use `fontColor=#000000` because their background (`#85bbf0`) is light enough.
