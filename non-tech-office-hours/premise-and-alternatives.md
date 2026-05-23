# Premise Challenge & Alternatives

Run both of these before writing the artifact drafts. Neither is skippable.

---

## Phase 3 — Premise Challenge

Before proposing solutions, surface the premises the founder is operating on. They are usually invisible to the person holding them. Your job is to drag them into daylight and force the founder to either agree explicitly or rethink.

Ask yourself, then surface to the founder:

1. **Is this the right problem?** Could a different framing yield a dramatically simpler or more useful solution?
2. **What happens if we do nothing?** Real pain point, or hypothetical one?
3. **What existing tools or workarounds already partially solve this?** Map what could be reused, partnered with, or stitched together — don't reinvent.
4. **Who pays, and why now?** What's the moment in their week, quarter, or fiscal year when they would actually take out a card?
5. **What does the founder believe about the customer that they have not tested?** The most dangerous premises are the unstated ones.
6. **What about distribution?** How does the customer find out this exists? Who tells them? Where do they look when the pain hits?
7. **If the deliverable is something the technical co-founder builds, how does the customer get their hands on it?** App store? Direct URL? Sales call? Word of mouth? Code without distribution is code nobody uses.

### Stricter rule: 5-7 premises, not 3-5

Each premise must be a statement that, **if wrong, would change the design.** "Users want a fast app" is not a premise — it's a truism. "Customers will pay $99/month rather than $49 because compliance officers will fight for the higher tier" is a premise. "The wedge is the weekly summary email, not the dashboard" is a premise.

Output them as a numbered list, each phrased as a clear declarative the founder can either agree with or push back on:

```
PREMISES:
1. [declarative statement] — do you agree?
2. [declarative statement] — do you agree?
3. [declarative statement] — do you agree?
4. [declarative statement] — do you agree?
5. [declarative statement] — do you agree?
```

### The agree-back gate

For each premise, ask the founder to **rephrase it in their own words** before they agree. If they cannot, the premise is not yet shared understanding — it's just words on a screen. Push again.

If they disagree with a premise, **revise your understanding** and loop back. Don't paper over disagreement. A premise the founder doesn't actually believe is a landmine the technical co-founder will step on next month.

### Common premises worth surfacing — non-technical founder edition

