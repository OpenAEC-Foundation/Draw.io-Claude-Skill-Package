# Methods Reference: Network Diagram Implementation

Complete style strings and attribute reference for network shapes, connections, and zones.

---

## 1. Cisco19 Device Styles

### Router

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.router;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 78 x 53. ALWAYS use `cisco19` — NEVER use the legacy `cisco` namespace.

### Switch (Layer 2)

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.switch;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 78 x 53.

### Switch (Layer 3)

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.layer_3_switch;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 78 x 53.

### Firewall

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.firewall;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 78 x 53.

### Server

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 50 x 65. Taller than wide to represent a tower server.

### Wireless Access Point

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.access_point;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 50 x 50.

### Laptop / Workstation

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.laptop;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 50 x 40.

### Load Balancer

```
shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.load_balancer;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;
```

Dimensions: 78 x 53.

---

## 2. AWS Resource Icon Styles

### EC2 Instance

```
shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;fillColor=#ED7100;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

### RDS Database

```
shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.rds;fillColor=#C925D1;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

### S3 Bucket

```
shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.s3;fillColor=#3F8624;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

### Lambda Function

```
shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.lambda;fillColor=#ED7100;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

### ALB / ELB

```
shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.elastic_load_balancing;fillColor=#8C4FFF;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

---

## 3. AWS Group Container Styles

### Region

```
points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_region;strokeColor=#00A4A6;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=1;
```

### VPC

```
points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_vpc;strokeColor=#8C4FFF;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#AAB7B8;dashed=0;
```

### Public Subnet

```
points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_subnet;strokeColor=#7AA116;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#248814;dashed=0;
```

### Private Subnet

```
points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_subnet;strokeColor=#147EBA;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=0;
```

---

## 4. Azure Resource Styles

### Virtual Machine

```
shape=mxgraph.azure.virtual_machine;fillColor=#0078D4;strokeColor=#ffffff;fontColor=#ffffff;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

### SQL Database

```
shape=mxgraph.azure.sql_database;fillColor=#0078D4;strokeColor=#ffffff;fontColor=#ffffff;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 50 x 60.

### Virtual Network

```
shape=mxgraph.azure.virtual_network;fillColor=#0078D4;strokeColor=#ffffff;fontColor=#ffffff;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

---

## 5. GCP Resource Styles

### Compute Engine

```
shape=mxgraph.gcp2.compute_engine;fillColor=#4285F4;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

### Cloud SQL

```
shape=mxgraph.gcp2.cloud_sql;fillColor=#4285F4;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;
```

Dimensions: 60 x 60.

---

## 6. Generic Network Shapes

### Internet Cloud

```
shape=cloud;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=14;
```

Dimensions: 200 x 100.

### Database Cylinder

```
shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;
```

Dimensions: 120 x 80.

---

## 7. Connection Styles

### Physical Link (Bidirectional)

```
endArrow=none;html=1;strokeWidth=2;
```

ALWAYS use for physical network connections. NEVER use `endArrow=classic`.

### Backbone / Trunk Link

```
endArrow=none;html=1;strokeWidth=3;strokeColor=#0066CC;
```

### Redundant / Standby Link

```
endArrow=none;html=1;strokeWidth=2;strokeColor=#CC0000;dashed=1;
```

### Logical Data Flow

```
endArrow=classic;html=1;strokeWidth=1;dashed=1;
```

Use ONLY for logical overlays, NEVER for physical topology.

### Wireless Link

```
endArrow=none;html=1;strokeWidth=1;dashed=1;dashPattern=3 3;strokeColor=#009900;
```

---

## 8. Zone Container Styles

### DMZ

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF0000;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF0000;container=1;collapsible=0;
```

### Internal LAN

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#009900;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#009900;container=1;collapsible=0;
```

### WAN / External

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#0066CC;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#0066CC;container=1;collapsible=0;
```

### Management

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF9900;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF9900;container=1;collapsible=0;
```

---

## 9. Object Wrapper (Metadata)

Use `<object>` for devices that carry IP, hostname, or VLAN metadata:

```xml
<object label="Device Label" id="dev1" ip="10.0.0.1" hostname="dev01" vlan="100">
  <mxCell style="..." vertex="1" parent="1">
    <mxGeometry x="100" y="100" width="78" height="53" as="geometry" />
  </mxCell>
</object>
```

The `label` attribute supports HTML and overrides the `value` attribute. Custom attributes (`ip`, `hostname`, `vlan`) appear in Draw.io tooltips and are accessible via the properties panel.
