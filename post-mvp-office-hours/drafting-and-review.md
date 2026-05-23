# Drafting, Self-Review, and Reading Back the Three Artifacts

This file covers three phases:

- **Phase 6** — Draft the artifacts **internally** (in scratch, not yet as artifacts). Plain English. Grounded in the session.
- **Phase 7** — Run five autonomous review passes (the C-criteria) over all internal drafts before any artifact is created. Continue until a full sweep produces no substantive changes.
- **Phase 8** — Create the artifacts, walk the founder through them, and run the read-back gate. Revisions update the artifacts in place.

After Phase 8, move to [closing.md](closing.md).

---

## Artifact production environment

The agent infers the environment from the tools available to it:

- **Claude.ai web**: artifacts are produced via the artifacts UI (the
  `<antArtifact>` markup convention). They render side-by-side, are
  downloadable, and shareable via link.
- **Claude Code / Codex / Cursor / any agent with file tools**: write
  the artifacts to disk via the `Write` tool in the current working
  directory. Filenames as named above.

If neither artifact-rendering nor file-write capability is available,
dump the artifact contents into the chat as fenced markdown blocks
labeled with the filename — this is the worst case and the founder
must manually copy them out.

Do not duplicate the artifacts across modes (only use the most capable
mode the environment supports).

---

## The output

The deliverables are **two or three markdown artifacts** depending on route:

| Route | Artifacts produced |
|---|---|
| Searching | `WHERE_YOU_ARE.md` + `WHAT_TO_DO_NEXT.md` |
| Approaching | `WHERE_YOU_ARE.md` + `WHAT_TO_DO_NEXT.md` |
| Claims-PMF | `WHERE_YOU_ARE.md` + `WHAT_TO_DO_NEXT.md` + `WHAT_INVESTORS_WILL_ASK.md` |
| Fundraise-ready | `WHERE_YOU_ARE.md` + `WHAT_TO_DO_NEXT.md` + `WHAT_INVESTORS_WILL_ASK.md` |

**Why artifacts:**

- The founder can **download** each artifact as a `.md` file directly.
- The founder can **publish** an artifact via shareable link.
- You can **update artifacts in place** across multiple turns. When the read-back gate surfaces a revision, edit the artifact directly.
- A single conversation can hold **multiple artifacts** simultaneously.

**Hard constraints all artifacts share:**

1. **Plain English only.** Read it back as if speaking to a sharp 12-year-old. If a sentence requires domain knowledge to parse, rewrite it.
2. **Quote the founder.** Anywhere they used a specific phrase or named a specific person, use their exact words.
3. **No hedging on locked sections; honest hedging on open sections.** If a section can't be filled in honestly, write "Unknown — to be resolved by [specific action]." Don't paper over uncertainty with plausible-sounding text.

---

## Phase 6 — Drafting (internal only)

Draft all applicable documents **in scratch, not in the chat, and not yet as artifacts.** You will create the artifacts only after Phase 7 has refined them. The founder should not see the draft work — they should see the cleaned version.

### `WHERE_YOU_ARE.md` template

````markdown
# WHERE_YOU_ARE.md — {Title in plain English}

Date: {YYYY-MM-DD}
Route: {Searching | Approaching | Claims-PMF | Fundraise-ready}

This document is your grounded picture of where you actually stand.
Not where you hope to be — where the evidence says you are today.

## Diagnostic Placement and Signals

**Segment:** {Searching | Approaching | Claims-PMF | Fundraise-ready}

**Signals that placed you here:**
- {Signal 1 — specific, from the diagnostic questions}
- {Signal 2}
- {Signal 3 — at least two must be stated; these are the signals from the 4-segment table in diagnostic.md}

If you believe this placement is wrong, name the signal that was missed — a specific metric, quote, or behavior, not a feeling.

## Real vs. Vanity Metrics

{Walk through every metric the founder cited in the session.}

