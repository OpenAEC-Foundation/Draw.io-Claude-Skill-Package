# Examples: Draw.io Syntax Metadata

Working XML examples for every metadata pattern. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Multi-Page Diagram (Two Pages)

```xml
<mxfile compressed="false">
  <diagram id="page-overview" name="Overview">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="2" value="System Overview"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;fontSize=16;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="200" height="80" as="geometry" />
        </mxCell>
        <object id="3" label="See Details" link="data:page/id,page-detail">
          <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
                  vertex="1" parent="1">
            <mxGeometry x="100" y="220" width="200" height="60" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
  <diagram id="page-detail" name="Detail View">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <mxCell id="10" value="Detail Component A"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
                vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
        </mxCell>
        <mxCell id="11" value="Detail Component B"
                style="rounded=1;whiteSpace=wrap;html=1;fillColor=#FFF2CC;strokeColor=#D6B656;"
                vertex="1" parent="1">
          <mxGeometry x="320" y="100" width="160" height="60" as="geometry" />
        </mxCell>
        <mxCell id="12" style="edgeStyle=orthogonalEdgeStyle;html=1;"
                edge="1" source="10" target="11" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 2. Multi-Layer Diagram

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
              guides="1" tooltips="1" connect="1" arrows="1"
              fold="1" page="1" pageScale="1" pageWidth="1169"
              pageHeight="827" math="0" shadow="0">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="layer-bg" value="Background" parent="0" />
    <mxCell id="layer-anno" value="Annotations" parent="0" visible="0" />

    <!-- Background layer content -->
    <mxCell id="2" value="" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F5F5F5;strokeColor=#CCCCCC;"
            vertex="1" parent="layer-bg">
      <mxGeometry x="50" y="50" width="500" height="400" as="geometry" />
    </mxCell>

    <!-- Default layer content -->
    <mxCell id="3" value="Web Server" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
    </mxCell>
    <mxCell id="4" value="Database" style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
            vertex="1" parent="1">
      <mxGeometry x="350" y="100" width="80" height="100" as="geometry" />
    </mxCell>
    <mxCell id="5" style="edgeStyle=orthogonalEdgeStyle;html=1;"
            edge="1" source="3" target="4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Annotations layer content (hidden by default) -->
    <mxCell id="6" value="TODO: Add load balancer" style="text;html=1;whiteSpace=wrap;fontColor=#FF0000;fontStyle=2;"
            vertex="1" parent="layer-anno">
      <mxGeometry x="100" y="60" width="200" height="30" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Custom Properties with object Wrapper

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="srv1" label="Web Server" tooltip="Primary web server — handles all HTTP traffic"
            ip="10.0.1.10" environment="production" owner="platform-team" cost_center="CC-4200">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
    <object id="db1" label="PostgreSQL" tooltip="Primary database — read/write"
            ip="10.0.2.5" port="5432" environment="production" owner="data-team">
      <mxCell style="shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
              vertex="1" parent="1">
        <mxGeometry x="350" y="80" width="80" height="100" as="geometry" />
      </mxCell>
    </object>
    <object id="conn1" label="HTTPS" protocol="TLS 1.3" port="443">
      <mxCell style="edgeStyle=orthogonalEdgeStyle;html=1;" edge="1"
              source="srv1" target="db1" parent="1">
        <mxGeometry relative="1" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 4. File-Level Variables with Placeholders

```xml
<mxfile compressed="false"
        vars='{"project":"Atlas","version":"2.1","author":"Jane Doe","env":"staging"}'>
  <diagram id="page-1" name="Architecture">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <object id="2" label="%project% v%version%" placeholders="1">
          <mxCell style="text;html=1;whiteSpace=wrap;fontSize=18;fontStyle=1;align=center;"
                  vertex="1" parent="1">
            <mxGeometry x="100" y="30" width="300" height="40" as="geometry" />
          </mxCell>
        </object>
        <object id="3" label="Environment: %env%" placeholders="1">
          <mxCell style="text;html=1;whiteSpace=wrap;fontSize=12;fontColor=#999999;"
                  vertex="1" parent="1">
            <mxGeometry x="100" y="70" width="300" height="30" as="geometry" />
          </mxCell>
        </object>
        <object id="4" label="Author: %author% — %date%" placeholders="1">
          <mxCell style="text;html=1;whiteSpace=wrap;fontSize=10;fontColor=#AAAAAA;"
                  vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="300" height="25" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Renders as:
- "Atlas v2.1"
- "Environment: staging"
- "Author: Jane Doe — (current date)"

---

## 5. Placeholder Scope Resolution (Parent Overrides File Vars)

