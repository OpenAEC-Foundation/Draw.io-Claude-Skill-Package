# Methods Reference: Architecture Diagram Implementation

Complete style strings and attribute reference for C4 model, cloud architecture, and deployment diagram shapes.

---

## 1. C4 Model Shapes

### Person

```
shape=mxgraph.c4.person2;whiteSpace=wrap;html=1;align=center;metaEdit=1;points=[[0.5,0,0],[1,0.5,0],[1,0.75,0],[0.75,1,0],[0.5,1,0],[0.25,1,0],[0,0.75,0],[0,0.5,0]];fillColor=#08427b;fontColor=#ffffff;strokeColor=#073763;fontSize=11;
```

Dimensions: 200 x 180. ALWAYS use `shape=mxgraph.c4.person2` — this is the standard C4 person icon with head-and-torso silhouette.

### Software System (Internal)

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#1168bd;fontColor=#ffffff;strokeColor=#0b4884;fontSize=11;align=center;
```

Dimensions: 300 x 150. Blue (#1168bd) indicates an internal system that the team builds or owns.

### Software System (External)

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#999999;fontColor=#ffffff;strokeColor=#8A8A8A;fontSize=11;align=center;
```

Dimensions: 240 x 150. Gray (#999999) indicates a system outside the team's control.

### Container

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#438dd5;fontColor=#ffffff;strokeColor=#3C7FC0;fontSize=11;align=center;
```

Dimensions: 240 x 150. Medium blue (#438dd5) for containers (web apps, APIs, databases, etc.).

### Component

```
rounded=1;whiteSpace=wrap;html=1;fillColor=#85bbf0;fontColor=#000000;strokeColor=#78A8D8;fontSize=11;align=center;
```

Dimensions: 200 x 120. Light blue (#85bbf0) for components. Note: `fontColor=#000000` (black text) because the background is light.

### C4 System Boundary

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#1168bd;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#1168bd;container=1;collapsible=0;
```

Use this to group containers within a system boundary on container-level diagrams. ALWAYS set `container=1;collapsible=0;`.

---

## 2. C4 Relationship

### Standard Relationship

```
endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;
```

ALWAYS include a descriptive `value` attribute. ALWAYS use `endArrow=classic` for directed relationships.

### Async Relationship

```
endArrow=classic;html=1;strokeColor=#707070;fontColor=#707070;fontSize=10;dashed=1;
```

Use `dashed=1` to indicate asynchronous communication (message queues, events).

---

## 3. C4 Label Format

ALWAYS use this HTML pattern for the `value` attribute:

```
&lt;b&gt;Element Name&lt;/b&gt;&lt;br&gt;[Type Tag]&lt;br&gt;&lt;br&gt;Description text here
```

Type tags by element:

| Element | Type Tag Format |
|---------|----------------|
| Person | `[Person]` |
| Software System | `[Software System]` |
| External System | `[External System]` |
| Container | `[Container: Technology]` (e.g., `[Container: Java Spring Boot]`) |
| Component | `[Component: Technology]` (e.g., `[Component: Spring MVC Controller]`) |

NEVER omit the type tag. NEVER omit the description.

---

## 4. AWS Group Container Styles

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

## 5. AWS Resource Icon Base Style

ALWAYS append to every AWS resource icon:

```
sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;outlineConnect=0;
```

---

## 6. Azure Resource Base Style

ALWAYS append to every Azure stencil:

```
sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;
```

---

## 7. GCP Resource Base Style

ALWAYS append to every GCP stencil:

```
sketch=0;html=1;whiteSpace=wrap;verticalLabelPosition=bottom;verticalAlign=top;align=center;
```

ALWAYS use `mxgraph.gcp2.*` — NEVER use the legacy `mxgraph.gcp.*` namespace.

---

## 8. Deployment Node Styles

### Environment Node

```
shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#f5f5f5;strokeColor=#666666;fontStyle=1;verticalAlign=top;
```

Use for top-level deployment environments (Production, Staging, etc.).

### Server Node

```
shape=cube;whiteSpace=wrap;html=1;size=10;container=1;fillColor=#dae8fc;strokeColor=#6c8ebf;fontStyle=1;verticalAlign=top;
```

Use for individual servers or VM instances. Nested inside environment nodes.

### Application Artifact

```
shape=note;whiteSpace=wrap;html=1;fillColor=#dae8fc;strokeColor=#6c8ebf;
```

Dimensions: 120 x 60. Represents a deployed JAR, WAR, Docker image, or binary.

### Database Artifact

```
shape=cylinder3;whiteSpace=wrap;html=1;fillColor=#d5e8d4;strokeColor=#82b366;size=10;
```

Dimensions: 100 x 80. Represents a deployed database instance.

---

## 9. UML Component Shape

For component diagrams that need the UML component icon:

```
shape=component;whiteSpace=wrap;html=1;align=center;fillColor=#85bbf0;strokeColor=#78A8D8;fontColor=#000000;
```

Dimensions: 160 x 80. The `shape=component` adds the stereotypical two-tab UML component icon.

### Provided Interface (Lollipop)

```
shape=lollipop;whiteSpace=wrap;html=1;direction=south;
```

Dimensions: 40 x 30. Represents a provided interface on a component.

### Required Interface (Socket)

```
shape=requires;whiteSpace=wrap;html=1;direction=south;
```

Dimensions: 40 x 30. Represents a required interface on a component.

---

## 10. Multi-Cloud Zone Container

When a diagram depicts resources from multiple cloud providers, ALWAYS place each provider's resources inside a separate zone:

```
rounded=1;whiteSpace=wrap;html=1;fillColor=none;strokeColor=#<color>;strokeWidth=2;dashed=1;verticalAlign=top;fontStyle=1;fontSize=12;fontColor=#<color>;container=1;collapsible=0;
```

| Provider | strokeColor / fontColor |
|----------|------------------------|
| AWS | `#FF9900` |
| Azure | `#0078D4` |
| GCP | `#4285F4` |
