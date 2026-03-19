# Examples: Architecture Diagram Implementation

Working XML examples for architecture diagram patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. C4 System Context Diagram

A complete system context showing a person, two internal systems, and two external systems.

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <mxCell id="person1" value="&lt;b&gt;Customer&lt;/b&gt;&lt;br&gt;[Person]&lt;br&gt;&lt;br&gt;Uses the web app to browse products and place orders" style="shape=mxgraph.c4.person2;whiteSpace=wrap;html=1;align=center;metaEdit=1;points=[[0.5,0,0],[1,0.5,0],[1,0.75,0],[0.75,1,0],[0.5,1,0],[0.25,1,0],[0,0.75,0],[0,0.5,0]];fillColor=#08427b;fontColor=#ffffff;strokeColor=#073763;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="350" y="20" width="200" height="180" as="geometry" />
    </mxCell>

    <mxCell id="sys1" value="&lt;b&gt;E-Commerce Platform&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Handles product catalog, shopping cart, and order processing" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="300" y="300" width="300" height="150" as="geometry" />
    </mxCell>

    <mxCell id="sys2" value="&lt;b&gt;Inventory System&lt;/b&gt;&lt;br&gt;[Software System]&lt;br&gt;&lt;br&gt;Tracks stock levels across warehouses" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="300" y="520" width="300" height="150" as="geometry" />
    </mxCell>

    <mxCell id="ext1" value="&lt;b&gt;Payment Gateway&lt;/b&gt;&lt;br&gt;[External System]&lt;br&gt;&lt;br&gt;Processes payments via Stripe API" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#999999;fontColor=#ffffff;strokeColor=#8A8A8A;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="700" y="300" width="240" height="150" as="geometry" />
    </mxCell>

    <mxCell id="ext2" value="&lt;b&gt;Email Service&lt;/b&gt;&lt;br&gt;[External System]&lt;br&gt;&lt;br&gt;Sends transactional emails via SendGrid" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#999999;fontColor=#ffffff;strokeColor=#8A8A8A;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="700" y="520" width="240" height="150" as="geometry" />
    </mxCell>

    <mxCell id="r1" value="Browses and places orders" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="person1" target="sys1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r2" value="Sends payment requests to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="sys1" target="ext1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r3" value="Sends emails using" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="sys1" target="ext2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r4" value="Queries stock levels from" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="sys1" target="sys2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. C4 Container Diagram

Zooms into the E-Commerce Platform system, showing its containers.

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Person -->
    <mxCell id="person1" value="&lt;b&gt;Customer&lt;/b&gt;&lt;br&gt;[Person]&lt;br&gt;&lt;br&gt;Uses the web app" style="shape=mxgraph.c4.person2;whiteSpace=wrap;html=1;align=center;metaEdit=1;points=[[0.5,0,0],[1,0.5,0],[1,0.75,0],[0.75,1,0],[0.5,1,0],[0.25,1,0],[0,0.75,0],[0,0.5,0]];fillColor=#08427b;fontColor=#ffffff;strokeColor=#073763;fontSize=11;" vertex="1" parent="1">
      <mxGeometry x="350" y="20" width="200" height="180" as="geometry" />
    </mxCell>

    <!-- System Boundary -->
    <mxCell id="boundary" value="E-Commerce Platform [Software System]" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#1168bd;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#1168bd;container=1;collapsible=0;" vertex="1" parent="1">
      <mxGeometry x="100" y="260" width="700" height="350" as="geometry" />
    </mxCell>

    <!-- Containers inside boundary -->
    <mxCell id="web" value="&lt;b&gt;Web Application&lt;/b&gt;&lt;br&gt;[Container: React]&lt;br&gt;&lt;br&gt;Delivers the storefront SPA to the browser" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#438dd5;fontColor=#ffffff;strokeColor=#3C7FC0;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="30" y="50" width="240" height="120" as="geometry" />
    </mxCell>

    <mxCell id="api" value="&lt;b&gt;API Server&lt;/b&gt;&lt;br&gt;[Container: Node.js Express]&lt;br&gt;&lt;br&gt;Handles REST API requests for products, cart, orders" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#438dd5;fontColor=#ffffff;strokeColor=#3C7FC0;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="310" y="50" width="240" height="120" as="geometry" />
    </mxCell>

    <mxCell id="db" value="&lt;b&gt;Database&lt;/b&gt;&lt;br&gt;[Container: PostgreSQL]&lt;br&gt;&lt;br&gt;Stores product catalog, user accounts, and orders" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#438dd5;fontColor=#ffffff;strokeColor=#3C7FC0;fontSize=11;align=center;size=10;" vertex="1" parent="boundary">
      <mxGeometry x="180" y="220" width="200" height="100" as="geometry" />
    </mxCell>

    <mxCell id="queue" value="&lt;b&gt;Message Queue&lt;/b&gt;&lt;br&gt;[Container: RabbitMQ]&lt;br&gt;&lt;br&gt;Handles async order processing events" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#438dd5;fontColor=#ffffff;strokeColor=#3C7FC0;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="430" y="220" width="240" height="100" as="geometry" />
    </mxCell>

    <!-- External System -->
    <mxCell id="ext1" value="&lt;b&gt;Payment Gateway&lt;/b&gt;&lt;br&gt;[External System]&lt;br&gt;&lt;br&gt;Processes payments" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#999999;fontColor=#ffffff;strokeColor=#8A8A8A;fontSize=11;align=center;" vertex="1" parent="1">
      <mxGeometry x="860" y="340" width="200" height="120" as="geometry" />
    </mxCell>

    <!-- Relationships -->
    <mxCell id="r1" value="Visits" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="person1" target="web">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r2" value="Makes API calls to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="web" target="api">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r3" value="Reads/writes" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="api" target="db">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r4" value="Publishes events to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;dashed=1;" edge="1" parent="1" source="api" target="queue">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r5" value="Sends payment requests to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="api" target="ext1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. AWS Architecture Diagram

