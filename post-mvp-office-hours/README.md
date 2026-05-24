# post-mvp-office-hours

An Agent Skill for Claude. Office hours methodology for any founder — technical or non-technical, solo or co-founded — who has shipped a product and needs an honest read on where they stand, what to do next, and (if the data supports it) how to survive a partner meeting.

**[Download the latest skill bundle (.zip)](https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip)** — see installation below. On claude.ai web, upload the zip as-is via Customize → Skills. On Claude Code or any other coding agent, ask the agent to install it from the link.

Runs a 4-segment diagnostic (Searching / Approaching / Claims-PMF / Fundraise-ready) before any strategy work. Calibrated to AI-native production economics. Adversarial by design — data exists at this stage, which makes deflection easier and honesty rarer. This skill does not let either slide.

## What you get out of a session

Three markdown artifacts, created in the conversation and downloadable as `.md` files:

1. **`WHERE_YOU_ARE.md`** (always produced) — PMF placement against the 4-segment spectrum, with the specific signals that determined it. Real vs. vanity metric breakdown. A defensibility check (route-gated section for Claims-PMF and Fundraise-ready only). A kill list of the assumptions that did not survive the session.

2. **`WHAT_TO_DO_NEXT.md`** (always produced) — the headline move: one thing, justified. Supporting work ranked by impact. A 90-day falsification window with a specific milestone. Abandon conditions — the signals that would make the current bet wrong. Route-calibrated to where the diagnostic placed you.

3. **`WHAT_INVESTORS_WILL_ASK.md`** (Claims-PMF and Fundraise-ready routes only) — 10 partner-meeting questions, asked one at a time with pushbacks harsher than the diagnostic. For each question: the founder's draft answer, the likely push-back from a partner, and any gap that needs to close before the meeting. This artifact is never produced for Searching or Approaching founders — they are not ready for it, and producing it would be a form of flattery.

## How it's different

- **Diagnostic-first.** A 5-question intake (Phase 2) places the founder on the 4-segment spectrum before any strategy work begins. No placement, no strategy. This phase is non-skippable.
- **Harder grilling because data exists.** At post-MVP, founders can wave at dashboards, cite vanity metrics, and deflect to recent feature work. This skill applies Principle 10 (Reality before projection): behavioral data beats user interviews beats founder narrative beats slide-deck claims. When the founder projects, the skill names it.
- **Adaptive on founder type.** The session calibrates to technical or non-technical founder. For technical founders, a counter-grill runs on every architectural claim about uniqueness, difficulty to build, or moat — testing cost-to-replicate today (not 2023), whether the moat is in code or in data/distribution/network effects, patent exposure, and counter-architecture risk.
- **Route-gated investor mirror.** Phase 4-IM (the 10-question partner-meeting simulation) runs only for Claims-PMF and Fundraise-ready routes. Searching and Approaching founders skip it automatically — this is not an option they can override.
- **PMF before moat.** The moats-and-network-effects wiki (NFX + Helmer 7 Powers) is available but walked only for Claims-PMF and Fundraise-ready routes. Moat thinking before PMF is a distraction; this skill enforces that.
- **3 artifacts instead of 2.** The third artifact (investor mirror prep) is route-gated and reflects real diagnostic placement — not aspirational placement.
- **Autonomous self-review before you see anything.** Phase 7 runs five explicit, non-skippable passes (clarity, justification, zero-hallucination, completeness, cross-document consistency) over all drafted artifacts before any of them are created. You do not see this pass. Nothing plausible-sounding but untraceable to what you actually said survives it.

## Installation

### Claude.ai (web app)

1. Download the [skill zip](https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip).
2. In claude.ai, open **Customize → Skills** (Customize is in your settings / sidebar).
3. Click the **+** button at the top of the Skills panel.
4. Choose **Create skill → Upload a skill**.
5. **Upload the zip file as-is — do not unzip it.** Claude.ai unpacks it for you.
6. Start a new chat and trigger the skill by saying something like: *"Run post-MVP office hours. Start by reading SKILL.md."*

