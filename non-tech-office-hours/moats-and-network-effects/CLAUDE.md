# moats-and-network-effects — Wiki Schema

This is an LLM-readable wiki, not a human-readable document set. The agent
(SKILL.md, phase modules) walks this graph during the defensibility grill
phase to look up moat types, kill-tests, and case studies.

## Architecture

Three layers:

- `raw/` — immutable source documents. Never edit these. New ingestion
  goes here as new files; existing files are not modified.
- `wiki/concepts/` — one entity per file, canonical taxonomy. The agent
  walks here for definitions and kill-tests.
- `wiki/examples/` — one startup case study per file. The agent walks
  here when the founder cites a comparable company, to challenge the analog.

## When to walk which directory

**Walk `wiki/concepts/`** when:
- The founder claims a specific moat type ("we have network effects").
  Pull the canonical definition and the kill-test. Push back if the
  claimed mechanism does not match the canonical mechanism.
- The founder asks "what kind of moat is this." Walk to the closest
  matching concept page and explain in plain language.
- The defensibility grill needs to test whether a claimed moat survives
  the AI-native cost collapse. Walk to `ai-native-moat-shift.md`.

**Walk `wiki/examples/`** when:
- The founder cites a comparable ("we are like Uber for X"). Walk to the
  matching example page. Compare the founder's mechanism to the example's
  mechanism. If the analog fails at the mechanism level, push back.
- The founder needs grounding for an abstract concept. Pull one or two
  example pages alongside the concept page.

## When NOT to walk this wiki

**Do not walk the wiki for Searching-route founders** (PMF-before-moat
hard rule, per SKILL.md). A Searching-route founder asking about moats
is procrastinating on PMF. Redirect to customer-pulse questions.

## Page template — concepts

Every concept page MUST follow this structure exactly:

```
# <Concept Name>

**Category:** <e.g., 2-Sided Network Effects, or Helmer Power>
**Source:** <raw/<filename>.md, section anchor>

## Definition

<One paragraph in plain language. No jargon.>

## Mechanism

<2-3 bullets. The specific cause-and-effect that produces defensibility.>

## When it applies

<2-3 bullets. The conditions under which a startup can claim this moat.>

## Kill-test

<One question or test the agent uses to falsify a founder's claim of
this moat type. Concrete. Either passes or fails.>

## AI-native erosion check

<One paragraph. Has 1,000x engineering capacity + software factories
made this moat easier or harder to build in 2026 than in 2023? If
easier, the moat has eroded — explain how.>

## Related concepts

- [[other-concept-name]]
- [[other-concept-name]]

## Case studies

- [[examples/<startup>-<concept>]]
- [[examples/<startup>-<concept>]]
```

## Page template — examples

Every example page MUST follow this structure exactly:

```
# <Startup> — <Concept Name>

**Concept:** [[<concept-page-name>]]
**Source:** <raw/<filename>.md, section anchor>

## What they built

<2-3 sentences. The product and the customer.>

## The mechanism

<2-3 bullets. The specific way the concept manifests in this startup.>

## Why the analog often fails

<One paragraph. The most common way a founder uses this comparable
incorrectly. The agent uses this when the founder says "we're like
<startup> for X.">

## Related examples

- [[examples/<other-startup>-<other-concept>]]
```

## Linting rules

Run periodically (manual for now; automated later):

1. Every concept page has all 7 required sections (Definition, Mechanism,
   When it applies, Kill-test, AI-native erosion check, Related concepts,
   Case studies).
2. Every example page has all 4 required sections.
3. Every `[[wiki-link]]` resolves to an actual file.
4. No concept page exceeds 400 words. Brevity is the point.
5. No example page exceeds 300 words.
