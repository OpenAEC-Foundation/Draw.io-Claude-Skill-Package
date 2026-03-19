# Draw.io Skill Package — REQUIREMENTS

## Quality Guarantees

Every skill in this package MUST meet the following criteria:

### 1. Format-correct
- SKILL.md < 500 lines
- Valid YAML frontmatter with `name` and `description`
- `name`: kebab-case, max 64 characters, prefix `drawio-`
- `description`: max 1024 characters, includes trigger keywords
- `references/` directory with: methods.md, examples.md, anti-patterns.md

### 2. XML-accurate
- All mxGraph XML examples MUST be valid and parseable
- Style strings MUST use correct property names and values
- Cell IDs MUST be unique within examples
- Parent-child relationships MUST be consistent

### 3. Version-explicit
- Target: Current Draw.io (diagrams.net) open-source version
- mxGraph XML format: version 2 (current)
- Note breaking changes between mxGraph versions where applicable

### 4. Anti-pattern-free
- Every skill MUST document known mistakes in references/anti-patterns.md
- Common XML malformation patterns documented
- Style string errors documented

### 5. Deterministic
- Use ALWAYS/NEVER language
- No hedging words: "might", "consider", "often", "usually"
- Decision trees for conditional logic

### 6. Self-contained
- Each skill works independently without requiring other skills
- All necessary context included within the skill
- Cross-references to related skills are informational only

### 7. English-only
- All skill content in English
- Claude reads English, responds in any language
- No Dutch, German, or other languages in skill files

## Per-Category Requirements

### Core Skills
- MUST cover the complete mxGraph XML schema
- MUST include coordinate system documentation
- MUST document compressed vs uncompressed format

### Syntax Skills
- MUST include complete attribute catalogs
- MUST show both minimal and full examples
- MUST document all valid values for enum-type attributes

### Implementation Skills
- MUST produce complete, valid .drawio files
- MUST include realistic diagram examples (not just toy examples)
- MUST document diagram-type-specific shapes and connection patterns

### Error Skills
- MUST include real error scenarios with reproduction steps
- MUST provide fix patterns for every documented error

### Agent Skills
- MUST include decision trees for diagram type selection
- MUST validate generated XML against schema rules
