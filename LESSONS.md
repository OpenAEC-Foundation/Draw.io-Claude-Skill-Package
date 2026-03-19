# Draw.io Skill Package — LESSONS

## Lessons Learned

_Lessons from this project and inherited from Blender/ERPNext packages._

### L-001: Research Before Skills
**Source:** Blender package, ERPNext package
**Lesson:** ALWAYS complete deep research (vooronderzoek) before writing any skills. Skills written without research require major rewrites.

### L-002: Deterministic Language
**Source:** ERPNext package
**Lesson:** ALWAYS use ALWAYS/NEVER language in skills. Avoid "might", "consider", "often", "usually". Deterministic skills produce deterministic code.

### L-003: Description Triggers
**Source:** Blender package (L-006)
**Lesson:** Skill descriptions MUST include trigger keywords. No "Deterministic" prefix. Format: "{What it does}. Triggers: {keywords}".

### L-004: Batch Quality Gates
**Source:** Blender package
**Lesson:** ALWAYS run validation between skill batches. Never start batch N+1 before batch N passes all quality checks.

### L-005: English-Only Skills
**Source:** Both packages
**Lesson:** All skill content MUST be in English. Claude reads English and responds in the user's language automatically.

### L-006: 500-Line Limit
**Source:** ERPNext package
**Lesson:** SKILL.md files exceeding 500 lines lose effectiveness. Split into the main file + references/ for detailed content.

### L-007: Self-Contained Skills
**Source:** Both packages
**Lesson:** Each skill MUST work independently. Cross-references are informational only, never required.

### L-008: Progressive Disclosure (Anthropic Official)
**Source:** Anthropic "Complete Guide to Building Skills for Claude" (2026)
**Lesson:** Skills use a 3-level progressive disclosure system: (1) YAML frontmatter — ALWAYS in system prompt, (2) SKILL.md body — loaded when relevant, (3) Linked files — loaded on demand. Keep SKILL.md focused; move details to references/.

### L-009: Description = Trigger Mechanism
**Source:** Anthropic Official Guide
**Lesson:** The description field is HOW Claude decides to load a skill. Format: `[What it does] + [When to use it] + [Key capabilities]`. MUST include trigger phrases users would actually say. Under 1024 chars. No XML tags.

### L-010: No README.md in Skill Folders
**Source:** Anthropic Official Guide
**Lesson:** NEVER include README.md inside a skill folder. All documentation goes in SKILL.md or references/. Repo-level README is separate and for human visitors.

### L-011: Skill Structure Expanded
**Source:** Anthropic Official Guide
**Lesson:** Official skill structure includes scripts/ (executable code) and assets/ (templates, fonts, icons) alongside references/. Consider using these for validation scripts and diagram templates.

### L-012: allowed-tools Field
**Source:** Anthropic Official Guide, Claude Code Plugin Docs
**Lesson:** YAML frontmatter supports an `allowed-tools` field to restrict which tools a skill can use. Format: `"Bash(python:*) Bash(npm:*) WebFetch"`. Use for MCP-dependent skills to specify required tools.

### L-013: Plugin Distribution Model
**Source:** Claude Code Plugin Docs, anthropics/skills repo
**Lesson:** Skills can be distributed as Claude Code plugins with `.claude-plugin/plugin.json` manifest. Install via `/plugin marketplace add`. Consider submitting to official Anthropic marketplace at claude.ai/settings/plugins/submit.

### L-014: Research → Core Files Flow
**Source:** User feedback, 2026-03-16
**Lesson:** Research findings MUST ALWAYS be verwerkt (processed) into the core bestanden (CLAUDE.md, REQUIREMENTS.md, LESSONS.md, DECISIONS.md, SOURCES.md, WAY_OF_WORK.md). Na verwerking: markeer het research document met een verwerkt-status. Research is pas "af" als het in de core files staat.

### L-015: NOOIT Fundamentele Vragen Interpreteren
**Source:** User feedback, 2026-03-16
**Lesson:** NOOIT fundamentele vragen zelf interpreteren of beantwoorden. ALTIJD expliciet aan de user vragen. Leg open vragen vast in OPEN-QUESTIONS.md. Dit geldt voor alle architectuur-, scope-, aanpak- en toolkeuze-beslissingen. Interpretaties zijn ALLEEN toegestaan voor triviale implementatiedetails.

### L-016: AI XML Generation — Always Uncompressed
**Source:** drawio.com/doc/faq/ai-drawio-generation, B1 research (2026-03-19)
**Lesson:** ALWAYS generate uncompressed mxGraph XML (full `<mxGraphModel>` tags, not Base64). Draw.io compresses automatically on save. Simplified format (just `<mxGraphModel>` without `<mxfile>`/`<diagram>` wrappers) is also valid — Draw.io wraps it automatically.

### L-017: Perimeter Must Match Shape
**Source:** mxConstants JS API, B1 research (2026-03-19)
**Lesson:** Non-rectangular shapes MUST have a matching `perimeter` value in their style (e.g., `ellipse` requires `perimeter=ellipsePerimeter`). Missing perimeter causes wrong connection point routing.

### L-018: Mermaid Conversion Limitation
**Source:** B1 research (2026-03-19)
**Lesson:** Mermaid-to-Draw.io conversion produces a SINGLE compound shape, NOT individually editable mxGraph cells. For full editability, ALWAYS generate native mxGraph XML instead of converting from Mermaid.

### L-019: Container Coordinates Are Relative
**Source:** B1 research (2026-03-19)
**Lesson:** Child cells inside containers/groups use coordinates RELATIVE to the parent container, NOT absolute canvas coordinates. This is a common source of positioning bugs.
