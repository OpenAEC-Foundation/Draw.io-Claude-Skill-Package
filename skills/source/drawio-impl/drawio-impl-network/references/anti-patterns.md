# Anti-Patterns: Network Diagram Implementation

What NOT to do when generating network diagrams in Draw.io, with explanations of why each pattern fails.

---

## AP-01: Using Legacy Cisco Namespace

### WRONG

```xml
<mxCell id="rtr" value="Router" style="shape=mxgraph.cisco.routers.router;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="rtr" value="Router" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.router;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### Why It Fails

The `mxgraph.cisco.*` namespace uses outdated iconography from the legacy Cisco stencil set. The `mxgraph.cisco19.*` namespace is the current set with modern icons. ALWAYS use `cisco19` for new diagrams.

---

## AP-02: Using Directed Arrows for Physical Links

### WRONG

```xml
<mxCell id="link1" style="endArrow=classic;html=1;strokeWidth=2;"
        edge="1" parent="1" source="router" target="switch">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="link1" style="endArrow=none;html=1;strokeWidth=2;"
        edge="1" parent="1" source="router" target="switch">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

### Why It Fails

Physical network links (Ethernet cables, fiber, wireless) are bidirectional. An arrow implies one-way data flow, which is incorrect for physical topology. ALWAYS use `endArrow=none` for physical connections. Reserve `endArrow=classic` for logical data flow overlays only.

---

## AP-03: Using Generic Rectangles for Network Devices

### WRONG

```xml
<mxCell id="fw" value="Firewall" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#FF6666;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="120" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="fw" value="Firewall" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.firewall;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### Why It Fails

Network diagrams rely on visual convention — readers instantly recognize device type from the stencil icon. A generic rectangle forces readers to read the label to identify the device. ALWAYS use the appropriate stencil shape from the correct vendor namespace.

---

## AP-04: Missing Zone Containers

### WRONG

```xml
<!-- DMZ label as a text cell (NOT a container) -->
<mxCell id="dmz_label" value="DMZ" style="text;html=1;fontSize=14;fontStyle=1;fontColor=#FF0000;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="300" width="60" height="30" as="geometry" />
</mxCell>
<!-- Server placed at root level, not inside a zone -->
<mxCell id="srv" value="Web Server" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;..."
        vertex="1" parent="1">
  <mxGeometry x="120" y="340" width="50" height="65" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- DMZ as a container -->
<mxCell id="dmz" value="DMZ" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF0000;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF0000;container=1;collapsible=0;"
        vertex="1" parent="1">
  <mxGeometry x="80" y="300" width="250" height="150" as="geometry" />
</mxCell>
<!-- Server inside the DMZ container -->
<mxCell id="srv" value="Web Server" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;"
        vertex="1" parent="dmz">
  <mxGeometry x="20" y="40" width="50" height="65" as="geometry" />
</mxCell>
```

### Why It Fails

A text label is a visual decoration only — it has no structural relationship to the devices beneath it. When a user moves the "DMZ" label, the servers stay behind. With `container=1`, moving the zone moves all child devices. ALWAYS use containers for network zones and set `parent` on child devices.

---

## AP-05: Missing sketch=0 on Stencil Shapes

### WRONG

```xml
<mxCell id="sw" value="Switch" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.switch;html=1;whiteSpace=wrap;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="sw" value="Switch" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.switch;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### Why It Fails

Without `sketch=0`, Draw.io may render the stencil in hand-drawn "sketch" mode (if the global setting is enabled), distorting the precision iconography. ALWAYS include `sketch=0` on stencil-based shapes to force clean rendering.

---

## AP-06: Missing Label Positioning on Icon Shapes

### WRONG

```xml
<mxCell id="rtr" value="Router" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.router;sketch=0;html=1;whiteSpace=wrap;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<mxCell id="rtr" value="Router" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.router;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;"
        vertex="1" parent="1">
  <mxGeometry x="200" y="200" width="78" height="53" as="geometry" />
</mxCell>
```

### Why It Fails

Without `verticalLabelPosition=bottom;verticalAlign=top;`, the label text renders on top of the icon graphic, making both unreadable. ALWAYS position labels below icon-style shapes.

---

## AP-07: Mixing Cloud Provider Stencils Without Separation

### WRONG

```xml
<!-- AWS and Azure icons in the same flat layout, no zone separation -->
<mxCell id="ec2" value="EC2" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;..." vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="60" height="60" as="geometry" />
</mxCell>
<mxCell id="vm" value="Azure VM" style="shape=mxgraph.azure.virtual_machine;..." vertex="1" parent="1">
  <mxGeometry x="200" y="100" width="60" height="60" as="geometry" />
</mxCell>
```

### RIGHT

```xml
<!-- AWS zone -->
<mxCell id="aws_zone" value="AWS" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF9900;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF9900;container=1;collapsible=0;" vertex="1" parent="1">
  <mxGeometry x="40" y="40" width="250" height="200" as="geometry" />
</mxCell>
<mxCell id="ec2" value="EC2" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;..." vertex="1" parent="aws_zone">
  <mxGeometry x="90" y="60" width="60" height="60" as="geometry" />
</mxCell>

<!-- Azure zone -->
<mxCell id="azure_zone" value="Azure" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#0078D4;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#0078D4;container=1;collapsible=0;" vertex="1" parent="1">
  <mxGeometry x="340" y="40" width="250" height="200" as="geometry" />
</mxCell>
<mxCell id="vm" value="Azure VM" style="shape=mxgraph.azure.virtual_machine;..." vertex="1" parent="azure_zone">
  <mxGeometry x="90" y="60" width="60" height="60" as="geometry" />
</mxCell>
```

### Why It Fails

Mixing cloud provider icons without visual separation creates confusion about which resources belong to which provider. In multi-cloud diagrams, ALWAYS place each provider's resources inside a clearly labeled zone container with the provider's brand color.

---

## AP-08: Using collapsible=1 on Network Zones

### WRONG

```xml
<mxCell id="dmz" value="DMZ" style="...container=1;collapsible=1;..."
        vertex="1" parent="1">
```

### RIGHT

```xml
<mxCell id="dmz" value="DMZ" style="...container=1;collapsible=0;..."
        vertex="1" parent="1">
```

### Why It Fails

Collapsible zones hide their contents when collapsed, making network devices disappear from the diagram. Network zones MUST remain visible at all times. ALWAYS use `collapsible=0`.
