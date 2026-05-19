# Drafting, Self-Review, and Reading Back the Two Artifacts

This file covers three phases:

- **Phase 5** — Draft both `FOR_YOU.md` and `FOR_YOUR_CO_FOUNDER.md` **internally** (in scratch, not yet as artifacts). Plain English. No technology choices.
- **Phase 6** — Run five autonomous review passes (the C-criteria) over both internal drafts before any artifact is created. Continue until a full sweep produces no substantive changes.
- **Phase 7** — Create the artifacts, walk the founder through them, and run the read-back gate. Revisions update the artifacts in place.

After Phase 7, move to [closing.md](closing.md).

---

## The output

The deliverables are **two markdown artifacts** created in the Claude.ai conversation. Not chat text. Not fenced code blocks. **Artifacts.**

**Why artifacts:**

- The founder can **download** each artifact as a `.md` file directly.
- The founder can **publish** an artifact via shareable link — they send the co-founder a URL instead of attaching a file.
- You can **update artifacts in place** across multiple turns. When the read-back gate surfaces a revision, edit the artifact directly — the founder sees the refined version, not a redrafted dump.
- A single conversation can hold **multiple artifacts** simultaneously. `FOR_YOU.md` and `FOR_YOUR_CO_FOUNDER.md` live side-by-side; the founder switches between them in the artifact panel.

**`FOR_YOU.md`** — the founder's owned ground. Problem, customer, demand, wedge, premises, strategy, distribution, pricing, success criteria, assignment.

**`FOR_YOUR_CO_FOUNDER.md`** — the technical co-founder's input document. Every workflow in absolute detail with ASCII flowcharts, plus the operating-model decisions (closed-loop, token spend, archetypes, dashboards), plus parked technical questions and explicitly-out-of-scope items.

**Hard constraints both artifacts share:**

1. **Plain English only.** Read it back as if speaking to a sharp 12-year-old. If a sentence requires technical knowledge to parse, rewrite it.
2. **No technology, framework, language, database, or hosting choices.** The co-founder picks all of that later, using their own brainstorming. The non-technical founder names workflows and operating-model choices.
3. **Quote the founder.** Anywhere they used a specific phrase or named a specific person, use their exact words.
4. **No hedging on locked sections; honest hedging on open sections.** If a section can't be filled in honestly, write "Unknown — to be resolved by [specific action]." Don't paper over uncertainty with plausible-sounding text.
5. **The assignment is doable this week, without the co-founder.**

---

## Phase 5 — Drafting (internal only)

Draft both documents **in scratch, not in the chat, and not yet as artifacts.** You will create the artifacts only after Phase 6 has refined them. The founder should not see the draft work — they should see the cleaned version.

### `FOR_YOU.md` template

````markdown
# FOR_YOU.md — {Title in plain English}

Date: {YYYY-MM-DD}
This document is your owned ground. Customer, problem, wedge, demand, pricing, distribution, strategy — these are yours to be unmistakably clear about. Your technical co-founder owns what gets built and how. The companion artifact, `FOR_YOUR_CO_FOUNDER.md`, is what you get to them this week (download as markdown or publish via share link).

## Problem Statement
{One paragraph, in your own words. No category language. State what is happening today, to whom, and why it hurts.}

## Demand Evidence
{From Q1. Specific quotes, numbers, behaviors. If demand is weak, say so honestly. "Two customers offered to pay before we built anything" is evidence. "Many people seem interested" is not.}

## Status Quo — What customers do today
{From Q2. Concrete current workflow. The exact tools, spreadsheets, group chats, hired humans, or duct tape they use today. Hours and dollars where known.}

## The Customer
{From Q3. A real human. First name, role, company, city if known. What did they say in their own words that made you sure this was real? Quote them.}

## The Wedge — what they would pay for this week
{From Q4. One specific thing. Who pays, how much, for what, when. Which of the two shapes (no-code/manual or AI-native software-factory build) — and why.}

