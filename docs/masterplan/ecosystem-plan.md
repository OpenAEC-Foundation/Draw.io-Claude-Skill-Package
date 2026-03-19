# Plan: Draw.io Skill Package Ecosystem

## Context

We hebben eerder twee succesvolle skill packages gebouwd (Blender 73 skills, ERPNext 28 skills) en een Open-Agents orchestratie framework (28 skills, 1629 agent templates). De user wil nu:
1. Een **Draw.io Skill Package** met dezelfde research-first 7-fase aanpak
2. Een **Skill-Package-Workflow-Template** repo om het proces te standaardiseren
3. Een **custom Draw.io MCP Server** geoptimaliseerd voor het skill package
4. **Skip permissions** + basis mappenstructuur in de lokale workspace

---

## Executievolgorde

**Project A (eerst): Skill-Package-Workflow-Template** → versnelt Project B
**Project B (daarna): Draw.io Skill Package** → gebruikt de template
**Project C (parallel met B, vanaf fase 5): Custom Draw.io MCP Server** → afhankelijk van B's research

---

## Project A: Skill-Package-Workflow-Template

**Locatie:** `C:\Users\Freek Heijting\Documents\GitHub\Skill-Package-Workflow-Template`

### Bronbestanden om te extraheren:
- `Blender-...\CLAUDE.md` — 8 protocollen (P-001 t/m P-008), meest mature
- `Blender-...\WAY_OF_WORK.md` — orchestratie model, 7-fase methodologie
- `ERPNext-...\WAY_OF_WORK.md` — session recovery, project status tracking
- `ERPNext-...\tools\quick_validate.py` — validatie script (118 regels)
- `ERPNext-...\tools\package_skill.py` — packaging script (71 regels)
- `Blender-...\REQUIREMENTS.md` — quality guarantees template
- `Blender-...\docs\masterplan\masterplan.md` — definitief masterplan formaat

### Structuur:
```
Skill-Package-Workflow-Template/
├── README.md
├── LICENSE
├── CLAUDE.md.template
├── WAY_OF_WORK.md.template
├── REQUIREMENTS.md.template
├── ROADMAP.md.template
├── DECISIONS.md.template
├── LESSONS.md.template
├── SOURCES.md.template
├── CHANGELOG.md.template
├── INDEX.md.template
├── CONTRIBUTING.md.template
├── SECURITY.md.template
├── docs/
│   ├── masterplan/
│   │   ├── raw-masterplan.md.template
│   │   └── masterplan.md.template
│   └── research/
│       ├── vooronderzoek.md.template
│       └── topic-research.md.template
├── skills/
│   └── {tech}/{category}/{skill-name}/
│       ├── SKILL.md.template
│       └── references/
│           ├── methods.md.template
│           ├── examples.md.template
│           └── anti-patterns.md.template
├── tools/
│   ├── quick_validate.py
│   ├── package_skill.py
│   ├── scaffold_project.py
│   └── batch_validate.py
├── .claude/
│   └── settings.local.json.template
└── examples/
    ├── erpnext-skill-example/
    └── blender-skill-example/
```

### Fasen: 2 sessies
- **A1:** Extract en generaliseer uit bestaande packages
- **A2:** Valideer, test scaffold script, publish v1.0.0

---

## Project B: Draw.io Skill Package

**Locatie:** `C:\Users\Freek Heijting\Documents\Git\Draw.io`

### Geschatte skill inventaris: 22 skills

| Categorie | Skills | Aantal |
|-----------|--------|--------|
| **core/** | xml-format, styles, geometry | 3 |
| **syntax/** | cells, connections, styles, metadata | 4 |
| **impl/** | flowcharts, swimlanes, architecture, er-diagrams, bpmn, uml, mindmaps, network, templates, csv-import, mermaid-conversion | 11 |
| **errors/** | xml, rendering | 2 |
| **agents/** | diagram-generator, code-validator | 2 |

### Fasen (7-fase methodologie):

**B0: Bootstrap** — DONE
**B1: Raw Masterplan** — scope, skill inventaris → `docs/masterplan/raw-masterplan.md`
**B2: Deep Research** — 4 vooronderzoek documenten (XML, styles, diagrams, integration)
**B3: Masterplan Refinement** — definitief `docs/masterplan/masterplan.md`
**B4: Topic-Specific Research** — per-skill research
**B5: Skill Creation** — 6 batches, 3-5 agents per batch
**B6: Validatie** — batch_validate.py
**B7: Publicatie** — INDEX.md, README.md, v1.0.0

---

## Project C: Custom Draw.io MCP Server

**Locatie:** `C:\Users\Freek Heijting\Documents\Git\Draw.io\mcp-server\`

### 18 MCP Tools:
- Generatie (4): create_diagram, add_cell, add_connection, add_page
- Bewerking (4): edit_cell, delete_cell, move_cell, restyle
- Query (3): read_diagram, list_cells, get_cell
- Conversie (4): from_csv, from_mermaid, to_svg, to_png
- Templates (2): from_template, list_templates
- Validatie (1): validate

### Architectuur: TypeScript + @modelcontextprotocol/sdk

### Fasen (parallel met B5+):
- C1: Core library (parser, builder, style engine) — na B2
- C2: Generatie + query tools
- C3: Bewerking + conversie tools
- C4: Templates + integratie
- C5: Documentatie
