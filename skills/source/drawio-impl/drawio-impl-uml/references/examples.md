# Examples: UML Diagram Implementation

Working XML examples for UML diagram patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Complete UML Class Diagram (3 Classes, 3 Relationship Types)

A class diagram with inheritance, composition, and association.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Class: Animal (abstract) -->
    <mxCell id="cls_animal" value="&lt;i&gt;&lt;&lt;abstract&gt;&gt;&lt;/i&gt;&#xa;Animal" style="swimlane;fontStyle=3;align=center;startSize=40;container=1;collapsible=0;childLayout=stackLayout;fillColor=#e1d5e7;strokeColor=#9673a6;" vertex="1" parent="1">
      <mxGeometry x="200" y="40" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="cls_animal_attr" value="- name: String&#xa;- age: int&#xa;# species: String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls_animal">
      <mxGeometry y="40" width="200" height="54" as="geometry" />
    </mxCell>
    <mxCell id="cls_animal_sep" value="" style="line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;strokeColor=#9673a6;" vertex="1" parent="cls_animal">
      <mxGeometry y="94" width="200" height="8" as="geometry" />
    </mxCell>
    <mxCell id="cls_animal_ops" value="+ makeSound(): void&#xa;+ move(distance: int): void" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls_animal">
      <mxGeometry y="102" width="200" height="48" as="geometry" />
    </mxCell>

    <!-- Class: Dog (inherits Animal) -->
    <mxCell id="cls_dog" value="Dog" style="swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="60" y="280" width="200" height="130" as="geometry" />
    </mxCell>
    <mxCell id="cls_dog_attr" value="- breed: String&#xa;- trained: boolean" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls_dog">
      <mxGeometry y="26" width="200" height="36" as="geometry" />
    </mxCell>
    <mxCell id="cls_dog_sep" value="" style="line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;strokeColor=#6c8ebf;" vertex="1" parent="cls_dog">
      <mxGeometry y="62" width="200" height="8" as="geometry" />
    </mxCell>
    <mxCell id="cls_dog_ops" value="+ makeSound(): void&#xa;+ fetch(item: String): void&#xa;+ sit(): void" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls_dog">
      <mxGeometry y="70" width="200" height="60" as="geometry" />
    </mxCell>

    <!-- Class: Collar (composed by Dog) -->
    <mxCell id="cls_collar" value="Collar" style="swimlane;fontStyle=1;align=center;startSize=26;container=1;collapsible=0;childLayout=stackLayout;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="360" y="280" width="200" height="110" as="geometry" />
    </mxCell>
    <mxCell id="cls_collar_attr" value="- color: String&#xa;- material: String" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls_collar">
      <mxGeometry y="26" width="200" height="36" as="geometry" />
    </mxCell>
    <mxCell id="cls_collar_sep" value="" style="line;strokeWidth=1;fillColor=none;align=left;verticalAlign=middle;spacingTop=-1;spacingLeft=3;spacingRight=10;rotatable=0;labelPosition=left;points=[];portConstraint=eastwest;strokeColor=#82b366;" vertex="1" parent="cls_collar">
      <mxGeometry y="62" width="200" height="8" as="geometry" />
    </mxCell>
    <mxCell id="cls_collar_ops" value="+ engrave(text: String): void" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=top;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=0;" vertex="1" parent="cls_collar">
      <mxGeometry y="70" width="200" height="40" as="geometry" />
    </mxCell>

    <!-- Generalization: Dog -> Animal -->
    <mxCell id="gen1" style="endArrow=block;endFill=0;html=1;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="cls_dog" target="cls_animal">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Composition: Dog -> Collar (Dog owns Collar) -->
    <mxCell id="comp1" value="1" style="startArrow=diamond;startFill=1;endArrow=none;html=1;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="cls_dog" target="cls_collar">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

This example demonstrates:
- Abstract class with `fontStyle=3` and `<<abstract>>` stereotype.
- 3-compartment pattern: attributes, separator line, operations.
- UML visibility prefixes (`-` private, `#` protected, `+` public).
- Generalization edge with `endArrow=block;endFill=0` (hollow triangle).
- Composition edge with `startArrow=diamond;startFill=1` (filled diamond).
- `&#xa;` for line breaks within compartments.

---

