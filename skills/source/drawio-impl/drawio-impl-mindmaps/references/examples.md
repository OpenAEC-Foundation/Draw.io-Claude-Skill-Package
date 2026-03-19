# Examples: Draw.io Mind Maps

Working XML examples for every mind map pattern. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal Mind Map (Central Topic + 3 Branches)

The simplest valid mind map. Three main branches radiate from a central topic.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Central Topic -->
    <mxCell id="center" value="My Project"
            style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=16;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="200" width="160" height="80" as="geometry" />
    </mxCell>

    <!-- Branch 1: Goals (Blue, upper-left) -->
    <mxCell id="b1" value="Goals"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="100" y="80" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Branch 2: Resources (Green, upper-right) -->
    <mxCell id="b2" value="Resources"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="540" y="80" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Branch 3: Risks (Yellow, bottom-center) -->
    <mxCell id="b3" value="Risks"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="320" y="360" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Curved connectors (no arrows) -->
    <mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
            edge="1" source="center" target="b1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#82b366;"
            edge="1" source="center" target="b2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#d6b656;"
            edge="1" source="center" target="b3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Full Mind Map (3 Levels Deep)

Central topic with 3 main branches, each having 2–3 sub-branches.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Central Topic -->
    <mxCell id="center" value="Software Architecture"
            style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=16;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="340" y="250" width="180" height="90" as="geometry" />
    </mxCell>

    <!-- Branch 1: Frontend (Blue) -->
    <mxCell id="fe" value="Frontend"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="80" y="80" width="130" height="45" as="geometry" />
    </mxCell>
    <mxCell id="fe_1" value="React"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="10" y="150" width="100" height="30" as="geometry" />
    </mxCell>
    <mxCell id="fe_2" value="TypeScript"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="130" y="150" width="100" height="30" as="geometry" />
    </mxCell>
    <mxCell id="fe_3" value="CSS Modules"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="70" y="200" width="100" height="30" as="geometry" />
    </mxCell>

    <!-- Branch 2: Backend (Green) -->
    <mxCell id="be" value="Backend"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="620" y="80" width="130" height="45" as="geometry" />
    </mxCell>
    <mxCell id="be_1" value="Node.js"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="600" y="150" width="100" height="30" as="geometry" />
    </mxCell>
    <mxCell id="be_2" value="PostgreSQL"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="720" y="150" width="100" height="30" as="geometry" />
    </mxCell>

    <!-- Branch 3: DevOps (Purple) -->
    <mxCell id="ops" value="DevOps"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="80" y="420" width="130" height="45" as="geometry" />
    </mxCell>
    <mxCell id="ops_1" value="Docker"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="10" y="490" width="100" height="30" as="geometry" />
    </mxCell>
    <mxCell id="ops_2" value="CI/CD"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="130" y="490" width="100" height="30" as="geometry" />
    </mxCell>

    <!-- Branch 4: Testing (Yellow) -->
    <mxCell id="test" value="Testing"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="620" y="420" width="130" height="45" as="geometry" />
    </mxCell>
    <mxCell id="test_1" value="Jest"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="600" y="490" width="100" height="30" as="geometry" />
    </mxCell>
    <mxCell id="test_2" value="Cypress"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f5f5f5;strokeColor=#666666;fontSize=11;"
            vertex="1" parent="1">
      <mxGeometry x="720" y="490" width="100" height="30" as="geometry" />
    </mxCell>

    <!-- Level 0-1 connectors (thick, colored) -->
    <mxCell id="ec_fe" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
            edge="1" source="center" target="fe" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_be" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#82b366;"
            edge="1" source="center" target="be" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_ops" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#9673a6;"
            edge="1" source="center" target="ops" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_test" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#d6b656;"
            edge="1" source="center" target="test" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Level 1-2 connectors (thin, gray) -->
    <mxCell id="ec_fe1" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="fe" target="fe_1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_fe2" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="fe" target="fe_2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_fe3" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="fe" target="fe_3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_be1" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="be" target="be_1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_be2" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="be" target="be_2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_ops1" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="ops" target="ops_1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_ops2" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="ops" target="ops_2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_test1" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="test" target="test_1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="ec_test2" style="endArrow=none;html=1;curved=1;strokeColor=#999999;"
            edge="1" source="test" target="test_2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Concept Map with Labeled Relationships

