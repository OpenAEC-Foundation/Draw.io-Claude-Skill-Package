# Methods Reference: Draw.io XML Error Diagnosis

Systematic methods for detecting and fixing Draw.io XML errors.

---

## 1. XML Well-Formedness Validation

**Method:** Parse the XML document with a strict XML parser before opening in Draw.io.

**Steps:**
1. Feed the complete XML string to an XML parser.
2. If parsing fails, the error message identifies the line and character position.
3. Common parse failures: unclosed tags, unescaped ampersands, mismatched quotes.

**Required Tag Closure Patterns:**

| Element | Correct Self-Close | Correct Open/Close |
|---------|-------------------|-------------------|
| `mxCell` (no children) | `<mxCell id="2" ... />` | N/A — ALWAYS self-close |
| `mxCell` (with geometry) | N/A | `<mxCell id="2" ...>` + `</mxCell>` |
| `mxGeometry` (no children) | `<mxGeometry ... />` | N/A — ALWAYS self-close |
| `mxGeometry` (with points) | N/A | `<mxGeometry ...>` + `</mxGeometry>` |
| `mxPoint` | `<mxPoint x="0" y="0" ... />` | N/A — ALWAYS self-close |

---

## 2. Structural Cell Verification

**Method:** Check that the two mandatory structural cells exist in every `<root>` element.

**Steps:**
1. Locate every `<root>` element in the document (one per page).
2. Verify `<mxCell id="0" />` exists as a direct child.
3. Verify `<mxCell id="1" parent="0" />` exists as a direct child.
4. Verify id="0" has NO `parent` attribute.
5. Verify id="1" has `parent="0"` and NO `vertex`, `edge`, or `style` attributes.

**Mandatory Structure:**
```xml
<root>
  <mxCell id="0" />
  <mxCell id="1" parent="0" />
  <!-- all content cells after these two -->
</root>
```

---

## 3. Duplicate ID Detection

**Method:** Collect all cell identifiers and check for uniqueness.

**Steps:**
1. Extract all `id` attributes from `<mxCell>`, `<object>`, and `<UserObject>` elements.
2. Build a set of seen IDs.
3. Any ID that appears more than once is a duplicate.
4. Check across ALL `<diagram>` pages — IDs MUST be unique file-wide.

**ID Rules:**
- `"0"` and `"1"` are reserved for structural cells. NEVER use them for content.
- Sequential integers (`"2"`, `"3"`, `"4"`, ...) are the safest for AI generation.
- Draw.io uses random alphanumeric IDs (e.g., `"aB3x-Kz9q"`), but any unique string works.

---

## 4. Parent Reference Integrity Check

**Method:** Verify every `parent` attribute points to an existing cell.

**Steps:**
1. Build a set of all cell IDs in the current `<root>`.
2. For every cell with a `parent` attribute, verify the parent ID exists in the set.
3. Verify the parent hierarchy forms a tree (no circular references).
4. Verify layer cells (direct children of id="0") have `parent="0"`.
5. Verify content cells have `parent="1"` or the ID of a valid group/container.

**Valid Parent Chain:**
```
id="0" (no parent)
  id="1" parent="0" (default layer)
    id="2" parent="1" (shape on default layer)
    id="3" parent="1" (group container on default layer)
      id="4" parent="3" (child of group)
```

---

## 5. Style String Validation

**Method:** Parse the semicolon-separated style string and validate each property.

**Steps:**
1. Split the style string by `;` (semicolons).
2. For each segment:
   - If it contains `=`, it is a key-value pair. Validate the key name.
   - If it does NOT contain `=`, it is a leading shape identifier (MUST be the first segment only).
3. Check for required properties: `html=1` (all cells), `whiteSpace=wrap` (labeled vertices).
4. Check boolean values use `1`/`0`, NEVER `true`/`false`.
5. Check color values use `#RRGGBB` format, `none`, or named CSS colors.

**Valid Style String Anatomy:**
```
[shapeIdentifier;]key1=value1;key2=value2;...;keyN=valueN[;]
```

