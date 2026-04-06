---
description: >
  Run a full feature brainstorm session — from ambiguous problem space to design-ready user stories. Chains pm-thinking-coach → idea-validator → feature-story-writer. Use when starting work on a new feature with no clear direction yet. Produces three artifacts: session-brief.md, validation-[direction].md, and stories-[direction].md.
argument-hint: "[feature area or problem space, e.g. 'onboarding for new enterprise users']"
---

# /brainstorm-feature

A full end-to-end brainstorm session for designers working without adequate PM support. Three phases. Three artifacts. One clear direction ready to design.

---

## Phase 1 — PM Session
*Use the `pm-thinking-coach` skill*

Open with:
> "Hey — I'm your PM. Catch me up. What are you working on?"

Run the full pm-thinking-coach session:
- Context intake (user, outcome, workaround, known vs. assumed, constraints)
- Opportunity mapping (3–5 customer opportunities, OST-framed)
- Competitive landscape (ask + search + interpret)
- Market and business angle
- Assumption mapping
- 2–4 directions with a lean

Save output to `session-brief.md`.
Generate persona visualization card.

When complete, transition:
> "We've got a solid brief. You're leaning toward [Direction X]. Ready to pressure-test it?"

If yes → Phase 2.
If the user wants to sit with it → stop here. They can run `/idea-validator` later.

---

## Phase 2 — Idea Validation
*Use the `idea-validator` skill*

Read `session-brief.md`. Do not re-ask anything already answered.

Run all four validation checks:
- User-direction fit
- JTBD integrity
- Assumption stress-test (with ranked assumption table)
- Differentiation

Produce a verdict: ✅ holds / ⚠️ holds with conditions / ❌ fundamental problem.

Save output to `validation-[direction-name].md`.

When complete, transition:
> "[Verdict]. [1-sentence rationale.] Ready to turn this into stories you can design from?"

If ✅ or ⚠️ with conditions met → offer Phase 3.
If ❌ → suggest returning to session brief. Do not proceed to stories.

---

## Phase 3 — Story Writing
*Use the `feature-story-writer` skill*

Read `session-brief.md` and `validation-[direction-name].md`. Do not re-ask anything already answered.

Scope the epic → present story index → write stories in priority order, starting with the one that tests the critical assumption.

Save output to `stories-[direction-name].md`.

Close with:
> "These stories are ready to design from. Start with [story title] — it tests [critical assumption] and will teach you the most. When you're ready to hand off to engineering or a coding agent, say 'generate PRD' to continue."

---

## Phase 4 — PRD Generation (optional)
*Use the `story-to-prd` skill*

Read `stories-[direction-name].md`, `validation-[direction-name].md`, and `session-brief.md`.

Generate the full PRD: summary, background, personas, goals and metrics, value proposition, scoped feature requirements with acceptance criteria, constraints and risks, release approach.

Save output to `prd-[direction-name].md`.

Phase 4 is optional — only run if the user asks for it. Not everyone who writes stories needs a PRD immediately. The handoff prompt in Phase 3 plants the offer; the user decides when.

---

## Artifacts Produced

| File | Contents | Produced in |
|---|---|---|
| `session-brief.md` | Persona, JTBD, opportunity map, competitive landscape, market angle, directions, lean | Phase 1 |
| `validation-[direction].md` | Four-check validation, verdict, critical assumption, cheapest test | Phase 2 |
| `stories-[direction].md` | Full story set with acceptance criteria, assumption mapping, honest takes | Phase 3 |
| `prd-[direction].md` | Full PRD: summary, background, personas, metrics, feature scope, constraints, release approach | Phase 4 (optional) |

---

## Notes

- Each phase can also be run independently as a standalone skill.
- If the user already has a session brief from a previous session, Phase 1 can be skipped — start with `/idea-validator` directly.
- If the user already has a validated direction, skip to `/feature-story-writer` directly.
- If the user already has stories, skip to `/story-to-prd` directly.
- Phase 4 is opt-in. The feature-story-writer plants the offer; the user decides when to generate the PRD.
- The command does not loop indefinitely. If Phase 2 returns ❌, the session ends with a specific redirect, not a re-run.
