# Methods Reference: Draw.io Code Validator

Systematic methods for executing the 8-stage validation pipeline.

---

## Method 1: Full Pipeline Execution

**When to Use:** ALWAYS. Run on every Draw.io XML before output.

**Steps:**
1. Receive the complete XML string.
2. Execute Stage 1 (XML Well-Formedness). If FAIL, attempt auto-fix and re-run. If STILL FAIL, stop and report.
3. Execute Stage 2 (Structure Check). If FAIL, auto-fix and re-run. If STILL FAIL, stop and report.
4. Execute Stage 3 (ID Uniqueness). If FAIL, auto-fix and re-run.
5. Execute Stage 4 (Parent-Child Integrity). If FAIL, auto-fix and re-run.
6. Execute Stages 5-8 in sequence. Collect all warnings.
7. Generate the error report using the standard format.
8. If auto-fixes were applied, present both the report and the corrected XML.

---

## Method 2: Stage 1 — XML Well-Formedness Validation

**Procedure:**
1. Attempt to parse the XML as a well-formed XML document.
2. Check every opening tag has a matching close or self-close.
3. Verify all attribute values are in double quotes.
4. Scan all attribute values for raw `<`, `>`, `&` characters.
5. Check `<diagram>` element content — it MUST contain `<mxGraphModel>`, NOT Base64 text.

**Tag Closure Rules:**

| Element | Without Children | With Children |
|---------|-----------------|---------------|
| `mxCell` | `<mxCell ... />` | `<mxCell ...> <mxGeometry .../> </mxCell>` |
| `mxGeometry` | `<mxGeometry ... />` | `<mxGeometry ...> <mxPoint .../> </mxGeometry>` |
| `mxPoint` | `<mxPoint ... />` | N/A — ALWAYS self-close |
| `Array` | N/A | `<Array as="..."> <mxPoint .../> </Array>` |

**Escaping Rules:**

| Character | MUST Escape To | In Context |
|-----------|---------------|------------|
| `<` | `&lt;` | Inside attribute values |
| `>` | `&gt;` | Inside attribute values |
| `&` | `&amp;` | Inside attribute values |
| `"` | `&quot;` | Inside double-quoted attribute values |

---

## Method 3: Stage 2 — Structure Check

**Procedure:**
1. Locate every `<root>` element (one per `<diagram>` page).
2. For each `<root>`:
   a. Verify `<mxCell id="0"/>` exists with NO `parent`, `vertex`, `edge`, or `style` attributes.
   b. Verify `<mxCell id="1" parent="0"/>` exists with NO `vertex`, `edge`, or `style` attributes.
   c. Verify id="0" appears before id="1" in document order.
3. Verify `<root>` is inside `<mxGraphModel>`.
4. Verify `<mxGraphModel>` is inside `<diagram>`.

**Structural Cell Rules:**
- id="0" is the invisible root — it anchors the hierarchy.
- id="1" is the default layer — all visible content references it as parent.
- These two cells NEVER have styles, vertex/edge flags, or visual properties.

---

## Method 4: Stage 3 — ID Uniqueness Validation

**Procedure:**
1. Collect all `id` attributes from `<mxCell>`, `<object>`, and `<UserObject>` elements across ALL pages.
2. Build a frequency map of each ID.
3. Any ID with count > 1 is a duplicate — report it as BLOCKING.
4. Verify id="0" appears exactly once and id="1" appears exactly once.
5. Verify no cell has `id=""` (empty string).

**ID Assignment Strategy for Auto-Fix:**
1. Find the maximum numeric ID in the document.
2. For each duplicate (after the first occurrence), assign max + 1, max + 2, etc.
3. Update all `parent`, `source`, and `target` references pointing to the old duplicate ID.
4. NEVER reassign the FIRST occurrence of a duplicate — only reassign subsequent ones.

---

## Method 5: Stage 4 — Parent-Child Integrity Validation

