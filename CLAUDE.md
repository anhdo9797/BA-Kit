# CLAUDE.md

## Project Overview

BA-Kit is an **agent squad of 33 specialists** for Requirements Engineering.
Multi-platform: **Antigravity IDE**, **Claude Code**, **Claude CoWork**.

Standards: BABOK v3, IEEE 29148, ISO 25010, INVEST.

## Architecture

```
.agent/skills/ba-*/SKILL.md   — 33 Agent Skill definitions
.agent/skills/_shared/         — Shared utilities & knowledge search skill
.agent/scripts/                — BM25+ Knowledge Search Engine (Python)
.agent/data/*.csv              — 831 indexed knowledge entries (23 domains)
.agent/templates/              — 14 BA document templates (BRD, SRS, FRD, etc.)
.agent/wiki/                   — Living knowledge wiki (2-tier: concepts/decisions)
docs/                          — Documentation and guides
ebooks/                        — Synthesized book knowledge
```

## Key Commands

```bash
# Knowledge search
python3 .agent/scripts/ba_search.py "query" --domain elicitation
python3 .agent/scripts/ba_search.py "query" --multi-domain

# Coverage checker
python3 .agent/scripts/coverage_checker.py outputs/project-name/

# Generate DOCX output
python3 .agent/scripts/gen_docx.py input.md output.docx
```

## Agent Activation

Agents are activated via `@ba-{name}` in Antigravity or as `SKILL.md` files in Claude Code.

**`@ba-master` is the dispatcher** — route all unclear requests through it first.

### Core Routing
- `@ba-master` — start here for any new request
- `@ba-elicitation` — gather requirements from stakeholders
- `@ba-writing` — write US/BRD/SRS/API specs
- `@ba-validation` — INVEST check, quality review
- `@ba-quality-gate` — PASS/CONDITIONAL/REJECT scoring (8 dimensions)
- `@ba-auditor` — full project health dashboard

## Product Delivery Workflow (MANDATORY for any feature/PRD work)

```
Phase 0 Discovery Interview → G0 → Phase 1 PRD Draft → G1 → Phase 2 Wireframe → G2
  → Phase 3 Review → G3 → Phase 4 PRD Final + Design Final → G4 → Phase 5 Development
```

- **Always interview first**: `@ba-master` runs Phase 0 (`@ba-elicitation` PRD Discovery Mode) before any PRD, wireframe or design — no exceptions.
- **Gates need explicit user approval**; never chain into the next phase on your own.
- **PRD format is fixed**: `.agent/templates/prd-template.md` (team screen-spec format). No extra sections.
- Unknowns → `[TBD-xx]` Open Questions, never invented.
- PRD reasoning: read sibling PRDs in `draft/` first and apply Reasoning lenses L1–L13 (template §3).
- Wireframe: Markdown (ASCII) first → approve (G2a) → HTML. **Never write to Figma without explicit confirmation.**
- Artifacts live in `outputs/<project>/<feature>/` (`_status.md`, `00-discovery/`, `01-prd-draft/`, `02-wireframe/`, `03-review/`, `04-final/`); resume from `_status.md`.
- Full protocol: `.agent/skills/ba-master/SKILL.md` → "Product Delivery Workflow".

## Behavioral Principles

Every agent follows **System 2 Reflection**: draft → critique → refine.

- ALWAYS verify math with Python, links with Grep, standards with WebSearch
- NEVER assume user intent — use `@ba-elicitation` to clarify
- NEVER hallucinate file contents — check with Grep/Read tools

## Handoff Protocol

Agents hand off via structured output blocks. See `.agent/skills/_shared/` for
shared handoff templates and cross-agent conventions.
