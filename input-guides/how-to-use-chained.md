# Using the Full Chain

The `/brainstorm-feature` command runs all four skills in sequence, passing context forward automatically. This is the recommended flow when you're starting from scratch on a new feature.

---

## When to Use the Full Chain

- You're starting a new feature with no clear direction yet
- You want to do the thinking rigorously before touching design tools
- You want four artifacts at the end: session brief, validation, stories, PRD

---

## How to Start

```bash
/brainstorm-feature [feature area or problem space]
```

Examples:
```bash
/brainstorm-feature onboarding for a senior AI companion app
/brainstorm-feature notification system for a B2B analytics dashboard  
/brainstorm-feature collaborative workspace for remote design teams
```

You can also just invoke it with no argument and the PM will open with "Hey — catch me up."

---

## What Happens in Each Phase

### Phase 1 — PM Thinking Coach
*Estimated exchanges: 5-10*

The PM opens the conversation and drives it. Your job is to answer honestly. The PM will:
- Ask about your user group (using a specific real person as a lens)
- Probe the outcome, the workaround, what's known vs. assumed, and constraints
- Search competitors and bring ones you didn't mention
- Map opportunities before letting you think about solutions
- Surface the market and business angle
- Generate 2-4 directions and take a lean

At the end: `session-brief.md` is saved. The PM offers to hand off to validation.

**You can stop here.** The session brief alone is a useful artifact — take it to a team meeting, use it to brief a PM, or let it sit while you do more research.

---

### Phase 2 — Idea Validator
*Estimated time: one pass, no back-and-forth needed*

The validator reads `session-brief.md` and runs without asking questions you've already answered. It:
- Checks user-direction fit
- Checks JTBD integrity
- Maps and ranks assumptions with cheapest tests
- Checks differentiation against competitive landscape
- Runs Design+Engineering and Leadership persona critiques
- Gives a verdict

At the end: `validation-[direction].md` is saved. The validator offers to hand off to story writing.

**If the verdict is ❌:** The session ends here with a specific redirect — go back to a named phase in the session brief. Do not push through to stories with a broken direction.

**If the verdict is ⚠️:** Conditions are named explicitly. You can address them now or proceed with the conditions as design constraints.

---

### Phase 3 — Feature Story Writer
*Write as many or as few stories as you need*

The story writer reads both upstream files and starts from your persona and direction — no repeated questions. It:
- Scopes the epic into 3-6 story titles
- Asks which stories to write (you don't have to write all of them)
- Writes stories in priority order — critical assumption story first
- Flags the "assumption this tests" field for each story

At the end: `stories-[direction].md` is saved. The story writer offers to generate a PRD.

**You can stop here.** Stories are sufficient to start designing. The PRD is for when you're ready to hand off to engineering.

---

### Phase 4 — Story to PRD *(optional)*
*One pass, no back-and-forth*

The PRD skill reads all three upstream files and generates the full document. No questions unless context is missing.

At the end: `prd-[direction].md` is saved.

---

## The Artifacts

After a full run, your working directory will contain:

```
session-brief.md              ← PM session output
validation-[direction].md     ← Validation + persona critiques + verdict
stories-[direction].md        ← Story set with acceptance criteria
prd-[direction].md            ← Full PRD ready for engineering
```

These files are designed to be shared. Drop `prd-[direction].md` into Claude Code, share `session-brief.md` with your PM, or use `stories-[direction].md` as the basis for a design review.

---

## Resuming a Previous Session

The skills read existing files in the working directory. If you ran Phase 1 yesterday and want to continue today:

```bash
# Resume from validation
/idea-validator
# It reads session-brief.md automatically

# Resume from story writing  
/feature-story-writer
# It reads both files automatically

# Generate PRD from existing stories
/story-to-prd
# It reads all three files automatically
```

---

## Saving Your Context

After your first session, tell the PM: "Save this for next time." It writes a `user-context.md` with your product context, target user group, and team setup. Future sessions skip the setup questions and start faster.

`user-context.md` is gitignored — it's local to your machine and never committed.