**Procedure:**
1. Build a map: `cell_id -> cell_element` for all cells.
2. For each cell with a `parent` attribute:
   a. Verify the parent ID exists in the map.
   b. Verify no circular chain (A parent of B, B parent of A).
   c. Verify cell id="0" has no parent attribute.
3. For each cell WITHOUT a `parent` attribute (except id="0"):
   Report as orphan — missing parent reference.

**Circular Reference Detection:**
1. For each cell, follow the parent chain upward.
2. Track visited IDs in a set.
3. If the current ID is already in the visited set, a cycle exists.
4. The chain MUST terminate at id="0" (the root).

---

## Method 6: Stage 5 — Style String Validation

**Procedure:**
1. For each cell with a `style` attribute:
   a. Split the style string by `;`.
   b. For each token: split by `=` to get property and value.
   c. The first token MAY be a shape identifier without `=` (e.g., `ellipse`).
   d. Verify each property name is a known Draw.io style property.
   e. Verify boolean properties use `1`/`0`, NOT `true`/`false`.
   f. Verify `html=1` is present.
   g. For vertices with a `value` attribute, verify `whiteSpace=wrap` is present.
2. Check vertex/edge style separation:
   a. If cell has `edge="1"`, flag vertex-only properties.
   b. If cell has `vertex="1"`, flag edge-only properties.

**Style String Syntax Rules:**
- Properties separated by `;`
- Key-value pairs joined by `=` with NO spaces
- Leading shape identifier has no `=` sign
- Trailing `;` is conventional
- Property names are camelCase

---

## Method 7: Stage 6 — Geometry Validation

**Procedure:**
1. For each vertex cell (`vertex="1"`):
   a. Verify it has a child `<mxGeometry>` element.
   b. Verify `width` and `height` are present and > 0.
   c. Verify `as="geometry"` is set.
   d. Flag dimensions outside 10-2000 range.
2. For each edge cell (`edge="1"`):
   a. Verify its `<mxGeometry>` has `relative="1"`.
   b. Verify `as="geometry"` is set.
3. For all `<mxPoint>` elements:
   a. Verify `x` and `y` are numeric values.

---

## Method 8: Stage 7 — Connection Validation

**Procedure:**
1. Build a set of all vertex IDs (cells with `vertex="1"`).
2. For each edge cell (`edge="1"`):
   a. If `source` is present, verify it exists in the vertex set.
   b. If `target` is present, verify it exists in the vertex set.
   c. If both `source` and `target` are missing, verify explicit waypoints exist.
   d. If `source` equals `target`, flag as potential self-loop.
3. Validate `edgeStyle` values against the known list.
4. Validate `endArrow` and `startArrow` values against the known list.

---

## Method 9: Stage 8 — Perimeter Validation

**Procedure:**
1. For each vertex cell, determine its shape type from the style string.
2. Look up the required perimeter for that shape type.
3. If the shape is NOT a rectangle/rounded and has no explicit `perimeter=`, report a warning.
4. If the shape has `perimeter=` but it does not match the expected value, report a mismatch warning.

**Shape Detection from Style:**
- First token without `=` indicates the shape (e.g., `ellipse`, `rhombus`).
- `shape=<name>` explicitly sets the shape.
- If no shape token and no `shape=`, the shape is a rectangle (default).

---

## Method 10: Auto-Fix Application

**When to Use:** After detecting errors that have documented auto-fix procedures.

**Rules:**
1. ALWAYS report the original error BEFORE applying the fix.
2. ALWAYS list every auto-fix that was applied.
3. ALWAYS re-run the failed stage after auto-fix to confirm it passes.
4. NEVER apply auto-fixes silently.
5. For BLOCKING stages: auto-fix and re-run. If still failing, report manual fix needed.
6. For WARNING stages: auto-fix and include in the report.

**Auto-Fix Priority Order:**
1. Structural fixes (add missing cells, fix nesting)
2. ID fixes (reassign duplicates)
3. Parent reference fixes (reset orphans)
4. Style fixes (add html=1, fix booleans)
5. Geometry fixes (add relative=1, fix dimensions)
6. Perimeter fixes (add correct perimeter)