A typical three-tier AWS architecture with Region, VPC, and subnet nesting.

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Region -->
    <mxCell id="region" value="eu-west-1" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_region;strokeColor=#00A4A6;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=1;" vertex="1" parent="1">
      <mxGeometry x="40" y="40" width="700" height="500" as="geometry" />
    </mxCell>

    <!-- VPC -->
    <mxCell id="vpc" value="VPC 10.0.0.0/16" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_vpc;strokeColor=#8C4FFF;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#AAB7B8;dashed=0;" vertex="1" parent="region">
      <mxGeometry x="20" y="40" width="660" height="440" as="geometry" />
    </mxCell>

    <!-- Public Subnet -->
    <mxCell id="pub_subnet" value="Public Subnet 10.0.1.0/24" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_subnet;strokeColor=#7AA116;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#248814;dashed=0;" vertex="1" parent="vpc">
      <mxGeometry x="20" y="40" width="280" height="370" as="geometry" />
    </mxCell>

    <!-- Private Subnet -->
    <mxCell id="priv_subnet" value="Private Subnet 10.0.2.0/24" style="points=[[0,0],[0.25,0],[0.5,0],[0.75,0],[1,0],[1,0.25],[1,0.5],[1,0.75],[1,1],[0.75,1],[0.5,1],[0.25,1],[0,1],[0,0.75],[0,0.5],[0,0.25]];outlineConnect=0;gradientColor=none;html=1;whiteSpace=wrap;fontSize=12;fontStyle=1;container=1;pointerEvents=0;collapsible=0;recursiveResize=0;shape=mxgraph.aws4.group;grIcon=mxgraph.aws4.group_subnet;strokeColor=#147EBA;fillColor=none;verticalAlign=top;align=left;spacingLeft=30;fontColor=#147EBA;dashed=0;" vertex="1" parent="vpc">
      <mxGeometry x="340" y="40" width="280" height="370" as="geometry" />
    </mxCell>

    <!-- ALB in public subnet -->
    <mxCell id="alb" value="ALB" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.elastic_load_balancing;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;outlineConnect=0;" vertex="1" parent="pub_subnet">
      <mxGeometry x="110" y="60" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- EC2 in public subnet -->
    <mxCell id="ec2_web" value="Web Server" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;outlineConnect=0;" vertex="1" parent="pub_subnet">
      <mxGeometry x="110" y="180" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- EC2 in private subnet -->
    <mxCell id="ec2_app" value="App Server" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.ec2;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;outlineConnect=0;" vertex="1" parent="priv_subnet">
      <mxGeometry x="110" y="60" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- RDS in private subnet -->
    <mxCell id="rds" value="PostgreSQL" style="shape=mxgraph.aws4.resourceIcon;resIcon=mxgraph.aws4.rds;sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;outlineConnect=0;" vertex="1" parent="priv_subnet">
      <mxGeometry x="110" y="200" width="60" height="60" as="geometry" />
    </mxCell>

    <!-- Connections -->
    <mxCell id="c1" value="Routes to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="alb" target="ec2_web">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c2" value="API calls" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="ec2_web" target="ec2_app">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="c3" value="Reads/writes" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="ec2_app" target="rds">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. Deployment Diagram