## 2. Sequence Diagram (3 Lifelines, Sync + Return Messages)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Lifeline: Client -->
    <mxCell id="ll1" value="Client" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=#dae8fc;strokeColor=#6c8ebf;size=40;" vertex="1" parent="1">
      <mxGeometry x="80" y="40" width="100" height="350" as="geometry" />
    </mxCell>

    <!-- Lifeline: Server -->
    <mxCell id="ll2" value="Server" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=#d5e8d4;strokeColor=#82b366;size=40;" vertex="1" parent="1">
      <mxGeometry x="280" y="40" width="100" height="350" as="geometry" />
    </mxCell>

    <!-- Lifeline: Database -->
    <mxCell id="ll3" value="Database" style="shape=umlLifeline;perimeter=lifelinePerimeter;whiteSpace=wrap;html=1;container=1;collapsible=0;recursiveResize=0;outlineConnect=0;fillColor=#fff2cc;strokeColor=#d6b656;size=40;" vertex="1" parent="1">
      <mxGeometry x="480" y="40" width="100" height="350" as="geometry" />
    </mxCell>

    <!-- Sync: Client -> Server -->
    <mxCell id="msg1" value="login(user, pass)" style="html=1;verticalAlign=bottom;endArrow=block;endFill=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="130" y="120" as="sourcePoint" />
        <mxPoint x="330" y="120" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Sync: Server -> Database -->
    <mxCell id="msg2" value="findUser(user)" style="html=1;verticalAlign=bottom;endArrow=block;endFill=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="330" y="170" as="sourcePoint" />
        <mxPoint x="530" y="170" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Return: Database -> Server -->
    <mxCell id="msg3" value="userRecord" style="html=1;verticalAlign=bottom;endArrow=open;endFill=0;dashed=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="530" y="220" as="sourcePoint" />
        <mxPoint x="330" y="220" as="targetPoint" />
      </mxGeometry>
    </mxCell>

    <!-- Return: Server -> Client -->
    <mxCell id="msg4" value="authToken" style="html=1;verticalAlign=bottom;endArrow=open;endFill=0;dashed=1;" edge="1" parent="1">
      <mxGeometry relative="1" as="geometry">
        <mxPoint x="330" y="270" as="sourcePoint" />
        <mxPoint x="130" y="270" as="targetPoint" />
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

This example demonstrates:
- Three lifelines with `shape=umlLifeline;perimeter=lifelinePerimeter`.
- Synchronous messages: `endArrow=block;endFill=1` (filled arrowhead).
- Return messages: `endArrow=open;endFill=0;dashed=1` (dashed, open arrowhead).
- Absolute point-based positioning for messages.
- 50px vertical spacing between messages.

---

## 3. Use Case Diagram (Actor + System Boundary + 3 Use Cases)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Actor: Customer -->
    <mxCell id="actor1" value="Customer" style="shape=umlActor;verticalLabelPosition=bottom;verticalAlign=top;html=1;outlineConnect=0;" vertex="1" parent="1">
      <mxGeometry x="60" y="140" width="30" height="55" as="geometry" />
    </mxCell>

    <!-- System Boundary -->
    <mxCell id="sys" value="Online Store" style="rounded=1;whiteSpace=wrap;html=1;container=1;collapsible=0;fillColor=none;strokeColor=#666666;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=14;" vertex="1" parent="1">
      <mxGeometry x="160" y="40" width="300" height="300" as="geometry" />
    </mxCell>

    <!-- Use Case: Browse Products -->
    <mxCell id="uc1" value="Browse Products" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sys">
      <mxGeometry x="60" y="30" width="180" height="60" as="geometry" />
    </mxCell>

    <!-- Use Case: Place Order -->
    <mxCell id="uc2" value="Place Order" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sys">
      <mxGeometry x="60" y="120" width="180" height="60" as="geometry" />
    </mxCell>

    <!-- Use Case: Make Payment -->
    <mxCell id="uc3" value="Make Payment" style="ellipse;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="sys">
      <mxGeometry x="60" y="210" width="180" height="60" as="geometry" />
    </mxCell>

    <!-- Association: Customer -> Browse -->
    <mxCell id="a1" style="endArrow=none;html=1;" edge="1" parent="1" source="actor1" target="uc1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Association: Customer -> Place Order -->
    <mxCell id="a2" style="endArrow=none;html=1;" edge="1" parent="1" source="actor1" target="uc2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Include: Place Order includes Make Payment -->
    <mxCell id="inc1" value="&lt;&lt;include&gt;&gt;" style="endArrow=open;endFill=1;dashed=1;html=1;" edge="1" parent="1" source="uc2" target="uc3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

