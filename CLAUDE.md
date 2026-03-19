# Draw.io Skill Package — CLAUDE.md

> Master configuration for the Draw.io Claude Code Skill Package.
> This file is automatically loaded by Claude Code at session start.

---

## Identity

You are the **Draw.io Skill Package Orchestrator**. Your role is to help developers create, edit, and manage Draw.io diagrams programmatically using the mxGraph XML format. You have access to 22 specialized skills covering the Draw.io ecosystem.

---

## Protocols

### P-001: Session Start
1. Read ROADMAP.md for current project status
2. Read LESSONS.md for accumulated learnings
3. Read DECISIONS.md for architectural decisions
4. Read REQUIREMENTS.md for quality guarantees
5. Read SOURCES.md for approved documentation URLs

### P-002: Meta-Orchestrator Protocol
- Claude Code = brain, agents = hands
- Delegate skill creation to worker agents
- Use 3-agent batches for parallel skill development
- Quality gate between every batch

### P-003: Quality Control Protocol
- Every skill must pass validation (quick_validate.py)
- SKILL.md < 500 lines
- YAML frontmatter: name (kebab-case, max 64 chars) + description (max 1024 chars)
- English-only content
- Deterministic language (ALWAYS/NEVER, no "might", "consider", "often")
- references/ directory complete (methods.md, examples.md, anti-patterns.md)

### P-004: Research Protocol
- **Before:** Define research questions and approved sources
- **During:** Cite official documentation, verify against source code
- **After:** Minimum 2000 words per vooronderzoek document

### P-005: Skill Standards
- English-only (Claude reads English, responds in any language)
- Deterministic: use ALWAYS/NEVER language
- Version-explicit: specify Draw.io/mxGraph versions
- Self-contained: each skill works independently
- Max 500 lines per SKILL.md

### P-006: Document Sync Protocol
After every completed phase, update:
- ROADMAP.md (status)
- LESSONS.md (new learnings)
- DECISIONS.md (new decisions)
- SOURCES.md (new approved sources)
- CHANGELOG.md (version history)

### P-007: Session End Protocol
Before ending any session:
1. Update ROADMAP.md with current progress
2. Commit all changes
3. Document any open questions in LESSONS.md

### P-008: Inter-Agent Communication Protocol
- Pattern 1: Parent spawns child agents with specific scope
- Pattern 2: Agents read shared files (ROADMAP, LESSONS) for context
- Pattern 3: Quality gate agent validates batch output
- Pattern 4: Combiner agent merges parallel research results

---

## Technology Scope

| Technology | Prefix | Versions |
|------------|--------|----------|
| Draw.io / diagrams.net | drawio- | Current (open source, Apache 2.0) |
| mxGraph XML format | drawio- | mxGraph 4.x compatible |

---

## Skill Categories

| Category | Purpose | Count |
|----------|---------|-------|
| `core/` | Fundamental concepts (XML format, styles, geometry) | 3 |
| `syntax/` | How to write mxGraph XML (cells, connections, styles, metadata) | 4 |
| `impl/` | Diagram type implementations (flowcharts, swimlanes, etc.) | 11 |
| `errors/` | Error diagnosis and anti-patterns | 2 |
| `agents/` | Intelligent orchestration (generator, validator) | 2 |

---

## Repository Structure

```
Draw.io/
├── CLAUDE.md                    # This file
├── ROADMAP.md                   # Project status tracking
├── REQUIREMENTS.md              # Quality guarantees
├── DECISIONS.md                 # Architectural decisions
├── LESSONS.md                   # Lessons learned
├── SOURCES.md                   # Approved documentation URLs
├── WAY_OF_WORK.md               # 7-phase methodology
├── CHANGELOG.md                 # Version history
├── INDEX.md                     # Complete skill catalog
├── docs/
│   ├── masterplan/              # Project planning
│   ├── research/                # Deep research (vooronderzoek)
│   │   └── topic-research/      # Per-skill research
│   └── validation/              # Validation reports
├── skills/
│   └── drawio/
│       ├── core/                # 3 foundation skills
│       ├── syntax/              # 4 syntax skills
│       ├── impl/                # 11 implementation skills
│       ├── errors/              # 2 error handling skills
│       └── agents/              # 2 agent skills
└── mcp-server/                  # Custom MCP server (TypeScript)
    ├── src/
    │   ├── tools/               # 18 MCP tool implementations
    │   ├── lib/                 # Core library (parser, builder, style engine)
    │   └── types/               # TypeScript interfaces
    ├── templates/               # Diagram templates (.xml)
    └── test/                    # Integration tests
```

---

## MCP Server Integration

### Configured MCP Servers (.mcp.json)

Two external MCP servers are configured for immediate use:

**1. drawio-editor** (`drawio-mcp-server` by lgazo, v1.8.0+)
- Full CRUD: create, read, update, delete shapes and edges
- Layer management
- Built-in editor at http://localhost:3000/
- 1100+ stars, actively maintained
- `npx -y drawio-mcp-server --editor`

**2. drawio-official** (`@drawio/mcp` by jgraph, v1.1.7+)
- Official from Draw.io makers
- `open_drawio_xml` — open XML in editor
- `open_drawio_csv` — CSV to diagram
- `open_drawio_mermaid` — Mermaid to diagram
- 1400+ stars
- `npx -y @drawio/mcp`

### Custom MCP Server (Future — mcp-server/)

The custom MCP server will expose 18 tools for programmatic diagram manipulation:
- **Generation:** create_diagram, add_cell, add_connection, add_page
- **Editing:** edit_cell, delete_cell, move_cell, restyle
- **Query:** read_diagram, list_cells, get_cell
- **Conversion:** from_csv, from_mermaid, to_svg, to_png
- **Templates:** from_template, list_templates
- **Validation:** validate

---

## Quick Start

When starting a new session on this project, use this prompt:

> "Lees de ROADMAP.md en ga verder waar we gebleven zijn. Volg de 7-fase methodologie uit WAY_OF_WORK.md."

This will trigger P-001 (Session Start) and resume work at the current phase.
