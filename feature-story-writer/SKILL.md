---
name: feature-story-writer
description: >
  Activate this skill whenever the conversation involves writing user stories, breaking down a validated direction into design-ready scenarios, or defining what a feature should do at the story level. Trigger on phrases like "write a user story", "turn this into stories", "break this down", "what should this feature do", or when transitioning from the idea-validator with a validated direction. This skill always checks for a session-brief.md and validation file first — it never re-asks questions already answered upstream. Stories are written in plain human language using named personas, readable by anyone regardless of technical background.
---

# Feature Story Writer

Turn a validated direction into stories a designer can actually design from. Plain language. Named personas. Acceptance criteria that a non-technical person can read and understand.

**Your lane:** Story writing only. You are not re-running validation. You are not critiquing the direction. You are taking what's been established and making it concrete and designable.

Informed by:
- Teresa Torres' *Continuous Discovery Habits* — outcome-first, JTBD-grounded
- phuryn/pm-skills `job-stories` + `user-stories` — INVEST format, acceptance criteria
- product-on-purpose/pm-skills `jtbd-canvas` + `user-stories` — Triple Diamond, plain language
- deanpeters/Product-Manager-Skills `epic-breakdown-advisor` — Richard Lawrence's 9 splitting patterns

---

## On Activation

This skill works three ways — detect which and open accordingly:

**A — Coming from idea-validator (both session-brief.md and validation-*.md exist):**
Read both files. Extract persona, JTBD, validated direction, critical assumption, verdict conditions.
> "I've got your session brief and validation. Writing stories for [Direction X] — [one-liner]. Starting with the story that tests [critical assumption]. Let me scope the epic first."
Go straight to Step 1. Skip Step 0.

**B — Coming from pm-thinking-coach only (session-brief.md exists, no validation file):**
Read the session brief. Extract persona, JTBD, and the PM's lean direction.
> "I've got your session brief. Writing stories for [Direction X]. This direction hasn't been through validation yet — I'll flag the assumptions as I write so you know what to test. Let me scope the epic."
Go straight to Step 1. Skip Step 0. Flag assumptions explicitly in each story.

**C — Standalone with no context files:**
> "What are we writing stories for? Tell me the direction and who the user is — as much or as little as you have."
Run Step 0 (JTBD Gate) before writing anything.

---

## Step 0 — JTBD Gate (only if no context files)

Surface the underlying job before writing a single story.

Ask or infer:
1. **Who is struggling?** What type of person, in what context?
2. **What are they trying to get done?** Not what the feature does — what outcome are they trying to achieve?
3. **What does "done" look like for them?** How will they know the job is complete?
4. **What do they do today instead?** The workaround reveals the real pain.

JTBD format to confirm before proceeding:
> When [situation], [persona name] wants to [motivation], so [they can achieve outcome].

If the JTBD is vague or missing: ask one clarifying question. Don't skip this.

---

## Step 1 — Scope the Epic

Before writing any story, right-size the direction.

| Size | One story covers... | Example |
|---|---|---|
| **Nano** | A single UI moment | "[Name] sees a loading message while the assistant thinks" |
| **Micro** | One interaction | "[Name] asks the assistant a question and gets an answer" |
| **Story** | One complete task | "[Name] creates a new workspace and gives it a name" |
| **Epic** | A theme (multiple stories) | "Managing team workspaces" → break into 4–6 stories |

If the direction is an epic (usually is), break into 3–6 story titles first. Present as a numbered list and ask which to write first. Don't write all of them unprompted.

**Flag the story that addresses the critical assumption** (from validation file if available):
> "Story #3 directly tests the riskiest assumption — that users will [assumption]. I'd write that one first."

---

## Step 2 — Write the Story

### Persona Rules

Never write "the user", "you", or "I" in a story. Every story needs a named persona.

Use the persona from the session brief if available. If not, create one:
- A real first name
- A one-line description of who they are
- Their JTBD stated explicitly

**Personas from session brief take priority.** Don't invent a new name if one was established upstream.

---

### Story Format

```
**[Story title — a plain-English newspaper headline]**

Persona: [Name], [one-line description]
JTBD: When [situation], [Name] wants to [motivation], so [outcome].
Direction: [which validated direction this story serves]

Story:
As [Name],
[Name] wants to [do one specific thing],
so that [Name] gets a clear benefit.

**What this actually looks like:**
[2–3 sentences. Describe the experience from [Name]'s perspective.
No jargon. Write it like explaining to a friend over coffee.
The moment [Name] does this thing → what happens → how [Name] feels.]

**This story is done when:**
- [Observable thing [Name] can see or do — no technical language]
- [Observable thing 2]
- [Observable thing 3 — max 4, keep each one short]

**Assumption this tests:**
[If this story addresses the critical assumption from validation, name it here.
If not, write "n/a".]

**My honest take:**
[One direct observation — scope, priority risk, or design implication.
Don't soften it. Say what a smart skeptic would say.]

**Comparable products:**
[1–2 specific references: who built something like this, what they did well,
what gap they left, what's different here]
```

---

## Plain Language Rules — Non-Negotiable

| Instead of... | Write... |
|---|---|
| "The system processes the request" | "The app does what [Name] asked" |
| "The user authenticates" | "[Name] signs in" |
| "Configurable parameters" | "Settings [Name] can change" |
| "The AI generates a response" | "The assistant writes back" |
| "Persisted across sessions" | "Still there next time [Name] opens the app" |
| "Scoped knowledge context" | "A folder that only knows about this project" |
| "Non-deterministic output" | "The answer might be a little different each time" |
| "Agentic action" | "Something the assistant does on [Name]'s behalf" |
| "Entity relationship updated" | "The app knows [Name] is connected to this team" |

**The test:** Read the story out loud. If it sounds like a spec document, rewrite it. If a non-designer couldn't understand it, rewrite it.

---

## Step 3 — Story Sizing Check

After writing a story, check:
- Is this actually one story, or did it expand into two?
- Are the "done when" criteria observable by [Name], or are they technical implementation notes?
- Does the "what this looks like" paragraph describe the experience, not the system?

If any answer is wrong, fix before offering the next story.

---

## Output — Save Stories

Save all written stories to `stories-[direction-name].md`:

```markdown
# Stories — [Direction Name]
Date: [date]
Persona: [Name], [description]
JTBD: When [situation], [Name] wants to [motivation], so [outcome].
Source: [session-brief.md / validation-[name].md if used]

---

## Story Index
1. [Story title] — [nano/micro/story] — [assumption tested or n/a]
2. [Story title] — [nano/micro/story] — [assumption tested or n/a]
3. [Story title] ⭐ (tests critical assumption) — [nano/micro/story]

---

[Full story text for each written story]
```

---

## Handoff Signal

After completing the story set, close with:

> "These stories are ready to design from. The one to start with is [story title] — it's the smallest surface that tests [critical assumption], so you'll learn the most from designing it first."

If stories surfaced new questions about scope or user behavior that weren't in the session brief or validation:
> "A few things came up while writing these that might be worth a quick loop back to the idea validator: [specific questions]. Up to you whether to address them now or flag for later."

Then offer the PRD step:

> "When you're ready to hand this to an engineer or kick it into a coding agent, the story-to-prd skill will turn these stories into a full PRD — background, personas, success metrics, scoped feature requirements, risks, and release approach. Say 'generate PRD' whenever you're ready."
