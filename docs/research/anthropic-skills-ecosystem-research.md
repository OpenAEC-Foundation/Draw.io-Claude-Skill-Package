# Anthropic Skills Ecosystem Research

> Onderzocht op 2026-03-16. Bronnen: Anthropic Complete Guide to Building Skills for Claude (PDF), github.com/anthropics/skills, code.claude.com/docs/en/plugins, Claude Code release notes March 2026.
>
> **VERWERKT:** Inzichten verwerkt naar core bestanden op 2026-03-16:
> - LESSONS.md: L-008 t/m L-014 toegevoegd
> - DECISIONS.md: D-008 t/m D-011 toegevoegd
> - SOURCES.md: 10 Anthropic ecosystem bronnen toegevoegd
> - CLAUDE.md: Skill structure + plugin distributie nog te updaten in volgende sessie
> - REQUIREMENTS.md: allowed-tools + assets/ + scripts/ nog te verwerken
> - WAY_OF_WORK.md: Plugin packaging fase nog toe te voegen

---

## 1. Official Skill Structure (from Anthropic Guide)

A skill is a folder containing:
- **SKILL.md** (required): Instructions in Markdown with YAML frontmatter
- **scripts/** (optional): Executable code (Python, Bash, etc.)
- **references/** (optional): Documentation loaded as needed
- **assets/** (optional): Templates, fonts, icons used in output

### YAML Frontmatter Fields

**Required:**
- `name`: kebab-case, no spaces/capitals, must match folder name
- `description`: MUST include WHAT + WHEN (trigger conditions), under 1024 chars, no XML tags

**Optional:**
- `license`: MIT, Apache-2.0, etc.
- `compatibility`: 1-500 chars, environment requirements
- `allowed-tools`: Restrict tool access (e.g., `"Bash(python:*) Bash(npm:*) WebFetch"`)
- `metadata`: Custom key-value pairs (author, version, mcp-server, category, tags)

### Security Restrictions
- No XML angle brackets (< >) in frontmatter
- No "claude" or "anthropic" in skill names (reserved)
- Frontmatter appears in Claude's system prompt — malicious content could inject instructions

---

## 2. Progressive Disclosure (Critical Design Principle)

Three-level system:
1. **Level 1 (YAML frontmatter):** ALWAYS loaded in system prompt. Provides just enough info for Claude to know when to use the skill.
2. **Level 2 (SKILL.md body):** Loaded when Claude thinks the skill is relevant. Contains full instructions.
3. **Level 3 (Linked files):** Additional files Claude can discover on demand (references/, scripts/, assets/).

This minimizes token usage while maintaining specialized expertise.

---

## 3. Description Field Best Practices

Structure: `[What it does] + [When to use it] + [Key capabilities]`

### Good Examples:
```
description: Analyzes Figma design files and generates developer handoff documentation. Use when user uploads .fig files, asks for "design specs", "component documentation", or "design-to-code handoff".
```

### Bad Examples:
```
description: Helps with projects.  # Too vague
description: Creates sophisticated multi-page documentation systems.  # Missing triggers
```

---

## 4. Three Skill Categories (Anthropic's Classification)

### Category 1: Document & Asset Creation
- Creating consistent, high-quality output (documents, presentations, apps, designs, code)
- Key techniques: embedded style guides, template structures, quality checklists
- No external tools required

### Category 2: Workflow Automation
- Multi-step processes with consistent methodology
- Key techniques: step-by-step workflow with validation gates, templates, iterative refinement loops

### Category 3: MCP Enhancement
- Workflow guidance on top of MCP tool access
- Key techniques: coordinates multiple MCP calls, embeds domain expertise, provides context, error handling
- **MCP = Kitchen (tools), Skills = Recipes (how to use tools)**

---

## 5. Five Proven Patterns

### Pattern 1: Sequential Workflow Orchestration
- Multi-step processes in specific order
- Explicit step ordering, dependencies, validation at each stage, rollback instructions

### Pattern 2: Multi-MCP Coordination
- Workflows spanning multiple services
- Clear phase separation, data passing between MCPs, validation before next phase

### Pattern 3: Iterative Refinement
- Output quality improves with iteration
- Explicit quality criteria, validation scripts, know when to stop

### Pattern 4: Context-Aware Tool Selection
- Same outcome, different tools depending on context
- Clear decision criteria, fallback options, transparency about choices

### Pattern 5: Domain-Specific Intelligence
- Specialized knowledge beyond tool access
- Domain expertise embedded in logic, compliance checks, comprehensive documentation

---

## 6. Testing & Quality Metrics

### Three Testing Areas:
1. **Triggering tests:** Skill triggers on obvious tasks, paraphrased requests, NOT on unrelated topics
2. **Functional tests:** Valid outputs, API calls succeed, error handling works, edge cases covered
3. **Performance comparison:** Prove skill improves vs baseline (fewer messages, fewer errors, fewer tokens)

### Quantitative Targets:
- Skill triggers on 90% of relevant queries
- Completes workflow in X tool calls
- 0 failed API calls per workflow

---

## 7. Plugin Architecture (Claude Code)

### Plugin Structure:
```
my-plugin/
├── .claude-plugin/plugin.json    # Manifest (name, description, version, author)
├── commands/                     # Slash commands (Markdown files)
├── agents/                       # Custom agent definitions
├── skills/                       # Agent Skills with SKILL.md files
├── hooks/hooks.json              # Event handlers
├── .mcp.json                     # MCP server configurations
├── .lsp.json                     # LSP server configurations
└── settings.json                 # Default settings (e.g., default agent)
```

### Key Distinction:
- `commands/` = user-invoked slash commands (like `/my-plugin:hello`)
- `skills/` = model-invoked (Claude auto-loads based on task context)

### Plugin vs Standalone:
- Standalone (`.claude/`): personal, project-specific, short skill names
- Plugin: shareable, versioned, namespaced (`/plugin-name:skill`)

---

## 8. Anthropic Skills Repository (github.com/anthropics/skills)

- **94.7k stars**, 10.2k forks, 23 commits, 10 contributors
- Skills categories: Creative & Design, Development & Technical, Enterprise & Communication
- Document Skills (source-available): docx, pdf, pptx, xlsx
- Open standard: agentskills.io
- Install via: `/plugin marketplace add anthropics/skills`

---

## 9. Skills API (Programmatic Use)

- `/v1/skills` endpoint for listing and managing skills
- `container.skills` parameter in Messages API
- Version control via Claude Console
- Works with Claude Agent SDK
- Requires Code Execution Tool beta

---

## 10. Claude Code March 2026 Updates

- **Voice mode** with `/voice` command (push-to-talk, 20 languages incl. Dutch)
- **Opus 4.6** with 1M context on all plans
- **`/loop`** command for recurring tasks
- **Plugin deduplication** for MCP servers
- **claude-api skill** for building with Anthropic SDK
- **Session naming** improvements
- **Multi-language STT** support

---

## 11. Implications for Draw.io Skill Package

### Must align with:
1. Official SKILL.md + references/ + scripts/ + assets/ structure
2. Progressive disclosure (frontmatter triggers, body instructions, references for detail)
3. Description format: `[What] + [When/Triggers] + [Capabilities]`
4. No README.md inside skill folders
5. allowed-tools field to restrict tool access where appropriate
6. Consider publishing as a Claude Code plugin with `.claude-plugin/plugin.json`

### Consider adding to our skill structure:
- `scripts/` directory for validation scripts (e.g., XML validators)
- `assets/` directory for diagram templates
- `allowed-tools` in frontmatter for MCP-dependent skills

### Distribution strategy:
- GitHub repo with clear README (repo-level, not in skill folders)
- Plugin marketplace registration via `/plugin marketplace add`
- Consider submitting to official Anthropic marketplace: claude.ai/settings/plugins/submit
