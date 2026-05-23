# Design — founder-office-hours repo restructure + post-mvp-office-hours skill

- **Date:** 2026-05-23
- **Author:** Adnan
- **Status:** Draft — awaiting review

## 1. Goal

Two outcomes from one piece of work:

1. **Restructure the existing GitHub repo** (`adoistic/non-tech-office-hours`) into a multi-skill repo named `founder-office-hours`. The existing skill becomes a self-contained subfolder. A second peer skill, `post-mvp-office-hours`, joins it as a sibling subfolder. The repo gains a top-level README that explains both skills and points to two separate release-zip downloads.
2. **Design and specify** the new `post-mvp-office-hours` skill — an office-hours methodology for founders who have already shipped a product, focused on diagnosing where they actually stand on PMF and getting them investor-ready. It is more rigorous than the peer skill (because data exists post-MVP, so the founder can't hide behind "we will" anymore), and it handles any founder type (technical, non-technical, solo, or co-founder pair).

Both skills must be **completely decoupled** — each folder self-contained, each zip independently buildable, no file in either skill referencing the other.

## 2. Non-goals

- No new GitHub repo. The existing one is renamed, not replaced.
- No git submodules. The existing skill's nested `.git/` is removed; everything lives under the renamed repo's single `.git/`.
- No symlinks. Shared content is verbatim-duplicated.
- No shared source of truth across skills. Drift between the two copies is acceptable.
- No implementation of skill content in this spec. The spec commits to architecture; implementation (including scraping NFX and processing the Helmer YC-video transcript) follows in the writing-plans phase.
- No technical-stack choices for the new skill's behavior (the skill's design is content + prompts, not code).

## 3. Repo layout (after restructure)

```
founder-office-hours/                           ← renamed from non-tech-office-hours
├── README.md                                   ← NEW top-level (Section 9)
├── LICENSE                                     ← lifted up from current skill root
├── non-tech-office-hours/                      ← existing skill, moved into subfolder
│   ├── SKILL.md                                ← lightly edited (one cross-ref into wiki)
│   ├── README.md
│   ├── ai-native-context.md                    ← lightly edited (one cross-ref into wiki)
│   ├── principles.md
│   ├── forcing-questions.md
│   ├── premise-and-alternatives.md             ← lightly edited (one cross-ref into wiki)
│   ├── strategy.md                             ← lightly edited (one cross-ref into wiki)
│   ├── drafting-and-review.md
│   ├── closing.md
│   └── moats-and-network-effects/              ← NEW (verbatim, see Section 7)
│       ├── raw/
│       │   ├── nfx-network-effects-manual.md
│       │   └── yc-helmer-7-powers-transcript.md
│       ├── wiki/
│       │   ├── concepts/
│       │   └── examples/
│       └── CLAUDE.md
├── post-mvp-office-hours/                      ← NEW skill (Sections 4–8)
│   ├── SKILL.md
│   ├── README.md
│   ├── ai-native-context.md                    ← VERBATIM copy from peer skill
│   ├── principles.md                           ← verbatim copy + 2 new principles
│   ├── diagnostic.md                           ← NEW module
│   ├── forcing-questions.md                    ← adapted: data-backed
│   ├── premise-and-alternatives.md             ← adapted: post-MVP alternatives
│   ├── strategy.md                             ← adapted: refined with real data
│   ├── investor-mirror.md                      ← NEW module
│   ├── drafting-and-review.md                  ← adapted: three artifacts
│   ├── closing.md                              ← adapted: route-calibrated
│   └── moats-and-network-effects/              ← VERBATIM copy of same wiki
│       ├── raw/
│       ├── wiki/
│       │   ├── concepts/
│       │   └── examples/
│       └── CLAUDE.md
├── archive/
│   └── 00_START_HERE.md … 07_CLOSING.md        ← original numbered drafts
└── docs/
    └── superpowers/
        └── specs/
            └── 2026-05-23-founder-office-hours-restructure-and-post-mvp-skill-design.md   ← this file
```

**Release artifacts** (not committed; generated at release time and uploaded to GitHub Releases):

- `non-tech-office-hours.zip` — exactly the contents of `non-tech-office-hours/` directory
- `post-mvp-office-hours.zip` — exactly the contents of `post-mvp-office-hours/` directory

