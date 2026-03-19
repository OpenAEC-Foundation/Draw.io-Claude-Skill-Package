# Draw.io Skill Package — OPEN QUESTIONS

## Actieve Vragen

_Geen actieve vragen op dit moment._

---

## Beantwoorde Vragen

### Q-001: Plugin vs Standalone Distribution
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Zoals we deden voor de andere repos (Blender, ERPNext). Dat is ons voorbeeld.
**Actie:** Distributie-aanpak overnemen van bestaande skill packages.

### Q-002: Skill-Creator Skill Gebruiken?
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** skill-creator first. Anthropic's skill-creator als primair hulpmiddel, eigen methodologie als kwaliteitslaag eromheen.
**Actie:** skill-creator integreren in fase B5 (skill creation). Eigen 7-fase methodologie blijft de backbone.

### Q-003: agentskills.io Open Standard Compliance
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Nee, Claude-first. Focussen op het Claude ecosystem. Open standard is nice-to-have maar geen doel.
**Actie:** Geen extra werk voor agentskills.io compliance. Claude-specifieke features (allowed-tools, etc.) vrij gebruiken.

### Q-004: Scope van scripts/ Directory
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Zo compleet mogelijk. Gebruiker ontzorgen, zoveel mogelijk functionaliteit end-to-end.
**Actie:** Per skill: validators + generators + helpers. Scripts maken skills deterministic en betrouwbaar. E2E functionaliteit is het doel.

### Q-005: Bestaande Draw.io Skills Analyseren
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Ja, grondig analyseren. Alle bestaande Draw.io skills downloaden, testen, sterke/zwakke punten documenteren.
**Actie:** Opnemen als onderdeel van fase B2 (deep research). Aparte research doc: `community-skills-analysis.md`.

### Q-006: MCP Server — Build vs Fork
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Hybride. Bestaande MCP's bestuderen voor patronen, maar from scratch bouwen.
**Actie:** In fase C1: bestaande MCP servers analyseren (jgraph, Sujimoshi, lgazo). Eigen server bouwen met geleerde patronen.

### Q-007: Workflow Template — Wanneer Starten?
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Draw.io direct. Draw.io is al gebootstrapt. Template achteraf extraheren uit dit project.
**Actie:** Project A (Workflow Template) wordt LATER gedaan, na of parallel aan Draw.io. Draw.io = het levende voorbeeld waaruit we de template extraheren.

### Q-008: CLAUDE.md + REQUIREMENTS.md Updaten
**Status:** BEANTWOORD (2026-03-16)
**Antwoord:** Ja, nu updaten. Bootstrap fase (B0) is pas af als alle core files volledig up-to-date zijn.
**Actie:** CLAUDE.md en REQUIREMENTS.md nu updaten met: allowed-tools, scripts/, assets/, plugin packaging, skill-creator integratie.