Concept map showing relationships between concepts with labeled directed edges.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Concepts (no strict hierarchy) -->
    <mxCell id="c1" value="Water Cycle"
            style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=14;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="40" width="160" height="70" as="geometry" />
    </mxCell>
    <mxCell id="c2" value="Evaporation"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=12;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="80" y="180" width="130" height="40" as="geometry" />
    </mxCell>
    <mxCell id="c3" value="Condensation"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=12;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="540" y="180" width="130" height="40" as="geometry" />
    </mxCell>
    <mxCell id="c4" value="Precipitation"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=12;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="300" y="320" width="130" height="40" as="geometry" />
    </mxCell>
    <mxCell id="c5" value="Clouds"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontSize=12;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="540" y="320" width="130" height="40" as="geometry" />
    </mxCell>

    <!-- Labeled directed edges (concept map style) -->
    <mxCell id="r1" value="includes"
            style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
            edge="1" source="c1" target="c2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r2" value="includes"
            style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
            edge="1" source="c1" target="c3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r3" value="leads to"
            style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
            edge="1" source="c2" target="c3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r4" value="forms"
            style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
            edge="1" source="c3" target="c5" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="r5" value="produces"
            style="endArrow=classic;html=1;curved=1;strokeColor=#666666;fontSize=10;fontColor=#666666;"
            edge="1" source="c5" target="c4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <!-- Cross-link: precipitation feeds back to evaporation -->
    <mxCell id="r6" value="feeds"
            style="endArrow=classic;html=1;curved=1;dashed=1;strokeColor=#999999;fontSize=10;fontColor=#999999;"
            edge="1" source="c4" target="c2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. Mind Map with Rounded Rectangle Central Topic

Alternative style using a rounded rectangle instead of an ellipse for the root.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Central Topic (rounded rectangle) -->
    <mxCell id="center" value="Marketing Strategy"
            style="rounded=1;whiteSpace=wrap;html=1;arcSize=40;fillColor=#2d7600;fontColor=#ffffff;strokeColor=#1a4500;fontSize=15;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="280" y="220" width="180" height="70" as="geometry" />
    </mxCell>

    <!-- Branch 1: Digital (Blue, left) -->
    <mxCell id="b1" value="Digital"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="40" y="130" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Branch 2: Print (Green, right) -->
    <mxCell id="b2" value="Print"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="580" y="130" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Branch 3: Events (Purple, bottom-left) -->
    <mxCell id="b3" value="Events"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="60" y="360" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Branch 4: PR (Orange, bottom-right) -->
    <mxCell id="b4" value="PR"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="560" y="360" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Curved connectors -->
    <mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
            edge="1" source="center" target="b1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#82b366;"
            edge="1" source="center" target="b2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#9673a6;"
            edge="1" source="center" target="b3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#b85450;"
            edge="1" source="center" target="b4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 5. Mind Map with 6 Branches (Maximum Recommended)

Demonstrates radial distribution with many branches.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Central Topic -->
    <mxCell id="center" value="Business Plan"
            style="ellipse;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=16;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="350" y="270" width="180" height="90" as="geometry" />
    </mxCell>

    <!-- 6 branches distributed radially -->
    <mxCell id="b1" value="Vision"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="380" y="60" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="b2" value="Market"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="620" y="140" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="b3" value="Finance"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#fff2cc;strokeColor=#d6b656;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="640" y="380" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="b4" value="Operations"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#e1d5e7;strokeColor=#9673a6;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="380" y="500" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="b5" value="Team"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#f8cecc;strokeColor=#b85450;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="120" y="380" width="120" height="40" as="geometry" />
    </mxCell>
    <mxCell id="b6" value="Legal"
            style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d4e1f5;strokeColor=#4a86c8;fontSize=13;fontStyle=1;"
            vertex="1" parent="1">
      <mxGeometry x="120" y="140" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- All 6 curved connectors -->
    <mxCell id="e1" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#6c8ebf;"
            edge="1" source="center" target="b1" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#82b366;"
            edge="1" source="center" target="b2" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#d6b656;"
            edge="1" source="center" target="b3" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#9673a6;"
            edge="1" source="center" target="b4" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#b85450;"
            edge="1" source="center" target="b5" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e6" style="endArrow=none;html=1;curved=1;strokeWidth=2;strokeColor=#4a86c8;"
            edge="1" source="center" target="b6" parent="1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```