## 4. The new skill — `post-mvp-office-hours`

### 4.1 Audience and frame

For founders who have **already shipped a product**. May be technical or non-technical, solo or with co-founders. The skill is **adaptive on founder type** (Section 4.2). Its two goals, in order:

1. **Diagnose where the founder actually stands on PMF** (real data, not narrative)
2. **Get them ready to face actual investors** (only relevant if they have PMF or are close)

The grilling is **harder than the peer skill** because the founder has real data — usage, retention, revenue, churn, cohorts — or has to admit they haven't measured. Either confession is useful.

### 4.2 Founder-type handling

Adaptive based on whether the founder identifies as technical or non-technical, but with a **counter-grill protocol for technical founders**:

When a technical founder claims an architecture is unique, novel, or hard to build, the skill counter-grills using the AI-native cost collapse (the same operating substrate the peer skill already carries):

- *Cost-to-replicate today vs. 2023.* A 1,000x engineer with a software-factory setup can clone in a weekend what took six months pre-AI.
- *Is the moat the code or what's underneath?* Push the founder to identify whether their defensibility is in the code (which has collapsed in value) or in data, distribution, ops, or network effects (which haven't).
- *Patent and counter-architecture tests.* If it's truly novel: why isn't it patented? Could a different architecture get to the same outcome?
- *What partners are saying.* The skill cites YC partner commentary and Bessemer / a16z partner statements on the defensibility shift to ground the push-back, not as appeals to authority but as evidence of where smart capital has moved.

For non-technical founders: the skill does not push technical questions; if they raise a technical claim, it accepts it provisionally and routes to the business angle (same Technical Redirect Protocol as the peer skill, applied in reverse).

### 4.3 Output artifacts

Three markdown artifacts, produced via Claude.ai's artifacts feature (or written to disk in Claude Code):

1. **`WHERE_YOU_ARE.md`** — the brutal honest snapshot. PMF status (real vs. claimed), what's actually working, vanity vs. real traction, retention curve reality, defensibility check, kill list. Always produced.
2. **`WHAT_TO_DO_NEXT.md`** — the path forward. Intentionally wide-open: could be "have 20 customer conversations next week", "kill these three features", "pivot the wedge to this segment", "double down on this channel", "raise now", "don't raise yet, here's why", "fire the sales hire". One headline move + supporting work. Always produced.
3. **`WHAT_INVESTORS_WILL_ASK.md`** — the investor mirror. The 10 partner-meeting questions the founder will face, their draft answers, the gaps. **Only produced when the diagnostic routes the founder to Claims-PMF or Fundraise-ready** (Section 5.2). Useful regardless of whether the founder is raising in 7 days or 18 months — same questions a serious operator should answer cold.

### 4.4 Hard rules (post-MVP specific, added to peer's existing rules)

Peer's existing hard rules carry over verbatim. Two new rules specific to post-MVP:

- **Reality before projection.** Behavioral data beats user interviews beats founder narrative beats slide-deck claims. If the founder can't show the data, the data doesn't exist and that is the finding. Quote-back: when they cite a metric, ask how they measured it; if they didn't, that is the answer.
- **PMF before moat.** Do not grill on defensibility until the founder has earned the right to think about it (Claims-PMF or Fundraise-ready route only). A Searching-route founder asking about moats is procrastinating on the harder question of whether anyone wants the product. The moats-and-network-effects wiki is *available* if needed, but the skill does not force traversal unless the founder's PMF status warrants it.

## 5. Phase plan

### Phase 0 — Substrate reads (always)

Before any phase: read `ai-native-context.md`, then `principles.md`. If joining mid-conversation, re-read the thread. Same pattern as peer skill.

### Phase 1 — Reflection + conviction check (always)

Reflect back what the founder has built in one paragraph, using their words and direct quotes where possible. Then run the same 2-hour-with-coding-agents conviction check verbatim from the peer skill — AI-timeline calibration matters more post-MVP, not less.

### Phase 2 — Diagnostic intake (NEW, always)

A structured probe to place the founder on a 4-segment spectrum. Five questions, asked one at a time, push for evidence on each.

#### The 5 diagnostic questions

