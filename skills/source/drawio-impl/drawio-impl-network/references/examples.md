# Examples: Network Diagram Implementation

Working XML examples for network diagram patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal Network (3 Devices)

The simplest valid network: Internet cloud, firewall, and one server.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="cloud" value="Internet" style="shape=cloud;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=14;" vertex="1" parent="1">
      <mxGeometry x="200" y="20" width="200" height="100" as="geometry" />
    </mxCell>
    <mxCell id="fw" value="Firewall" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.firewall;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="261" y="170" width="78" height="53" as="geometry" />
    </mxCell>
    <mxCell id="srv" value="Server" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="275" y="300" width="50" height="65" as="geometry" />
    </mxCell>
    <mxCell id="c1" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="cloud" target="fw">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c2" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="fw" target="srv">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Star Topology (Switch + 4 Endpoints)

A central switch with four connected workstations in a star pattern.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Central Switch -->
    <mxCell id="sw" value="Access Switch" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.switch;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="261" y="220" width="78" height="53" as="geometry" />
    </mxCell>

    <!-- Workstations arranged around the switch -->
    <mxCell id="ws1" value="PC-1" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.laptop;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="50" height="40" as="geometry" />
    </mxCell>
    <mxCell id="ws2" value="PC-2" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.laptop;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="450" y="100" width="50" height="40" as="geometry" />
    </mxCell>
    <mxCell id="ws3" value="PC-3" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.laptop;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="100" y="370" width="50" height="40" as="geometry" />
    </mxCell>
    <mxCell id="ws4" value="PC-4" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.laptop;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="450" y="370" width="50" height="40" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="l1" style="endArrow=none;html=1;strokeWidth=1;" edge="1" parent="1" source="sw" target="ws1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="l2" style="endArrow=none;html=1;strokeWidth=1;" edge="1" parent="1" source="sw" target="ws2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="l3" style="endArrow=none;html=1;strokeWidth=1;" edge="1" parent="1" source="sw" target="ws3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="l4" style="endArrow=none;html=1;strokeWidth=1;" edge="1" parent="1" source="sw" target="ws4">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Three-Tier Enterprise Network with Zones

Full enterprise network with Internet, firewall, core, distribution, and access layers with zone boundaries.

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Internet -->
    <mxCell id="inet" value="Internet" style="shape=cloud;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=14;" vertex="1" parent="1">
      <mxGeometry x="300" y="20" width="200" height="100" as="geometry" />
    </mxCell>

    <!-- Edge Firewall -->
    <mxCell id="fw" value="Edge FW" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.firewall;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="361" y="170" width="78" height="53" as="geometry" />
    </mxCell>

    <!-- Core Router -->
    <mxCell id="core" value="Core RTR" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.router;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="361" y="290" width="78" height="53" as="geometry" />
    </mxCell>

    <!-- Distribution Switches -->
    <mxCell id="dsw1" value="Dist SW-1" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.layer_3_switch;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="161" y="420" width="78" height="53" as="geometry" />
    </mxCell>
    <mxCell id="dsw2" value="Dist SW-2" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.layer_3_switch;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
      <mxGeometry x="561" y="420" width="78" height="53" as="geometry" />
    </mxCell>

    <!-- DMZ Zone -->
    <mxCell id="dmz" value="DMZ (10.0.1.0/24)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#FF0000;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#FF0000;container=1;collapsible=0;" vertex="1" parent="1">
      <mxGeometry x="60" y="550" width="280" height="200" as="geometry" />
    </mxCell>

    <!-- Servers in DMZ -->
    <mxCell id="web1" value="Web-01" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="dmz">
      <mxGeometry x="30" y="50" width="50" height="65" as="geometry" />
    </mxCell>
    <mxCell id="web2" value="Web-02" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="dmz">
      <mxGeometry x="140" y="50" width="50" height="65" as="geometry" />
    </mxCell>

    <!-- Internal LAN Zone -->
    <mxCell id="lan" value="Internal LAN (10.0.2.0/24)" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#009900;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#009900;container=1;collapsible=0;" vertex="1" parent="1">
      <mxGeometry x="460" y="550" width="280" height="200" as="geometry" />
    </mxCell>

    <!-- Servers in LAN -->
    <mxCell id="app1" value="App-01" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="lan">
      <mxGeometry x="30" y="50" width="50" height="65" as="geometry" />
    </mxCell>
    <mxCell id="db1" value="DB-01" style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="lan">
      <mxGeometry x="140" y="50" width="50" height="65" as="geometry" />
    </mxCell>

    <!-- Core connections -->
    <mxCell id="e1" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="inet" target="fw">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="fw" target="core">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="core" target="dsw1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="core" target="dsw2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="dsw1" target="dmz">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e6" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="dsw2" target="lan">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Redundant cross-link -->
    <mxCell id="e7" style="endArrow=none;html=1;strokeWidth=2;strokeColor=#CC0000;dashed=1;" edge="1" parent="1" source="dsw1" target="dsw2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. AWS VPC Architecture