This example demonstrates:
- Actor with `shape=umlActor` outside the system boundary.
- System boundary with `container=1;dashed=1`.
- Use cases as children of the system boundary (`parent="sys"`).
- Plain association lines (no arrows) from actor to use case.
- Include relationship with `dashed=1` and `<<include>>` label.

---

## 4. State Machine Diagram (3 States + Transitions)

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Initial state -->
    <mxCell id="s0" value="" style="ellipse;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="175" y="30" width="30" height="30" as="geometry" />
    </mxCell>

    <!-- State: Idle -->
    <mxCell id="s1" value="&lt;b&gt;Idle&lt;/b&gt;&lt;hr&gt;entry / displayPrompt()&lt;br&gt;exit / clearScreen()" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;align=center;verticalAlign=top;arcSize=15;" vertex="1" parent="1">
      <mxGeometry x="110" y="100" width="160" height="80" as="geometry" />
    </mxCell>

    <!-- State: Processing -->
    <mxCell id="s2" value="&lt;b&gt;Processing&lt;/b&gt;&lt;hr&gt;entry / startJob()&lt;br&gt;do / runTask()" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;align=center;verticalAlign=top;arcSize=15;" vertex="1" parent="1">
      <mxGeometry x="110" y="230" width="160" height="80" as="geometry" />
    </mxCell>

    <!-- Final state -->
    <mxCell id="sf" value="" style="ellipse;html=1;shape=doubleCircle;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="175" y="360" width="30" height="30" as="geometry" />
    </mxCell>

    <!-- Transition: initial -> Idle -->
    <mxCell id="t0" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="s0" target="s1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Transition: Idle -> Processing -->
    <mxCell id="t1" value="submit [valid]" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="s1" target="s2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Transition: Processing -> Idle -->
    <mxCell id="t2" value="complete" style="endArrow=open;endFill=1;html=1;edgeStyle=orthogonalEdgeStyle;" edge="1" parent="1" source="s2" target="s1">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="60" y="270" />
          <mxPoint x="60" y="140" />
        </Array>
      </mxGeometry>
    </mxCell>

    <!-- Transition: Processing -> Final -->
    <mxCell id="t3" value="shutdown" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="s2" target="sf">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

This example demonstrates:
- Initial state as filled black circle.
- States with entry/do/exit actions using `<b>Name</b><hr>` HTML pattern.
- Final state with `shape=doubleCircle`.
- Transition labels in `event [guard] / action` format.
- Waypoints for a loopback transition.

---

## 5. Activity Diagram with Fork/Join

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Initial node -->
    <mxCell id="init" value="" style="ellipse;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="185" y="20" width="30" height="30" as="geometry" />
    </mxCell>

    <!-- Action: Receive Order -->
    <mxCell id="a1" value="Receive Order" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="140" y="80" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Fork bar -->
    <mxCell id="fork1" value="" style="shape=line;html=1;strokeWidth=6;strokeColor=#000000;fillColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="100" y="150" width="200" height="10" as="geometry" />
    </mxCell>

    <!-- Parallel Action: Pack Items -->
    <mxCell id="a2" value="Pack Items" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="40" y="200" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Parallel Action: Process Payment -->
    <mxCell id="a3" value="Process Payment" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="240" y="200" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Join bar -->
    <mxCell id="join1" value="" style="shape=line;html=1;strokeWidth=6;strokeColor=#000000;fillColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="100" y="280" width="200" height="10" as="geometry" />
    </mxCell>

    <!-- Action: Ship Order -->
    <mxCell id="a4" value="Ship Order" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="140" y="320" width="120" height="40" as="geometry" />
    </mxCell>

    <!-- Final node -->
    <mxCell id="final" value="" style="ellipse;html=1;shape=doubleCircle;fillColor=#000000;strokeColor=#000000;" vertex="1" parent="1">
      <mxGeometry x="185" y="400" width="30" height="30" as="geometry" />
    </mxCell>

    <!-- Edges -->
    <mxCell id="e0" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="init" target="a1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e1" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="a1" target="fork1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e2" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="fork1" target="a2">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e3" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="fork1" target="a3">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e4" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="a2" target="join1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e5" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="a3" target="join1">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e6" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="join1" target="a4">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
    <mxCell id="e7" style="endArrow=open;endFill=1;html=1;" edge="1" parent="1" source="a4" target="final">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

This example demonstrates:
- Fork bar with `shape=line;strokeWidth=6` splitting into parallel activities.
- Join bar reuniting parallel flows.
- Initial and final nodes matching state machine conventions.
- All activity edges using `endArrow=open;endFill=1`.