### Claude Code, Codex, Cursor, or any other coding agent

Easiest path: tell the agent to install it for you. Paste this link and say *"install this skill for me"*:

```
https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip
```

The agent will download, unzip, and place the skill in the right directory for whichever environment you're in.

### Manual install (Claude Code / Claude Desktop)

```sh
curl -L https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip -o /tmp/skill.zip
unzip /tmp/skill.zip -d ~/.claude/skills/
rm /tmp/skill.zip
```

Then invoke with `/post-mvp-office-hours` from any Claude Code session, or just describe the founder's situation — Claude will auto-load the skill when the description matches.

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Entry point, hard rules, phase order |
| [ai-native-context.md](ai-native-context.md) | AI-native operating substrate (1,000x engineers, defensibility shift, timeline corrective) |
| [principles.md](principles.md) | 11 operating principles + anti-sycophancy rules + 8 pushback patterns |
| [diagnostic.md](diagnostic.md) | Phase 2: 5 questions, 4-segment scoring, route announcement |
| [forcing-questions.md](forcing-questions.md) | Phase 3.1: 6 forcing questions adapted for data-backed answers |
| [premise-and-alternatives.md](premise-and-alternatives.md) | Phase 3.2: premise challenge + 6-alternative post-MVP menu |
| [investor-mirror.md](investor-mirror.md) | Phase 4-IM (route-gated): 10 partner-meeting questions |
| [strategy.md](strategy.md) | Phase 5: Playing-to-Win refined with real data, 90-day falsification windows |
| [drafting-and-review.md](drafting-and-review.md) | Phases 6-8: drafting 3 artifacts, C-criteria review, read-back gate |
| [closing.md](closing.md) | Phase 9: route-calibrated assignments and curated resources |
| [moats-and-network-effects/](moats-and-network-effects/) | Karpathy-style wiki on moats (NFX + Helmer 7 Powers). Walked only for Claims-PMF / Fundraise-ready routes. |

## Trigger phrases

The skill is designed to activate when any of these come up:

- "I've shipped, now what"
- "is this PMF?"
- "should I raise?"
- "what would a partner ask me?"
- "post-MVP office hours"
- "review my fundraise readiness"
- "investor mirror"
- "diagnose my startup"

## Do NOT use this skill when

- You haven't shipped anything yet — use a pre-build office-hours skill or brainstorming first.
- You need code, scaffolding, or technical implementation help — this skill stays on business and strategy.
- You want validation rather than honest diagnosis — this skill is adversarial by design, and will push back on narrative that isn't grounded in behavioral data.
- You're looking for a TAM analysis or market sizing exercise — this skill grounds in observed cohorts and real users, not slide-deck projections.

## Credit and source material

- Garry Tan (office-hours format from YC and gstack)
- YC partners: Jessica Livingston, Paul Graham, Michael Seibel, Dalton Caldwell
- Roger Martin (*Playing to Win* framework — used in Phase 5 and the strategy artifact)
- Hamilton Helmer (*7 Powers*, accessed via YC video — used in the moats wiki)
- NFX / James Currier (Network Effects Manual + 16-types taxonomy — used in the moats wiki)
- Sean Ellis (40% PMF test — informs diagnostic segment placement)
- Rahul Vohra (Superhuman PMF engine — informs the Claims-PMF diagnostic segment)
- Rob Fitzpatrick (*The Mom Test* — informs forcing-questions and customer-conversation pushbacks)
- Diana Hu, YC (AI-native company framework — used in ai-native-context.md)
- Andy Rachleff (original PMF articulation — informs the 4-segment spectrum)
- Andrej Karpathy (LLM-wiki architecture — used for the moats-and-network-effects module structure)

## Version

v2.0.0
