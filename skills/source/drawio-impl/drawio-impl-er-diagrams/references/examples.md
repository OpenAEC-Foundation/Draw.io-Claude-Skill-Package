# Examples: ER Diagram Implementation

Working XML examples for ER diagram patterns. Every example is valid mxGraph XML that Draw.io renders correctly.

---

## 1. Minimal ER Diagram (2 Entities, 1 Relationship)

The simplest valid ER diagram: two entities connected with a one-to-many relationship.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Entity: Department -->
    <mxCell id="ent_dept" value="Department" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="60" y="100" width="200" height="90" as="geometry" />
    </mxCell>
    <mxCell id="dept_pk" value="dept_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_dept">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="dept_f1" value="dept_name  VARCHAR(100)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_dept">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Entity: Employee -->
    <mxCell id="ent_emp" value="Employee" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="380" y="80" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="emp_pk" value="emp_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_emp">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="emp_fk" value="dept_id  FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=2;" vertex="1" parent="ent_emp">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="emp_f1" value="name  VARCHAR(100)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_emp">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="emp_f2" value="hire_date  DATE" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_emp">
      <mxGeometry y="120" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Relationship: Department 1:N Employee -->
    <mxCell id="rel1" value="employs" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_dept" target="ent_emp">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 2. Many-to-Many with Junction Table

A many-to-many relationship resolved through a junction (bridge) table.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Entity: Student -->
    <mxCell id="ent_stu" value="Student" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="60" y="80" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="stu_pk" value="student_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_stu">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="stu_f1" value="name  VARCHAR(100)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_stu">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="stu_f2" value="email  VARCHAR(255)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_stu">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Entity: Enrollment (Junction Table) -->
    <mxCell id="ent_enr" value="Enrollment" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#fff2cc;strokeColor=#d6b656;" vertex="1" parent="1">
      <mxGeometry x="380" y="80" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="enr_fk1" value="student_id  PK FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=6;" vertex="1" parent="ent_enr">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="enr_fk2" value="course_id  PK FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=6;" vertex="1" parent="ent_enr">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="enr_f1" value="enrolled_date  DATE" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_enr">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Entity: Course -->
    <mxCell id="ent_crs" value="Course" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="700" y="80" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="crs_pk" value="course_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_crs">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="crs_f1" value="title  VARCHAR(200)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_crs">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="crs_f2" value="credits  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_crs">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Relationship: Student 1:N Enrollment -->
    <mxCell id="rel1" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_stu" target="ent_enr">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Relationship: Course 1:N Enrollment -->
    <mxCell id="rel2" style="edgeStyle=entityRelationEdgeStyle;html=1;endArrow=ERmany;endFill=0;startArrow=ERone;startFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_crs" target="ent_enr">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 3. Optional Relationships (Zero-or-One, Zero-or-Many)

Demonstrates optional cardinality using `ERzeroToOne` and `ERzeroToMany`.

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Entity: User -->
    <mxCell id="ent_usr" value="User" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="60" y="100" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="usr_pk" value="user_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_usr">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="usr_f1" value="username  VARCHAR(50)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_usr">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="usr_f2" value="email  VARCHAR(255)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_usr">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Entity: Profile (optional 1:1 with User) -->
    <mxCell id="ent_prof" value="Profile" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#d5e8d4;strokeColor=#82b366;" vertex="1" parent="1">
      <mxGeometry x="380" y="40" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="prof_pk" value="profile_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_prof">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="prof_fk" value="user_id  FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=2;" vertex="1" parent="ent_prof">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="prof_f1" value="bio  TEXT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_prof">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Entity: LoginHistory (optional 0:N with User) -->
    <mxCell id="ent_log" value="LoginHistory" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#f5f5f5;strokeColor=#666666;" vertex="1" parent="1">
      <mxGeometry x="380" y="220" width="200" height="120" as="geometry" />
    </mxCell>
    <mxCell id="log_pk" value="login_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_log">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="log_fk" value="user_id  FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=2;" vertex="1" parent="ent_log">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="log_f1" value="login_time  TIMESTAMP" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_log">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Relationship: User 1:0..1 Profile (optional one-to-one) -->
    <mxCell id="rel1" style="edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERone;startFill=0;endArrow=ERzeroToOne;endFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_usr" target="ent_prof">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>

    <!-- Relationship: User 1:0..N LoginHistory (optional one-to-many) -->
    <mxCell id="rel2" style="edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERone;startFill=0;endArrow=ERzeroToMany;endFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_usr" target="ent_log">
      <mxGeometry relative="1" as="geometry" />
    </mxCell>
  </root>
</mxGraphModel>
```

---

## 4. Self-Referencing Relationship

An entity that references itself (e.g., Employee reports to Manager).

```xml
<mxGraphModel>
  <root>
    <mxCell id="0" />
    <mxCell id="1" parent="0" />

    <!-- Entity: Employee (self-referencing) -->
    <mxCell id="ent_emp" value="Employee" style="shape=table;startSize=30;container=1;collapsible=1;childLayout=tableLayout;fixedRows=1;rowLines=0;fontStyle=1;align=center;resizeLast=1;fillColor=#dae8fc;strokeColor=#6c8ebf;" vertex="1" parent="1">
      <mxGeometry x="200" y="100" width="200" height="150" as="geometry" />
    </mxCell>
    <mxCell id="emp_pk" value="emp_id  PK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=4;" vertex="1" parent="ent_emp">
      <mxGeometry y="30" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="emp_fk" value="manager_id  FK  INT" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;fontStyle=2;" vertex="1" parent="ent_emp">
      <mxGeometry y="60" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="emp_f1" value="name  VARCHAR(100)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_emp">
      <mxGeometry y="90" width="200" height="30" as="geometry" />
    </mxCell>
    <mxCell id="emp_f2" value="title  VARCHAR(100)" style="text;strokeColor=none;fillColor=none;align=left;verticalAlign=middle;spacingLeft=4;spacingRight=4;overflow=hidden;rotatable=0;whiteSpace=wrap;html=1;" vertex="1" parent="ent_emp">
      <mxGeometry y="120" width="200" height="30" as="geometry" />
    </mxCell>

    <!-- Self-referencing: Employee (manager) 0..1:N Employee -->
    <mxCell id="rel_self" value="manages" style="edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERzeroToOne;startFill=0;endArrow=ERmany;endFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_emp" target="ent_emp">
      <mxGeometry relative="1" as="geometry">
        <Array as="points">
          <mxPoint x="500" y="175" />
          <mxPoint x="500" y="225" />
        </Array>
      </mxGeometry>
    </mxCell>
  </root>
</mxGraphModel>
```

Note: Self-referencing edges require explicit waypoints via `<Array as="points">` to route the edge out and back to the same entity. Without waypoints, the edge collapses to zero length.

---

## 5. Mandatory Relationships (ERmandOne, ERoneToMany)

Demonstrates mandatory cardinality on both sides of a relationship.

```xml
<!-- Relationship: Company 1:1+ Department (mandatory both sides) -->
<mxCell id="rel_mand" value="has" style="edgeStyle=entityRelationEdgeStyle;html=1;startArrow=ERmandOne;startFill=0;endArrow=ERoneToMany;endFill=0;strokeColor=#666666;" edge="1" parent="1" source="ent_company" target="ent_department">
  <mxGeometry relative="1" as="geometry" />
</mxCell>
```

- `ERmandOne` at source: the company MUST have exactly one instance on this side.
- `ERoneToMany` at target: there MUST be at least one department (mandatory many).
