# Draw.io Claude Skill Package

<p align="center">
  <img src="docs/social-preview.png" alt="22 Deterministic Skills for Draw.io" width="100%">
</p>

## Overview

22 deterministic Claude skills for programmatic Draw.io diagram generation. Covers the complete mxGraph XML ecosystem: format, styles, geometry, 11 diagram types, error diagnosis, and intelligent orchestration.

## Skills

| Category | Skills | Purpose |
|----------|--------|---------|
| Core | 3 | XML format, style system, geometry |
| Syntax | 4 | Cells, connections, styles, metadata |
| Implementation | 11 | Flowcharts, swimlanes, architecture, ER, BPMN, UML, mind maps, network, templates, CSV import, Mermaid |
| Errors | 2 | XML errors, rendering issues |
| Agents | 2 | Diagram generator, code validator |
| **Total** | **22** | |

## End-to-End Setup: Van 0 naar "Claude tekent in Draw.io"

### Vereisten

- [Node.js](https://nodejs.org/) v18+
- [Claude Code](https://code.claude.com/) CLI
- Draw.io Desktop **of** een browser

### Stap 1: Clone en installeer skills

```bash
# Clone het skill package
git clone https://github.com/OpenAEC-Foundation/Draw.io-Claude-Skill-Package.git

# Optie A: Kopieer skills naar je globale Claude skills directory
cp -r Draw.io-Claude-Skill-Package/skills/source/* ~/.claude/skills/

# Optie B: Gebruik als project-level skills
cp -r Draw.io-Claude-Skill-Package/skills/source/* .claude/skills/

# Optie C: Refereer via --add-dir in een workspace
# claude --add-dir /pad/naar/Draw.io-Claude-Skill-Package
```

### Stap 2: Configureer MCP servers

Kopieer `.mcp.json` naar je project root, of merge met je bestaande config:

```bash
cp Draw.io-Claude-Skill-Package/.mcp.json .mcp.json
```

Dit configureert **3 complementaire MCP servers**:

| Server | Package | Wat het doet |
|--------|---------|-------------|
| `drawio-editor` | `drawio-mcp-server` (lgazo) | Live CRUD: shapes toevoegen/bewerken/verwijderen, layers beheren, WebSocket editor op `localhost:3000` |
| `drawio-converter` | `@drawio/mcp` (jgraph, officieel) | Opent XML/CSV/Mermaid direct in Draw.io browser of desktop app |
| `drawio-generator` | `drawio-mcp` | Geavanceerd genereren: 310+ shape presets, auto-layout, smart routing, themes, .drawio bestanden opslaan |

> **Welke server wanneer?**
> - Wil je een **bestand genereren en opslaan**? → `drawio-generator`
> - Wil je **live editen** in een browser? → `drawio-editor`
> - Wil je **Mermaid/CSV converteren** en openen in Draw.io? → `drawio-converter`

### Stap 3: Installeer MCP server dependencies

```bash
# Node.js MCP servers (auto-download via npx bij eerste gebruik)
# Optioneel pre-installeren voor snellere startup:
npm install -g drawio-mcp-server @drawio/mcp

# Python MCP server (drawio-generator) — de krachtigste van de drie:
pip install drawio-mcp
# Bron: https://github.com/yohasacura/drawio-mcp
```

### Stap 4: Verifieer dat alles werkt

Start Claude Code in je project directory:

```bash
claude
```

Typ in Claude:

```
Maak een simpele flowchart met 3 stappen en sla het op als test.drawio
```

Als je een `.drawio` bestand krijgt dat opent in Draw.io → alles werkt.

### Stap 5 (optioneel): Workspace opzetten

Voor een dedicated Draw.io workspace met alle functies:

```bash
mkdir draw-workspace && cd draw-workspace
cp /pad/naar/Draw.io-Claude-Skill-Package/.mcp.json .
cp /pad/naar/Draw.io-Claude-Skill-Package/CLAUDE.md .

# Start Claude met het skill package als extra directory
claude --add-dir /pad/naar/Draw.io-Claude-Skill-Package
```

## MCP Server Architectuur

```
┌─────────────────────────────────────────────────────┐
│                    Claude Code                       │
│                                                      │
│  ┌──────────────┐  ┌──────────────┐  ┌────────────┐ │
│  │ 22 Skills    │  │ CLAUDE.md    │  │ /commands  │ │
│  │ (on-demand)  │  │ (altijd)     │  │ (user)     │ │
│  └──────┬───────┘  └──────────────┘  └────────────┘ │
│         │                                            │
│  ┌──────▼────────────────────────────────────────┐  │
│  │              MCP Tool Layer                    │  │
│  │                                                │  │
│  │  drawio-generator    drawio-editor    drawio-  │  │
│  │  ├─ create           ├─ add_cell     converter │  │
│  │  ├─ build_dag        ├─ add_conn     ├─ xml    │  │
│  │  ├─ build_full       ├─ edit_cell    ├─ csv    │  │
│  │  ├─ add_vertices     ├─ delete       ├─ mermaid│  │
│  │  ├─ layout/polish    ├─ layers       └─────────│  │
│  │  ├─ style/theme      └──────────────           │  │
│  │  └─ save/load                                  │  │
│  └───────────────────────────────────────────────┘  │
│         │                    │                │      │
└─────────┼────────────────────┼────────────────┼──────┘
          ▼                    ▼                ▼
   .drawio bestanden    localhost:3000    Draw.io app
   (op schijf)         (live editor)    (desktop/browser)
```

## Hoe de Skills werken met MCP

De skills leren Claude **hoe** diagrammen te maken (mxGraph XML kennis), de MCP servers geven Claude **de handen** om het daadwerkelijk te doen:

1. **Gebruiker:** "Maak een ER-diagram van mijn database"
2. **Claude laadt:** `drawio-agents-diagram-generator` skill (orkestratie)
3. **Skill kiest:** `drawio-impl-er-diagrams` (technische details)
4. **Claude gebruikt:** `drawio-generator` MCP om het diagram te bouwen
5. **Resultaat:** `.drawio` bestand op schijf, klaar om te openen

## Quick Start Voorbeelden

### Flowchart
```
Maak een flowchart voor een login proces:
1. Gebruiker voert credentials in
2. Valideer input
3. Check database
4. Als geldig → dashboard, anders → foutmelding
```

### Architectuurdiagram
```
Maak een architectuurdiagram van een microservices systeem:
- API Gateway → Auth Service, User Service, Order Service
- User Service → PostgreSQL
- Order Service → MongoDB, Redis cache
```

### ER-Diagram
```
Maak een ER-diagram:
- Users (id, name, email)
- Orders (id, user_id, total, status)
- Products (id, name, price)
- OrderItems (order_id, product_id, quantity)
Met crow's foot notatie.
```

### Mermaid conversie
```
Converteer dit Mermaid diagram naar Draw.io:
graph TD
    A[Start] --> B{Is valid?}
    B -->|Yes| C[Process]
    B -->|No| D[Error]
    C --> E[End]
```

## Technology

- **Draw.io / diagrams.net** — Open source (Apache 2.0)
- **mxGraph XML format** — Version 4.x compatible
- **Claude Code** — Designed for Claude Code skill system
- **MCP (Model Context Protocol)** — 3 complementary servers

## Methodology

Built using the proven 7-phase research-first methodology. 4 deep research documents (3800+ lines), refined masterplan with agent prompts, 8 quality-gated batches.

## License

MIT

## Author

OpenAEC Foundation
