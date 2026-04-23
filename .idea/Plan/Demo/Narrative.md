# Demo Narrative

## 🎬 Title: "Govern Your Data with a Conversation"

## Target Length: 2–3 minutes

---

## Opening Hook (10 seconds)

> "OpenMetadata's mission is to take the chaos out of the data practitioner's life. Today, most of that chaos is the _governance loop_ — scan, classify, confirm, apply, notify. We turned that loop into one chat sentence: 50 tables tagged, with a confirmation gate, in under a minute, for under five cents."

Mission line is verbatim from [Project/VisionAlignment.md](../Project/VisionAlignment.md). Measurable claims are from [Project/PRD.md §Criterion 1 Potential Impact](../Project/PRD.md) and verified in the demo by a stopwatch + the `/metrics` endpoint.

## Demo Flow (90 seconds)

### Scene 1: Natural Language Search (20s)

- Show chat UI
- Type: "Show me all Tier 1 tables with PII data"
- Agent responds with structured table (10+ results)
- Point: "No OpenSearch DSL needed — just ask."

### Scene 2: Auto-Classification with prompt-injection defense (30s)

- Type: "Auto-classify PII in the customer_db"
- Agent scans 50 tables (timer visible), surfaces 12 PII candidates with confidence scores
- One row in the suggestions list shows `[SUSPICIOUS]` flag — a column whose description contained an injection attempt (per the planted seed data in [Demo/FailureRecovery.md §The Frozen Seed Dataset](./FailureRecovery.md))
- **HITL confirmation modal pops up** — shows `proposal_id`, risk badge (`HIGH RISK` for `patch_entity`), FQN list of affected columns, and ✓ Confirm / ✗ Cancel buttons
- User clicks ✓ Confirm → modal calls `POST /chat/confirm` → tags applied via `patch_entity`
- Point: "Five-layer defense: input neutralization, schema validation, tool allowlist, HITL gate, error envelope. We tested the same prompt-injection class that gitar-bot flagged on PR #27506."

### Scene 3: Lineage Impact Analysis (20s)

- Type: "What breaks if I drop the customers table?"
- Agent shows downstream impact: dashboards, pipelines, tables
- Highlights Tier 1 critical assets
- Point: "Before you make changes, know the blast radius."

### Scene 4: Multi-MCP (Optional, 20s)

- Type: "Create a GitHub issue for each untagged PII table"
- Agent calls OM MCP + GitHub MCP
- Shows created issues
- Point: "Cross-platform governance in one conversation."

## Value Slide (30 seconds)

> "Governance Copilot uses OpenMetadata's official AI SDK and MCP tools — no forks, no hacks.
> It addresses issues #26645 (Multi-MCP Orchestrator) and #26608 (Data Catalog Chat).
> Built in 7 days by a team of 4."

## Architecture Slide (15 seconds)

Show the Mermaid diagram from `Architecture/Overview.md`.

## Closing (15 seconds)

> "Try it yourself: clone, configure, chat. Governance made conversational."

---

## Recording Tips

- Resolution: 1920×1080
- Use OM dark mode colors (verified `#7147E8` from [openmetadata-ui/.../variables.less](../../../openmetadata-ui/src/main/resources/ui/src/styles/variables.less))
- No cursor jitter — smooth, rehearsed movements
- Add captions for key moments
- Keep terminal visible for setup (clone → run in <1 min)

## What if the demo breaks during recording

See [Demo/FailureRecovery.md](./FailureRecovery.md). Pre-recorded backup at `demo/backup_recording.mp4`; tab-switch in <10 seconds; never apologize repeatedly. The 3-rehearsal protocol (Apr 24-25) catches these issues before the final recording.

## Optional: 5th demo moment for the panel

If time permits and the panel asks "show me the engineering quality": tab-switch to a side terminal and curl `GET /api/v1/metrics` — show the 4 Golden Signals live, point out the same `request_id` appearing in `logs/agent.log` and the metrics labels. This is Persona 2 (Sriharsha) from [Project/JudgePersona.md](../Project/JudgePersona.md).