```xml
<mxfile compressed="false" vars='{"env":"staging"}'>
  <diagram id="page-1" name="Scope Demo">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <object id="1" label="Production Layer" env="production">
          <mxCell parent="0" />
        </object>
        <object id="2" label="Env: %env%" placeholders="1">
          <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Cell `id="2"` renders as **"Env: production"** (NOT "staging") because the layer (`id="1"`) has `env="production"` which takes priority over the file-level `vars`.

---

## 6. Cell-Level Placeholders with Custom Properties

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="2" label="Server: %hostname%&lt;br&gt;IP: %ip%&lt;br&gt;Status: %status%"
            placeholders="1" hostname="web-prod-01" ip="10.0.1.10" status="healthy">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#D5E8D4;strokeColor=#82B366;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="200" height="80" as="geometry" />
      </mxCell>
    </object>
    <object id="3" label="Server: %hostname%&lt;br&gt;IP: %ip%&lt;br&gt;Status: %status%"
            placeholders="1" hostname="web-prod-02" ip="10.0.1.11" status="degraded">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;"
              vertex="1" parent="1">
        <mxGeometry x="350" y="100" width="200" height="80" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 7. Tooltips and External Links

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="2" label="API Gateway" tooltip="Kong API Gateway v3.4 — Handles rate limiting, auth, and routing"
            link="https://docs.konghq.com">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
    <object id="3" label="Monitoring" tooltip="Grafana dashboard — click to open"
            link="https://grafana.example.com/d/abc123">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E1D5E7;strokeColor=#9673A6;"
              vertex="1" parent="1">
        <mxGeometry x="300" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

---

## 8. Tooltip with Placeholder Substitution

```xml
<mxfile compressed="false" vars='{"env":"production"}'>
  <diagram id="page-1" name="Infra">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <object id="2" label="%hostname%" placeholders="1"
                tooltip="Host: %hostname% | IP: %ip% | Env: %env%"
                hostname="web-prod-01" ip="10.0.1.10">
          <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
            <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

Tooltip renders as: "Host: web-prod-01 | IP: 10.0.1.10 | Env: production"

Note: `%env%` resolves from the file-level `vars` because the cell has no `env` attribute.

---

## 9. MathJax / LaTeX Formulas

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
              guides="1" tooltips="1" connect="1" arrows="1"
              fold="1" page="1" pageScale="1" pageWidth="1169"
              pageHeight="827" math="1" shadow="0">
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <mxCell id="2" value="$$E = mc^2$$"
            style="text;html=1;whiteSpace=wrap;align=center;fontSize=18;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="100" width="200" height="60" as="geometry" />
    </mxCell>
    <mxCell id="3" value="$$\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}$$"
            style="text;html=1;whiteSpace=wrap;align=center;fontSize=14;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="200" width="300" height="80" as="geometry" />
    </mxCell>
    <mxCell id="4" value="$$\sum_{n=1}^{\infty} \frac{1}{n^2} = \frac{\pi^2}{6}$$"
            style="text;html=1;whiteSpace=wrap;align=center;fontSize=14;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="320" width="300" height="80" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 10. Layer with Placeholder Inheritance

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <object id="1" label="Default Layer" region="eu-west-1" team="platform">
      <mxCell parent="0" />
    </object>
    <object id="layer-us" label="US Region" region="us-east-1" team="us-ops">
      <mxCell parent="0" />
    </object>

    <!-- Inherits region="eu-west-1" from default layer -->
    <object id="2" label="Server (%region%)" placeholders="1">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
      </mxCell>
    </object>

    <!-- Inherits region="us-east-1" from US layer -->
    <object id="3" label="Server (%region%)" placeholders="1">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;" vertex="1" parent="layer-us">
        <mxGeometry x="100" y="100" width="160" height="60" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

Cell `id="2"` renders as "Server (eu-west-1)". Cell `id="3"` renders as "Server (us-east-1)".

---

## 11. Predefined Placeholders (Page Info Footer)

```xml
<mxfile compressed="false">
  <diagram id="page-1" name="Architecture">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10"
                  guides="1" tooltips="1" connect="1" arrows="1"
                  fold="1" page="1" pageScale="1" pageWidth="1169"
                  pageHeight="827" math="0" shadow="0">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        <object id="2" label="%filename% — Page %pagenumber% of %pagecount% — %date%"
                placeholders="1">
          <mxCell style="text;html=1;whiteSpace=wrap;fontSize=9;fontColor=#999999;align=right;"
                  vertex="1" parent="1">
            <mxGeometry x="700" y="790" width="450" height="25" as="geometry" />
          </mxCell>
        </object>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 12. Tags for Search and Filter

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />
    <object id="2" label="Auth Service" tags="backend,security,critical">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F8CECC;strokeColor=#B85450;"
              vertex="1" parent="1">
        <mxGeometry x="100" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
    <object id="3" label="API Gateway" tags="backend,networking">
      <mxCell style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DAE8FC;strokeColor=#6C8EBF;"
              vertex="1" parent="1">
        <mxGeometry x="300" y="100" width="140" height="60" as="geometry" />
      </mxCell>
    </object>
  </root>
</mxGraphModel>
```

Tags enable filtering via the Tags panel in Draw.io (Edit > Edit Data or the toolbar Tags button).
