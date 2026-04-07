# Designer Brainstorm kit -- The ultimate PM simulator for designers

Four skills for designers who need to think like a PM — without waiting for one.

<img width="600" height="712" alt="Screenshot 2026-04-06 at 10 15 24 PM" src="https://github.com/user-attachments/assets/e2ee2eea-0e41-4b93-8a7e-ebe15c8e65e3" />


**Works with any AI.** Use as [Claude Code skills](#installation) for the full experience (persistent context, chained workflow, saved artifacts), or copy the [standalone prompt](./PROMPT.md) into any AI chat for instant PM-mode thinking.

---

## The Problem This Solves

You're a designer working on an ambiguous new feature. Your PM is helpful sometimes, absent others. You have ideas but no structured way to pressure-test them, no one asking the market questions, and no clean artifact to hand to engineering when you're done.

This suite gives you that structure — four skills that chain together from "I have a vague idea" to "here's a PRD ready to build from."

---

## The Four Skills

**The PM Thinking Coach** is your thought partner before any ideas are formed. It asks the questions a good PM would ask — who's the user really, what outcome are we improving, what do competitors do, why does the business care about this now. It runs a live competitive search, maps opportunities before solutions, and produces a session brief with a direction you can take into the next skill.

**The Idea Validator** pressure-tests a direction before you commit to designing it. Not a design critique — it operates upstream of any UI. It checks whether the user fits, whether the JTBD holds, whether the key assumptions are sound, and whether there's real differentiation. Two critic personas — Design + Engineering and Leadership — each give their read. A clear verdict comes out: hold, hold with conditions, or go back.

**The Feature Story Writer** turns a validated direction into stories a designer can actually design from. Plain language, named personas, observable acceptance criteria, and an honest take on each story's risk. Stories are prioritized by which one tests the most critical assumption first.

**The Story to PRD** converts the story set into a shareable Product Requirements Document — background, personas, goals and metrics, scoped feature requirements with acceptance criteria, constraints, risks, and release approach. Human-readable, but structured enough for a coding agent to act on directly.

---

## How It Works

```
PM Thinking Coach → Idea Validator → Feature Story Writer → Story to PRD
  session-brief.md   validation-*.md    stories-*.md         prd-*.md
```

Each skill reads what the previous one produced. You never answer the same question twice.

1. **Brainstorm** — PM Thinking Coach runs a 5-10 exchange session. Competitive search included. Saves `session-brief.md`.
2. **Validate** — Idea Validator reads the brief, runs four checks and two persona critiques, gives a verdict. Saves `validation-*.md`.
3. **Write stories** — Feature Story Writer reads both files, scopes the epic, writes stories starting with the one that tests the critical assumption. Saves `stories-*.md`.
4. **Generate PRD** — Story to PRD reads all three files, produces a full PRD ready to hand to engineering or drop into Claude Code. Saves `prd-*.md`.

Each skill also works standalone — you can enter the chain at any point.

---

## Installation

```bash
git clone https://github.com/sijingsun/designer-brainstorm-kit.git ~/.claude/skills/designer-brainstorm-kit
```

Then use in Claude Code — skills trigger automatically when you describe what you're doing, or invoke directly:

```bash
# Run the full chain
/brainstorm-feature onboarding for senior AI companion app

# Or invoke individual skills
/pm-thinking-coach
/idea-validator
/feature-story-writer
/story-to-prd
```

---

## Usage

```bash
# Start from scratch — full session
/brainstorm-feature [feature area or problem space]

# Already have a direction? Skip to validation
/idea-validator validate my onboarding concept for senior users

# Already validated? Go straight to stories
/feature-story-writer

# Already have stories? Generate the PRD
/story-to-prd
```

---

## Personalization

On first run, the PM Thinking Coach asks about your product context and target user group. Say "save this for next time" and it writes a `user-context.md` file that persists across sessions — so you don't repeat yourself every time you start a new feature.

You can customize:
- Product name, type, and constraints
- Target user group description
- Team context (solo designer, embedded with PM, no PM)
- Persona emphasis in the Idea Validator (weight executor view vs. leadership view)

---

## File Structure

| File | Purpose |
|---|---|
| `pm-thinking-coach/SKILL.md` | PM Thinking Coach — context intake, opportunity mapping, competitive search, session brief |
| `idea-validator/SKILL.md` | Idea Validator — four checks, persona critiques, verdict |
| `idea-validator/personas.md` | Design+Engineering and Leadership persona definitions |
| `feature-story-writer/SKILL.md` | Feature Story Writer — story format, plain language rules, priority ordering |
| `story-to-prd/SKILL.md` | Story to PRD — eight-section PRD generator |
| `commands/brainstorm-feature.md` | The chained workflow command — Phase 1→2→3→4 |
| `input-guides/how-to-use-standalone.md` | Guide for using each skill independently |
| `input-guides/how-to-use-chained.md` | Guide for running the full chain |
| `PROMPT.md` | Standalone prompt — paste into any AI chat |
| `user-context.md` | Your saved preferences (gitignored, created on demand) |

---

## What Gets Saved

Every session produces up to four artifacts in your working directory:

| Artifact | Contains |
|---|---|
| `session-brief.md` | Persona, JTBD, opportunity map, competitive landscape, market angle, directions, PM lean |
| `validation-[direction].md` | Four-check validation, persona critiques, verdict, critical assumption |
| `stories-[direction].md` | Full story set with acceptance criteria and honest takes |
| `prd-[direction].md` | Complete PRD ready for engineering handoff |

---

## Credits

Created by [@sijingsun](https://github.com/sijingsun) with Claude Code.

Informed by:
- Teresa Torres' *Continuous Discovery Habits* — Opportunity Solution Tree, JTBD-first
- Paweł Huryn's [PM Skills Marketplace](https://github.com/phuryn/pm-skills) — assumption mapping, prioritization, PRD structure
- product-on-purpose/pm-skills — Triple Diamond, hypothesis-driven development
- deanpeters/Product-Manager-Skills — feature investment framing, epic breakdown

## License

MIT
