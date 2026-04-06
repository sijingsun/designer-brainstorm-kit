---
name: story-to-prd
description: >
  Activate this skill when a designer or PM has a validated set of user stories and wants to convert them into a human-readable Product Requirements Document. Trigger on phrases like "turn this into a PRD", "generate a PRD from these stories", "I want to hand this to an engineer or stakeholder", "make this shareable", or "write up the requirements". Always checks for stories-*.md, validation-*.md, and session-brief.md first — does not re-ask what's already been established. Produces a clean, structured PRD a coding agent can also consume directly.
---

# Story to PRD

Convert user stories into a Product Requirements Document that a human engineer, stakeholder, or coding agent can pick up and act on without a walkthrough.

**Your job here:** Synthesize everything built across the brainstorm suite — the persona, the JTBD, the validated direction, the stories — into a single coherent document. No new research. No new decisions. Just a clean, well-structured PRD that captures what was agreed and makes it buildable.

**What makes a PRD useful vs. decorative:** Specificity. Vague requirements produce vague software. Every section should answer a question a builder would actually ask — not describe intent in the abstract.

Informed by:
- phuryn/pm-skills `create-prd` — 8-section PRD template: summary, background, objectives, segments, value propositions, solution, release planning
- product-on-purpose/pm-skills `prd` + `acceptance-criteria` + `edge-cases` — structured problem → solution → metrics, Given/When/Then criteria, error and recovery paths
- deanpeters/Product-Manager-Skills `prd-development` — problem → personas → solution → metrics → stories sequence

---

## On Activation

**First:** Check for the following files and read all that exist:
- `stories-*.md` — primary input, the stories to formalize
- `validation-*.md` — for critical assumptions, verdict, conditions
- `session-brief.md` — for persona, JTBD, competitive context, market angle

**If all three exist:**
> "I've got your stories, validation, and session brief. Generating the PRD for [Direction name] now — no questions needed."
Proceed directly to PRD generation.

**If only stories-*.md exists:**
> "I've got your stories. Missing the session brief and validation — I'll generate the PRD from the stories alone, but some sections (background, market context, assumptions) will be thinner. Want to add context, or should I proceed with what's here?"

**If nothing exists:**
> "What stories should I turn into a PRD? You can paste them here or point me to the file."
Accept pasted stories or a description. Generate a minimal PRD from what's provided.

---

## PRD Structure

Generate all eight sections. Adjust depth to available context — don't pad thin sections, flag what's missing instead.

---

### Section 1 — Summary

One paragraph. Written for someone who has 60 seconds. Covers:
- What is being built (one sentence)
- Who it's for (the primary persona)
- Why now (the market or business reason)
- What success looks like (one measurable outcome)

Do not use bullet points here. Write it as prose. If a stakeholder reads only this section, they should understand the bet being made.

---

### Section 2 — Background & Problem

**The problem:** What situation is this solving? Describe it from the user's perspective, not the product's. Use the JTBD from the session brief if available.

**Current workaround:** What does the user do today instead? Why is that insufficient?

**Why this matters now:** What's changed — in the market, in the user's behavior, in the competitive landscape — that makes this the right moment? Use competitive context from the session brief if available.

**What we're NOT solving:** Explicit scope boundary. Name 1-2 adjacent problems this PRD deliberately excludes. Prevents scope creep during build.

---

### Section 3 — Personas & User Segments

**Primary persona:** Name, one-line description, situation, JTBD statement.
```
Name: [Name]
Who: [One-line description]
Situation: [When this problem occurs in their life]
JTBD: When [situation], [Name] wants to [motivation], so [outcome].
Current workaround: [What they do today instead]
```

**Secondary persona (if applicable):** Same format. Include if the product has a distinct buyer vs. user (e.g., family member who sets up the product vs. senior who uses it daily).

**Who this is NOT for:** One sentence. Prevents the product from trying to serve everyone.

---

### Section 4 — Goals & Success Metrics