1. **What did you ship and when?** — surfaces age, scope, whether they can describe it without a pitch deck.
2. **Who's using it right now?** — counts, names, segments. Push past "users" to "the person who came back yesterday." Force specificity.
3. **What's growing and what isn't?** — usage, revenue, retention, referral. Force the cohort retention shape if they can describe it; if they cannot, note the absence as a finding.
4. **What did the last 10 customer conversations actually sound like?** — Mom-Test rigor. Are they still talking to users or hiding? Direct quotes preferred over summaries.
5. **What is your runway and what would you do with $2M today?** — runway truth + tests whether they have a clear use of capital (fundraise-readiness signal).

#### The 4 segments and their signals

| Segment | Signals |
|---|---|
| **Searching** | Shipped, low usage, retention unknown or flat, still iterating on the wedge, no clear "who has this problem badly" answer |
| **Approaching** | Some traction, retention shape exists but is mediocre, narrative is hardening, customer conversations still happening |
| **Claims-PMF** | Founder declares PMF, retention is good or flat-after-decay, but defensibility/scale-out untested |
| **Fundraise-ready** | PMF evidence + healthy cohort retention curve + meaningful revenue or growth + clear use of capital + ability to answer all 10 partner-meeting questions cleanly |

#### Routing announcement

After the 5 questions, the skill announces the route to the founder verbatim:

> Based on what you just said, I am placing you at **[segment]**. Here is why: [one sentence citing the strongest signal]. If that's wrong, push back now.

The founder may override. Sycophantic re-routing — accepting an override without the founder providing a new signal that actually changes the segment — is a failure mode and is called out in `principles.md`.

### Phase 3 — Common spine (all routes)

All four segments run this phase in order.

#### 3.1 Customer-pulse grill

Mom Test applied to post-MVP. When did you last talk to a user? What did they actually say (direct quotes)? What did they do after the call? Are you running toward conversations or hiding from them?

#### 3.2 Real-vs-vanity audit

For each metric the founder cited in the diagnostic, ask: is this a vanity metric or a leading indicator? Specific tests:

- Cohort retention shape > MAU growth
- Paying-after-trial > sign-ups
- Organic word-of-mouth > paid acquisition at this stage
- Power-user concentration > average engagement
- Real customer conversations > waitlist size

For each metric, the skill names which test it fails or passes.

#### 3.3 Premise challenge + alternatives

Surface 5–7 premises the founder must agree with (including AI-native premises). Then force 3 alternatives — but the alternative set is post-MVP-flavored:

- *Pivot the wedge* — keep the team, change the wedge
- *Double down on what's working* — kill everything else, ride the strongest signal
- *Kill a feature or segment* — reduce surface area to clarify the wedge
- *Change distribution* — same product, different channel
- *Raise now* — capital is the unblocker
- *Don't raise yet* — runway is fine, raising would distract from the real bottleneck

Stop and wait for the founder to choose. The choice gets locked into `WHAT_TO_DO_NEXT.md`.

### Phase 4 — Branch by route

#### Searching / Approaching route

**Customer-discovery deep dive.** The back half of the session focuses on customer behavior, the Sean Ellis 40% "very disappointed" test (run it or commit to running it), wedge refinement or repositioning.

Skips the investor mirror. `WHAT_INVESTORS_WILL_ASK.md` is **not produced** for these founders. The assignment (Phase 9) is heavy on customer conversations or a shipped narrow test.

#### Claims-PMF / Fundraise-ready route

**Investor mirror (Phase 4-IM).** The partner-meeting rehearsal. Walk through the 10 canonical questions (Section 5.4 below). For each, the founder gives their answer, then receives push-back ("a partner will follow up with..."). Gaps go straight into `WHAT_INVESTORS_WILL_ASK.md`. The skill also pulls the moats-and-network-effects wiki here (only here — PMF-before-moat rule).

### Phase 4-IM appendix — The 10 partner-meeting questions

For Claims-PMF and Fundraise-ready routes only.

1. What is the problem, in one sentence?
2. Who has it? Who has it badly enough to pay?
3. What did you build? Why this wedge?
4. Show me retention. Show me cohorts.
5. What is the unit-economics story?
6. Why now?
7. Why you?
8. What is your moat going to look like in 24 months when 1,000x engineers can rebuild your stack in a weekend?
9. What are you raising and what does it buy?
10. What is the one thing that would kill this?