AWS cloud architecture with Region, VPC, public/private subnets, and services.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Region -->
    <mxCell id="region" value="eu-west-1" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_region;strokeColor=#00A4A6;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="600" height="400" as="geometry" />
    </mxCell>

    <!-- VPC -->
    <mxCell id="vpc" value="VPC 10.0.0.0/16" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_vpc;strokeColor=#8C4FFF;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#AAB7B8;dashed=0;" vertex="1" parent="region">
      <mxGeometry x="20" y="40" width="560" height="340" as="geometry" />
    </mxCell>

    <!-- Public Subnet -->
    <mxCell id="pub_sub" value="Public 10.0.1.0/24" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_subnet;strokeColor=#7AA116;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#248814;dashed=0;" vertex="1" parent="vpc">
      <mxGeometry x="20" y="40" width="240" height="270" as="geometry" />
    </mxCell>

    <!-- Private Subnet -->
    <mxCell id="priv_sub" value="Private 10.0.2.0/24" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_subnet;strokeColor=#147EBA;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=0;" vertex="1" parent="vpc">
      <mxGeometry x="290" y="40" width="240" height="270" as="geometry" />
    </mxCell>

    <!-- ALB in public subnet -->
    <mxCell id="alb" value="ALB" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.elastic_load_balancing;fillColor=#8C4FFF;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;" vertex="1" parent="pub_sub">
      <mxGeometry x="90" y="50" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- EC2 in public subnet -->
    <mxCell id="ec2_web" value="Web EC2" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;fillColor=#ED7100;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;" vertex="1" parent="pub_sub">
      <mxGeometry x="90" y="160" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- RDS in private subnet -->
    <mxCell id="rds" value="RDS MySQL" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.rds;fillColor=#C925D1;strokeColor=#ffffff;fontColor=#232F3E;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;html=1;" vertex="1" parent="priv_sub">
      <mxGeometry x="90" y="100" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="a1" style="endArrow=classic;html=1;strokeWidth=1;" edge="1" parent="vpc" source="alb" target="ec2_web">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="a2" style="endArrow=classic;html=1;strokeWidth=1;" edge="1" parent="vpc" source="ec2_web" target="rds">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Rack Diagram

A simple server rack with stacked components.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Rack frame -->
    <mxCell id="rack" value="Rack A-01" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#333333;strokeWidth=2;verticalAlign=top;fontStyle=1;fontSize=12;container=1;collapsible=0;" vertex="1" parent="1">
      <mxGeometry x="100" y="40" width="220" height="440" as="geometry" />
    </mxCell>

    <!-- 1U Patch Panel -->
    <mxCell id="pp" value="Patch Panel (1U)" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=10;" vertex="1" parent="rack">
      <mxGeometry x="10" y="30" width="200" height="20" as="geometry" />
    </mxCell>

    <!-- 2U Core Switch -->
    <mxCell id="csw" value="Core Switch (2U)" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=10;" vertex="1" parent="rack">
      <mxGeometry x="10" y="60" width="200" height="40" as="geometry" />
    </mxCell>

    <!-- 1U Cable Management -->
    <mxCell id="cm1" value="Cable Mgmt" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#999999;fontSize=9;" vertex="1" parent="rack">
      <mxGeometry x="10" y="110" width="200" height="20" as="geometry" />
    </mxCell>

    <!-- 1U Server 1 -->
    <mxCell id="s1" value="Web Server 01 (1U)" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=10;" vertex="1" parent="rack">
      <mxGeometry x="10" y="140" width="200" height="20" as="geometry" />
    </mxCell>

    <!-- 1U Server 2 -->
    <mxCell id="s2" value="Web Server 02 (1U)" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=10;" vertex="1" parent="rack">
      <mxGeometry x="10" y="170" width="200" height="20" as="geometry" />
    </mxCell>

    <!-- 4U Storage -->
    <mxCell id="stor" value="SAN Storage (4U)" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontSize=10;" vertex="1" parent="rack">
      <mxGeometry x="10" y="200" width="200" height="80" as="geometry" />
    </mxCell>

    <!-- 2U UPS -->
    <mxCell id="ups" value="UPS (2U)" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=10;" vertex="1" parent="rack">
      <mxGeometry x="10" y="370" width="200" height="40" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 6. Device with IP Metadata (Object Wrapper)

Using the `<object>` element to attach IP and hostname metadata.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <object label="Core Router&lt;br&gt;&lt;font style=&quot;font-size:10px&quot;&gt;10.0.0.1&lt;/font&gt;" id="rtr" ip="10.0.0.1" hostname="core-rtr01" role="core">
      <mxCell style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.router;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
        <mxGeometry x="200" y="100" width="78" height="53" as="geometry" />
      </mxCell>
    </object>

    <object label="Web Server&lt;br&gt;&lt;font style=&quot;font-size:10px&quot;&gt;10.0.1.10&lt;/font&gt;" id="web" ip="10.0.1.10" hostname="web01" role="dmz">
      <mxCell style="shape=mxgraph.cisco19.rect;prIcon=mxgraph.cisco19.server;fillColor=#FAFAFA;strokeColor=#005073;sketch=0;html=1;verticalLabelPosition=bottom;verticalAlign=top;align=center;whiteSpace=wrap;" vertex="1" parent="1">
        <mxGeometry x="200" y="250" width="50" height="65" as="geometry" />
      </mxCell>
    </object>

    <mxCell id="link1" value="VLAN 10" style="endArrow=none;html=1;strokeWidth=2;" edge="1" parent="1" source="rtr" target="web">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