**Product goal:** The outcome this PRD is trying to move. One sentence, outcome-framed, not feature-framed.

**Success metrics:**

| Metric | What it measures | Target | Timeframe |
|---|---|---|---|
| [Primary metric] | [What user behavior this reflects] | [Specific number] | [30/60/90 days] |
| [Secondary metric] | [What this reflects] | [Target] | [Timeframe] |
| [Health metric] | [What this reflects] | [Target] | [Timeframe] |

**Anti-metrics:** What we explicitly do NOT want to optimize for, even if the number could go up. (Example: notification open rate — optimizing this could drive irritating behavior that destroys trust.)

**Critical assumption being tested:** Carry forward from validation file. This is the one thing that, if wrong, means we built the wrong thing.

---

### Section 5 — Value Proposition

**For the primary user:**
> "[Persona name] can finally [job to be done] without [current friction], because [what this product does differently]."

**For the buyer (if different from user):**
> "[Buyer persona] can [their job to be done] without [their current friction], because [what this product does for them]."

**Competitive differentiation:** 2-3 sentences. What does this do that the closest competitors don't? Use competitive landscape from session brief. Be specific — "better UX" is not differentiation.

---

### Section 6 — Solution & Feature Scope

This section translates stories into buildable scope. For each story in the stories file:

```
## [Story Title]
**Persona:** [Who this is for]
**Job:** [What they're trying to accomplish]
**Description:** [2-3 sentences: what the feature does, from the user's perspective. Plain language.]

**In scope:**
- [Specific thing that will be built]
- [Specific thing that will be built]

**Out of scope (this version):**
- [Adjacent thing deliberately excluded]

**Acceptance criteria:**
- Given [situation], when [action], then [observable outcome]
- Given [situation], when [action], then [observable outcome]
- [Edge case: what happens when X goes wrong]
- [Empty state: what the user sees before there's any data]

**Open questions:**
- [Unresolved decision that needs an answer before or during build]
```

Repeat for each story. Flag stories marked "title only" in the stories file as out of scope for this version, listed at the end of the section.

---

### Section 7 — Constraints & Risks

**Technical constraints:** What platforms, APIs, or existing systems does this depend on? What can't change?

**Design constraints:** What UX patterns or accessibility requirements are non-negotiable?

**Data & privacy:** What personal data does this feature collect, store, or process? Any regulatory considerations (GDPR, CCPA, local laws)?

**Key risks:**

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| [Critical assumption is wrong] | High | High | [Cheapest test before committing] |
| [Technical dependency fails] | [L/M/H] | [L/M/H] | [Fallback] |
| [User adoption risk] | [L/M/H] | [L/M/H] | [Mitigation] |

Carry the critical assumption and cheapest test from the validation file directly into the risks table.

---

### Section 8 — Release Approach

**Recommended sequence:** Which story ships first, and why? Use the story index priority from the stories file if available. Lead with the story that tests the critical assumption.

**MVP definition:** The minimum set of stories that delivers enough value to be worth releasing and enough signal to validate the core assumption. Name the stories explicitly.

**Phase 2 (if applicable):** What's deliberately deferred to a second release? Why?

**Launch considerations:**
- Who needs to know before this ships? (stakeholders, support, legal)
- Is there a soft launch / beta approach that reduces risk?
- What does the team monitor in the first 2 weeks post-launch?

---

## Output

Save the completed PRD to `prd-[direction-name].md`.

After saving, close with:

> "PRD saved. The story to start with is [story title] — it's the MVP core and tests [critical assumption] directly. Everything else in Phase 2 depends on what you learn from that one first."

If any section was thin due to missing context, flag it explicitly at the end:
> "Note: [Section X] is thin because [reason]. You may want to fill this in before handing off to engineering."

---

## Standalone Use

This skill works without any upstream files. If invoked standalone:
- Ask for the stories (paste or describe)
- Ask for the user and the problem if not in the stories
- Generate what's possible, flag what's missing
- Offer to connect to session-brief.md or validation-*.md if they exist elsewhere