Each question has push-back rules that live verbatim in `investor-mirror.md`. The answers and the gaps (questions the founder cannot answer cleanly) populate `WHAT_INVESTORS_WILL_ASK.md`.

### Phase 5 — Strategy clarity check (all routes)

Roger Martin's Playing-to-Win, applied with the same rigor as the peer skill: winning aspiration → where to play → how to win → capabilities → management systems → what-must-be-true watchlist. Five "what must be true" buckets including production economics. Strictest on coherence, most forgiving on certainty.

The "Strategy is not planning" hard rule from peer's SKILL.md carries over verbatim. Every strategic choice gets backup logic.

For Claims-PMF / Fundraise-ready routes: the strategy section is populated with real data (cohort retention, unit econ, channel mix). For Searching / Approaching: the strategy is articulated as a set of hypotheses to test, with the test plan named explicitly.

### Phase 6 — Draft three artifacts internally

Draft `WHERE_YOU_ARE.md`, `WHAT_TO_DO_NEXT.md`, and (route-gated) `WHAT_INVESTORS_WILL_ASK.md` in scratch. No artifacts created in the conversation yet.

### Phase 7 — Autonomous C-criteria self-review

Five named, numbered, non-skippable passes over all drafts:

1. **Clarity** — plain language, no jargon, no fluff
2. **Justification** — every claim traceable to what the founder said
3. **Zero-hallucination** — nothing plausible-sounding but unsupported gets through
4. **Completeness** — all relevant sections populated, no gaps
5. **Cross-document consistency** — the three artifacts agree with each other

Run until a full sweep produces no substantive changes. Founder does not see this pass.

### Phase 8 — Create artifacts + read-back gate

Create the artifacts in the conversation (artifacts feature on claude.ai; written files in Claude Code). Walk the founder through each. Read-back gate: force them to articulate the load-bearing sections in their own words. Revise artifacts in place if the read-back reveals fuzziness.

### Phase 9 — Closing + The Assignment

One concrete real-world action for the week, **calibrated to route**:

- **Searching:** "Have 20 customer conversations this week. Bring me the verbatim quotes."
- **Approaching:** "Run the Sean Ellis 40% survey. Bring me the percentage and the segmentation by Friday."
- **Claims-PMF:** "Build the cohort retention dashboard. Send me the shape."
- **Fundraise-ready:** "Draft your one-pager and the 10-question answer doc. Send to three trusted operators for kill-shot feedback."

