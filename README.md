# Draw.io Claude Skill Package

<p align="center">
  <img src="docs/social-preview.png" alt="22 Deterministic Skills for Draw.io" width="100%">
</p>

## Overview

22 deterministic Claude skills + MCP server for programmatic Draw.io diagram generation. Covers the complete mxGraph XML ecosystem: format, styles, geometry, 11 diagram types, error diagnosis, and intelligent orchestration.

## Skills

| Category | Skills | Purpose |
|----------|--------|---------|
| Core | 3 | XML format, style system, geometry |
| Syntax | 4 | Cells, connections, styles, metadata |
| Implementation | 11 | Flowcharts, swimlanes, architecture, ER, BPMN, UML, mind maps, network, templates, CSV import, Mermaid |
| Errors | 2 | XML errors, rendering issues |
| Agents | 2 | Diagram generator, code validator |
| **Total** | **22** | |

## MCP Server

This package includes a pre-configured MCP server (`drawio-mcp`) that gives Claude hands to actually create Draw.io diagrams:

- **310+ shape presets** — architecture, flowchart, BPMN, UML, network, mockup, etc.
- **Auto-layout** — Sugiyama (DAG), tree, grid, flowchart, smart routing
- **Containers & swimlanes** — proper nesting with parent-child relationships
- **Themes** — BLUE, GREEN, DARK, ORANGE, PURPLE + custom styling
- **File management** — create, save, load `.drawio` files directly

## Setup

### 1. Install the MCP server

```bash
pip install drawio-mcp
```

### 2. Install skills + MCP config

```bash
git clone https://github.com/OpenAEC-Foundation/Draw.io-Claude-Skill-Package.git

# Copy skills to your Claude skills directory
cp -r Draw.io-Claude-Skill-Package/skills/source/* ~/.claude/skills/

# Copy MCP config to your project
cp Draw.io-Claude-Skill-Package/.mcp.json your-project/.mcp.json
```

### 3. Start drawing

```bash
cd your-project
claude
```

Ask Claude to create any diagram — it generates `.drawio` files you open in Draw.io.

## How it works

```
┌──────────────────────────────────────────┐
│              Claude Code                  │
│                                           │
│  22 Skills         MCP: drawio-generator  │
│  (domain knowledge)   (the hands)         │
│                                           │
│  Skills teach HOW    MCP tools:           │
│  to structure         ├─ diagram()        │
│  mxGraph XML          ├─ draw()           │
│                       ├─ style()          │
│                       ├─ layout()         │
│                       └─ inspect()        │
└───────────────┬──────────────────────────┘
                ▼
         .drawio files → open in Draw.io
```

## Quick start examples

**Flowchart:**
> Maak een flowchart voor een login proces met validatie en error handling

**Architecture:**
> Maak een architectuurdiagram: API Gateway → Auth, Users, Orders → PostgreSQL

**ER-diagram:**
> Maak een ER-diagram met Users, Orders, Products en crow's foot notatie

**Dark theme dashboard:**
> Maak een donker-thema wireframe van een admin dashboard met sidebar en KPI cards

## Technology

- **Draw.io / diagrams.net** — Open source (Apache 2.0)
- **mxGraph XML format** — Version 4.x compatible
- **[drawio-mcp](https://github.com/yohasacura/drawio-mcp)** — MCP server (Python)
- **Claude Code** — Skill system + MCP integration

## Methodology

Built using the 7-phase research-first methodology. 4 deep research documents (3800+ lines), 8 quality-gated batches.

## License

MIT

## Author

OpenAEC Foundation