A production environment with two servers containing application and database artifacts.

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Production Environment -->
    <mxCell id="prod" value="&lt;b&gt;Production Environment&lt;/b&gt;" style="shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;verticalAlign=top;" vertex="1" parent="1">
      <mxGeometry x="60" y="40" width="600" height="280" as="geometry" />
    </mxCell>

    <!-- App Server -->
    <mxCell id="app_server" value="&lt;b&gt;App Server&lt;/b&gt;&lt;br&gt;Ubuntu 22.04 LTS" style="shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;verticalAlign=top;" vertex="1" parent="prod">
      <mxGeometry x="20" y="50" width="260" height="200" as="geometry" />
    </mxCell>

    <!-- API artifact -->
    <mxCell id="api_jar" value="api-server.jar" style="shape=note;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="app_server">
      <mxGeometry x="30" y="50" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- Worker artifact -->
    <mxCell id="worker" value="worker.jar" style="shape=note;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="app_server">
      <mxGeometry x="30" y="120" width="120" height="60" as="geometry" />
    </mxCell>

    <!-- DB Server -->
    <mxCell id="db_server" value="&lt;b&gt;DB Server&lt;/b&gt;&lt;br&gt;Ubuntu 22.04 LTS" style="shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;verticalAlign=top;" vertex="1" parent="prod">
      <mxGeometry x="320" y="50" width="260" height="200" as="geometry" />
    </mxCell>

    <!-- PostgreSQL artifact -->
    <mxCell id="pg" value="PostgreSQL 16" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;size=10;" vertex="1" parent="db_server">
      <mxGeometry x="70" y="60" width="100" height="80" as="geometry" />
    </mxCell>

    <!-- Connection -->
    <mxCell id="c1" value="JDBC" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="api_jar" target="pg">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. C4 Component Diagram

Zooms into the API Server container, showing internal components.

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1169" pageHeight="827">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Container Boundary -->
    <mxCell id="boundary" value="API Server [Container: Node.js Express]" style="rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#438dd5;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#438dd5;container=1;collapsible=0;" vertex="1" parent="1">
      <mxGeometry x="60" y="40" width="700" height="400" as="geometry" />
    </mxCell>

    <!-- Components -->
    <mxCell id="ctrl" value="&lt;b&gt;Order Controller&lt;/b&gt;&lt;br&gt;[Component: Express Router]&lt;br&gt;&lt;br&gt;Handles HTTP requests for order operations" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#85bbf0;fontColor=#000000;strokeColor=#78A8D8;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="30" y="50" width="200" height="120" as="geometry" />
    </mxCell>

    <mxCell id="svc" value="&lt;b&gt;Order Service&lt;/b&gt;&lt;br&gt;[Component: Business Logic]&lt;br&gt;&lt;br&gt;Validates and processes orders" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#85bbf0;fontColor=#000000;strokeColor=#78A8D8;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="280" y="50" width="200" height="120" as="geometry" />
    </mxCell>

    <mxCell id="repo" value="&lt;b&gt;Order Repository&lt;/b&gt;&lt;br&gt;[Component: Sequelize ORM]&lt;br&gt;&lt;br&gt;Provides data access for orders" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#85bbf0;fontColor=#000000;strokeColor=#78A8D8;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="280" y="240" width="200" height="120" as="geometry" />
    </mxCell>

    <mxCell id="pay" value="&lt;b&gt;Payment Client&lt;/b&gt;&lt;br&gt;[Component: HTTP Client]&lt;br&gt;&lt;br&gt;Integrates with external payment API" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#85bbf0;fontColor=#000000;strokeColor=#78A8D8;fontSize=11;align=center;" vertex="1" parent="boundary">
      <mxGeometry x="30" y="240" width="200" height="120" as="geometry" />
    </mxCell>

    <!-- External: Database -->
    <mxCell id="db" value="&lt;b&gt;Database&lt;/b&gt;&lt;br&gt;[Container: PostgreSQL]&lt;br&gt;&lt;br&gt;Stores order data" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#438dd5;fontColor=#ffffff;strokeColor=#3C7FC0;fontSize=11;align=center;size=10;" vertex="1" parent="1">
      <mxGeometry x="830" y="280" width="150" height="100" as="geometry" />
    </mxCell>

    <!-- Relationships -->
    <mxCell id="r1" value="Delegates to" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="ctrl" target="svc">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r2" value="Uses" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="svc" target="repo">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r3" value="Calls" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="svc" target="pay">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r4" value="Reads/writes via SQL" style="endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;" edge="1" parent="1" source="repo" target="db">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
