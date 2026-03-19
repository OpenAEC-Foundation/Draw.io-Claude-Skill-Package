# Examples: Draw.io Core XML Format

Working XML examples for common diagram patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal Valid Diagram (Simplified Format)

The absolute minimum to produce a visible shape:

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Hello World" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Two Shapes Connected by an Edge

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="End" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="350" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="connects" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Decision Diamond with Branching

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Check Status" style="shape=rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="120" height="80" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Approved" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="260" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="Rejected" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;"
            vertex="1" parent="1">
      <mxGeometry x="320" y="260" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="5" value="Yes" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="6" value="No" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. HTML Label with Formatting

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="&lt;b&gt;Web Server&lt;/b&gt;&lt;br&gt;&lt;span style=&quot;color:#999;font-size:11px;&quot;&gt;10.0.1.10:8080&lt;/span&gt;"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Group/Container with Children

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <!-- Group container -->
    <mxCell id="2" value="Server Cluster" style="group;rounded=1;whiteSpace=wrap;html=1;fillColor=#F5F5F5;strokeColor=#666666;dashed=1;"
            vertex="1" parent="1">
      <mxGeometry x="50" y="50" width="340" height="200" as="geometry" />
    </mxCell>
    <!-- Child 1 — coordinates RELATIVE to group -->
    <mxCell id="3" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="2">
      <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Child 2 — coordinates RELATIVE to group -->
    <mxCell id="4" value="App Server" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="2">
      <mxGeometry x="200" y="40" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Edge between children, also parented to the group -->
    <mxCell id="5" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="3" target="4" parent="2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 6. Edge with Waypoints

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="80" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="300" width="80" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="140" y="250" />
          <mxPoint x="440" y="250" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 7. Unconnected Edge (Floating Endpoints)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Floating Arrow" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="100" y="200" as="sourcePoint" />
        <mxPoint x="400" y="350" as="targetPoint" />
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 8. Multiple Layers

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Annotations" parent="0" />
    <!-- Shape on default layer -->
    <mxCell id="3" value="Main Content" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <!-- Shape on annotations layer -->
    <mxCell id="4" value="Note: review this" style="shape=note;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
            vertex="1" parent="2">
      <mxGeometry x="300" y="80" width="140" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 9. Multi-Page Diagram (Full Format Required)

```xml
<mxfile compressed="false">
  <diagram id="overview" name="System Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="Frontend" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
        <mxCell id="3" value="Backend" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
                vertex="1" parent="1">
          <mxGeometry x="300" y="100" width="120" height="60" as="geometry" />
        </mxCell>
        <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
                edge="1" source="2" target="3" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="detail" name="Backend Detail">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="5" value="API Gateway" style="rounded=1;whiteSpace=wrap;html=1;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
        <mxCell id="6" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#E1D5E7;strokeColor=#9673A6;"
                vertex="1" parent="1">
          <mxGeometry x="300" y="80" width="80" height="100" as="geometry" />
        </mxCell>
        <mxCell id="7" style="edgeStyle=orthogonalEdgeStyle;html=1;"
                edge="1" source="5" target="6" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 10. Custom Metadata with object Wrapper

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="2" label="Production DB" tooltip="PostgreSQL 15 cluster"
            link="https://monitoring.example.com/db"
            ip="10.0.2.5" port="5432" region="eu-west-1" cost_center="CC-4200">
      <mxCell style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#E1D5E7;strokeColor=#9673A6;"
              vertex="1" parent="1">
        <mxGeometry x="200" y="100" width="80" height="100" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 11. Placeholders with File-Level Variables

```xml
<mxfile compressed="false" vars='{"project":"Atlas","version":"2.1","env":"staging"}'>
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <object id="2" label="Project: %project% v%version%&lt;br&gt;Environment: %env%"
                placeholders="1">
          <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
                  vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="220" height="60" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Renders as: "Project: Atlas v2.1" and "Environment: staging".

---

## 12. Collapsible Container (Swimlane)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Service Layer" style="swimlane;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1" collapsed="0">
      <mxGeometry x="50" y="50" width="300" height="200" as="geometry">
        <mxRectangle x="50" y="50" width="160" height="30" as="alternateBounds" />
      </mxGeometry>
    </mxCell>
    <mxCell id="3" value="Auth Service" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="2">
      <mxGeometry x="20" y="40" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="4" value="Data Service" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="2">
      <mxGeometry x="160" y="40" width="120" height="40" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 13. Ellipse with Correct Perimeter

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="shape=ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="80" height="80" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Process" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="260" y="110" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 14. Edge with Label Offset

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Client" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Server" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="HTTPS" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry x="0" y="-15" relative="1" as="geometry">
        <mxPoint as="offset" />
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

The label "HTTPS" is positioned at the center of the edge (x=0), offset 15 pixels above the edge path (y=-15).