| Metric | What the founder said | Verdict |
|---|---|---|
| {Metric name} | {Founder's claim, in their words} | {Passes: leading-indicator OR Fails: vanity — explain why in one sentence} |
| {Metric name} | ... | ... |

A metric passes if it predicts future retention or revenue. It fails if it could look good while the business is actually dying (e.g., total signups, followers, press mentions, app-store downloads without retention data).

## Customer-Pulse Status

{Answer two questions directly:}

**Are they running toward customer conversations or hiding from them?**
{One paragraph. Cite what they said in the session about their last 10 customer conversations. Be specific — how many conversations, how recent, what format. If they could not describe 10, say so.}

**What the last conversation actually told them:**
{Direct quote or paraphrase from Q4 of the diagnostic. If they gave summaries rather than quotes, flag it.}

## Defensibility Check

{Route-gated:}
{If route is Claims-PMF or Fundraise-ready — include this section:}

**Claimed moat:** {What the founder said their durable advantage is}

**Moat type:** {Name the specific type — e.g., one of Helmer's 7 Powers, or an NFX network effect type. If the founder could not name a type, write "unnamed — not yet articulated."}

**Stress test:** {Does the moat survive: (1) 1,000x cheaper model inference in 18 months? (2) a well-funded competitor copying the stack in a weekend? If not, name what's actually durable and what's ephemeral.}

{If route is Searching or Approaching — include this line instead:}

[skipped — see PMF-before-moat principle: building a moat before demonstrating retention is premature. Return here when the cohort curve is flat-after-decay or better.]

## Strategy Snapshot

{The five Playing-to-Win choices. One paragraph each. Drawn from the strategy section of the session.}

**Winning Aspiration:** {One sentence: what winning looks like, with a time horizon.}

**Where to Play:** {Customer segment, geography, channel, and scope — what's in and what's explicitly out.}

**How to Win:** {The right-to-win in plain English. Specific enough that a competitor reading this would be uncomfortable. Not "we have AI." A named mechanism.}

**Capabilities Required:** {The two or three hard-to-copy capabilities the strategy depends on. If they can't name them, that's a gap.}

**Management Systems:** {What they track weekly, the signal the strategy is working, and the signal it isn't. Ties to the metrics table above.}

## Kill List

{Decisions to kill — features, segments, channels, hires, initiatives, experiments. These are things the founder agreed in the session are no longer worth attention.}

- {Kill 1 — what and why}
- {Kill 2}
- {Kill 3 — minimum 2; if the session produced no kill decisions, write "None named in this session — revisit next session."}
````

**Example (Approaching route, abbreviated):**

> **Segment:** Approaching  
> **Signals:** Shipped 6 weeks ago. 400 users with two named segments (solo accountants, small firms with under 5 staff). Retention curve exists — 40% still active after week 4, then flat-to-zero. Last 10 customer calls described as "mix of onboarding issues and one expansion ask."
>
> **Kill List:** Dropped the "team dashboard" feature — three customers asked for it but none were willing to pay more for it. Killing the LinkedIn outreach channel — zero activation from 200 connection requests. Both agreed in session.

---

### `WHAT_TO_DO_NEXT.md` template

````markdown
# WHAT_TO_DO_NEXT.md — {Title in plain English}

Date: {YYYY-MM-DD}
Route: {Searching | Approaching | Claims-PMF | Fundraise-ready}

This document is your operating contract for the next week and quarter.
One headline move. Everything else is in service of that move.

## The Headline Move

{One sentence. The single biggest bet the founder is making this week or this quarter. Specific enough that a third party could evaluate it without context.}

Example: "Run 10 unscripted discovery calls with solo accountants before the next session — no slides, no demo, just listening."

## Why This Move

{One paragraph. Connect the headline move directly to the diagnostic placement and the strategy. Why this move, at this moment, for this company? If the reasoning requires more than one paragraph, the move may be too complicated.}

## Supporting Work

{3-5 bullets. Work that enables the headline move, or that runs in parallel without conflicting with it.}

- {Supporting action 1}
- {Supporting action 2}
- {Supporting action 3}
- {Supporting action 4 — optional}
- {Supporting action 5 — optional}

## The 90-Day Milestone

{One specific, falsifiable outcome. Not a goal — an outcome the founder could hand to a skeptic and have evaluated. Numbers where possible. Named milestones over vague directions.}

Example: "By {date 90 days out}, we have 3 paying customers each at $500/month, all in the solo-accountant segment, all retained for at least 60 days."

## What Would Tell You to Abandon This Path

{At least two conditions. These are honest kill-switches — signals that the headline move is wrong, not just slow.}

- {Abandon condition 1: specific, observable, time-bounded — e.g., "If after 10 discovery calls fewer than 3 people describe the problem as an active pain, the segment hypothesis is wrong."}
- {Abandon condition 2}
````

**Example (Claims-PMF route, abbreviated):**

> **Headline Move:** Close two expansion contracts with existing enterprise customers in the next 30 days — same ICP, higher seat count.
>
> **Why This Move:** The diagnostic shows flat-after-decay retention among enterprise ICPs and a healthy NPS score, but zero expansion revenue to date. If the moat is workflow depth, expansion is the next proof point. We are not ready to raise until we can show a customer growing their contract value.
>
> **90-Day Milestone:** By August 22, $15k MRR with at least 2 customers paying more this quarter than they did last quarter.
>
> **Abandon conditions:** If neither of the two target accounts expands within 30 days despite direct outreach, the moat may not be as deep as claimed — pivot to figuring out why before raising.

---

### `WHAT_INVESTORS_WILL_ASK.md` template (route-gated: Claims-PMF and Fundraise-ready only)

````markdown
# WHAT_INVESTORS_WILL_ASK.md — {Company name} Partner-Meeting Prep

Date: {YYYY-MM-DD}
Route: {Claims-PMF | Fundraise-ready}

This document maps the 10 partner-meeting questions to your current answers,
the follow-up pushback you will receive, and the gaps you need to close
before walking into a real partner meeting.

Each section has three parts:
1. **Their answer** — what you said in the session, in your words
2. **Push-back you will receive** — what the partner will follow up with
3. **Gap to close** — what you don't yet have, if anything

---

## Q1: What is the problem, in one sentence?

**Their answer:** {Founder's answer from the investor-mirror session, quoted or closely paraphrased}

**Push-back you will receive:** {The specific follow-up from investor-mirror.md Q1 that applies — e.g., "You used the word 'platform' — strip it out. What's the actual problem?"}

**Gap to close:** {What the founder does not yet have. "None" is a valid answer if the answer was clean and survived pushback.}

---

## Q2: Who has it? Who has it badly enough to pay?

**Their answer:** {Founder's answer}

**Push-back you will receive:** {From investor-mirror.md Q2 pushback rules — e.g., "You named a segment, not a person. A partner will push to a named archetype with a job title and a specific spend."}

**Gap to close:** {What's missing}

---

## Q3: What did you build? Why this wedge?

**Their answer:** {Founder's answer}

**Push-back you will receive:** {From investor-mirror.md Q3 — narrowing test, non-consensus belief test}

**Gap to close:** {What's missing}

---

## Q4: Show me retention. Show me cohorts.

**Their answer:** {Founder's answer — including the cohort curve shape if they described it}

**Push-back you will receive:** {From investor-mirror.md Q4 — e.g., "MAU growth can mask churn. I want the cohort curve." If they cannot describe the curve shape, the gap is the curve itself.}

**Gap to close:** {What's missing}

---

## Q5: What is the unit-economics story?

**Their answer:** {LTV/CAC if cited, payback period if cited}

**Push-back you will receive:** {From investor-mirror.md Q5 — LTV/CAC test, payback test}

**Gap to close:** {What's missing}

---

## Q6: Why now?

**Their answer:** {Structural change cited, or absence of one}

**Push-back you will receive:** {From investor-mirror.md Q6 — "Hot is not why. What structural shift makes this solvable now and unsolvable three years ago?"}

**Gap to close:** {What's missing}

---

## Q7: Why you?

**Their answer:** {Specific unfair advantage cited, or pedigree only}

**Push-back you will receive:** {From investor-mirror.md Q7 — pedigree-is-not-why-you test}

**Gap to close:** {What's missing}

---

## Q8: What is your moat going to look like in 24 months?

**Their answer:** {Named moat type, or absence of one}

**Push-back you will receive:** {From investor-mirror.md Q8 — "Both of those are ephemeral. What's the durable underlying mechanism?"}

**Gap to close:** {What's missing — specifically whether they can name a Helmer Power or NFX type}

---

## Q9: What are you raising and what does it buy?

**Their answer:** {Amount, use of funds, milestone it reaches}

**Push-back you will receive:** {From investor-mirror.md Q9 — "What does $X buy that $X/2 doesn't?"}

**Gap to close:** {What's missing}

---

## Q10: What is the one thing that would kill this?

**Their answer:** {Named kill condition, or deflection}

**Push-back you will receive:** {From investor-mirror.md Q10 — "More specific. What single event in the next 12 months would end this company?"}

**Gap to close:** {What's missing — a founder who cannot name a kill condition has not stress-tested the business}
````

**Example (Fundraise-ready route, Q1 only):**

> **Their answer:** "Ops teams at logistics companies spend 6 hours a week reconciling carrier invoices by hand because no carrier sends data in the same format."
>
> **Push-back you will receive:** "One sentence — that was close but two ideas are in there. Which part is the problem: the time spent, or the format inconsistency? A partner will compress you further."
>
> **Gap to close:** Sharpen to one sentence before the meeting. Current answer survives first pushback but would need one more compression pass.

---

## Phase 7 — The Autonomous C-Criteria Self-Review

**This phase is non-skippable.** After drafting all applicable documents internally, and BEFORE creating any artifact, run five explicit, numbered, non-skippable passes. The founder does not see this work — it is internal partner work that produces cleaner output. You can think aloud through each pass to keep yourself honest, but no artifact is created until all five passes converge.

Continue running passes until a full sweep through all five produces zero substantive changes. Typically this takes 2–3 sweeps.

**Hard rule:** if you find yourself wanting to write a plausible-sounding number, detail, customer name, or quote that the founder did not actually give you in the conversation — that is hallucination. Flag it and either ask the founder for the missing detail or remove it and replace with "Unknown — to be resolved by [specific action]." Never paper over with plausible filler.

### Pass 1 — CLARITY

Walk through every section of all documents. For each section, ask:

> Would a sharp 12-year-old understand this without help?

Rewrite anything that fails. Specifically check:

- Jargon (define on first use or remove)
- Undefined acronyms
- Ambiguous pronouns ("it," "they," "this") where the referent isn't immediately clear
- Sentences that require external context to parse
- Tables where column headers don't explain themselves
- Metric names that are undefined (e.g., "DAU" without saying what counts as a daily active user)

### Pass 2 — JUSTIFICATION

Walk through every claim in all documents. For each:

- Every segment placement (does the evidence cited match the 4-segment table in diagnostic.md?)
- Every strategic choice (winning aspiration, where-to-play, how-to-win, each capability, each system)
- Every kill-list decision (why was this killed? Is the reasoning stated?)
- Every headline move (is the "why this move" paragraph actually connected to the diagnostic and the strategy?)

Ask: **is the reasoning for this readable from the document alone, without referring to the chat?**

If a justification depends on chat context, write it into the document explicitly. If a choice has no justification, mark it for follow-up: either ask the founder for the missing reasoning, or weakly-support it and note it explicitly as "weakly supported — confirm before building."

### Pass 3 — ZERO HALLUCINATION (the strict pass)

Walk through every concrete detail in all documents:

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

Walk through the structural requirements of all documents:

For `WHERE_YOU_ARE.md`, check each section is present and non-trivial:
- [ ] Diagnostic Placement (segment named, at least 2 signals cited from the 4-segment table)
- [ ] Real vs. Vanity Metrics (every metric the founder cited is in the table with a verdict)
- [ ] Customer-Pulse Status (answered: running toward customers or hiding? Last conversation described specifically)
- [ ] Defensibility Check (present and route-appropriate: full section for Claims-PMF/Fundraise-ready; skip line for Searching/Approaching)
- [ ] Strategy Snapshot (all five Playing-to-Win choices are present and non-trivial)
- [ ] Kill List (at least 2 items, or explicit note that none were named)

For `WHAT_TO_DO_NEXT.md`, check:
- [ ] Headline Move (one sentence, specific, falsifiable)
- [ ] Why This Move (one paragraph connecting to diagnostic and strategy)
- [ ] Supporting Work (3–5 bullets)
- [ ] 90-Day Milestone (one specific, falsifiable outcome — not a goal)
- [ ] Abandon Conditions (at least 2 specific, observable, time-bounded kill-switches)

For `WHAT_INVESTORS_WILL_ASK.md` (Claims-PMF and Fundraise-ready only):
- [ ] All 10 questions present (Q1–Q10)
- [ ] Each question has all three subsections: Their Answer, Push-back, Gap to Close
- [ ] "Their answer" is the founder's actual answer from the investor-mirror session — not what they should have said
- [ ] "Push-back" is sourced from investor-mirror.md — the specific follow-up that applies, not a generic challenge
- [ ] "Gap to close" is honest: "None" only if the answer survived pushback cleanly

For each missing required section, either fill it from the session or mark it "Unknown — to be resolved by [specific action this week]."

### Pass 5 — CROSS-DOCUMENT CONSISTENCY (the bridge pass)

This pass checks coherence across all applicable documents. The number of documents depends on route (2 for Searching/Approaching; 3 for Claims-PMF/Fundraise-ready).

**Always check (2-document pass):**

- Does the diagnostic placement in `WHERE_YOU_ARE.md` match the headline move in `WHAT_TO_DO_NEXT.md`? A Searching founder's headline move should be discovery-oriented, not fundraising-oriented.
- Does the strategy snapshot in `WHERE_YOU_ARE.md` support the headline move in `WHAT_TO_DO_NEXT.md`? The how-to-win should be legible in the supporting work.
- Does the kill list in `WHERE_YOU_ARE.md` create any contradictions in `WHAT_TO_DO_NEXT.md`? (e.g., a killed channel shouldn't appear in supporting work)
- Do the 90-day milestone and the abandon conditions in `WHAT_TO_DO_NEXT.md` reflect the management systems cited in `WHERE_YOU_ARE.md`?

**Additional checks for Claims-PMF and Fundraise-ready (3-document pass):**

- Does the defensibility check in `WHERE_YOU_ARE.md` match the moat answer in Q8 of `WHAT_INVESTORS_WILL_ASK.md`? If they conflict, the founder has two different stories about their moat. Resolve it.
- Does the 90-day milestone in `WHAT_TO_DO_NEXT.md` connect to the unit-economics story in Q5 of `WHAT_INVESTORS_WILL_ASK.md`? If the milestone is "close 2 enterprise accounts" but the unit-economics story is unresolved, the gap should appear in Q5's "Gap to close."
- Are there gaps in `WHAT_INVESTORS_WILL_ASK.md` that should generate actions in `WHAT_TO_DO_NEXT.md`'s supporting work? Example: "Gap to close: cohort curve not yet described" in Q4 should translate to "Pull and describe the D30 cohort curve" in supporting work.

### After all five passes

If any pass produced changes, run the WHOLE SWEEP again — all five passes — to confirm the changes didn't introduce new issues. Only when one complete sweep produces zero substantive changes are the documents clean.

If after 3 full sweeps something still flags but you can't fix it (because the missing information has to come from the founder), surface it as a question. Don't fake-fill it.

### What the founder doesn't see

The founder does NOT see the C-criteria review work. They just see the final artifact. If they ask "how did you check this?", you can tell them — but the work itself is internal. Don't narrate each pass to the founder; that breaks the experience.

---

## Phase 8 — Create artifacts, founder read-back

After Phase 7 passes clean, create the artifacts and walk the founder through them.

### Step 1 — Create `WHERE_YOU_ARE.md` as an artifact

Create the artifact using the markdown content from the internal draft (cleaned by Phase 7). Use the artifact's filename slot: `WHERE_YOU_ARE.md`.

Tell the founder:

> I've created your grounded picture as an artifact — `WHERE_YOU_ARE.md`. Take a look, then I'll ask you to read back five sections to me in your own words. The artifact stays here in our conversation — if anything needs revision, I'll edit it in place so you see the cleaner version, not a redrafted dump.

### Step 2 — Run the read-back gate for `WHERE_YOU_ARE.md`

Wait for the founder to confirm they can articulate **five load-bearing sections in their own words**, without re-reading the artifact word-for-word:

1. **Diagnostic placement** — what segment they are in, and the two signals that put them there
2. **The single metric in the table they are most proud of** — and whether it actually passed the vanity test
3. **Customer-pulse** — what the last real customer conversation told them
4. **The headline strategy choice (How to Win)** — the right-to-win in their own words, not the artifact's
5. **The kill list** — at least one item they agreed to kill and why

The founder may glance at the artifact to remember section names — that's fine. The goal is that they can articulate the *meaning* of each section in their own words, not memorize the words.

If any of the five fails the read-back, revise that section. **Update the artifact in place** — do not create a new artifact, do not paste the revision in the chat. Then re-run a focused pass: Clarity + Cross-Document Consistency on the affected sections. Don't re-run the full Phase 7 — just the affected slice.

### Step 3 — Create `WHAT_TO_DO_NEXT.md` as a separate artifact

Once `WHERE_YOU_ARE.md` is locked, create `WHAT_TO_DO_NEXT.md` as a separate artifact.

Tell the founder:

> Here's your operating contract for the next week and quarter — `WHAT_TO_DO_NEXT.md`. I'll ask you to read back four sections in your own words before we move on.

### Step 4 — Run the read-back gate for `WHAT_TO_DO_NEXT.md`

Wait for the founder to articulate **four load-bearing sections**:

1. **The headline move** — in one sentence, in their own words, without reading from the artifact
2. **Why this move now** — the connection to the diagnostic and the strategy, in their own words
3. **The 90-day milestone** — specific, falsifiable, in their own words
4. **The first abandon condition** — the signal that would tell them to stop and change direction

If any fails, revise in place and re-run a focused slice.

### Step 5 — Create `WHAT_INVESTORS_WILL_ASK.md` (Claims-PMF and Fundraise-ready only)

For Searching and Approaching routes: skip this step. Move to Step 6.

For Claims-PMF and Fundraise-ready: create `WHAT_INVESTORS_WILL_ASK.md` as a third artifact.

Tell the founder:

> Here's your partner-meeting prep document — `WHAT_INVESTORS_WILL_ASK.md`. It maps each of the 10 questions to your current answer, the follow-up you'll receive, and what you need to close before walking into a real meeting. I'll ask you to read back four sections before we close out.

### Step 6 — Run the read-back gate for `WHAT_INVESTORS_WILL_ASK.md` (route-gated)

For Claims-PMF and Fundraise-ready only. Wait for the founder to articulate **four load-bearing questions**:

1. **Q1 (Problem)** — the one-sentence problem statement in their own words, without reading from the artifact
2. **Q4 (Retention)** — the cohort curve shape they described and why it does or does not show PMF
3. **Q8 (Moat)** — the named moat type and why it survives the 24-month stress test
4. **Their single biggest gap** — the "Gap to close" item across all 10 questions that, if unresolved, would most likely kill the fundraise

If any fails, revise in place. For Q8 in particular: if the founder cannot articulate the moat in their own words after seeing it in the artifact, the defensibility check in `WHERE_YOU_ARE.md` may also need revision — run Cross-Document Consistency on both.

### Step 7 — Move to Phase 9 — Closing

See [closing.md](closing.md).
