# Examples: Draw.io Syntax Cells

Working XML examples for every cell pattern. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Simple Vertex (Rounded Rectangle)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Process Step" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Non-Rectangular Shape (Diamond with Perimeter)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Decision" style="shape=rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="120" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Ellipse Shape

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="shape=ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="100" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. Two Vertices Connected by an Edge

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Source" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Target" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Edge with Label

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Client" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Server" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="HTTPS Request" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
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

## 7. Floating Edge (No Source/Target)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Annotation" style="edgeStyle=orthogonalEdgeStyle;html=1;dashed=1;"
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

## 8. UserObject Wrapper with Custom Properties

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="srv1" label="Web Server" tooltip="Primary web server"
            ip="10.0.1.10" environment="production" team="platform">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
              vertex="1" parent="1">
        <mxGeometry x="200" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 9. UserObject with Hyperlink

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="doc1" label="API Docs" link="https://api.example.com/docs"
            tooltip="Click to open documentation">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E1D5E7;strokeColor=#9673A6;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 10. Edge with Metadata (object Wrapper on Edge)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Service A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Service B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="1">
      <mxGeometry x="400" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <object id="conn1" label="gRPC" protocol="HTTP/2" port="50051" latency_ms="12">
      <mxCell style="edgeStyle=orthogonalEdgeStyle;html=1;"
              edge="1" source="2" target="3" parent="1">
        <mxGeometry relative="1" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 11. HTML Label with Formatting

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="&lt;b&gt;Database&lt;/b&gt;&lt;br&gt;&lt;i style=&quot;color:#666;&quot;&gt;PostgreSQL 15&lt;/i&gt;"
            style="shape=cylinder3;whiteSpace=wrap;html=1;boundedLbl=1;size=15;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="100" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 12. HTML Label with Table

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="&lt;table style=&quot;width:100%;font-size:12px;&quot;&gt;&lt;tr&gt;&lt;th colspan=&quot;2&quot; style=&quot;background:#DAE8FC;padding:4px;&quot;&gt;users&lt;/th&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td style=&quot;padding:2px 4px;&quot;&gt;id&lt;/td&gt;&lt;td style=&quot;padding:2px 4px;&quot;&gt;INT PK&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td style=&quot;padding:2px 4px;&quot;&gt;name&lt;/td&gt;&lt;td style=&quot;padding:2px 4px;&quot;&gt;VARCHAR&lt;/td&gt;&lt;/tr&gt;&lt;tr&gt;&lt;td style=&quot;padding:2px 4px;&quot;&gt;email&lt;/td&gt;&lt;td style=&quot;padding:2px 4px;&quot;&gt;VARCHAR&lt;/td&gt;&lt;/tr&gt;&lt;/table&gt;"
            style="shape=mxgraph.basic.rect;whiteSpace=wrap;html=1;fillColor=#FFFFFF;strokeColor=#000000;overflow=fill;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="180" height="120" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 13. Placeholders with Variable Substitution

```xml
<mxfile compressed="false" vars='{"project":"Atlas","version":"2.1"}'>
  <diagram id="page-1" name="Overview">
    <mxGraphModel>
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <object id="2" label="Project: %project% v%version%&#10;Server: %name%" placeholders="1"
                name="web-01">
          <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
                  vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="220" height="60" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Renders as: "Project: Atlas v2.1" and "Server: web-01" on separate lines.

---

## 14. Container with Child Shapes

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="10" value="Server Group" style="rounded=1;whiteSpace=wrap;html=1;container=1;fillColor=#F5F5F5;strokeColor=#666666;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="320" height="200" as="geometry" />
    </mxCell>
    <mxCell id="11" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="10">
      <mxGeometry x="20" y="40" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="12" value="App Server" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="10">
      <mxGeometry x="170" y="40" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="13" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="11" target="12" parent="10">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

Note: child coordinates (x="20", y="40") are RELATIVE to the container's top-left corner. The edge also has `parent="10"` to stay inside the container.

---

## 15. Invisible Group

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="20" style="group" vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="300" height="150" as="geometry" />
    </mxCell>
    <mxCell id="21" value="Item A" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="20">
      <mxGeometry x="10" y="10" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="22" value="Item B" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="20">
      <mxGeometry x="160" y="10" width="120" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 16. Collapsible Swimlane Container

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="30" value="Module A" style="swimlane;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" collapsed="0" parent="1">
      <mxGeometry x="100" y="100" width="300" height="200" as="geometry">
        <mxRectangle x="100" y="100" width="160" height="30" as="alternateBounds" />
      </mxGeometry>
    </mxCell>
    <mxCell id="31" value="Component X" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="30">
      <mxGeometry x="20" y="40" width="120" height="50" as="geometry" />
    </mxCell>
    <mxCell id="32" value="Component Y" style="rounded=1;whiteSpace=wrap;html=1;"
            vertex="1" parent="30">
      <mxGeometry x="160" y="40" width="120" height="50" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 17. Multiple Layers

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="layer-bg" value="Background" parent="0" />
    <mxCell id="layer-anno" value="Annotations" parent="0" visible="0" />
    <mxCell id="10" value="Background Box" style="rounded=0;whiteSpace=wrap;html=1;fillColor=#F5F5F5;strokeColor=#CCCCCC;"
            vertex="1" parent="layer-bg">
      <mxGeometry x="50" y="50" width="500" height="400" as="geometry" />
    </mxCell>
    <mxCell id="20" value="Main Content" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="150" y="150" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="30" value="Note: review this" style="shape=note;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
            vertex="1" parent="layer-anno">
      <mxGeometry x="300" y="100" width="140" height="60" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 18. Decision Flow with Branching Edges

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="Start" style="shape=ellipse;perimeter=ellipsePerimeter;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="220" y="20" width="80" height="50" as="geometry" />
    </mxCell>
    <mxCell id="3" value="Valid?" style="shape=rhombus;perimeter=rhombusPerimeter;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
            vertex="1" parent="1">
      <mxGeometry x="200" y="120" width="120" height="80" as="geometry" />
    </mxCell>
    <mxCell id="4" value="Process" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="260" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="5" value="Reject" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;"
            vertex="1" parent="1">
      <mxGeometry x="320" y="260" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="6" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="2" target="3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="7" value="Yes" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="3" target="4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="8" value="No" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="3" target="5" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