- The customer is willing to change their existing workflow (most aren't, unless the pain is severe).
- The customer can be reached cheaply (most can't, unless distribution is solved).
- The customer pays directly (vs. their boss, their company, their insurance, their advertiser).
- The wedge is something the technical co-founder can ship in ≤ 4 weeks.
- The first 10 customers can be acquired by hand, not by funnel.
- There is a single "trigger moment" when the customer realizes they need this.
- The founder is the right person to sell this (industry, network, story).

### Common premises worth surfacing — AI-native edition

These are specific to the operating environment described in [ai-native-context.md](ai-native-context.md). Most founders are operating under these implicitly without having articulated them. Drag them into daylight.

- **The production-economics premise.** "We're betting that AI-native build economics — token-maxing, software factories — let us ship and iterate substantially faster than incumbents. If we end up running on pre-AI-era economics, this strategy fails."
- **The closed-loop-as-moat premise.** "We're betting the data we accumulate from our own queryable operations becomes a moat — competitors without the same closed loop fall behind. If most customer-relevant data lives outside our reach or our competitors can replicate the loop quickly, this isn't defensible."
- **The incumbent-vulnerability premise** (RFS 2 plays specifically). "We're betting the legacy SaaS incumbent in this space genuinely can't move — that their codebase and SOPs are heavy enough that they can't ship an AI-native version in time. If they spin up a skunkworks team and ship in 12 months, we lose our window."
- **The wedge-shape premise.** "We're betting the right wedge is [no-code / software-factory] rather than the other. If demand turns out to require the other shape, we have to redo the build approach."
- **The conviction premise.** "We're betting the founder personally develops conviction with AI tooling and remains the AI Founder archetype. If the founder delegates AI strategy to the technical co-founder, the company stops being AI-native at the leadership level."

Surface the ones that apply. Don't force premises that don't fit the founder's situation.

---

## Phase 4 — Alternatives Generation (MANDATORY, MINIMUM 3)

Produce **3 distinct approaches.** Not 2. Three is the minimum here — because for a non-technical founder, the cost of skipping an alternative is that the technical co-founder builds the obvious one before anyone has thought about the unobvious one.

### Format

```
APPROACH A: [Name]
  Summary (plain English, 1-2 sentences):
  What the customer experiences:
  What the founder does this week to test it:
  What the technical co-founder builds (high level, no jargon):
  Effort:  [S / M / L]
  Risk:    [Low / Med / High]
  Pros:    [2-3 bullets]
  Cons:    [2-3 bullets]

APPROACH B: [Name]
  ...

APPROACH C: [Name]
  ...

RECOMMENDATION: [X] because [one-line reason tied to the founder's stated goal]
```

### The required shape of the three approaches

One must be the **"no-code" / manual / concierge approach.** What if the technical co-founder builds nothing for the first 10 customers, and the founder runs it manually? Spreadsheets, emails, phone calls, hand-edited PDFs. This is not a failure mode — it is how most product companies actually start, and it gives the technical co-founder the gift of building the right thing instead of the imagined thing.

One must be the **"minimum viable build"** — the smallest thing the technical co-founder could ship in 2-4 weeks using AI-native build economics (software factory, agent fleet). In 2026 this is dramatically smaller than the same option looked in 2023; calibrate accordingly. See [ai-native-context.md](ai-native-context.md) if you find yourself thinking in pre-AI-era timelines.

One must be the **"ideal architecture" or the "AI-native rebuild" or "creative/lateral."** Often the most interesting version is none of:
- A SaaS app that customers log into
- A copy of the incumbent's product but cheaper

…and instead:
- A **closed-loop agent system** that watches the customer's existing workflow (in Slack, in their ERP, in their email) and acts on it without requiring them to change anything.
- A **service-as-software** play where the founder + AI agents deliver the outcome directly (Cranston's accounting model), not a tool the customer operates.
- A **layer on top of the incumbent** that absorbs the work humans do today (Burnt's pattern), leaving the incumbent's system in place but quietly hollowing it out.

For founders attacking RFS 2 categories (legacy SaaS incumbents), the AI-native-rebuild option is often the *recommended* one, not the creative add-on. Push the founder to consider whether it's the right shape before defaulting to "we'll build a SaaS app."

If a chosen alternative claims a moat, walk `moats-and-network-effects/wiki/concepts/` to name the specific Helmer power or NFX network-effect type, and confirm the mechanism is real, not aspirational.

### Avoid these failure modes

- **Three flavors of the same thing.** "Mobile app vs. web app vs. desktop app" is one approach with cosmetic variation. The founder will see through it.
- **A strawman option.** Don't include an obviously-bad approach just to make your favorite look good.
- **Hedging the recommendation.** Pick one. Say why. Use the founder's stated goal as the reason. If you can't pick, the alternatives aren't differentiated enough.
- **Implementation creep in the descriptions.** Each approach should be described in business / customer terms — what the customer sees, not what gets built. The "what the technical co-founder builds" line should be one sentence at most, and free of jargon.

### Why the no-code option matters here

For a non-technical founder, the worst outcome of these sessions is: "we agreed on the plan, my co-founder started building, and three months later we realized nobody wanted it." The no-code option is the antidote. It is the version where you find out in 2 weeks instead of 3 months, by doing the work yourself.

If the founder rejects the no-code option, push: "What specifically about this product cannot be tested by hand first?" Often the answer reveals that the technical part is the founder's *comfort*, not the customer's *need*.

### STOP HERE

After presenting the approaches and recommendation, **wait for the founder to choose** before moving to strategy. Even if your recommendation seems obviously right, the founder must explicitly pick. Writing the artifact draft without explicit approval is the failure mode this gate prevents.

A typical response is "go with A" or "I want B but with C's distribution plan." Both are valid. Loop back briefly to confirm any merged version, then proceed.

---

## After alternatives are approved

Move to **Phase 4 — Strategy** ([strategy.md](strategy.md)). The alternative the founder picked is *how* they will execute. The strategy phase is the bet about *why* it wins on a chosen playing field — and the logic that must hold for the bet to land. Without the strategy, the chosen approach is a plan, not a strategy. Don't let the founder skip past it.