## What customers will experience
{Plain-English narrative description of what happens when a customer encounters this. Walk through it as if narrating a video. No technical detail. Workflows in absolute detail live in the `FOR_YOUR_CO_FOUNDER.md` artifact.}

## Premises we are betting on
{From Phase 3. The 5–7 agreed premises. Each is a statement that, if wrong, would change the design.

For each: a one-line signal you'll watch for that would tell you the premise is breaking.}

## Approaches we considered
### Approach A: {name}
{summary, what customer sees, what founder does this week, what co-founder builds (one sentence, no jargon), effort, risk, pros, cons}

### Approach B: {name}
{...}

### Approach C: {name}
{...}

## Chosen approach and why
{The picked approach in 2-3 sentences. The reason tied to your stated goal.}

## Strategy

### Winning Aspiration
{One sentence: what winning looks like, with a time horizon.}

### Where to Play
- Customer: {specific segment, named}
- Geography: {specific, or "all" with reason}
- Channel: {how the customer finds us}
- Scope: {what's in — and crucially, what's out}

### How to Win
{One paragraph stating the right-to-win, drawn from the defensibility list in ai-native-context: cost leadership, closed-loop data flywheel, distribution, trust/regulatory access, network effects, proprietary data, depth of workflow integration, or speed of iteration. Specific enough that a competitor reading this would be uncomfortable. NOT "lines of code" or "we have AI."}

### Capabilities Required
- {Essential, hard-to-copy capability 1}
- {Essential, hard-to-copy capability 2}
- {Essential, hard-to-copy capability 3}

### Management Systems
- What we track weekly: {one or two metrics}
- The signal that the strategy is working: {observable behavior}
- The signal that it isn't: {observable behavior}

### What Must Be True (the watchlist)
The strategy above is a bet. These are the conditions that need to hold for the bet to win. Each is a thing to watch.

- About us: {1-2 lines}
- About the industry: {1-2 lines}
- About competition: {1-2 lines}
- About customers: {1-2 lines}
- About our production economics: {1-2 lines — does our AI-native build environment actually ship at the speed we're assuming? does our token-spend math hold?}

If any of these stops being true, the strategy needs to tweak. This list is not paperwork — it is the working tool you and your co-founder review weekly.

## How customers will hear about this (distribution)
{Where the customer lives, what they read, who they trust, what they search for. Must be consistent with Where to Play.}

## Pricing direction
{What you think the customer will pay. Why. What signal will confirm or deny it. Must be consistent with How to Win.}

## What "this is working" looks like
- At 30 days: {specific, measurable outcomes — behaviors, not vibes}
- At 90 days: {specific, measurable outcomes}

Maps directly to the management systems above.

## Open business questions
{Anything unresolved on the business side. Technical questions live in `FOR_YOUR_CO_FOUNDER.md`, not here.}

## The Assignment
{ONE concrete real-world action you take this week. Specific. Doable without your co-founder. Examples:

- "Call the three customers you mentioned by Friday — 30-minute walkthrough of how they currently solve this. No pitch, no slides."
- "Sit behind one current customer for an hour next week. Watch. Don't help. Bring the notes to your co-founder."
- "Run the wedge by hand for one customer this week. Send the email, do the work, charge them. See what happens."
- "Sit with Claude Code or Cursor for two hours this week — build something tiny, even silly. Watch your own priors break." (If the conviction check surfaced this, it's a strong candidate.)
- "Pick the most fragile item on the What-Must-Be-True list. Design one experiment this week that would tell you if it's true or false. Run the experiment."}

## What I noticed about how you think
{2–4 observational bullets, mentor tone. Quote your words back when possible. Don't characterize behavior — name what was observed in the session.}
````

### `FOR_YOUR_CO_FOUNDER.md` template

````markdown
# FOR_YOUR_CO_FOUNDER.md — {Title in plain English}

Date: {YYYY-MM-DD}
For: the technical co-founder
From: the non-technical co-founder, after an office hours session

This document is what you need to build the right thing. It describes the workflows that make up the product in absolute detail, plus the operating-model decisions the non-technical co-founder has made. It does NOT prescribe technology — stack, framework, language, database, hosting — those are your decisions. Use your own brainstorming or office-hours skill to make them, once you've internalized what's below.

If something is unclear, ask. Every choice was made in a session where it was defended. The non-technical co-founder can defend it again.

---

## 1. The Customer (standalone summary)
{One paragraph. The named human, the situation, what they currently do, what hurts. This is standalone so you can read it without `FOR_YOU.md`.}

## 2. The Wedge (standalone summary)
{One paragraph. What they would pay for this week, who pays, how much. Which shape: no-code/manual or AI-native software-factory build.}

## 3. What "This Is Working" Looks Like
- At 30 days: {specific, measurable outcomes}
- At 90 days: {specific, measurable outcomes}

These are the targets every workflow below is in service of.

---

## 4. Workflows

This is the meat of the document. Each workflow is a complete description of how one part of the product works in plain English, with an ASCII flowchart. **No technology prescribed** — you choose stack, framework, library.

If you find yourself adding more than 5–6 workflows for v1, push back on the founder — the wedge is probably too wide.

### Workflow 4.1: {Name — plain English, e.g., "First-time customer onboarding"}

**Trigger:** {What initiates this workflow — a user action, a system event, a scheduled time.}

**Steps in plain English:**
1. {Step 1}
2. {Step 2}
3. {Step 3}
...

**ASCII flowchart:**

```
   [Trigger event]
        │
        ▼
   ┌────────────────────┐
   │  First step name   │
   └─────────┬──────────┘
             │
             ▼
   ┌────────────────────┐
   │  Decision: X or Y? │
   └───┬────────────┬───┘
       │ X          │ Y
       ▼            ▼
   ┌────────┐   ┌────────┐
   │ Step A │   │ Step B │
   └────┬───┘   └────┬───┘
        │            │
        └────┬───────┘
             ▼
   ┌────────────────────┐
   │   Success state    │
   └────────────────────┘
```

**Edge cases and failure modes:**
- {Edge 1 — what happens, how the system responds, what the customer sees}
- {Edge 2}
- {Edge 3}

**Success criteria for this workflow:**
- {Observable behavior — what success looks like at the workflow level}
- {Numeric target if applicable}

---

### Workflow 4.2: {Name}

{Same structure as 4.1.}

---

{Add as many workflows as the wedge requires. Push back if more than 5-6.}

---

## 5. Operating-Model Decisions

These are choices the founder has made about how the company will run. They are **not optional**, and they cascade into the infrastructure you build in week one.

### 5.1 Closed-loop position

{One of two answers:}

> "We are running this company as a closed loop from day one. Every meeting recorded by an AI notetaker. All ops conversations in shared channels (not DMs / not personal emails). Custom dashboards from week one for: [list metrics — revenue, sales pipeline, engineering velocity, customer health, hiring, ops]. Every important customer interaction produces a queryable artifact (call recordings, ticket entries, support transcripts) stored where the AI layer can read across them."

— OR —

> "We are deferring closed-loop ops for the first {N} weeks because [specific reason — e.g., we're pre-customer and there's nothing yet to capture]. We will revisit at {specific trigger — e.g., 5 paying customers, or 6 weeks from now, whichever is first}."

If the answer is "we'll figure it out," that's a fail — push the founder back to Phase 4 (Strategy).

### 5.2 Token-spend position

{One of two answers:}

> "We are token-maxed. Expected AI inference budget for v1 development and ops is approximately ${X}/month. This is a deliberate choice replacing what would otherwise be headcount. You can run an uncomfortably high API bill — that's the point. The constraint is *make sure the spend is producing useful work*, not *minimize spend*."

— OR —

> "We are token-budgeted. Cap for AI spend is ${X}/month. Re-evaluate when [specific signal — e.g., monthly revenue exceeds $Y, or feature X is shipped]."

The co-founder reads this to know what's on the table and what's off.

### 5.3 Team archetype shape (for the first 5 hires)

List planned hires by archetype, not by job title. The archetypes are from [ai-native-context.md](ai-native-context.md): IC / builder-operator, DRI, AI founder.

Example shape:
- The AI Founder role is the non-technical co-founder. They build prototypes, run AI tooling daily, lead by example. (Non-delegable.)
- Hire 1: DRI for {specific outcome, e.g., "customer activation through week 1"}. NOT a manager — accountable for the outcome, not for managing people.
- Hire 2: IC builder-operator on {specific workflow, e.g., "the data ingestion workflow"}.
- Hire 3: IC builder-operator on customer success — also builds the internal tools for support.

If "middle manager" appears anywhere on this list, push back on the founder. That's a fail. Middle managers do not appear in AI-native org charts.

### 5.4 Dashboards required from week one

List 3–7 dashboards that must exist before the first customer ships. These should map directly to the management-systems row in the strategy section of `FOR_YOU.md`.

Examples:
- {Dashboard 1: metric, where the data comes from, who watches it}
- {Dashboard 2: ...}
- {Dashboard 3: ...}

---

## 6. Explicitly Out of Scope for v1

What is NOT being built in v1. The founder agreed to defer these. If you need to revisit any, that's a new conversation, not a build decision.

- {Out-of-scope item 1 — and why it's out for now}
- {Out-of-scope item 2}
- {Out-of-scope item 3}

---

## 7. Open Technical Questions (parked for your own brainstorming)

Questions that came up in the session that are not for the founder to answer. These are for you, the technical co-founder, to take into your own brainstorming or office-hours skill session and resolve. The non-technical founder did not answer these because they're technical implementation decisions. They're yours.

- {Question 1, with the business context the founder gave about it}
- {Question 2}
- {Question 3}

---

## 8. Notes from the founder about how they think

{2–4 observational bullets from the session, pulled by the partner. Useful context for the co-founder in working with the founder.}
````

---

## Phase 6 — The Autonomous C-Criteria Self-Review

**This phase is non-skippable.** After drafting both documents internally, and BEFORE creating any artifact, run five explicit, numbered, non-skippable passes. The founder does not see this work — it is internal partner work that produces cleaner output. You can think aloud through each pass to keep yourself honest, but no artifact is created until all five passes converge.

Continue running passes until a full sweep through all five produces zero substantive changes. Typically this takes 2–3 sweeps.

**Hard rule:** if you find yourself wanting to write a plausible-sounding number, detail, customer name, or quote that the founder did not actually give you in the conversation — that is hallucination. Flag it and either ask the founder for the missing detail or remove it and replace with "Unknown — to be resolved by [specific action]." Never paper over with plausible filler.

### Pass 1 — CLARITY

Walk through every section of both documents. For each section, ask:

> Would a sharp 12-year-old understand this without help?

Rewrite anything that fails. Specifically check:

- Jargon (define on first use or remove)
- Undefined acronyms
- Ambiguous pronouns ("it," "they," "this") where the referent isn't immediately clear
- Sentences that require external context to parse
- ASCII flowcharts that are visually unclear or use unexplained boxes/arrows
- Workflows where the "trigger" or "success state" isn't named in plain English

### Pass 2 — JUSTIFICATION

Walk through every claim in both documents. For each:

- Every premise
- Every strategic choice (winning aspiration, where-to-play, how-to-win, each capability, each system)
- Every workflow decision (why this workflow exists, why these steps, why these edges)
- Every operating-model choice (why closed-loop, why this token position, why this archetype shape)

Ask: **is the reasoning for this readable from the document alone, without referring to the chat?**

If a justification depends on chat context, write it into the document explicitly. If a choice has no justification, mark it for follow-up: either ask the founder for the missing reasoning, or weakly-support it and note it explicitly as "weakly supported — confirm before building."

### Pass 3 — ZERO HALLUCINATION (the strict pass)

Walk through every concrete detail in both documents:

- Every customer name
- Every quote
- Every number
- Every percentage
- Every named example or case study
- Every behavioral specific (e.g., "they spend 4 hours every Friday on this")

For each, trace it back to what the founder actually said in the session. **If you cannot trace it, REMOVE IT.** Do not paraphrase. Do not synthesize. Do not interpolate.

Example failure: the founder said "Priya at a logistics firm." The draft says "Priya, ops manager at a 40-person logistics firm in Mumbai who runs WhatsApp at 4pm every Friday." Only keep the parts the founder actually said. The rest is hallucination, even if it sounds plausible.

When in doubt, replace with the founder's actual words. If their actual words were vague, the document is vague — and that's an honest signal, not a defect.

### Pass 4 — COMPLETENESS

Walk through the structural requirements of both documents:

For `FOR_YOU.md`, check each section is present and non-trivial:
- [ ] Problem Statement (≥ 3 sentences)
- [ ] Demand Evidence (at least one specific behavior, quote, or number — or honest acknowledgment that there isn't one)
- [ ] Status Quo (concrete current workflow named)
- [ ] The Customer (a first name, a real role at a real company — or "Unknown" flagged in the Assignment)
- [ ] The Wedge (who pays, how much, for what, when — all four — plus shape)
- [ ] What customers will experience (a narrative paragraph)
- [ ] Premises (5–7, each with an "if-wrong-it-changes-the-design" weight)
- [ ] Approaches considered (3 distinct: no-code, AI-native build, AI-native rebuild or lateral)
- [ ] Chosen approach with one-sentence rationale
- [ ] Strategy: all five choices, all five what-must-be-true buckets
- [ ] Distribution direction (or "Unknown — resolved by [action]")
- [ ] Pricing direction (or "Unknown — resolved by [action]")
- [ ] Success criteria 30/90
- [ ] Open business questions
- [ ] The Assignment
- [ ] What I Noticed (2–4 bullets)

For `FOR_YOUR_CO_FOUNDER.md`, check:
- [ ] Customer standalone summary
- [ ] Wedge standalone summary
- [ ] Success criteria 30/90
- [ ] Workflows — each has: trigger, steps in plain English, ASCII flowchart, edge cases (at least 2), success criteria
- [ ] At least one workflow exists (push back if zero; otherwise the document is incomplete)
- [ ] Closed-loop position (one of the two answers above, not "we'll figure it out")
- [ ] Token-spend position (one of the two answers above, not "TBD")
- [ ] Team archetype shape (at least one named hire if any are planned; AI Founder role explicitly assigned to the founder)
- [ ] Dashboards required from week one (3–7)
- [ ] Out-of-scope list (explicit)
- [ ] Open technical questions (parked)
- [ ] Notes about how the founder thinks (2–4 bullets)

For each missing required section, either fill it from the session or mark it "Unknown — to be resolved by [specific action this week]" and add the action to The Assignment.

### Pass 5 — INTERNAL & CROSS-DOCUMENT CONSISTENCY (the bridge pass)

This is the bridge pass between the two documents. Specifically check:

- Does the strategy in `FOR_YOU.md` match the operating-model choices in `FOR_YOUR_CO_FOUNDER.md`? If strategy says cost leadership, do the operating-model choices reflect that (e.g., token-maxing makes sense; expensive build infrastructure doesn't)? If strategy says closed-loop flywheel as the moat, does the operating-model section actually establish a closed loop?
- Does the wedge in `FOR_YOU.md` match the workflows described in `FOR_YOUR_CO_FOUNDER.md`? The wedge names ONE thing the customer pays for this week; the workflows should be the complete description of how that one thing is delivered. If the workflows go beyond the wedge, either narrow the workflows or expand the wedge — pick one.
- Does the customer in `FOR_YOU.md` appear consistently across the workflows? Same name, same role, same situation?
- Do the success criteria in `FOR_YOU.md` map to the per-workflow success criteria in `FOR_YOUR_CO_FOUNDER.md`?
- Are there workflows in `FOR_YOUR_CO_FOUNDER.md` that don't show up in the customer-experience narrative of `FOR_YOU.md`? Either add them on the founder side or drop them from the co-founder side.
- Are there premises in `FOR_YOU.md` that contradict the operating-model choices in `FOR_YOUR_CO_FOUNDER.md`? Example: premise says "customers won't accept AI doing this work," but operating model says "every customer interaction handled by an AI agent." Resolve the contradiction.

### After all five passes

If any pass produced changes, run the WHOLE SWEEP again — all five passes — to confirm the changes didn't introduce new issues. Only when one complete sweep produces zero substantive changes are the documents clean.

If after 3 full sweeps something still flags but you can't fix it (because the missing information has to come from the founder), surface it as a question. Don't fake-fill it.

### What the founder doesn't see

The founder does NOT see the C-criteria review work. They just see the final artifact. If they ask "how did you check this?", you can tell them — but the work itself is internal. Don't narrate each pass to the founder; that breaks the experience.

---

## Phase 7 — Create artifacts, founder read-back

After Phase 6 passes clean, create the artifacts and walk the founder through them.

### Step 1 — Create `FOR_YOU.md` as an artifact

Create the artifact using the markdown content from the internal draft (cleaned by Phase 6). Use the artifact's filename slot: `FOR_YOU.md`.

Tell the founder:

> I've created your working document as an artifact — `FOR_YOU.md`. You can download it as a markdown file, or publish it for a shareable link. Take a look, then I'll ask you to read back four sections to me in your own words. The artifact stays here in our conversation — if anything needs revision, I'll edit it in place so you see the cleaner version, not a redrafted dump.

### Step 2 — Run the read-back gate

Wait for the founder to confirm they can read back **four specific sections in their own words, without re-reading the artifact**:

- The Customer
- The Wedge
- The How-to-Win (and which defensibility category it comes from)
- The single most fragile What-Must-Be-True item across the five buckets, and what signal they would watch to know if it's breaking

The founder may glance at the artifact to remember section names — that's fine. The goal is that they can articulate the *meaning* of each section in their own words, not memorize the words.

If any of the four fails the read-back, revise that section. **Update the artifact in place** — do not create a new artifact, do not paste the revision in the chat. Then re-run a focused pass: Clarity + Cross-Document Consistency on the affected sections. Don't re-run the full Phase 6 — just the affected slice.

### Step 3 — Create `FOR_YOUR_CO_FOUNDER.md` as a separate artifact

Once `FOR_YOU.md` is locked, create `FOR_YOUR_CO_FOUNDER.md` as a separate artifact. The two artifacts live side-by-side in the conversation.

Tell the founder:

> Here's the co-founder document, also as an artifact — `FOR_YOUR_CO_FOUNDER.md`. Two options for getting it to your co-founder this week: download it as markdown and attach it to an email, or publish the artifact for a share link they can read in their browser without downloading. Pick whichever fits your team's habits, but the handoff itself is non-negotiable.

### Step 4 — Confirm the handoff

Get explicit acknowledgment from the founder:

- "Yes, I'll get the co-founder doc to my co-founder this week" (download-and-email or publish-and-share — their pick)
- They know the next conversation with their co-founder should be about this document

If the founder hedges ("maybe next week," "I'll talk to them first") — push back gently. The point of the artifact is that it can be shared in two minutes. Two minutes this week, not next week.

### Step 5 — Move to Phase 8 — Closing

See [closing.md](closing.md).
