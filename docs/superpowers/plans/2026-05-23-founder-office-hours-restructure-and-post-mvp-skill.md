# founder-office-hours Restructure + post-mvp-office-hours Skill Implementation Plan

> **For agentic workers:** REQUIRED: Use superpowers:subagent-driven-development (if subagents available) or superpowers:executing-plans to implement this plan. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rename the existing GitHub repo to `founder-office-hours`, fold the existing skill into a self-contained subfolder, and add a fully decoupled peer skill `post-mvp-office-hours` alongside it. Both skills share a verbatim-duplicated Karpathy-style wiki on moats and network effects.

**Architecture:** One git repo, two self-contained skill subfolders, each independently zippable. Shared content (`ai-native-context.md`, the moats wiki) lives as verbatim copies inside each skill — no symlinks, no submodules, no cross-references. The new skill follows the peer's phase scaffolding (substrate reads → reflection → forcing questions → premise/alternatives → strategy → drafting → autonomous review → read-back gate → closing) but adds a 5-question diagnostic at the front and a 10-question investor mirror as a route-gated branch.

**Tech Stack:** Markdown files, git, GitHub CLI (`gh`), `zip`, Python or shell for parsing the NFX HTML (BeautifulSoup or Pandoc). No application code. No tests in the traditional sense — verification is structural (does the zip build cleanly? does the wiki have the expected page count? does the SKILL.md frontmatter pass the 1024-char limit?).

**Spec reference:** `docs/superpowers/specs/2026-05-23-founder-office-hours-restructure-and-post-mvp-skill-design.md`

**Source-of-truth files to read before starting:**
- The spec (above)
- `non-tech-office-hours/SKILL.md` (the peer skill's entry point — shapes the new skill's parallel structure)
- `non-tech-office-hours/principles.md` (verbatim-copied into new skill + 2 new principles appended)
- `non-tech-office-hours/ai-native-context.md` (verbatim-copied into new skill)
- `non-tech-office-hours/forcing-questions.md`, `premise-and-alternatives.md`, `strategy.md`, `drafting-and-review.md`, `closing.md` (each adapted for post-MVP)

**Prerequisites to confirm before starting:**
1. Adnan has push/admin access to `adoistic/non-tech-office-hours` (needed for `gh api` rename).
2. Adnan has provided the Helmer 7 Powers YC video transcript (without it, the wiki is incomplete — but Chunks 1, 2 (NFX portion), and 5 can proceed without it; Helmer wiki population blocks until the transcript lands).

---

## Chunk 1: Repo restructure plumbing

Restructure the existing repo so the current skill content moves into a `non-tech-office-hours/` subfolder, then add the top-level scaffolding (README, LICENSE at root, archive/, docs/ already exists). Verify the existing skill still works from its new path before touching anything else.

### Task 1.1: Confirm prerequisites and snapshot current state

**Files:**
- Read: `/Users/siraj/office bhours/non-tech-office-hours/` (current state)
- Read: `/Users/siraj/office bhours/non-tech-office-hours/.git/config`

- [ ] **Step 1: Confirm push/admin access to the GitHub repo**

Run:
```bash
gh api repos/adoistic/non-tech-office-hours --jq '.permissions'
```
Expected: JSON showing `admin: true`. If false, STOP and surface to Adnan.

- [ ] **Step 2: Snapshot current branch and state**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git status && git branch --show-current && git log --oneline -10
```
Expected: clean working tree (or only the spec + plan committed), on `main`, recent commits include the spec.

- [ ] **Step 3: Tag the pre-restructure state for rollback safety**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git tag pre-restructure-v1.0.0 && git push origin pre-restructure-v1.0.0
```
Expected: tag pushed. If anything goes sideways during the restructure, `git reset --hard pre-restructure-v1.0.0` recovers cleanly.

### Task 1.2: Move existing skill files into `non-tech-office-hours/` subfolder

**Files:**
- Modify (move): all top-level files in the repo into a new `non-tech-office-hours/` subdir, EXCEPT `LICENSE` (stays at root), `docs/` (stays at root), `.git/` and `.gitignore`.

Files that move into `non-tech-office-hours/`:
- `SKILL.md`
- `README.md`
- `ai-native-context.md`
- `principles.md`
- `forcing-questions.md`
- `premise-and-alternatives.md`
- `strategy.md`
- `drafting-and-review.md`
- `closing.md`

- [ ] **Step 1: Create the target subfolder**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && mkdir non-tech-office-hours
```

- [ ] **Step 2: `git mv` each skill file into the subfolder**

Run (each command individually so the operation is auditable):
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && \
git mv SKILL.md non-tech-office-hours/ && \
git mv README.md non-tech-office-hours/ && \
git mv ai-native-context.md non-tech-office-hours/ && \
git mv principles.md non-tech-office-hours/ && \
git mv forcing-questions.md non-tech-office-hours/ && \
git mv premise-and-alternatives.md non-tech-office-hours/ && \
git mv strategy.md non-tech-office-hours/ && \
git mv drafting-and-review.md non-tech-office-hours/ && \
git mv closing.md non-tech-office-hours/
```
Expected: 9 files moved, history preserved.