**Common Invalid Property Names (AI Inventions):**
| Invalid | Correct |
|---------|---------|
| `backgroundColor` | `fillColor` |
| `borderColor` | `strokeColor` |
| `borderWidth` | `strokeWidth` |
| `font-size` | `fontSize` |
| `font-style` | `fontStyle` |
| `text-align` | `align` |
| `border-radius` | `rounded=1;arcSize=N` |
| `opacity` | `opacity` (this one is correct, 0-100) |

---

## 6. HTML Escaping Verification

**Method:** Check that all HTML content in `value` attributes is properly XML-escaped.

**Steps:**
1. Find all `value` attributes that contain HTML content.
2. Verify `<` is encoded as `&lt;`.
3. Verify `>` is encoded as `&gt;`.
4. Verify `&` is encoded as `&amp;` (except when part of an entity like `&lt;`).
5. Verify `"` inside attribute values is encoded as `&quot;`.
6. Check for double-escaping: `&amp;lt;` is WRONG (it renders as literal `&lt;`).

**Escaping Depth Rule:**
- Plain text label: No escaping needed in `value` attribute (except `"` and `&`).
- HTML label with `html=1`: Escape ALL HTML tags once for XML.
- HTML label with inline CSS: Escape both the HTML tags AND quotes in CSS `style=""`.

**Example of Correct Triple-Level Escaping:**
```xml
value="&lt;div style=&quot;color:red&quot;&gt;Error&lt;/div&gt;"
```

---

## 7. Edge Geometry Validation

**Method:** Verify edge cells have correct geometry configuration.

**Steps:**
1. Find all cells with `edge="1"`.
2. Verify each edge has `<mxGeometry relative="1" as="geometry" />` or `<mxGeometry relative="1" as="geometry">`.
3. If the edge has `source` and `target` attributes, verify both referenced cells exist and have `vertex="1"`.
4. If the edge has NO `source` or `target`, verify `sourcePoint` and `targetPoint` mxPoint elements exist inside the geometry.
5. Verify waypoint arrays use `<Array as="points">` with absolute `<mxPoint>` coordinates.

---

## 8. Compression Detection and Handling

**Method:** Determine whether diagram content is compressed and handle accordingly.

**Steps:**
1. Check the `compressed` attribute on `<mxfile>`.
2. Inspect the content of each `<diagram>` element:
   - If it contains an `<mxGraphModel>` child element: content is uncompressed (correct for AI).
   - If it contains a text node (string of characters): content is compressed.
3. To decompress: Base64-decode -> raw INFLATE (no zlib headers) -> URL-decode.
4. NEVER generate compressed content. ALWAYS output uncompressed `<mxGraphModel>`.

---

## 9. Shape Name Validation

**Method:** Verify all shape names reference real Draw.io shapes.

**Steps:**
1. Extract the `shape=` value from each vertex's style string (if present).
2. Also check for leading shape identifiers (bare words before the first `=`).
3. Validate against the known shape categories:
   - Built-in primitives: `rectangle`, `ellipse`, `rhombus`, `triangle`, `hexagon`, `cylinder`, `cloud`, `actor`, `swimlane`, `line`, `image`, `label`, `arrow`
   - Extended: `cylinder3`, `document`, `parallelogram`, `step`, `trapezoid`, `process`, `callout`, `note`, `doubleEllipse`, `cross`, `plus`, `orEllipse`, `sumEllipse`, `sortShape`, `collate`, `curlyBracket`, `singleArrow`, `doubleArrow`, `dataStorage`, `manualInput`, `card`, `internalStorage`, `offPageConnector`, `delay`, `display`, `loopLimit`, `umlLifeline`, `folder`, `cube`, `partialRectangle`
   - Stencil libraries: MUST follow `mxgraph.<library>.<shape>` pattern
4. Flag any shape name that does not match a known value.

---

## 10. Container/Group Validation

**Method:** Verify groups and containers are correctly configured.

**Steps:**
1. Find all cells that are referenced as `parent` by other cells (excluding id="0" and id="1").
2. Verify each such cell has `container=1` in its style.
3. Verify child cell coordinates are relative to the parent (small x/y values, not large canvas-absolute values).
4. For swimlanes: verify `startSize` is set and `container=1` is present.
5. Verify no circular parent references exist.
