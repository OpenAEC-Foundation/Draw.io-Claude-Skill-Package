# Draw.io Skill Package — DECISIONS

## Architectural Decisions

### D-001: Research-First Methodology
**Date:** 2026-03-16
**Decision:** Use the proven 7-phase research-first methodology from Blender and ERPNext packages.
**Rationale:** This approach produces higher-quality, deterministic skills because research precedes creation.

### D-002: Custom MCP Server
**Date:** 2026-03-16
**Decision:** Build a custom TypeScript MCP server instead of using existing community MCP servers.
**Rationale:** Existing servers (jgraph/drawio-mcp, Sujimoshi/drawio-mcp) don't integrate optimally with our skill package patterns. A custom server can expose exactly the 18 tools we need and use the same XML knowledge encoded in our skills.

### D-003: Skill Package + MCP Co-location
**Date:** 2026-03-16
**Decision:** The MCP server lives inside the skill package repo at `mcp-server/`.
**Rationale:** Keeps the skill package and its tooling together. The skills define WHAT to do, the MCP server provides HOW to do it programmatically.

### D-004: TypeScript for MCP Server
**Date:** 2026-03-16
**Decision:** Use TypeScript with @modelcontextprotocol/sdk for the MCP server.
**Rationale:** TypeScript is the standard for MCP servers, aligns with the Draw.io codebase (JavaScript), and has the best SDK support.

### D-005: 22 Skills Preliminary Count
**Date:** 2026-03-16
**Decision:** Target 22 skills across 5 categories (core: 3, syntax: 4, impl: 11, errors: 2, agents: 2).
**Rationale:** Based on initial technology landscape analysis. Will be refined in Phase B3 after deep research.

### D-006: Parallel Execution Strategy
**Date:** 2026-03-16
**Decision:** MCP server development starts after Phase B2 (deep research) and runs parallel to skill creation.
**Rationale:** The MCP server needs the XML format knowledge from research, but doesn't need to wait for all skills to be complete.

### D-007: Workflow Template Extraction
**Date:** 2026-03-16
**Decision:** Extract a general Skill-Package-Workflow-Template to `C:\Users\Freek Heijting\Documents\GitHub\Skill-Package-Workflow-Template` before starting the Draw.io package.
**Rationale:** Accelerates this and all future skill package projects by standardizing the repeatable process.

### D-008: Align with Anthropic Official Skill Specification
**Date:** 2026-03-16
**Decision:** Align our skill structure with the official Anthropic specification from "The Complete Guide to Building Skills for Claude" and the agentskills.io open standard.
**Rationale:** Ensures compatibility with Claude.ai, Claude Code, and API. Enables distribution via the official Anthropic marketplace. Future-proofs against ecosystem changes.

### D-009: Add scripts/ and assets/ to Skill Structure
**Date:** 2026-03-16
**Decision:** Extend our skill structure beyond SKILL.md + references/ to include scripts/ (for XML validation scripts) and assets/ (for diagram templates).
**Rationale:** Official Anthropic spec supports these directories. Validation scripts make skills deterministic (code > language for critical checks). Diagram templates provide immediate value.

### D-010: Plugin Distribution Strategy
**Date:** 2026-03-16
**Decision:** Package the Draw.io skill package as a Claude Code plugin with `.claude-plugin/plugin.json` for marketplace distribution, in addition to the standalone skills format.
**Rationale:** Plugin format enables `/plugin marketplace add` installation, namespacing, version management, and submission to the official Anthropic marketplace (94.7k stars repo).

### D-011: Phase B0.5 — Anthropic Ecosystem Research
**Date:** 2026-03-16
**Decision:** Add a dedicated research phase (B0.5) to study the Anthropic skills ecosystem: claude.com/skills, the Complete Guide PDF, anthropics/skills repo, plugin docs, and recent updates.
**Rationale:** Anthropic releases weekly updates. Our package must be current with the latest specifications, patterns, and distribution mechanisms. This research is already partially complete.

### D-012: skill-creator First Approach
**Date:** 2026-03-16
**Decision:** Use Anthropic's built-in skill-creator as the primary tool for skill generation, with our 7-phase methodology as the quality backbone.
**Rationale:** skill-creator generates properly formatted SKILL.md with frontmatter, suggests trigger phrases, and reviews skills. Combines Anthropic's latest best practices with our proven research-first quality process.

### D-013: E2E Scripts per Skill
**Date:** 2026-03-16
**Decision:** Bundle comprehensive scripts/ per skill: validators, generators, and helpers. Goal: fully support the user with maximum end-to-end functionality.
**Rationale:** Anthropic's guide: "Code is deterministic; language interpretation isn't." Scripts make skills reliable and testable.

