# non-tech-office-hours

An Agent Skill for Claude. Office hours methodology for a non-technical founder paired with a technical co-founder, building a tech startup in the AI-native era of 2026.

Pushes hard on specificity, behavioral evidence, and strategic coherence (Roger Martin's Playing-to-Win framework). Calibrates to AI-native production economics (software factories, token-maxing, closed-loop ops). Refuses to drift into technology choices — those belong to the technical co-founder, in their own session.

## What you get out of a session

Two markdown artifacts, created in the conversation and downloadable as `.md` files (or shareable via published link):

1. **`FOR_YOU.md`** — the founder's owned ground. Problem, customer, demand, wedge, premises, strategy (winning aspiration → where to play → how to win → capabilities → management systems → what-must-be-true watchlist), distribution, pricing, success criteria, the week's assignment.

2. **`FOR_YOUR_CO_FOUNDER.md`** — the technical co-founder's input document. Every workflow described in absolute detail (trigger → steps in plain English → ASCII flowchart → edge cases → success criteria), plus the operating-model decisions the founder owns (closed-loop ops position, token-spend position, three-archetype team shape, dashboards from week one), plus explicitly-out-of-scope items and parked technical questions for the co-founder's own brainstorming. No tech stack. No framework choices. No architecture. Those are the co-founder's call.

## How it's different

- **One question at a time, pushed at least twice.** No batching.
- **No vague answers.** "Small businesses" gets pushed until you name a specific human.
- **Behavior beats interest.** Waitlists, "people love it," "VCs are excited" — none of it counts.
- **Strategy is held to a different standard.** The strategy phase is the strictest on coherence and most forgiving on certainty. You can't prove a strategy in advance — but you have to articulate it cleanly, with the logic that backs every choice.
- **AI-native by default.** Calibrated to 2026 production economics (1,000x engineers, software factories, closed-loop ops, token-maxing). The wedge question now has two real shapes: no-code/manual AND software-factory build, both ship-able in seven days.
- **Autonomous self-review before you see anything.** After drafting the two artifacts internally, the partner runs five named passes (clarity, justification, zero-hallucination, completeness, cross-document consistency) before any artifact is created. Anything plausible-sounding but not traceable to what you actually said gets removed.
- **Two artifacts, not one chat dump.** The output is created using Claude.ai's artifacts feature — downloadable, publishable, editable across turns.

## Installation

### Claude Code (CLI / desktop)

Copy the entire `non-tech-office-hours/` directory into your skills folder:

```sh
cp -r non-tech-office-hours ~/.claude/skills/
```

Then invoke from any Claude Code session:

```
/non-tech-office-hours
```

Or just describe your situation — Claude will auto-load the skill when the description in `SKILL.md`'s frontmatter matches what you're doing.

### Claude.ai (web app)

Two ways:

**As a Project.** Create a new Project in Claude.ai. Upload all the markdown files in `non-tech-office-hours/` to the project. Open a chat in the project and say:

> Run office hours on this idea. Start by reading `SKILL.md`.

The project files load automatically into every chat in that project. Claude will read SKILL.md first, then the supporting files as instructed.

**Ad hoc upload.** Attach all the `.md` files to a new conversation and tell Claude to start by reading `SKILL.md`. Works the same way; you just lose project-scoped persistence.

### Claude Desktop

If you have Claude Desktop with skills installed, drop the `non-tech-office-hours/` folder into your skills directory. Format and behavior are identical to Claude Code.

## Files

| File | Purpose |
| --- | --- |
| [SKILL.md](SKILL.md) | Entry point. YAML frontmatter + meta-instructions. Read first. |
| [principles.md](principles.md) | Nine operating principles, eight pushback patterns, anti-sycophancy rules, the "answer it back" gate. |
| [ai-native-context.md](ai-native-context.md) | Operating substrate. Teaches the partner the AI-native shift, closed-loop framework, software factories, token-maxing, three archetypes, the two YC Summer 2026 RFSes, the defensibility shift, and Claude's own AI-timeline-estimation weakness with the corrective rule. Read before any phase. |
| [forcing-questions.md](forcing-questions.md) | The six forcing questions with stricter pass criteria. Q4 (wedge) covers both no-code and software-factory shapes. |
| [premise-and-alternatives.md](premise-and-alternatives.md) | Premise challenge (5–7 premises, including AI-native premises) + three forced alternatives (no-code, AI-native minimum build, AI-native rebuild / lateral). |
| [strategy.md](strategy.md) | Roger Martin's Playing-to-Win framework. The defensibility list ("lines of code is no longer a moat") updated for AI-native. Five buckets in what-must-be-true, including production economics. |
| [drafting-and-review.md](drafting-and-review.md) | **Three phases:** Phase 5 drafts both artifacts internally. Phase 6 runs five autonomous review passes. Phase 7 creates the artifacts in the conversation and runs the read-back gate. Templates for both `FOR_YOU.md` and `FOR_YOUR_CO_FOUNDER.md` are inside. |
| [closing.md](closing.md) | What I noticed about how you think + a personal note + curated resources + the non-negotiable handoff (get the co-founder doc to your co-founder this week). |

## Trigger phrases

The skill is designed to activate when any of these come up:

- "I have an idea"
- "Help me think through my startup"
- "I want to plan what to build"
- "Office hours"
- "I'm not sure what to tell my co-founder yet"
- "Can we work through what I'm building?"

Any session where customer clarity, wedge definition, or strategic articulation is the bottleneck.

**Do NOT use this skill when:**
- The founder is already past business clarity and wants implementation help. (This skill stays on the business side; redirect technical questions to the co-founder's own brainstorming.)
- The founder is asking for code, a tech stack recommendation, or a deployment plan. (This skill explicitly does not produce those.)
- The founder has no technical co-founder and is trying to figure out how to build alone. (This skill's whole premise is the founder/co-founder division of labor.)

## Credit and source material

- Forcing-questions methodology draws on YC-style office-hours practice and Rob Fitzpatrick's *Mom Test* approach to customer discovery.
- Strategy phase uses Roger Martin's *Playing to Win* framework.
- AI-native operating context distills Diana Hu's framework for AI-native companies, the YC Summer 2026 Requests for Startups (the closed-loop / company-legible-to-AI thesis and the AI-native challenger thesis), and the 1,000x engineer claim from OpenAI's application infrastructure team.
- The AI-timeline-estimation corrective is grounded in the 2025 research paper *"Can LLMs Perceive Time?"* and the structural observation that AI models cannot estimate AI-assisted task durations from pre-AI-era training data.

## Version

1.0.0 — initial release.
