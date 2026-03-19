# Anti-Patterns Reference: Draw.io Code Validator

Patterns that ALWAYS produce broken or degraded diagrams. NEVER use these patterns.

---

## AP-001: Skipping Validation Stages

**Pattern:** Running only Stages 1-4 (blocking) and skipping Stages 5-8 (warnings).

**Why It Fails:** Warning-stage issues cause visual defects that confuse users — edges connecting to wrong points, labels at canvas origin, text overflowing shapes. The diagram "works" but looks broken.

**Correct Pattern:** ALWAYS run ALL 8 stages. Warning stages take minimal additional effort and catch the most visible user-facing issues.

---

## AP-002: Validating Partial XML Snippets

**Pattern:** Validating only the cells that were just added or modified, not the complete file.

```xml
<!-- NEVER validate only this snippet: -->
<mxCell id="5" value="New" style="rounded=0;whiteSpace=wrap;html=1;"
        vertex="1" parent="1">
  <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
</mxCell>
```

**Why It Fails:** The snippet alone passes Stage 5 (valid style), but the full file may already have an id="5" (Stage 3 failure) or parent="1" may not exist if structural cells were removed (Stage 4 failure).

**Correct Pattern:** ALWAYS validate the COMPLETE file after every modification. NEVER validate isolated snippets.

---

## AP-003: Silent Auto-Fixing

**Pattern:** Automatically correcting errors without reporting them to the user.

**Why It Fails:** The user does not learn about the mistake and repeats it in future diagrams. Silent fixes also mask systematic generation issues that need root-cause correction.

**Correct Pattern:** ALWAYS report every error found, then list every auto-fix applied. The user MUST see both the problem and the solution.

---

## AP-004: Accepting Structural Failures with Warnings

**Pattern:** Downgrading Stage 1-4 errors to warnings and delivering the XML anyway.

```
# NEVER DO THIS
VALIDATION RESULT: PASS (with warnings)
  [S2-W1] Missing root cell id="0" — WARNING
```

**Why It Fails:** Missing structural cells cause Draw.io to fail completely. There is no "partial success" for structural errors — the diagram either loads or it does not.

**Correct Pattern:** Stages 1-4 are ALWAYS BLOCKING. NEVER downgrade them to warnings. If a blocking stage fails and auto-fix cannot resolve it, report FAIL and do NOT deliver the XML.

---

## AP-005: Fixing IDs Without Updating References

**Pattern:** Reassigning a duplicate ID without updating `parent`, `source`, and `target` references.

```xml
<!-- Original: two cells with id="5" -->
<mxCell id="5" value="A" vertex="1" parent="1" ... />
<mxCell id="5" value="B" vertex="1" parent="1" ... />
<mxCell id="6" edge="1" source="5" target="7" parent="1" ... />

<!-- WRONG fix: renamed second id="5" to id="8" but edge still points to "5" -->
<mxCell id="5" value="A" vertex="1" parent="1" ... />
<mxCell id="8" value="B" vertex="1" parent="1" ... />
<mxCell id="6" edge="1" source="5" target="7" parent="1" ... />
<!-- Edge now connects to "A" instead of "B" — silent logical error -->
```

**Why It Fails:** The edge was supposed to connect to "B" (the second cell originally with id="5"), but after renaming only the ID without updating the edge's source, it now connects to "A".

**Correct Pattern:** When reassigning duplicate IDs, ALWAYS identify which references (parent, source, target) pointed to each instance and update them to the correct new ID. This requires understanding the diagram's intended structure.

---

## AP-006: Trusting Shape Names Without Verification

**Pattern:** Accepting any `shape=` value without checking it against the known shape registry.

```xml
<!-- NEVER accept invented shapes without flagging them -->
<mxCell id="2" style="shape=server;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

**Why It Fails:** `shape=server` does not exist in Draw.io. The shape renders as a plain rectangle (sometimes with a red X), defeating the purpose of using a specific shape.

**Correct Pattern:** Stage 5 MUST verify every `shape=` value against the known built-in shapes list and the `mxgraph.*` stencil library pattern. Flag unknown shapes as warnings.

---

## AP-007: Ignoring Perimeter Mismatches

**Pattern:** Validating styles without checking perimeter-to-shape consistency.

```xml
<!-- Ellipse WITHOUT ellipsePerimeter -->
<mxCell id="2" style="ellipse;whiteSpace=wrap;html=1;" vertex="1" parent="1">
```

**Why It Fails:** Edges connecting to this ellipse use the default rectanglePerimeter, causing connection points to appear at the bounding box corners instead of on the ellipse boundary. Visually, arrows "float" near the shape instead of touching it.

**Correct Pattern:** Stage 8 MUST verify that non-rectangle shapes have the matching perimeter property. ALWAYS add the correct perimeter for ellipses, rhombuses, triangles, hexagons, and parallelograms.

---

## AP-008: Validating Only New Diagrams

**Pattern:** Running the validation pipeline only when creating diagrams from scratch, but skipping it when editing existing diagrams.

**Why It Fails:** Edits can introduce all the same errors: duplicate IDs (if the new cell reuses an existing ID), broken parent references (if a container was deleted but children remain), style errors (if copying styles from one cell type to another).

**Correct Pattern:** ALWAYS run the full 8-stage pipeline after ANY modification — creation, editing, deletion, or restructuring. The pipeline is idempotent and fast; there is no reason to skip it.

---

## AP-009: Using true/false for Boolean Style Properties

**Pattern:** Writing `rounded=true` or `dashed=false` in style strings.

```
<!-- NEVER DO THIS -->
style="rounded=true;dashed=true;shadow=true;whiteSpace=wrap;html=1;"
```

**Why It Fails:** Draw.io silently ignores string boolean values. The shape appears without rounding, dashing, or shadow. There is no error message — the properties are simply not applied.

**Correct Pattern:** ALWAYS use `1` for true and `0` for false:
```
style="rounded=1;dashed=1;shadow=1;whiteSpace=wrap;html=1;"
```

Stage 5 MUST flag every `=true` and `=false` occurrence and auto-fix to `=1` and `=0`.

---

## AP-010: Delivering XML Without Running the Pipeline

**Pattern:** Generating Draw.io XML and presenting it to the user without running any validation.

**Why It Fails:** AI-generated XML frequently contains:
- Missing structural cells (id="0", id="1")
- Invented shape names
- Unescaped HTML in value attributes
- Duplicate IDs from loop-based generation
- Missing html=1 and whiteSpace=wrap

These errors cause diagrams to fail silently or look wrong. The user blames Draw.io instead of the XML.

**Correct Pattern:** ALWAYS run the full 8-stage validation pipeline on every piece of Draw.io XML before presenting it to the user. This is a non-negotiable quality gate.