### D-014: Community Skills Analysis in Research Phase
**Date:** 2026-03-16
**Decision:** Thoroughly analyze all existing Draw.io community skills (ekusiadadus/draw-mcp, drawio-diagrams-enhanced, softaworks/agent-toolkit) as part of phase B2.
**Rationale:** Learn from existing approaches and mistakes. Document findings in `community-skills-analysis.md`.

### D-015: Hybride MCP Server Approach
**Date:** 2026-03-16
**Decision:** Study existing MCP servers (jgraph, Sujimoshi, lgazo) for patterns, but build our own server from scratch.
**Rationale:** Best of both worlds: learn from existing implementations, but without the technical debt of a fork.

### D-016: Draw.io Direct, Template Later
**Date:** 2026-03-16
**Decision:** Develop the Draw.io skill package directly (Project B). Extract the Skill-Package-Workflow-Template (Project A) afterwards.
**Rationale:** The Draw.io workspace is already bootstrapped. The template will be extracted as a living example, not as an abstract design.

### D-017: Claude-First, No agentskills.io Compliance
**Date:** 2026-03-16
**Decision:** Focus on the Claude ecosystem. No explicit agentskills.io open standard compliance.
**Rationale:** Freely use Claude-specific features (allowed-tools, plugin marketplace, progressive disclosure) without cross-platform restrictions.

### D-018: Dual External MCP Configuration
**Date:** 2026-03-19
**Decision:** Configure two external MCP servers for immediate usability: `drawio-mcp-server` (lgazo, CRUD) + `@drawio/mcp` (jgraph, official).
**Rationale:** `drawio-mcp-server` (1100+ stars, v1.8.0, actively maintained) provides full programmatic CRUD on diagram elements including layers and a built-in editor. `@drawio/mcp` (1400+ stars, official from jgraph) provides direct integration with the Draw.io editor for CSV/Mermaid conversion. Together they cover all immediate needs while the custom MCP server (D-002) is built later.

### D-019: Keep 22 Skills Unchanged After Research
**Date:** 2026-03-19
**Decision:** Keep all 22 skills from raw masterplan unchanged after deep research review.
**Rationale:** All 4 vooronderzoek documents (3800+ lines) confirm sufficient scope for each skill. No overlaps warrant merging, no gaps require new skills. core-styles vs syntax-styles have clear scope boundaries (system understanding vs property catalog).

### D-020: Cap Batches at 3 Parallel Agents
**Date:** 2026-03-19
**Decision:** Maximum 3 agents per batch, resulting in 8 batches for 22 skills.
**Rationale:** WORKFLOW.md standard: "3 agents per batch (optimal for Claude Code Agent tool)". Raw masterplan had batches of 4 — adjusted for reliability.

### D-021: Skip Separate Topic Research Phase (B4)
**Date:** 2026-03-19
**Decision:** Skip Phase B4 (Topic-Specific Research) as a separate phase. Agent prompts include specific source URLs for inline WebFetch during skill creation.
**Rationale:** The 4 vooronderzoek documents (3800+ lines) provide comprehensive coverage. Each agent prompt includes relevant research document references and WebFetch URLs. Separate topic research docs would be redundant.

### D-022: Directory Structure Follows WORKFLOW Standard
**Date:** 2026-03-19
**Decision:** Use `skills/source/drawio-{category}/{skill-name}/` directory structure.
**Rationale:** Aligns with WORKFLOW.md standard for all skill packages. Differs from CLAUDE.md's initial `skills/drawio/` — the WORKFLOW standard takes precedence.

### D-023: Core-Styles vs Syntax-Styles Scope Boundary
**Date:** 2026-03-19
**Decision:** Maintain separate core-styles and syntax-styles skills with clear scope boundaries: core-styles covers system understanding (format, inheritance, perimeters, color system), syntax-styles covers the complete property reference catalog (120+ properties).
**Rationale:** Research confirmed both skills have sufficient distinct scope. core-styles is for understanding HOW the style system works, syntax-styles is for looking up WHAT properties exist. Different audiences, no duplication.

### D-024: Extended YAML Frontmatter Fields
**Date:** 2026-03-19
**Decision:** Add license, compatibility, and metadata fields to all skill YAML frontmatter, beyond the minimum name+description.
**Rationale:** WORKFLOW template standard requires these fields for distribution readiness. Enables future plugin marketplace submission.