The non-negotiable handoff (replacing peer skill's "get the doc to your co-founder this week") is: the founder commits to a measurement and brings the result back next session.

## 6. Module files for the new skill

| File | Purpose | Source relative to peer skill |
|---|---|---|
| `SKILL.md` | Entry point + meta-instructions + hard rules | New, but structurally parallel to peer's SKILL.md |
| `README.md` | Public-facing skill description + install instructions | New |
| `ai-native-context.md` | AI-native operating substrate | **Verbatim copy** of peer's |
| `principles.md` | Operating principles + pushback patterns | **Verbatim copy** of peer's + 2 new principles (Section 4.4) |
| `diagnostic.md` | Phase 2: the 5 questions, scoring rubric, routing script, override protocol | NEW |
| `forcing-questions.md` | Adapted Mom-Test rigor for post-MVP (Phase 3.1) | Adapted: data-backed, not future-projected |
| `premise-and-alternatives.md` | Phase 3.3 | Adapted: post-MVP alternatives (Section 5.3) |
| `strategy.md` | Phase 5: Playing-to-Win refined with real data | Adapted: same framework, real-data inputs |
| `investor-mirror.md` | Phase 4-IM: 10 partner-meeting questions + push-back rules | NEW |
| `drafting-and-review.md` | Phases 6, 7, 8: drafting, C-criteria review, read-back | Adapted: three artifacts instead of two |
| `closing.md` | Phase 9: what I noticed + personal note + curated resources + the Assignment | Adapted: route-calibrated assignment |

## 7. The `moats-and-network-effects/` Karpathy-style wiki

Lives **verbatim in both** `non-tech-office-hours/` and `post-mvp-office-hours/`. Each skill owns its copy; edits do not auto-propagate.

### 7.1 Architecture (three layers)

Following Karpathy's LLM-wiki pattern: a knowledge base built for an LLM agent to read mid-conversation, not for human browsing.

```
moats-and-network-effects/
├── raw/                        ← immutable source documents
│   ├── nfx-network-effects-manual.md
│   └── yc-helmer-7-powers-transcript.md
├── wiki/                       ← agent-generated, one entity per file
│   ├── concepts/               ← canonical taxonomy + kill-tests
│   └── examples/               ← startup case studies for grounding
└── CLAUDE.md                   ← schema + navigation rules for the agent
```

### 7.2 Sources

Two sources only — no source proliferation:

1. **NFX Network Effects Manual** — scraped from `https://www.nfx.com/library` during implementation. Distinguish core taxonomy content (which feeds `wiki/concepts/`) from case-study content (which feeds `wiki/examples/`).
2. **Helmer's 7 Powers** — YC video transcript provided by user (not the book). One transcript file in `raw/`, one concept page in `wiki/concepts/` per power.

### 7.3 Wiki page principles

- **One entity per file.** Not one section of a document — one *concept* or one *case study*.
- **`[[wiki-links]]`** between pages. The agent walks the graph by following links, not full-text search.
- **Each page is interpretable standalone.** Source metadata, parent doc reference, and enough context that an agent landing mid-walk does not need to load the whole wiki.
- **No embeddings, no vector DB.** Structure does the work at this scale.

### 7.4 Skill behavior referencing the wiki

The skill's `CLAUDE.md` inside the wiki specifies two navigation rules for the agent:

- **Walk to `concepts/` pages** for definitions, kill-tests, and AI-native erosion checks when the founder claims a moat type.
- **Walk to `examples/` pages** when the founder cites a comparable company ("we are like Uber for X") — to challenge whether the analog holds at the mechanism level, not just the surface story.

### 7.5 Gating rule

The skill does not walk the wiki for Searching-route founders. Moat thinking is gated on Claims-PMF or Fundraise-ready route (PMF-before-moat hard rule, Section 4.4).

### 7.6 Bilateral updates to existing peer skill

Three additive edits to `non-tech-office-hours/` files (each a single cross-reference, not a structural change):

- `ai-native-context.md` — defensibility shift section gains a pointer: *"For the full taxonomy of network effects and Helmer's 7 Powers, see `moats-and-network-effects/CLAUDE.md`."*
- `strategy.md` — "how to win" section gains: *"When a strategic bet rests on a moat, name the moat type using Helmer's taxonomy. See `moats-and-network-effects/wiki/concepts/`."*
- `premise-and-alternatives.md` — when an alternative includes "build a moated version," require the founder to name the specific Helmer power and walk the wiki to confirm the mechanism.

All cross-references are **within-skill** (a skill referencing its own embedded wiki). No cross-skill references.

## 8. Decoupling rules (hard)

These rules are enforced on every implementation task:

1. **Each skill folder is self-contained.** Everything it needs lives inside its own folder.
2. **Each zip is independently buildable.** `zip -r <skill>.zip <skill>/` from the repo root produces a working, complete skill.
3. **No file inside either skill references the other skill.** Not `SKILL.md`, not `README.md`, not any phase module. The agent reading either skill should be unable to tell from the skill files alone that a peer exists.
4. **Cross-skill navigation lives only in the repo's top-level `README.md`** (Section 9), which sits above both skills and is excluded from both zips.
5. **Shared content is verbatim-duplicated, not symlinked or referenced.** `ai-native-context.md` and the entire `moats-and-network-effects/` directory exist as independent copies in each skill.
6. **Drift between copies is acceptable and expected.** Edits to one copy do not auto-propagate. The implementation plan must include explicit "sync both copies" steps when the shared content changes.

## 9. Top-level `README.md`

Lives at the repo root (`founder-office-hours/README.md`), not inside either skill's folder.

### Content outline

- **Header:** `# founder-office-hours` — one-paragraph framing (collection of Agent Skills for founders; office-hours methodology adapted from Garry Tan's gstack practice, made portable for any Claude-compatible environment).
- **The skills table** — two rows: peer skill (audience: non-technical founder pre-build, output: two artifacts) and new skill (audience: any founder post-MVP, output: three artifacts).
- **Download section** — two release-zip links, one per skill. Install instructions live inside each skill's own README.
- **What both skills share** — AI-native operating substrate, operating principles, Karpathy-style moats wiki (NFX + Helmer YC video), Playing-to-Win.
- **What's different** — peer is pre-build and business-only; new skill is post-ship with adaptive founder-type grilling.
- **Acknowledgments section** — explicit credits:
    - Garry Tan (office-hours format from YC and gstack work)
    - Y Combinator partners (Jessica Livingston, Paul Graham, Michael Seibel, Dalton Caldwell, et al.)
    - Roger Martin (Playing-to-Win framework)
    - Hamilton Helmer (7 Powers; accessed via YC video)
    - NFX / James Currier (Network Effects Manual + 16-types taxonomy)
    - Sean Ellis (40% PMF test)
    - Rahul Vohra (Superhuman PMF engine)
    - Rob Fitzpatrick (The Mom Test)
    - Diana Hu, YC (AI-native company framework)
    - Andy Rachleff (original PMF articulation)
    - Andrej Karpathy (LLM-wiki architecture)
- **License** — link to LICENSE at repo root.

## 10. Writing discipline (applied to every file produced)

Per user direction: with advanced models, prompt engineering = telling the AI very clearly what it should do while talking with founders. Every file follows these conventions:

- **Direct, imperative instructions.** "Do X. Push back on Y. Never do Z." Not "consider," not "you might want to."
- **Concrete scripts.** Where the AI needs to speak to the founder, the exact phrasing is in the file (the same way peer's SKILL.md scripts the conviction check verbatim).
- **Decision trees, not paragraphs.** Routing logic and pushback rules expressed as explicit "if X → do Y" rules.
- **Gates are named, numbered, and non-skippable.** Phase 7's C-criteria review, the read-back gate, the moat-gating-on-PMF rule, the technical-claim counter-grill — each has a clear identifier.
- **Bans are explicit and listed.** The skill's SKILL.md ban list includes: no code, no scaffolding, no technology choices when the founder is non-technical, no pre-AI-era timelines, no pushing moat thinking on Searching-route founders, no batching questions, no sycophantic re-routing.

## 11. Implementation prerequisites

Items required before implementation can fully proceed (to be sequenced in the writing-plans output):

1. **Helmer YC-video transcript** — user-provided. Without it, `raw/yc-helmer-7-powers-transcript.md` is empty and the wiki cannot be built.
2. **NFX Network Effects Manual scrape** — first implementation task. Scrape `https://www.nfx.com/library`, isolate the canonical manual document(s), distinguish core taxonomy from case studies.
3. **GitHub repo rename access** — `gh api` call to rename `adoistic/non-tech-office-hours` → `adoistic/founder-office-hours`. GitHub auto-redirects from old URLs.
4. **Removal of nested `.git/`** — the existing `non-tech-office-hours/` has its own `.git/`. After moving its contents into a `non-tech-office-hours/` subfolder under the renamed repo, the nested `.git/` is deleted (its history is preserved on GitHub via the rename).

## 12. Out of scope for this spec

- The actual content of the NFX scrape (deferred to implementation; the spec commits to the structure, not the content)
- The actual content of the Helmer wiki pages (deferred to implementation; user must provide the YC transcript first)
- Specific filenames inside `wiki/concepts/` and `wiki/examples/` (these emerge deterministically from the raw sources; the spec commits to the principle of one-entity-per-file)
- Any UI / client-side changes
- Anything inside any skill other than `non-tech-office-hours/` and `post-mvp-office-hours/`

## 13. Acceptance criteria

The work is complete when:

1. The GitHub repo is renamed to `founder-office-hours` and its layout matches Section 3.
2. The existing skill is fully functional from its new subfolder location, with the three light cross-reference edits applied.
3. The new `post-mvp-office-hours/` skill is fully populated per Sections 4–6, with the 5-question diagnostic, the 10-question investor mirror, the three artifacts logic, the C-criteria review, and the route-calibrated assignment all in place.
4. Both copies of `moats-and-network-effects/` exist with `raw/` (containing both sources), `wiki/concepts/` (one page per network-effect type and per Helmer power), `wiki/examples/` (case studies), and `CLAUDE.md` (navigation rules).
5. The top-level README explains both skills and lists all acknowledgments per Section 9.
6. Two release zips can be built independently and each is a functional skill.
7. No file inside either skill references the peer skill.
8. The spec review loop has approved this design and the user has reviewed the written spec.
