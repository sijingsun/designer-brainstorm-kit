# Using Skills Standalone

Each skill in this suite works independently. You don't need to run the full chain. Enter at whichever point matches where you are.

---

## PM Thinking Coach — standalone

**When to use:** You have a vague idea, a problem space, or just a feeling that something is worth building. You haven't formed directions yet.

**What to say:**
```
/pm-thinking-coach
```
Or just describe what you're working on — the skill triggers automatically.

**What it needs from you:**
Nothing upfront. It opens with "Hey — I'm your PM. Catch me up." and drives the conversation from there.

**What you get:**
- A structured session via conversation (5-10 exchanges)
- A live competitive search included — no need to do this yourself
- `session-brief.md` saved to your working directory

**Tips:**
- Answer honestly about what's research vs. assumption — that's where the most value comes from
- When it asks about a specific person, use a real one. You'll zoom back out to the group later.
- If it's heading somewhere unhelpful, say so — it adjusts

---

## Idea Validator — standalone

**When to use:** You already have a direction — something specific you're considering building. You want to pressure-test it before opening Figma.

**What to say:**
```
/idea-validator validate my onboarding concept — a family member sets up a profile for their elderly parent before the parent opens the app
```
Or just invoke it and describe your direction when asked.

**What it needs from you:**
- A direction (one-liner is fine)
- The user it's for
- Their JTBD if you have it (or it will surface it)

**What it reads automatically:**
- `session-brief.md` if it exists — skips any question already answered there

**What you get:**
- Four validation checks (user fit, JTBD integrity, assumption stress-test, differentiation)
- Two persona critiques (Design+Engineering and Leadership) — invoke one or both
- A verdict: ✅ / ⚠️ / ❌
- `validation-[direction].md` saved

**Invoking specific personas:**
```
# Just the executor view
/idea-validator — give me the design and engineering take

# Just the leadership view  
/idea-validator — what would a VP say about this?

# Both (default)
/idea-validator
```

---

## Feature Story Writer — standalone

**When to use:** You have a validated (or at least decided) direction and want to write stories to design from.

**What to say:**
```
/feature-story-writer
```
Or say "write stories for [direction]" and it picks it up.

**What it reads automatically:**
- `stories-*.md` and `validation-*.md` if they exist — skips anything already established
- Falls back to asking for persona, JTBD, and direction if no files exist

**What you get:**
- A scoped story index (3-6 titles) before any stories are written
- Stories in priority order — critical assumption story first
- `stories-[direction].md` saved

**Tips:**
- When it presents the story index, tell it which stories to write and in what order — you don't have to write all of them
- The "my honest take" field is the most useful part for decision-making — don't skip it
- Stories 4-6 are often written as titles only. Ask for the full story when you're ready for them.

---

## Story to PRD — standalone

**When to use:** You have stories (from the story writer or from anywhere) and want to produce a shareable PRD.

**What to say:**
```
/story-to-prd
```
Or say "generate a PRD from these stories" and paste them.

**What it reads automatically:**
- `stories-*.md`, `validation-*.md`, `session-brief.md` — uses all available context
- Works from pasted stories alone if no files exist

**What you get:**
- An 8-section PRD saved to `prd-[feature-name].md`
- Ready to share with stakeholders or drop into Claude Code

**Tips:**
- The richer the upstream context (session brief + validation), the better the PRD sections on background, personas, and market angle
- If you're running standalone with just stories, Section 2 (background) and Section 5 (value proposition) will be thinner — the skill flags this
- The anti-metrics field in Section 4 is worth filling carefully — it prevents teams from optimizing for the wrong thing

---

## Entering Mid-Chain

You can skip phases entirely if you already have the outputs:

| You have | Start here |
|---|---|
| Nothing yet | `pm-thinking-coach` |
| A direction in mind | `idea-validator` |
| A validated direction | `feature-story-writer` |
| Stories written | `story-to-prd` |
| A session brief from a previous session | `idea-validator` (it reads the file) |