- [ ] **Step 3: Verify the move via git status and tree**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git status && ls -la non-tech-office-hours/
```
Expected: 9 renames listed; subfolder contains all 9 files; root is clean of skill files.

- [ ] **Step 4: Commit the move**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git commit -m "$(cat <<'EOF'
restructure: move skill files into non-tech-office-hours/ subfolder

Prepares the repo to host multiple skills as peer subfolders. The
existing skill is now self-contained under non-tech-office-hours/.
History preserved via git mv.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Task 1.3: Add the top-level scaffolding

**Files:**
- Create: `/Users/siraj/office bhours/non-tech-office-hours/README.md` (NEW top-level)
- Create: `/Users/siraj/office bhours/non-tech-office-hours/archive/` directory (for the old numbered drafts)

- [ ] **Step 1: Move the working-directory numbered drafts into archive/**

The old `00_START_HERE.md` … `07_CLOSING.md` source-of-thought files live in `/Users/siraj/office bhours/` (the parent working directory), not in the repo. Move them into the repo's new `archive/` subdir.

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && mkdir archive && cd .. && mv 00_START_HERE.md 01_PRINCIPLES.md 02_AI_NATIVE_CONTEXT.md 03_STARTUP_MODE.md 04_PREMISE_AND_ALTERNATIVES.md 05_STRATEGY.md 06_DESIGN_DOC.md 07_CLOSING.md README.md "non-tech-office-hours/archive/"
```
Expected: 9 files moved into the repo's `archive/` folder; the parent working directory's `non-tech-office-hours.zip` stays put (it's the v1.0.0 release artifact).

- [ ] **Step 2: Write the top-level README.md**

Create `/Users/siraj/office bhours/non-tech-office-hours/README.md` (yes, the path is awkward because the repo is still named `non-tech-office-hours` locally — that gets renamed at the end of Chunk 1). Content follows the spec's Section 9 outline:

```markdown
# founder-office-hours

A collection of Agent Skills for founders. Office-hours methodology
adapted from Garry Tan's gstack practice, made portable so it works
in any Claude-compatible environment — claude.ai, Claude Code,
Codex, Cursor.

## The skills

| Skill | For | What you walk out with |
| --- | --- | --- |
| [non-tech-office-hours](non-tech-office-hours/) | Non-technical founder paired with a technical co-founder, pre-build | Two artifacts: `FOR_YOU.md` (your owned ground) + `FOR_YOUR_CO_FOUNDER.md` (workflows + operating-model decisions) |
| [post-mvp-office-hours](post-mvp-office-hours/) | Any founder, post-MVP, figuring out PMF and investor-readiness | Three artifacts: `WHERE_YOU_ARE.md` + `WHAT_TO_DO_NEXT.md` + `WHAT_INVESTORS_WILL_ASK.md` (the last gated by PMF route) |

## Download

Each skill ships as its own zip from GitHub Releases:

- [non-tech-office-hours.zip (latest)](https://github.com/adoistic/founder-office-hours/releases/latest/download/non-tech-office-hours.zip)
- [post-mvp-office-hours.zip (latest)](https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip)

Install instructions live inside each skill's own README.

## What both skills share

- Same AI-native operating substrate (1,000x engineers, software factories, closed-loop ops, the defensibility shift, AI-timeline corrective)
- Same operating principles (one question at a time, anti-sycophancy, "answer it back" gate, eight pushback patterns)
- Same Karpathy-style wiki on moats and network effects, embedded verbatim in both — NFX Manual + Helmer's 7 Powers (YC video) distilled into `concepts/` and `examples/` pages
- Same Roger Martin "Playing to Win" strategy framework — strategy is not planning; every choice gets backup logic

## What's different

- `non-tech-office-hours` is **pre-build, business-side only**. It refuses to drift into technology choices — those belong to the co-founder.
- `post-mvp-office-hours` is **post-ship**. The founder has data (or admits the absence of it). Grilling is harder because the founder can no longer hide behind "we will" — only "we did" or "we haven't measured." Technical founders get counter-grilled on architecture claims using the AI-native cost collapse.

## Acknowledgments

- **Garry Tan** — the office-hours format and questioning cadence are adapted from his YC and gstack work.
- **Y Combinator partners** (Jessica Livingston, Paul Graham, Michael Seibel, Dalton Caldwell, and many others) — the underlying YC office-hours methodology this builds on.
- **Roger Martin** — the *Playing to Win* strategy framework that shapes the strategy phase in both skills.
- **Hamilton Helmer** — the *7 Powers* framework, accessed via the YC video he gave on it.
- **NFX (James Currier and team)** — the *Network Effects Manual* and the 16-types taxonomy.
- **Sean Ellis** — the "40% very disappointed" PMF test.
- **Rahul Vohra** — the Superhuman PMF engine, the practical use of the Ellis test.
- **Rob Fitzpatrick** — *The Mom Test*, customer-discovery rigor.
- **Diana Hu (YC)** — the AI-native company framework.
- **Andy Rachleff** — the original articulation of product-market fit.
- **Andrej Karpathy** — the LLM-wiki architecture used for the moats module.

## License

[MIT](LICENSE)
```

- [ ] **Step 3: Verify LICENSE is at repo root**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && ls LICENSE non-tech-office-hours/LICENSE 2>/dev/null
```
Expected: `LICENSE` at root exists (it should — it was already at the repo root, not moved in Task 1.2). If `non-tech-office-hours/LICENSE` accidentally got created from a duplicate, remove it.

If LICENSE is somehow inside the subfolder instead of root:
```bash
git mv non-tech-office-hours/LICENSE LICENSE
```

- [ ] **Step 4: Commit the top-level scaffolding**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git add README.md archive/ && git commit -m "$(cat <<'EOF'
add top-level README + archive/ of original numbered drafts

README explains both skills (existing peer + the new post-MVP one)
and lists all acknowledgments per the spec's Section 9. archive/
preserves the original 00_-07_ source-of-thought drafts.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Task 1.4: Verify peer skill still works from new path

**Files:**
- Read: `non-tech-office-hours/SKILL.md`
- Read: `non-tech-office-hours/README.md`

- [ ] **Step 1: Check internal links in moved files for any absolute path assumptions**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours/non-tech-office-hours" && grep -nE '\[.*\]\(.*\.md\)' *.md
```
Expected: all markdown links should be relative (e.g., `[ai-native-context.md](ai-native-context.md)`), not absolute. If any link points to a parent directory or uses absolute paths, fix it.

- [ ] **Step 2: Verify SKILL.md frontmatter still passes 1024-char description limit**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours/non-tech-office-hours" && python3 -c "
import re
content = open('SKILL.md').read()
match = re.search(r'description:\s*(.*?)\n---', content, re.DOTALL)
if match:
    desc = match.group(1).strip()
    print(f'Description length: {len(desc)} chars')
    assert len(desc) <= 1024, f'Description exceeds 1024-char limit'
    print('OK')
"
```
Expected: description length under 1024.

- [ ] **Step 3: Test-build the existing skill zip from its new location**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && rm -f /tmp/non-tech-test.zip && zip -r /tmp/non-tech-test.zip non-tech-office-hours -x '*.DS_Store' && unzip -l /tmp/non-tech-test.zip
```
Expected: zip lists `non-tech-office-hours/SKILL.md`, `README.md`, and all 7 other module files. Approximately 140-160 KB.

- [ ] **Step 4: Commit if any fixes were needed (otherwise skip)**

If Step 1 or 2 surfaced fixes, commit them with message: `fix: relative paths after restructure`.

### Task 1.5: Rename the GitHub repo

**Files:** (no local file changes — this is a GitHub-side rename)

- [ ] **Step 1: Push all local commits before renaming**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git push origin main
```
Expected: push succeeds.

- [ ] **Step 2: Rename the repo on GitHub via gh api**

Run:
```bash
gh api -X PATCH repos/adoistic/non-tech-office-hours -f name='founder-office-hours'
```
Expected: 200 response with the new repo metadata. GitHub auto-redirects old URLs.

- [ ] **Step 3: Update the local origin remote**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git remote set-url origin https://github.com/adoistic/founder-office-hours.git && git remote -v
```
Expected: origin points to the new URL.

- [ ] **Step 4: Verify by fetching**

Run:
```bash
cd "/Users/siraj/office bhours/non-tech-office-hours" && git fetch origin && git status
```
Expected: clean fetch, branch up to date.

- [ ] **Step 5: (Optional) Rename the local working directory to match**

The local working directory is currently `/Users/siraj/office bhours/non-tech-office-hours/`. Renaming to `founder-office-hours` keeps the local path consistent with the repo name. **Note: this changes the absolute path used throughout the rest of the plan** — track the new path going forward.

Run:
```bash
cd "/Users/siraj/office bhours/" && mv non-tech-office-hours founder-office-hours
```

After this step, **all subsequent paths in this plan are `/Users/siraj/office bhours/founder-office-hours/...` instead of `.../non-tech-office-hours/...`**.

(If the local rename is skipped, the plan still works — the GitHub repo is renamed, the local folder name is just legacy.)

### Chunk 1 review checkpoint

After completing all tasks above, dispatch the plan-document-reviewer with this chunk's content + the spec path. Iterate until approved before moving to Chunk 2.

---

## Chunk 2: Raw source ingestion (NFX scrape + Helmer transcript intake)

Pull the two canonical sources into the repo. Both land in `non-tech-office-hours/moats-and-network-effects/raw/` (we'll mirror to the post-mvp skill in Chunk 4). Output is the raw markdown of both sources; Chunk 3 reads those raw files directly to generate the wiki pages — no intermediate structured form is required at this stage.

### Task 2.1: Scrape and convert the NFX Network Effects Manual

**Files:**
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/nfx-network-effects-manual.md`
- Create (temp): `/tmp/nfx-manual.html` (raw HTML, not committed)

- [ ] **Step 1: Create the wiki directory structure**

Run:
```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && mkdir -p moats-and-network-effects/raw moats-and-network-effects/wiki/concepts moats-and-network-effects/wiki/examples
```

- [ ] **Step 2: Confirm pandoc is installed**

Run:
```bash
command -v pandoc || (echo "Install pandoc first: brew install pandoc (macOS) or apt-get install pandoc (Linux)"; exit 1)
```
Expected: pandoc path printed. If not installed, install it before continuing.

- [ ] **Step 3: Fetch the raw NFX manual HTML**

Run:
```bash
curl -sL --fail --user-agent 'Mozilla/5.0' 'https://www.nfx.com/post/network-effects-manual' -o /tmp/nfx-manual.html && wc -c /tmp/nfx-manual.html
```
Expected: 200+ KB of HTML. If under 50KB or `curl` exits non-zero, the request likely failed or was redirected.

- [ ] **Step 4: Verify the fetched page is actually the canonical manual (not a redirect)**

Run:
```bash
grep -oE '<title>[^<]+</title>' /tmp/nfx-manual.html | head -1
```
Expected: the title contains "Network Effects Manual" (or close — e.g., "The Network Effects Manual: 16 Network Effects"). If the title does not match, NFX has restructured — investigate by starting from `https://www.nfx.com/library` and finding the new canonical URL.

- [ ] **Step 5: Convert HTML to clean markdown**

```bash
pandoc -f html -t gfm /tmp/nfx-manual.html -o /tmp/nfx-manual-raw.md && wc -l /tmp/nfx-manual-raw.md
```
Expected: 600-1200 lines of markdown.

- [ ] **Step 6: Inspect and clean the markdown**

Read `/tmp/nfx-manual-raw.md`. Heuristic for cleaning:
- **Keep:** content from the first H1/H2 matching "Network Effects" through the last paragraph before "Related posts", "Subscribe", or "Comments"
- **Strip:** cookie banners, nav menus, social-share widgets, related-post lists, subscribe boxes, footer credits
- **Keep:** image references (alt text + filename in markdown), do not download images (wiki is text-only)
- **Preserve:** all inline hyperlinks

Save the cleaned version:
```bash
cp /tmp/nfx-manual-raw.md "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/nfx-network-effects-manual.md"
```

- [ ] **Step 7: Verify all 16 effects are present (per-term check)**

A simple total-line grep can pass even when an effect is missing. This iterates each effect name individually and asserts ≥1 hit:

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw" && python3 -c "
effects = [
    'physical', 'protocol', 'personal utility', 'personal network',
    'market network', 'hub-and-spoke', 'marketplace', 'platform',
    'asymptotic', 'expertise', 'data network', 'tech performance',
    'language', 'belief', 'bandwagon', 'tribal'
]
text = open('nfx-network-effects-manual.md').read().lower()
missing = [e for e in effects if e not in text]
if missing:
    print(f'MISSING effects: {missing}')
    raise SystemExit(1)
print(f'All 16 effect names present.')
"
```
Expected: "All 16 effect names present." If any are missing, the scrape was incomplete or NFX has renamed effects — investigate.

- [ ] **Step 8: Commit the raw NFX manual**

Run:
```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/raw/nfx-network-effects-manual.md && git commit -m "$(cat <<'EOF'
wiki: ingest NFX Network Effects Manual as raw source

Scraped and converted from https://www.nfx.com/post/network-effects-manual.
First of two raw sources for the Karpathy-style wiki on moats and
network effects. Will be parsed into wiki/concepts/ and wiki/examples/
pages in the next task.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Task 2.2: Fetch the two NFX deep-dive essays (Expertise, Tribal)

**Files:**
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/nfx-expertise-network-effects.md`
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/nfx-tribal-network-effects.md`

- [ ] **Step 1: Find the deep-essay URLs in the parsed manual**

Run:
```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw" && grep -B1 -A1 -iE '"read the full essay"|tribal-network-effects|expertise-network-effects' nfx-network-effects-manual.md
```
Expected: two URLs found, one for tribal and one for expertise. URLs likely follow the pattern `/post/<slug>`.

If grep returns nothing, search the raw HTML at `/tmp/nfx-manual.html` for `href` attributes around the words "Expertise" and "Tribal."

- [ ] **Step 2: Fetch each deep essay and convert to markdown**

For each URL (replace `<expertise-url>` and `<tribal-url>` with the actual URLs found):
```bash
curl -sL --user-agent 'Mozilla/5.0' '<expertise-url>' -o /tmp/nfx-expertise.html && \
pandoc -f html -t gfm /tmp/nfx-expertise.html -o "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/nfx-expertise-network-effects.md"

curl -sL --user-agent 'Mozilla/5.0' '<tribal-url>' -o /tmp/nfx-tribal.html && \
pandoc -f html -t gfm /tmp/nfx-tribal.html -o "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/nfx-tribal-network-effects.md"
```

Clean both files of header/footer noise using the same heuristic as Task 2.1 Step 6 (keep content from the first H1/H2 of the essay through the last paragraph before "Related posts" / "Subscribe" / "Comments"; preserve inline links and image alt text).

- [ ] **Step 3: Commit the deep-dive essays**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/raw/nfx-expertise-network-effects.md moats-and-network-effects/raw/nfx-tribal-network-effects.md && git commit -m "wiki: ingest NFX Expertise + Tribal deep-dive essays"
```

### Task 2.3: Intake the Helmer YC video transcript

**Files:**
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/yc-helmer-7-powers-transcript.md`

**This task blocks on Adnan providing the transcript. If the transcript is not yet available, complete the rest of Chunk 2 + Chunk 3's NFX-only work, then pause for the transcript before completing Chunk 3's Helmer pages.**

- [ ] **Step 1a: Ask Adnan for the transcript and the source video URL**

Ask verbatim:

> Do you have the Helmer 7 Powers YC video transcript ready? Please share:
> 1. The transcript file (or paste contents)
> 2. The YouTube/source URL for the video so we can cite it

- [ ] **Step 1b: Branch on availability**

- **If transcript provided:** continue to Step 2 of this task.
- **If transcript not yet ready:** mark this task as blocked. Continue with Chunk 3 Tasks 3.1–3.4 + 3.6 + 3.7 (everything except Task 3.5 which depends on the transcript). Pause Chunk 3 at Task 3.5 until the transcript arrives, then resume here at Step 2.

- [ ] **Step 2: Save the transcript verbatim**

Save the user-provided transcript to:
```
founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw/yc-helmer-7-powers-transcript.md
```

Add a header at the top of the file:
```markdown
# Helmer 7 Powers — YC Video Transcript

Source: YC video on Hamilton Helmer's 7 Powers framework (URL: <provided-by-Adnan>)
Transcript-source: <user-provided / auto-transcribed / official YC>
Ingested: 2026-05-23

---

[Transcript body, verbatim]
```

- [ ] **Step 3: Verify all 7 powers are mentioned (per-term check)**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/raw" && python3 -c "
powers = [
    'scale economies', 'network economies', 'counter-positioning',
    'switching costs', 'branding', 'cornered resource', 'process power'
]
text = open('yc-helmer-7-powers-transcript.md').read().lower()
missing = [p for p in powers if p not in text]
if missing:
    print(f'MISSING powers: {missing}')
    raise SystemExit(1)
print('All 7 powers present.')
"
```
Expected: "All 7 powers present." If any are missing, the transcript is incomplete or the speaker uses non-canonical phrasing — investigate before continuing.

- [ ] **Step 4: Commit the transcript**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/raw/yc-helmer-7-powers-transcript.md && git commit -m "wiki: ingest Helmer 7 Powers YC video transcript"
```

### Chunk 2 review checkpoint

Dispatch the plan-document-reviewer for Chunk 2. Iterate until approved.

---

## Chunk 3: Wiki construction in non-tech-office-hours

Generate the agent-readable wiki from the raw sources. This is the biggest content chunk — ~26 concept pages + ~12 example pages + 1 CLAUDE.md schema file. Each page follows a strict template so the LLM agent can navigate consistently.

### Task 3.1: Write the wiki's CLAUDE.md schema file

**Files:**
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/CLAUDE.md`

- [ ] **Step 1: Write CLAUDE.md with the agent navigation rules**

Content:

```markdown
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
```

- [ ] **Step 2: Commit the schema**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/CLAUDE.md && git commit -m "wiki: add CLAUDE.md schema and navigation rules"
```

### Task 3.2: Write the umbrella concept pages

**Files:**
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/network-effects.md`
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/moats.md`
- Create: `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/ai-native-moat-shift.md`

- [ ] **Step 1: Write `network-effects.md` (umbrella for the 16 NFX types)**

Follows the concept template. Definition section names what a network effect is. Mechanism section explains the general "more users → more value for each user" loop. Kill-test asks: "Does each new user actually increase value for existing users? If you turned off the network, would the product still work?" Lists all 16 sub-types under "Related concepts" as `[[<effect-name>]]` links.

- [ ] **Step 2: Write `moats.md` (umbrella for all defensibility, both NFX and Helmer)**

Definition section names what a moat is (per Buffett / Helmer / NFX). Mechanism section names the 4 high-level categories: network effects, scale economies, switching costs / lock-in, brand. Cross-references Helmer's 7 Powers as the canonical framework. Kill-test: "If a competitor with 10x your capital and a 1,000x-engineer team showed up tomorrow, what specifically stops them from replicating your position?" Lists all Helmer powers + the network-effects umbrella under "Related concepts."

- [ ] **Step 3: Write `ai-native-moat-shift.md`**

Cross-cuts both NFX and Helmer sources. Definition section names the shift: pre-AI moats based on engineering effort have collapsed; post-AI durable moats are data, distribution, ops, network effects, regulatory, and brand. Mechanism: 1,000x engineering capacity + software factories collapses code-as-moat to zero. Kill-test: "Of your claimed moat, how much rests on code or engineering speed (vulnerable) vs. data, network, distribution, ops, or brand (durable)?" Related concepts: links to all Helmer powers + the network-effects umbrella, plus `ai-native-context.md` in the parent skill.

- [ ] **Step 4: Commit the umbrellas**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/wiki/concepts/ && git commit -m "wiki: add umbrella concept pages (network-effects, moats, ai-native-moat-shift)"
```

### Task 3.3: Write the 16 NFX network-effect concept pages

**Files (one per effect, all in `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/`):**

Direct (5):
- `physical-network-effects.md`
- `protocol-network-effects.md`
- `personal-utility-network-effects.md`
- `personal-network-effects.md`
- `market-network-effects.md`

Hub-and-Spoke (1):
- `hub-and-spoke-network-effects.md`

2-Sided (3):
- `two-sided-marketplace.md`
- `platform-network-effects.md`
- `asymptotic-marketplace.md`

Other (2):
- `expertise-network-effects.md` (sources the deep-dive essay from Task 2.2)
- `data-network-effects.md`

Tech Performance (1):
- `tech-performance-network-effects.md`

Social (4):
- `language-network-effects.md`
- `belief-network-effects.md`
- `bandwagon-network-effects.md`
- `tribal-network-effects.md` (sources the deep-dive essay from Task 2.2)

- [ ] **Step 1: For each of the 16 effects, write a concept page following the template**

Each page sources from the corresponding H3 section in `raw/nfx-network-effects-manual.md`. The agent doing the implementation should:

1. Read the H3 section for that effect in the raw manual.
2. Extract the definition into the page's `Definition` section (plain language; rewrite if needed to remove jargon).
3. Extract the mechanism into 2-3 bullets in the `Mechanism` section.
4. Identify the "when it applies" conditions from the manual.
5. **Write a Kill-test specific to this effect.** Examples:
   - For `two-sided-marketplace.md`: "Are buyers actually returning because more sellers joined, or are they returning for other reasons (e.g., habit, price)?"
   - For `data-network-effects.md`: "Does each new data point measurably improve the product for existing users? Not 'will' — has it measurably?"
   - For `tribal-network-effects.md`: "If 50% of the tribal members left, would the remaining 50% still feel the same identity around the product?"
6. Write the AI-native erosion check: most network effects are *strengthened* in the AI era (data network effects especially), but the agent should be honest about which are easier to fake or replicate.
7. List 2-4 related concepts as `[[wiki-links]]`.
8. List 1-3 case studies (which will exist after Task 3.4).

Each page should be under 400 words.

- [ ] **Step 2: Verify all 16 files exist and follow the template**

Run:
```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts" && ls *.md | wc -l && for f in *network-effects.md *marketplace.md *platform-network-effects.md; do echo "=== $f ==="; grep -c '^## ' "$f"; done
```
Expected: at least 19 files total (3 umbrellas + 16 effects), each concept page has ≥7 H2 headings (matching the 7 required sections in the CLAUDE.md template).

- [ ] **Step 3: Commit the 16 NFX concept pages**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/wiki/concepts/ && git commit -m "$(cat <<'EOF'
wiki: add 16 NFX network-effect concept pages

One page per effect type from the NFX Network Effects Manual, each
following the CLAUDE.md template (definition, mechanism, when it
applies, kill-test, AI-native erosion check, related concepts,
case studies). Brevity enforced: each page under 400 words.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Task 3.4: Write the example pages (startup case studies)

**Files (in `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/examples/`):**

At minimum, write these case study pages (extracted from NFX manual; more may emerge during the parse):

- `att-physical-network.md` (Theodore Vail, 1908)
- `ethernet-protocol.md`
- `bitcoin-protocol.md`
- `facebook-personal-network.md`
- `linkedin-personal-network.md`
- `whatsapp-personal-utility.md`
- `ebay-two-sided-marketplace.md`
- `craigslist-two-sided-marketplace.md`
- `uber-two-sided-marketplace.md`
- `salesforce-expertise.md`
- `excel-expertise.md`
- `google-language.md`
- `apple-bandwagon.md`
- `airbnb-two-sided-marketplace.md` (if mentioned)

- [ ] **Step 1: For each case study, write an example page following the template**

Each page is ≤300 words. Source the content from the case study mentions interspersed in the raw NFX manual. The page's `Why the analog often fails` section is the most important — that's the agent's grilling tool when the founder says "we're like Uber for X." Be specific:

For `uber-two-sided-marketplace.md`, the "why the analog often fails" section might read:
> Founders citing Uber as a comparable usually fail to acknowledge that Uber's network effect was *local* (drivers and riders in the same city) and *liquidity-dependent* (the network only worked once each city hit a density threshold). If the founder's "Uber for X" doesn't have a local liquidity mechanism, the analog breaks. Also: Uber's actual moat in 2026 is regulatory + brand + cornered driver supply, not network effects per se — the network effect was the on-ramp, not the durable moat.

- [ ] **Step 2: Verify all example pages exist**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/examples" && ls *.md | wc -l
```
Expected: 10+ files.

- [ ] **Step 3: Commit example pages**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/wiki/examples/ && git commit -m "wiki: add startup case study example pages"
```

### Task 3.5: Write the 7 Helmer concept pages (blocks on transcript availability from Task 2.3)

**Files:**
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/scale-economies.md`
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/network-economies.md` (Helmer's term for network effects; note the cross-reference to the NFX umbrella)
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/counter-positioning.md`
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/switching-costs.md`
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/branding.md`
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/cornered-resource.md`
- `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts/process-power.md`

- [ ] **Step 1: For each of the 7 powers, write a concept page following the template**

Source from `raw/yc-helmer-7-powers-transcript.md`. For each:

1. Extract Helmer's definition (he is precise; quote where possible).
2. Mechanism — Helmer is explicit about cause-and-effect.
3. **When it applies** — Helmer's "Power Progression" framework specifies when in a company's lifecycle each power is created (origination → takeoff → stability). Capture this.
4. Kill-test specific to the power. Examples:
   - For `counter-positioning.md`: "Does your business model create an outcome a competitor literally cannot replicate without harming their existing business? Name the specific harm."
   - For `process-power.md`: "Could a well-funded competitor with 1,000 engineers replicate your process in 18 months by hiring 3-5 of your senior people? If yes, it's not process power, it's just hard work."
5. AI-native erosion check — Helmer's powers were defined pre-AI. Process power has eroded most (1,000x engineers compress timelines). Counter-positioning, cornered resource, and switching costs have held up well.
6. Related concepts: link the umbrella `moats.md`, the other Helmer powers, and any NFX effects that map cleanly (e.g., network-economies → network-effects umbrella).

- [ ] **Step 2: Cross-reference `network-economies.md` ↔ `network-effects.md`**

In `network-economies.md`, the `Related concepts` section should explicitly include `[[network-effects]]` and explain in one sentence: *Helmer's "network economies" is the same phenomenon NFX calls "network effects" — see that umbrella for the 16-type taxonomy.*

In `network-effects.md` (already written in Task 3.2), add an analogous cross-reference back.

- [ ] **Step 3: Verify all 7 Helmer pages exist**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/concepts" && ls scale-economies.md network-economies.md counter-positioning.md switching-costs.md branding.md cornered-resource.md process-power.md
```
Expected: all 7 files listed.

- [ ] **Step 4: Commit the Helmer pages**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git add moats-and-network-effects/wiki/concepts/ && git commit -m "wiki: add 7 Helmer Powers concept pages"
```

### Task 3.6: Lint the wiki

**Files:**
- Read: all files in `founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki/`

- [ ] **Step 1: Verify all wiki-links resolve**

Write a small Python script (or use grep) to:
1. Extract every `[[<link>]]` from every wiki page.
2. Check each resolves to an actual filename in `concepts/` or `examples/`.

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki" && \
python3 -c "
import re, os
from pathlib import Path

base = Path('.')
all_pages = set()
for p in base.rglob('*.md'):
    all_pages.add(p.stem)

broken = []
for p in base.rglob('*.md'):
    text = p.read_text()
    for match in re.finditer(r'\[\[([^\]]+)\]\]', text):
        link = match.group(1).split('/')[-1]  # handle [[examples/foo]]
        if link not in all_pages:
            broken.append((p, link))

if broken:
    print('Broken links:')
    for p, link in broken:
        print(f'  {p}: [[{link}]]')
    raise SystemExit(1)
else:
    print(f'All {sum(1 for _ in base.rglob(\"*.md\"))} pages have valid links.')
"
```
Expected: no broken links.

- [ ] **Step 2: Verify each concept page has all 7 required sections AND each example page has all 4 required sections**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki" && \
python3 -c "
import re
from pathlib import Path

concept_required = ['Definition', 'Mechanism', 'When it applies', 'Kill-test', 'AI-native erosion check', 'Related concepts', 'Case studies']
example_required = ['What they built', 'The mechanism', 'Why the analog often fails', 'Related examples']

missing = []
for p in Path('concepts').glob('*.md'):
    text = p.read_text()
    for section in concept_required:
        if not re.search(rf'^## {re.escape(section)}\s*$', text, re.MULTILINE):
            missing.append((p.name, section, 'concept'))
for p in Path('examples').glob('*.md'):
    text = p.read_text()
    for section in example_required:
        if not re.search(rf'^## {re.escape(section)}\s*$', text, re.MULTILINE):
            missing.append((p.name, section, 'example'))

if missing:
    for name, section, kind in missing:
        print(f'{kind}/{name} missing: {section}')
    raise SystemExit(1)
else:
    print('All concept and example pages complete.')
"
```

This also tightens the regex with `\s*$` anchors so "Kill-test" does not match "Kill-testing".

Expected: "All concept and example pages complete." printed.

- [ ] **Step 3: Verify word counts**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects/wiki" && \
for f in concepts/*.md; do
    wc -w "$f" | awk '{ if ($1 > 400) print "OVER 400 WORDS: " $2 " (" $1 " words)" }'
done && \
for f in examples/*.md; do
    wc -w "$f" | awk '{ if ($1 > 300) print "OVER 300 WORDS: " $2 " (" $1 " words)" }'
done
```
Expected: no over-limit warnings.

- [ ] **Step 4: Commit any lint fixes**

If lint produced fixes, commit with message `wiki: lint fixes (broken links / missing sections / over-length)`.

### Task 3.7: Apply the 3 cross-reference edits to existing peer skill files

**Files:**
- Modify: `founder-office-hours/non-tech-office-hours/ai-native-context.md`
- Modify: `founder-office-hours/non-tech-office-hours/strategy.md`
- Modify: `founder-office-hours/non-tech-office-hours/premise-and-alternatives.md`

- [ ] **Step 1: Edit `ai-native-context.md`**

Find the defensibility-shift section (around the section that names "lines of code is no longer a moat"). Add a single sentence at the end of that paragraph:

> For the full taxonomy of network effects (16 types) and the canonical moat framework (Helmer's 7 Powers), see `moats-and-network-effects/CLAUDE.md` and walk the wiki when the defensibility grill calls for it.

- [ ] **Step 2: Edit `strategy.md`**

Find the "how to win" section (Roger Martin's Playing-to-Win — the place where the defensibility list lives). Add at the end of the section:

> When a strategic bet rests on a moat, name the moat type using Helmer's taxonomy (`moats-and-network-effects/wiki/concepts/`). Generic moat claims fail the strategy check; named moats with mechanisms can be tested.

- [ ] **Step 3: Edit `premise-and-alternatives.md`**

Find the section that constrains the three forced alternatives. Add a sentence to whichever alternative covers "build a moated version" (likely the AI-native rebuild / lateral one):

> If a chosen alternative claims a moat, walk `moats-and-network-effects/wiki/concepts/` to name the specific Helmer power or NFX network effect type, and confirm the mechanism is real, not aspirational.

- [ ] **Step 4: Verify edits and commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours" && git diff && git add ai-native-context.md strategy.md premise-and-alternatives.md && git commit -m "$(cat <<'EOF'
peer skill: add cross-refs into moats-and-network-effects wiki

Three light edits to ai-native-context.md, strategy.md, and
premise-and-alternatives.md. Each adds a single sentence pointing
into the new wiki when the relevant moat / defensibility decision
arises. Within-skill references only (per the decoupling rule).

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Chunk 3 review checkpoint

Dispatch the plan-document-reviewer for Chunk 3. Iterate until approved.

---

## Chunk 4: Mirror the wiki to post-mvp-office-hours/

Create the new skill's empty folder, verbatim-copy the entire `moats-and-network-effects/` directory into it. This chunk is tiny but enforces the decoupling rule.

### Task 4.1: Create the new skill folder and copy the wiki

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/` directory
- Create: `founder-office-hours/post-mvp-office-hours/moats-and-network-effects/` (verbatim copy)

- [ ] **Step 1: Create the new skill folder**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && mkdir post-mvp-office-hours
```

- [ ] **Step 2: Copy the wiki verbatim**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp -R non-tech-office-hours/moats-and-network-effects post-mvp-office-hours/
```

- [ ] **Step 3: Verify the copy is byte-identical**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && diff -r non-tech-office-hours/moats-and-network-effects post-mvp-office-hours/moats-and-network-effects && echo "OK: identical"
```
Expected: no differences, "OK: identical" printed.

- [ ] **Step 4: Commit the mirror**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/ && git commit -m "$(cat <<'EOF'
mirror moats-and-network-effects wiki into post-mvp-office-hours

Verbatim copy per the decoupling rule. Each skill owns its own copy
of the wiki. Edits do not auto-propagate; future updates must be
applied to both copies manually.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Chunk 4 review checkpoint

Dispatch the plan-document-reviewer for Chunk 4. (Likely trivial review; main thing is confirming the diff check passes.) Iterate until approved.

---

## Chunk 5: post-mvp-office-hours skill files

Write the 11 files that constitute the new skill. Two are verbatim copies of peer files (`ai-native-context.md`, `principles.md` with additions), two are NEW (`diagnostic.md`, `investor-mirror.md`), and the rest are adapted from peer.

### Task 5.1: Copy ai-native-context.md verbatim

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/ai-native-context.md` (verbatim from peer)

- [ ] **Step 1: Copy and verify**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/ai-native-context.md post-mvp-office-hours/ai-native-context.md && diff non-tech-office-hours/ai-native-context.md post-mvp-office-hours/ai-native-context.md && echo "OK: identical"
```
Expected: identical.

**However** — the peer's `ai-native-context.md` was edited in Task 3.7 Step 1 to add a cross-reference into the wiki. Since we want the new skill to also reference *its own* wiki copy, the edit ports over as-is (the relative path `moats-and-network-effects/CLAUDE.md` resolves correctly in both skills because each has its own wiki copy).

- [ ] **Step 2: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/ai-native-context.md && git commit -m "post-mvp: copy ai-native-context.md verbatim from peer skill"
```

### Task 5.2: Copy principles.md and append 2 new principles

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/principles.md` (peer's content + 2 new principles)

- [ ] **Step 1: Copy peer's principles.md**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/principles.md post-mvp-office-hours/principles.md
```

- [ ] **Step 2: Append the 2 new principles**

Edit `post-mvp-office-hours/principles.md`. Find the end of the existing 9 principles (the section header for the next section will be the boundary — likely "Anti-sycophancy rules" or "The Answer-it-back gate"). Insert these two new principles before that boundary:

```markdown
### Principle 10 — Reality before projection

Behavioral data beats user interviews beats founder narrative beats slide-deck claims.

When the founder cites a metric, ask: how did you measure that? If they did not measure it, the metric does not exist and that is the finding.

When the founder says "users love it," ask: which user, what did they do after the call, what would they do if it went away. Cite specifics or accept that the claim is unsupported.

Pre-build, projection is all founders have. Post-MVP, projection is a tell — they have data and are choosing to talk about hypotheticals instead.

### Principle 11 — PMF before moat

Do not grill on defensibility until the founder has earned the right to think about it.

The Searching and Approaching routes do not run the moat grill. The wiki at `moats-and-network-effects/` is available but unused. A Searching-route founder asking about moats is procrastinating on the harder question of whether anyone actually wants the product.

The Claims-PMF and Fundraise-ready routes earn moat thinking. For them, the wiki is the working tool — concept pages for definitions and kill-tests, example pages for analog-busting.

This rule overrides any temptation to "be thorough" on defensibility for founders without PMF. Thoroughness on the wrong question is a sycophancy pattern in disguise.
```

- [ ] **Step 3: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/principles.md && git commit -m "$(cat <<'EOF'
post-mvp: principles.md = peer's + 2 new post-MVP principles

Principle 10 (Reality before projection) and Principle 11 (PMF before
moat) are post-MVP-specific. The 9 existing principles, anti-sycophancy
rules, answer-it-back gate, and pushback patterns carry over verbatim.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Task 5.3: Write diagnostic.md (NEW module)

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/diagnostic.md`

- [ ] **Step 1: Write `diagnostic.md`**

Content structure:

```markdown
# Phase 2 — Diagnostic Intake

This phase places the founder on a 4-segment spectrum that determines
the rest of the session. It is non-skippable and runs after Phase 1
(reflection + conviction check).

## How to use this file

Ask the 5 questions one at a time. Push on each until the answer is
specific and evidence-based. Do not batch. Do not skip ahead.

After all 5 questions, score the founder against the 4-segment signal
table and announce the route to them verbatim using the script in
"Announcing the route" below.

## The 5 questions

### Q1: What did you ship and when?

Pushback rules:
- If they describe a vision instead of a product, push: "What's actually
  running in production right now? Walk me through the URL or app."
- If they describe a v0.1 from 8 weeks ago and have not updated since,
  ask why. A stalled MVP is a finding.
- If they describe a pitch deck, redirect: "I'm asking about what users
  can actually use today."

### Q2: Who's using it right now?

Pushback rules:
- If they say "users" or "customers" without a count, push: "How many — give me the number. If you don't know the number, that's the answer."
- If the count is a sign-up count rather than active users, push: "How many came back this week? Last week?"
- If they cite a segment ("SMBs", "developers"), push to a person: "Name the user who logged in yesterday. What's their job title? What did they do in the product?"
- If they cannot name a specific user, that's a finding. They are not close enough to their users.

### Q3: What's growing and what isn't?

Pushback rules:
- If they cite a growth metric (MAU, signups, revenue), push: "What's the cohort retention curve look like? Flat after some decay, or still falling?"
- If they cannot describe the cohort curve, that is the finding. They are either not measuring it or hiding from it.
- If they cite revenue growth without retention data, push: "Revenue growth without retention is paid acquisition burning cash. Show me the retention."
- If they cite "engaged users," push: "Engaged how? What did the user do that counts as engagement? Why does that action matter?"
- If something is NOT growing, push: "Why isn't that growing? What have you tried? What did the experiments tell you?"

### Q4: What did the last 10 customer conversations actually sound like?

Pushback rules:
- If they cannot describe 10 conversations, push: "How many have you actually had? If under 10, that's a finding — you're not close enough to your users."
- If they give summaries ("they liked it"), push: "Direct quotes. What did they actually say. Not what you took from it — what they said."
- If they describe sales calls only, push: "I'm asking about discovery calls. Are you still doing those? When was the last one?"
- If the conversations all sound similar, push: "Either you have one tight segment or you're only talking to the same kind of user. Which?"
- If the conversations are months old, push: "What happened in the last 30 days of conversations?"

### Q5: What is your runway and what would you do with $2M today?

Pushback rules:
- If the runway is unknown, push: "Find out before this session ends. A founder who doesn't know their runway is operating blind."
- If they say "we'd hire engineers", push: "Engineers to do what specifically? Name the milestone $2M reaches that $0 doesn't."
- If they say "we'd raise more after that", push: "Stop. What does $2M *finish*? If it doesn't finish a clear milestone, you're not ready to raise."
- If the use-of-funds is vague ("growth"), push: "Channel by channel. Which channel takes $X to scale to what? Show me the math."
- If they cannot name a concrete milestone $2M reaches, they are not Fundraise-ready regardless of other signals.

## The 4-segment signal table

| Segment | Signals (≥2 must match) |
|---------|--------------------------|
| Searching | Q1: shipped, Q2: <100 users or unclear count, Q3: retention unknown or flat-to-zero, Q4: customer conversations sparse or hand-wavy, Q5: runway >12 months but no clear capital use |
| Approaching | Q1: shipped + iterating, Q2: 100-1000 users with named segments, Q3: retention shape exists but is decaying-to-zero, Q4: still talking to customers regularly, Q5: runway tight enough that capital use matters |
| Claims-PMF | Q1: shipped + stable, Q2: 1000+ users or paid customers with named ICPs, Q3: retention is flat-after-decay or genuinely flat, Q4: customer conversations are now sales calls or expansion calls, Q5: founder has a coherent answer for capital use |
| Fundraise-ready | All of Claims-PMF AND: Q3: cohort curves shared without prompting, Q4: NPS/Sean Ellis numbers cited unprompted, Q5: founder can name the 6-12 partner-meeting questions and has draft answers |

## Announcing the route

After scoring, say to the founder verbatim:

> Based on what you just said, I'm placing you at **<segment>**.
> Here's why: <one specific signal you can cite>.
> If that's wrong, push back now — but you'll need to give me a
> signal I missed, not just a different feeling about it.

## Override protocol

The founder may override the placement. If they do:

1. Ask for the specific signal you missed.
2. If they give a real signal (e.g., "I didn't mention we have a
   $50k MRR contract with X"), re-score and move them up a segment.
3. If they give a feeling without a signal ("I just think we're more
   ready than that"), refuse to re-route. Say: "Without a signal I
   missed, I'm holding the placement. We can re-test at the end of
   the session if the rest of the conversation surfaces something."

## Failure mode (anti-sycophancy)

Re-routing without a new signal is sycophantic. The founder should
leave the diagnostic feeling they were graded honestly, not flattered.
A founder who declares Fundraise-ready and is actually Approaching is
the most expensive failure mode in this skill — they'll go raise on
flawed positioning. Better to under-place than over-place.
```

- [ ] **Step 2: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/diagnostic.md && git commit -m "post-mvp: write diagnostic.md (5 questions, 4 segments, route announcement)"
```

### Task 5.4: Write investor-mirror.md (NEW module)

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/investor-mirror.md`

- [ ] **Step 1: Write `investor-mirror.md`**

Content structure:

```markdown
# Phase 4-IM — The Investor Mirror

This module runs only for Claims-PMF and Fundraise-ready routes
(per the diagnostic). The Searching and Approaching routes skip this
entire phase and end with customer-discovery assignments.

## How to use this file

Walk the founder through the 10 partner-meeting questions, one at a
time. For each:

1. Ask the question verbatim.
2. Let them answer.
3. Apply the push-back from "Push-back rules" below.
4. Record any unanswerable gap straight into WHAT_INVESTORS_WILL_ASK.md.

This is the closest the skill gets to a real partner meeting. The
push-backs are deliberately harsher than the diagnostic.

## The 10 questions

### Q1: What is the problem, in one sentence?

Push-back rules:
- If they take more than one sentence, stop them. Make them compress.
- If the sentence contains the word "platform," push: "Strip the word
  platform out. What's the actual problem?"
- If the problem is "users want X," push: "Who specifically wants X
  badly enough to pay or change behavior?"

### Q2: Who has it? Who has it badly enough to pay?

Push-back rules:
- "SMBs" / "developers" / "marketers" is not a person. Push to a named
  archetype with a job title.
- Ask: "What does this person spend right now to solve this problem,
  even if poorly?"

### Q3: What did you build? Why this wedge?

Push-back rules:
- If the wedge is broad ("we serve mid-market SaaS"), push: "Narrow it
  until you can name one specific job-to-be-done in one specific
  team in one specific company size."
- If the wedge reasoning is "we saw an opportunity," push: "What
  unfair advantage or non-consensus belief led you to this wedge
  specifically — that a generalist competitor wouldn't have?"
- If the founder retrofits the wedge ("we narrowed to X because Y
  was working"), that's a positive signal — push to confirm the
  narrowing is permanent or experimental.
- Reference the moats-and-network-effects wiki only if they claim
  the wedge is moated. Walk to the specific concept page they imply.

### Q4: Show me retention. Show me cohorts.

Push-back rules:
- If they cite MAU growth instead of cohort retention, redirect: "MAU
  growth can mask churn. I want the cohort curve."
- If they cannot describe the curve shape, that's a finding. Record it.
- If the curve decays to zero, push: "Then you don't have PMF yet,
  regardless of the revenue. Why do you think you have PMF?"

### Q5: What is the unit-economics story?

Push-back rules:
- If they cannot name LTV/CAC, ask: "What does a customer cost to
  acquire? What do they pay across their lifetime?"
- If LTV/CAC is healthy but payback is >24 months, push on the
  capital efficiency story.

### Q6: Why now?

Push-back rules:
- "Now" must reference a structural change (regulation, technology
  shift, behavior shift, capital market shift), not just "now is when
  we got around to it."
- If the answer is "AI is hot now," push: "Hot is not why. What
  structural shift makes this problem solvable now and unsolvable
  three years ago?"

### Q7: Why you?

Push-back rules:
- Pedigree alone is not why-you. Push to specific unfair advantage:
  prior built X, lived the problem for Y years, have access to Z
  that competitors can't get.
- If they say "we're just better executors," push: "What does a
  partner see in 60 seconds that confirms that?"

### Q8: What is your moat going to look like in 24 months when 1,000x engineers can rebuild your stack in a weekend?

Push-back rules:
- This is the question where the moats-and-network-effects wiki gets
  walked hard. The founder MUST name a specific moat type
  (Helmer's 7 Powers or NFX network effect type).
- If they say "great execution" or "speed of iteration," push: "Both
  of those are ephemeral. What's the durable underlying mechanism?"
- For technical founders claiming architectural uniqueness, apply
  the counter-grill from SKILL.md (AI-native cost collapse, patent
  test, alternative-architecture test).

### Q9: What are you raising and what does it buy?

Push-back rules:
- "We're raising $X" is not enough. Push: "What does $X buy that $X/2
  doesn't, and what does $X/2 buy that $X doesn't?"
- If the use of funds is generic ("hiring, growth"), push to specific
  milestones the capital reaches.

### Q10: What is the one thing that would kill this?

Push-back rules:
- If they say "competition" or "market changes," push: "More specific.
  What single event, if it happened in the next 12 months, would end
  this company?"
- A founder who cannot name a kill condition has not stress-tested
  the business. That's a finding.

## What counts as a "real" answer vs. deflection

For each question, a real answer:
- Is specific (a named customer, a number, a structural change)
- Survives one round of follow-up without retreating
- Does not require the founder to add caveats that contradict an
  earlier answer

A deflection:
- Pivots to a related-but-different topic
- Cites authority ("our investors told us...")
- Adds hedging that wasn't in the original answer

When you see a deflection, name it. Say: "That's a deflection from
the question I asked. Let me ask again."

## Output mapping to WHAT_INVESTORS_WILL_ASK.md

Each question → one section in the artifact, with three subsections:
- **Their answer** (what the founder said, in their words)
- **Push-back the founder will receive** (what a partner will follow
  up with)
- **Gap to close** (what they don't yet have, if anything)
```

- [ ] **Step 2: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/investor-mirror.md && git commit -m "post-mvp: write investor-mirror.md (10 partner-meeting questions + push-backs)"
```

### Task 5.5: Adapt forcing-questions.md

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/forcing-questions.md` (adapted from peer)

- [ ] **Step 1: Copy peer's forcing-questions.md as starting point**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/forcing-questions.md post-mvp-office-hours/forcing-questions.md
```

- [ ] **Step 2: Adapt for post-MVP context**

The peer's forcing questions assume pre-MVP (the founder is projecting). The post-MVP version assumes the founder has data and is either reporting it or hiding it. Edits to make:

1. **Reframe each question's pass criteria** from "specific projection" to "specific data + how it was measured."
2. **Remove the "wedge in 7 days" framing** — the founder has already shipped.
3. **Add explicit data-vs-hypothesis pushback** to each question. Example: peer's "Who's the customer?" becomes "Who's the customer? Name a person who actually paid you / used your product yesterday. Not your ICP slide — a person."
4. **Reframe Q4 (the wedge question)** for post-MVP: "What's the narrowest version of your product that still solves the core job for your sharpest customer?" — and then test if they've actually narrowed it or are still spread thin.

The number of questions stays at 6 (matching peer's structure).

- [ ] **Step 3: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/forcing-questions.md && git commit -m "post-mvp: adapt forcing-questions.md (data-backed, not future-projected)"
```

### Task 5.6: Adapt premise-and-alternatives.md

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/premise-and-alternatives.md` (adapted from peer)

- [ ] **Step 1: Copy peer's file**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/premise-and-alternatives.md post-mvp-office-hours/premise-and-alternatives.md
```

- [ ] **Step 2: Adapt the alternatives set for post-MVP**

The peer's three alternatives (no-code/manual, minimum AI-native build, AI-native rebuild/lateral) are pre-build alternatives. For post-MVP, the three alternatives become a choose-three-from-six menu:

1. **Pivot the wedge** — keep team, change wedge
2. **Double down on what's working** — kill everything else, ride strongest signal
3. **Kill a feature or segment** — reduce surface area
4. **Change distribution** — same product, different channel
5. **Raise now** — capital is the unblocker
6. **Don't raise yet** — runway is fine, raising would distract

The skill forces the founder to **pick the top 2-3 from this menu** and articulate which premises they're betting on for each. Stop and wait for the choice.

The 5-7 premises section stays structurally similar but the premises themselves shift to post-MVP-flavored (e.g., "We have already found PMF" is now a premise to evaluate, not assume).

- [ ] **Step 3: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/premise-and-alternatives.md && git commit -m "post-mvp: adapt premise-and-alternatives.md (6-alternative post-MVP menu)"
```

### Task 5.7: Adapt strategy.md

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/strategy.md` (adapted from peer)

- [ ] **Step 1: Copy peer's strategy.md**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/strategy.md post-mvp-office-hours/strategy.md
```

- [ ] **Step 2: Adapt for post-MVP**

The framework (Roger Martin's Playing-to-Win) is unchanged. What changes:

1. **Winning aspiration** — for post-MVP founders, this gets challenged with actual data ("Is the current trajectory consistent with this aspiration? If not, why?").
2. **Where to play** — now grounded in the founder's actual customer cohorts, not hypothetical segments.
3. **How to win** — the moat type must be named (link to `moats-and-network-effects/wiki/concepts/`) for Claims-PMF and Fundraise-ready routes only.
4. **Capabilities** — the founder names what they actually have, not what they hope to have.
5. **Management systems** — for post-MVP, this includes the cohort retention dashboard, the customer-feedback loop, the unit-economics tracker.
6. **What-must-be-true watchlist** — peer skill carries 5 buckets including production economics (per spec Section 5 Phase 5). The post-MVP version keeps all 5 buckets but **changes the falsification window**: each bucket gets a "what evidence in the next 90 days would falsify this assumption?" prompt, sharpening Roger Martin's framework for a founder with real data and a finite runway. Do not add a 6th bucket — refine the existing 5.

The "Strategy is not planning" hard rule from peer's SKILL.md remains the strictest enforcement standard.

- [ ] **Step 3: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/strategy.md && git commit -m "post-mvp: adapt strategy.md (Playing-to-Win refined with real data)"
```

### Task 5.8: Adapt drafting-and-review.md

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/drafting-and-review.md` (adapted from peer)

- [ ] **Step 1: Copy peer's drafting-and-review.md**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/drafting-and-review.md post-mvp-office-hours/drafting-and-review.md
```

- [ ] **Step 2: Adapt for three artifacts**

Major edits:

1. **Phase 5 (internal drafting)** — replaces the 2-artifact draft (`FOR_YOU.md`, `FOR_YOUR_CO_FOUNDER.md`) with the 3-artifact draft (`WHERE_YOU_ARE.md`, `WHAT_TO_DO_NEXT.md`, `WHAT_INVESTORS_WILL_ASK.md`). The third is route-gated: only drafted for Claims-PMF and Fundraise-ready routes.
2. **Phase 6 (autonomous C-criteria review)** — the 5 passes (clarity, justification, zero-hallucination, completeness, cross-document consistency) stay. The cross-document consistency pass now runs over 3 docs instead of 2.
3. **Phase 7 (create artifacts + read-back)** — the read-back gate now covers 4-5 load-bearing sections per artifact instead of 4 per artifact. Walk the founder through each artifact, get them to articulate the key sections in their own words.
4. **Templates** — write new templates for the three artifacts. Section structures:
   - `WHERE_YOU_ARE.md`: Diagnostic placement + signals → Real-vs-vanity metrics → Customer-pulse status → Defensibility check (route-gated) → Strategy snapshot → Kill list
   - `WHAT_TO_DO_NEXT.md`: The headline move (one sentence) → Why this move (one paragraph) → Supporting work (3-5 bullets) → The 90-day milestone → What would tell you to abandon this path
   - `WHAT_INVESTORS_WILL_ASK.md` (route-gated): Each of the 10 partner-meeting questions → founder's draft answer → push-back the partner will give → gap to close

- [ ] **Step 3: Detect Claude.ai vs. Claude Code environment for artifact production**

Add a section at the top of the file (or amend the existing equivalent in peer) that says:

```markdown
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
```

- [ ] **Step 4: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/drafting-and-review.md && git commit -m "post-mvp: adapt drafting-and-review.md (3 artifacts, 1 route-gated)"
```

### Task 5.9: Adapt closing.md

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/closing.md` (adapted from peer)

- [ ] **Step 1: Copy peer's closing.md**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && cp non-tech-office-hours/closing.md post-mvp-office-hours/closing.md
```

- [ ] **Step 2: Adapt for post-MVP route-calibrated closings**

Edits:

1. **What I noticed** section — adapt for post-MVP. The notice is now about how the founder relates to their data (running toward it or hiding from it), not just how they think.
2. **Personal note** — same shape as peer.
3. **Curated resources** — split by route:
   - Searching: Mom Test, Sean Ellis 40% test blog post, Vohra Superhuman PMF engine.
   - Approaching: same + cohort retention reading.
   - Claims-PMF / Fundraise-ready: NFX Network Effects Manual link, Helmer 7 Powers (YC video link), Suster "why now" essays, Bessemer 10 Laws / anti-portfolio.
4. **The Assignment** — route-calibrated, per the spec's Section 5 Phase 9:
   - Searching: "Have 20 customer conversations this week. Verbatim quotes."
   - Approaching: "Run the Sean Ellis 40% survey. Bring me the result + segmentation."
   - Claims-PMF: "Build the cohort retention dashboard."
   - Fundraise-ready: "Draft the one-pager + 10-question answer doc. Send to 3 trusted operators for kill-shot feedback."
5. **The non-negotiable handoff** — replace peer's "get the co-founder doc to your co-founder this week" with: "The founder commits to a measurement and brings the result back next session."

- [ ] **Step 3: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/closing.md && git commit -m "post-mvp: adapt closing.md (route-calibrated assignments)"
```

### Task 5.10: Write SKILL.md (the entry point)

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/SKILL.md`

- [ ] **Step 1: Write SKILL.md**

Structure mirrors peer's SKILL.md but with post-MVP-specific content. Key sections:

```markdown
---
name: post-mvp-office-hours
description: Office hours for any founder who has shipped a product, calibrated to the AI-native era. Diagnoses PMF status via a 5-question intake that places the founder on a 4-segment spectrum (Searching, Approaching, Claims-PMF, Fundraise-ready), then routes the session accordingly. Harder than pre-build office hours because the founder has real data — usage, retention, revenue, cohorts — or must admit they haven't measured. For Claims-PMF and Fundraise-ready routes, runs a 10-question partner-meeting rehearsal (the investor mirror), with a counter-grill for technical founders who claim architectural uniqueness using the AI-native cost collapse. Produces three markdown artifacts: WHERE_YOU_ARE.md, WHAT_TO_DO_NEXT.md, and (route-gated) WHAT_INVESTORS_WILL_ASK.md. Triggers: "I've shipped, now what", "is this PMF?", "should I raise?", "what would a partner ask me?", "post-MVP office hours". Do NOT use pre-build — use a pre-build office-hours skill or your own brainstorming first.
---

# Office Hours — post-MVP, any founder

You are now an **office hours partner** for a founder who has already
shipped a product. Your only deliverables are **three markdown artifacts**
— `WHERE_YOU_ARE.md`, `WHAT_TO_DO_NEXT.md`, and (route-gated)
`WHAT_INVESTORS_WILL_ASK.md`. The last is produced only for Claims-PMF
and Fundraise-ready routes.

## Before anything else — read the operating context

**Before you do anything in this session, read [ai-native-context.md](ai-native-context.md) end to end. Then read [principles.md](principles.md).**

[... full file structure ...]

## The Founder-Type Adaptive Protocol

The skill is adaptive on founder type. Treat anything the founder says
as provisionally accepted but subject to grilling:

- If they identify as technical: technical content is on the table.
  Apply the counter-grill below when they make architectural claims.
- If they identify as non-technical: do not pull them into technical
  discussions. If a technical question is load-bearing, park it for
  their technical co-founder or a future technical advisor.

### Counter-grill for technical-founder claims

When a technical founder claims their architecture is unique, hard to
build, or a moat:

1. Cost-to-replicate today vs. 2023. Walk through what a 1,000x
   engineer with a software-factory setup could do in a weekend.
   See ai-native-context.md.
2. Is the moat the code or what's underneath? Push them to identify
   whether defensibility is in the code (collapsed in value) or in
   data, distribution, ops, or network effects (durable). See
   moats-and-network-effects/CLAUDE.md.
3. Patent and counter-architecture test. If truly novel: why not
   patented? Could a different architecture get to the same outcome?
4. Cite YC partner and Bessemer / a16z partner commentary on the
   defensibility shift. Not as appeals to authority — as evidence
   of where smart capital has moved.

## Phase order

1. Phase 1 — Reflection + conviction check.
2. Phase 2 — Diagnostic intake. See diagnostic.md.
3. Phase 3 — Common spine (customer-pulse, real-vs-vanity, premise + alternatives). See forcing-questions.md and premise-and-alternatives.md.
4. Phase 4 — Branch by route:
   - Searching / Approaching → customer-discovery deep dive. Skip Phase 4-IM.
   - Claims-PMF / Fundraise-ready → Phase 4-IM (investor-mirror.md).
5. Phase 5 — Strategy clarity check. See strategy.md.
6. Phase 6 — Draft artifacts internally. See drafting-and-review.md.
7. Phase 7 — Autonomous C-criteria review.
8. Phase 8 — Create artifacts + read-back gate.
9. Phase 9 — Closing + the Assignment. See closing.md.

## Hard rules

[Carry over peer's hard rules verbatim, then add:]

- **PMF before moat.** Do not push moat thinking on Searching or
  Approaching routes. The wiki at moats-and-network-effects/ is
  available but unused for those routes.
- **Reality before projection.** Behavioral data beats user interviews
  beats founder narrative beats slide-deck claims.
- **Diagnostic placement is honest, not flattering.** Sycophantic
  re-routing is the most expensive failure mode.
- **Technical-founder counter-grill is non-optional.** Whenever a
  technical claim could be load-bearing, apply the protocol above.

## Escape hatches

[Same as peer's: respect "just do it" once, but Phase 2 (diagnostic),
Phase 3.3 (premise + alternatives), and Phase 7 (autonomous review)
are non-negotiable. Add: Phase 4-IM is route-gated and skipped
automatically for Searching/Approaching, not a thing the founder
can opt out of.]

## Operating principles

See principles.md.

Now: read ai-native-context.md, then principles.md, then re-read the
conversation (if mid-session), then begin with the reflection paragraph +
conviction check.
```

- [ ] **Step 2: Verify SKILL.md frontmatter description is under 1024 chars**

```bash
cd "/Users/siraj/office bhours/founder-office-hours/post-mvp-office-hours" && python3 -c "
import re
content = open('SKILL.md').read()
match = re.search(r'description:\s*(.*?)\n---', content, re.DOTALL)
if match:
    desc = match.group(1).strip()
    print(f'Description length: {len(desc)} chars')
    assert len(desc) <= 1024, 'description exceeds 1024 char limit'
    print('OK')
"
```
Expected: under 1024.

- [ ] **Step 3: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/SKILL.md && git commit -m "$(cat <<'EOF'
post-mvp: write SKILL.md (entry point, hard rules, phase order)

Mirrors peer's SKILL.md structure but adds: diagnostic-first phase
order, the founder-type adaptive protocol with technical counter-grill,
the PMF-before-moat hard rule, and route-gated phase handling for
the investor mirror.

Co-Authored-By: Claude Opus 4.7 (1M context) <noreply@anthropic.com>
EOF
)"
```

### Task 5.11: Write README.md (the user-facing skill description)

**Files:**
- Create: `founder-office-hours/post-mvp-office-hours/README.md`

- [ ] **Step 1: Write README.md following peer's structure**

Sections to include:
- One-paragraph framing (post-MVP, any founder, AI-native operating context, three artifacts)
- "What you get out of a session" — describe each of the 3 artifacts
- "How it's different" (from the peer skill) — diagnostic-first, harder grilling because data exists, adaptive founder type, route-gated investor mirror
- Installation (claude.ai web app, coding agents, manual install — same structure as peer, but pointing to the new zip URL)
- Files table (mapping each module file to its purpose)
- Trigger phrases (for skill auto-loading)
- "Do NOT use this skill when" section
- Credit and source material
- Version

Use peer's README.md as the structural template. Install URLs point to the new release zip:
```
https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip
```

- [ ] **Step 2: Commit**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git add post-mvp-office-hours/README.md && git commit -m "post-mvp: write README.md"
```

### Task 5.12: Decoupling audit

**Files:** all files in `founder-office-hours/post-mvp-office-hours/` and `founder-office-hours/non-tech-office-hours/`.

- [ ] **Step 1: Confirm no file inside either skill references the other (broad audit)**

The literal folder-name check is necessary but insufficient. Spec Section 8 item 3 says "the agent reading either skill should be unable to tell from the skill files alone that a peer exists" — that means catching subtler phrasings too:

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
echo "=== post-mvp referencing peer (literal name) ===" && \
(grep -rn 'non-tech-office-hours' post-mvp-office-hours/ && echo "FAIL" || echo "OK") && \
echo "=== peer referencing post-mvp (literal name) ===" && \
(grep -rn 'post-mvp-office-hours' non-tech-office-hours/ && echo "FAIL" || echo "OK") && \
echo "=== peer referencing post-mvp (subtler phrasings) ===" && \
(grep -rnE 'post.MVP|pre.build founder|the other variant|the other skill|peer skill' non-tech-office-hours/ && echo "REVIEW" || echo "OK") && \
echo "=== post-mvp referencing peer (subtler phrasings) ===" && \
(grep -rnE 'pre.MVP|non.technical founder paired|the other variant|the other skill|peer skill' post-mvp-office-hours/ && echo "REVIEW" || echo "OK")
```

- "OK" = clean. "FAIL" = literal cross-reference, must remove. "REVIEW" = phrasing that might or might not be a cross-reference — read the line and decide.
- The post-mvp skill discussing its own non-technical-vs-technical adaptive protocol is fine; the post-mvp skill saying "unlike the pre-MVP skill" is a violation.

- [ ] **Step 2: Confirm each skill zip is buildable and self-contained**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
rm -f /tmp/non-tech-test.zip /tmp/post-mvp-test.zip && \
zip -r /tmp/non-tech-test.zip non-tech-office-hours -x '*.DS_Store' && \
zip -r /tmp/post-mvp-test.zip post-mvp-office-hours -x '*.DS_Store' && \
unzip -l /tmp/non-tech-test.zip | tail -1 && \
unzip -l /tmp/post-mvp-test.zip | tail -1
```
Expected: both zips build cleanly; each contains its skill's files + the verbatim moats-and-network-effects/ wiki.

- [ ] **Step 3: Diff the wikis to confirm verbatim duplication**

```bash
diff -r "/Users/siraj/office bhours/founder-office-hours/non-tech-office-hours/moats-and-network-effects" "/Users/siraj/office bhours/founder-office-hours/post-mvp-office-hours/moats-and-network-effects" && echo "OK: wikis identical"
```
Expected: identical.

- [ ] **Step 4: Commit any fixes from the audit**

If anything was found, commit with message `decoupling: fix cross-references`.

### Chunk 5 review checkpoint

Dispatch the plan-document-reviewer for Chunk 5. Iterate until approved.

---

## Chunk 6: Release artifacts + validation

Build the two release zips, validate them in a clean install, tag the release, push to GitHub.

### Task 6.1: Build the release zips

**Files:**
- Modify: `founder-office-hours/.gitignore` (add `dist/`)
- Create: `dist/non-tech-office-hours.zip` (not committed)
- Create: `dist/post-mvp-office-hours.zip` (not committed)

- [ ] **Step 0: Ensure `dist/` is gitignored before building**

Run:
```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
grep -q '^dist/' .gitignore || echo 'dist/' >> .gitignore && \
git add .gitignore && \
git diff --cached --quiet || git commit -m "gitignore: exclude dist/ release artifacts"
```
Expected: either no-op (if already present) or one commit adding the rule.

- [ ] **Step 1: Build both zips fresh**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
mkdir -p dist && \
rm -f dist/non-tech-office-hours.zip dist/post-mvp-office-hours.zip && \
zip -r dist/non-tech-office-hours.zip non-tech-office-hours -x '*.DS_Store' && \
zip -r dist/post-mvp-office-hours.zip post-mvp-office-hours -x '*.DS_Store' && \
ls -lh dist/
```
Expected: two zip files, each likely 200KB-1MB depending on wiki size.

- [ ] **Step 2: Verify zip integrity**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
unzip -t dist/non-tech-office-hours.zip > /dev/null && echo "non-tech-office-hours.zip OK" && \
unzip -t dist/post-mvp-office-hours.zip > /dev/null && echo "post-mvp-office-hours.zip OK"
```
Expected: both OK.

### Task 6.2: Validate in a clean install

**Files:** none — this validates the zips work as installed skills.

- [ ] **Step 1: Test install in a temp directory**

```bash
cd /tmp && rm -rf skill-test && mkdir skill-test && cd skill-test && \
unzip "/Users/siraj/office bhours/founder-office-hours/dist/non-tech-office-hours.zip" && \
unzip "/Users/siraj/office bhours/founder-office-hours/dist/post-mvp-office-hours.zip" && \
ls
```
Expected: two skill directories unpack cleanly.

- [ ] **Step 2: Verify each unpacked skill has the full expected file inventory**

Use a Python check that asserts each required file/directory exists. Runs both skills' inventories:

```bash
cd /tmp/skill-test && python3 -c "
from pathlib import Path

peer = Path('non-tech-office-hours')
peer_required = [
    'SKILL.md', 'README.md', 'ai-native-context.md', 'principles.md',
    'forcing-questions.md', 'premise-and-alternatives.md', 'strategy.md',
    'drafting-and-review.md', 'closing.md',
    'moats-and-network-effects/CLAUDE.md',
    'moats-and-network-effects/raw',
    'moats-and-network-effects/wiki/concepts',
    'moats-and-network-effects/wiki/examples',
]
new = Path('post-mvp-office-hours')
new_required = peer_required + ['diagnostic.md', 'investor-mirror.md']
# new skill has the same module list except no 'forcing-questions.md' name override —
# it has its own forcing-questions.md (adapted), still named the same. So:
# new_required is peer_required + the 2 NEW files.

for skill, required in [(peer, peer_required), (new, new_required)]:
    missing = [r for r in required if not (skill / r).exists()]
    if missing:
        print(f'{skill.name} MISSING: {missing}')
        raise SystemExit(1)
    print(f'{skill.name}: all required files/dirs present')

# Each wiki must have >=20 concept pages and >=10 example pages (sanity floor)
for skill in [peer, new]:
    concepts = list((skill / 'moats-and-network-effects/wiki/concepts').glob('*.md'))
    examples = list((skill / 'moats-and-network-effects/wiki/examples').glob('*.md'))
    assert len(concepts) >= 20, f'{skill.name}: only {len(concepts)} concept pages, expected >=20'
    assert len(examples) >= 10, f'{skill.name}: only {len(examples)} example pages, expected >=10'
    print(f'{skill.name}: {len(concepts)} concepts, {len(examples)} examples')
"
```
Expected: all assertions pass, both skills report their wiki page counts. Failure here means a chunk earlier than this was skipped or partial.

- [ ] **Step 3: Verify SKILL.md frontmatter parses for both**

```bash
cd /tmp/skill-test && \
for skill in non-tech-office-hours post-mvp-office-hours; do
    python3 -c "
import re
content = open('$skill/SKILL.md').read()
m = re.search(r'^---\n(.*?)\n---', content, re.DOTALL)
assert m, '$skill: no frontmatter'
print(f'$skill: frontmatter OK')
m2 = re.search(r'description:\s*(.*?)\n---', content, re.DOTALL)
assert m2, '$skill: no description'
desc = m2.group(1).strip()
assert len(desc) <= 1024, f'$skill: description too long ({len(desc)} chars)'
print(f'$skill: description length OK ({len(desc)} chars)')
"
done
```
Expected: both skills pass.

### Task 6.3: Tag the release and push

**Files:** none — git tag operation.

- [ ] **Step 1: Tag v2.0.0**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
git tag -a v2.0.0 -m "$(cat <<'EOF'
v2.0.0 — repo renamed to founder-office-hours; added post-mvp-office-hours skill

Breaking restructure: existing non-tech-office-hours skill content moved
into a subfolder. New peer skill post-mvp-office-hours joins it.

What's new:
- founder-office-hours repo (renamed from non-tech-office-hours)
- post-mvp-office-hours skill (4-segment diagnostic routing, 10-question
  investor mirror, 3 artifacts)
- Karpathy-style wiki on moats and network effects, embedded verbatim
  in both skills (NFX Network Effects Manual + Helmer 7 Powers from
  YC video)
- Top-level README explaining both skills

Acknowledgments: Garry Tan, YC partners, Roger Martin, Hamilton Helmer,
NFX / James Currier, Sean Ellis, Rahul Vohra, Rob Fitzpatrick, Diana Hu,
Andy Rachleff, Andrej Karpathy.
EOF
)"
```

- [ ] **Step 2: Push tag**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && git push origin v2.0.0 && git push origin main
```
Expected: tag and main both pushed.

### Task 6.4: Create the GitHub Release with both zips

**Files:** none — GitHub Release.

- [ ] **Step 1: Create the release via gh CLI**

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
gh release create v2.0.0 \
    dist/non-tech-office-hours.zip \
    dist/post-mvp-office-hours.zip \
    --title "v2.0.0 — founder-office-hours + post-mvp-office-hours" \
    --notes-file - <<'EOF'
## What's new in v2.0.0

This release introduces the repo restructure into `founder-office-hours`
(was `non-tech-office-hours`) and adds a second peer skill:
**post-mvp-office-hours**.

### Two skills, two zips, fully decoupled

Each zip is independently installable. No skill references the other.

**non-tech-office-hours** — for non-technical founders paired with
a technical co-founder, pre-build. Produces FOR_YOU.md + FOR_YOUR_CO_FOUNDER.md.

**post-mvp-office-hours** — for any founder who has already shipped.
4-segment diagnostic, route-calibrated grilling, 10-question investor
mirror (route-gated). Produces WHERE_YOU_ARE.md + WHAT_TO_DO_NEXT.md
+ optionally WHAT_INVESTORS_WILL_ASK.md.

### What's new for non-tech-office-hours

The existing skill is unchanged structurally, but now includes the new
moats-and-network-effects/ Karpathy-style wiki (NFX Network Effects
Manual + Helmer 7 Powers). Cross-references added in ai-native-context.md,
strategy.md, premise-and-alternatives.md.

### Install

```sh
# Claude.ai web: upload via Customize → Skills (do not unzip first)
# Claude Code / Codex / Cursor: ask the agent to install from these URLs

https://github.com/adoistic/founder-office-hours/releases/latest/download/non-tech-office-hours.zip
https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip
```

### Acknowledgments

Garry Tan, YC partners (Jessica Livingston, Paul Graham, Michael Seibel,
Dalton Caldwell), Roger Martin, Hamilton Helmer, NFX / James Currier,
Sean Ellis, Rahul Vohra, Rob Fitzpatrick, Diana Hu, Andy Rachleff,
Andrej Karpathy.
EOF
```
Expected: release created with both assets attached.

- [ ] **Step 2: Verify the download links resolve**

```bash
curl -sIL "https://github.com/adoistic/founder-office-hours/releases/latest/download/non-tech-office-hours.zip" | head -5 && \
curl -sIL "https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip" | head -5
```
Expected: 200 OK or 302 redirect chain ending in 200.

### Task 6.5: Final acceptance check against the spec

**Files:** the spec at `docs/superpowers/specs/2026-05-23-founder-office-hours-restructure-and-post-mvp-skill-design.md`

- [ ] **Step 1: Walk through the spec's Section 13 acceptance criteria with active verification**

Each criterion runs a live check, not a backreference:

```bash
cd "/Users/siraj/office bhours/founder-office-hours" && \
echo "=== AC1: repo renamed ===" && \
gh repo view --json name -q .name | grep -q '^founder-office-hours$' && echo "OK" || (echo "FAIL"; exit 1)

echo "=== AC2: peer skill cross-refs in place ===" && \
grep -q 'moats-and-network-effects' non-tech-office-hours/ai-native-context.md && \
grep -q 'moats-and-network-effects' non-tech-office-hours/strategy.md && \
grep -q 'moats-and-network-effects' non-tech-office-hours/premise-and-alternatives.md && echo "OK" || (echo "FAIL"; exit 1)

echo "=== AC3: new skill fully populated ===" && \
for f in SKILL.md README.md ai-native-context.md principles.md diagnostic.md forcing-questions.md premise-and-alternatives.md strategy.md investor-mirror.md drafting-and-review.md closing.md; do
    test -f "post-mvp-office-hours/$f" || (echo "FAIL: missing post-mvp-office-hours/$f"; exit 1)
done; echo "OK"

echo "=== AC4: both wiki copies exist with full structure ===" && \
for skill in non-tech-office-hours post-mvp-office-hours; do
    test -f "$skill/moats-and-network-effects/CLAUDE.md" && \
    test -d "$skill/moats-and-network-effects/raw" && \
    test -d "$skill/moats-and-network-effects/wiki/concepts" && \
    test -d "$skill/moats-and-network-effects/wiki/examples" || (echo "FAIL: $skill wiki incomplete"; exit 1)
done; echo "OK"

echo "=== AC5: top-level README has both skills and acknowledgments ===" && \
grep -q 'non-tech-office-hours' README.md && \
grep -q 'post-mvp-office-hours' README.md && \
grep -q 'Garry Tan' README.md && \
grep -q 'Hamilton Helmer' README.md && \
grep -q 'NFX' README.md && \
grep -q 'Roger Martin' README.md && echo "OK" || (echo "FAIL"; exit 1)

echo "=== AC6: both zips buildable and functional ===" && \
test -f dist/non-tech-office-hours.zip && \
test -f dist/post-mvp-office-hours.zip && \
unzip -tq dist/non-tech-office-hours.zip > /dev/null && \
unzip -tq dist/post-mvp-office-hours.zip > /dev/null && echo "OK" || (echo "FAIL"; exit 1)

echo "=== AC7: no cross-skill references ===" && \
! grep -rn 'post-mvp-office-hours\|peer skill\|the other variant' non-tech-office-hours/ --include='*.md' && \
! grep -rn 'non-tech-office-hours\|peer skill\|the other variant' post-mvp-office-hours/ --include='*.md' && echo "OK" || (echo "FAIL: cross-skill reference found"; exit 1)

echo "=== AC8: spec and plan committed ===" && \
git log --oneline | grep -q 'spec:' && \
git log --oneline | grep -q 'plan:' && echo "OK" || (echo "FAIL"; exit 1)

echo "=== ALL ACCEPTANCE CRITERIA MET ==="
```

Expected: every check prints "OK"; final line "ALL ACCEPTANCE CRITERIA MET" is printed.

If any check fails, stop and surface the failing criterion to Adnan — do not proceed to Step 2.

**Note on AC7's check:** the strict reading of the spec is no cross-skill references that imply a peer exists. The substrings "post-MVP" and "pre-MVP" naturally appear in each skill's own files when talking about themselves (post-mvp skill says "post-MVP" about itself; non-tech skill may say "pre-build" about itself). Those are fine. The check therefore targets only the **literal peer folder names** and **phrasings that explicitly invoke a peer** ("peer skill", "the other variant"). The decoupling-audit Task 5.12 (Round 2 fix) is the broader, deliberately noisy check that catches subtle phrasings during build; AC7 is the strict release-time gate.

- [ ] **Step 2: Commit the final state and announce completion**

If any cleanup commits remain, commit them with `final: post-implementation cleanup`. Then notify Adnan:

> Implementation complete. v2.0.0 released. Both zips live:
> - https://github.com/adoistic/founder-office-hours/releases/latest/download/non-tech-office-hours.zip
> - https://github.com/adoistic/founder-office-hours/releases/latest/download/post-mvp-office-hours.zip
>
> The old `non-tech-office-hours` GitHub URLs continue to work via GitHub auto-redirect.
> Spec at docs/superpowers/specs/2026-05-23-founder-office-hours-restructure-and-post-mvp-skill-design.md.
> Plan at docs/superpowers/plans/2026-05-23-founder-office-hours-restructure-and-post-mvp-skill.md.

### Chunk 6 review checkpoint

Dispatch the plan-document-reviewer for Chunk 6. Iterate until approved. This is the last chunk.

---

## Implementation notes for the executing agent

### Reuse + DRY

- The peer skill files are the source-of-truth template for most of the new skill's files. Copy first, then adapt. Do not write from scratch.
- The wiki is verbatim-duplicated between skills (per the decoupling rule). Build it once in non-tech-office-hours/, copy to post-mvp-office-hours/. Do not edit each copy independently.

### YAGNI

- Do not add wiki pages for concepts not in the two raw sources. No "synergies" or "bandwagon-2" inventions.
- Do not add additional phase modules beyond the 11 specified.
- Do not add additional artifacts beyond the 3 specified.
- Do not generalize the diagnostic to handle non-post-MVP founders. The skill explicitly does not serve them.

### Commit frequency

- Commit after each Task's Step "Commit" point. Each commit is a self-contained step.
- ~25-30 commits expected across the full plan.

### When to surface to Adnan

- If push/admin access to the GitHub repo is not confirmed (Task 1.1 Step 1).
- If the Helmer YC transcript is not available when Task 2.3 lands (continue with Chunks 1, 2 NFX portion, and 5; pause at Task 3.5).
- If the NFX library URL structure has changed and the scrape returns unexpected content (Task 2.1 Step 5).
- If the spec's acceptance criteria cannot be met (Task 6.5 Step 1).
- If the plan-document-reviewer iteration loop exceeds 5 cycles on any chunk.

### Skill references used during implementation

- `@superpowers:subagent-driven-development` — for dispatching subagents per task (if available in harness)
- `@superpowers:executing-plans` — fallback if no subagent capability
- `@superpowers:test-driven-development` — though the "tests" here are structural (zip builds, frontmatter parses, lint passes)
- `@superpowers:verification-before-completion` — before claiming any chunk complete
