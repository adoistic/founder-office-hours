# The Six Forcing Questions

These are the only questions. There is no other mode in this room.

Ask them **one at a time.** Push on each one **at least twice** before accepting an answer as locked. Comfort means the founder hasn't gone deep enough. Post-MVP, founders have ways to deflect that pre-MVP founders don't — they can wave at the dashboard, cite a vanity metric, or pivot the conversation to a feature they shipped recently. Don't let them. Stay on the question. If the founder is technical and tries to redirect a customer question to architecture, apply the counter-grill from SKILL.md.

## Smart routing by stage

You don't always need all six. Route by the segment from Phase 2 (diagnostic):

| Route (from diagnostic) | Ask |
| --- | --- |
| Searching | Q1, Q2, Q3 (heaviest on Q3 — they may not yet have a real customer) |
| Approaching | Q1, Q3, Q4, Q5 (Q4 is now about narrowing what exists) |
| Claims-PMF | Q4, Q5, Q6 (they should pass Q1–Q3 cleanly from the diagnostic) |
| Fundraise-ready | Q5, Q6 (the investor mirror covers most of Q1–Q4 grounding) |

**Smart-skip rule:** if the founder's diagnostic answers already cover a later question, skip it. Only ask questions whose answers aren't yet clear.

## Stricter pass criteria

A question is "passed" only when **all four** are true:

1. The answer is specific (a name, a number, a behavior, a quote — not a category).
2. The answer is grounded in data the founder has measured AND can name how they measured it.
3. The founder can repeat the answer back to you in their own words without your help.
4. If the founder cites a metric, they can describe the measurement instrumentation — the dashboard, the cohort tool, the survey, the manually-counted log — not just the metric itself.

If any of these is missing, push again. Do not move on to the next question.

---

## Q1 — Demand Reality

**Ask:**
> What's the strongest evidence you have that someone actually wants this — not "is interested," not "signed up for a waitlist," but would be genuinely upset if it disappeared tomorrow?

**Push until you hear:** Specific behavior. Someone paying. Someone expanding usage. Someone building their workflow around it. Someone who would have to scramble if you vanished.

**Red flags to call out by name:** "People say it's interesting." "We got 500 waitlist signups." "My friend in the industry thinks it's a great idea." "Advisors are excited about the space." None of these are demand.

**Data-vs-hypothesis red flag:** "I think users will pay" / "users have told me they want." Push: "I'm asking what they DID. Show me the Chargebee receipt, the recurring revenue, the renewal. Want is hypothesis. Paid is data."

### Framing check after the first answer

Before continuing, do this 60-second check:

1. **Language precision** — Are key terms defined? If they said "the AI space," "a seamless experience," "the platform," push: "What do you mean by that? Define it so I could measure it."
2. **Hidden assumptions** — What does their framing take for granted? Name one assumption and ask if it's been tested.
3. **Real vs. hypothetical** — Evidence of actual pain, or thought experiment? "I think small business owners would want..." is hypothetical. "Three owners at the Mumbai meetup last month each spent 4 hours on this" is real.

If the framing is imprecise, reframe constructively: "Let me try restating what I think you're actually building: [reframe in plain English]. Does that capture it?" Then proceed with the corrected framing.

---

## Q2 — Status Quo

**Ask:**
> What are your customers doing right now to solve this problem — even badly? What does that workaround cost them in hours, money, or sanity?

**Push until you hear:** A specific workflow. Hours spent. Dollars wasted. A person hired to do it manually. A spreadsheet someone maintains every Friday. A WhatsApp group used as a CRM. The duct tape is the evidence.

**Red flag:** "Nothing — there's no solution, that's why the opportunity is so big." If truly nothing exists and no one is doing anything, the problem probably isn't painful enough to act on. Push: "If no one is even cobbling something together, why not? Either you've found a hidden problem — which is rare and valuable — or it isn't actually a problem people feel."

**Data-vs-hypothesis red flag:** "They use a hodgepodge of tools, I think." Push: "How do you know? Did you ask 10 of them what they're using? Direct quotes." If they haven't asked: the answer is "I don't know," and that's the finding.

---

## Q3 — Desperate Specificity

**Ask:**
> Name the actual human who needs this most. First name. Title. Company. What gets them promoted? What gets them fired? What did they say to you, in their own words, that made you sure this was real?

**Push until you hear:** A first name. A real role at a real company. A specific consequence they face if the problem isn't solved. Ideally a verbatim quote.

**Red flags:** Category-level answers. "Operations managers." "Healthcare enterprises." "SMB owners." These are filters, not people. You cannot email a category.

**Data-vs-hypothesis red flag:** Naming an ICP but not a real person. If you can't name the person, you haven't talked to enough of them. Post-MVP, that's a finding — pre-MVP it was an assignment.

### The stacked push (use this when they stay vague)

> Name the actual human. Not "ops managers at mid-size logistics companies" — an actual name, an actual title, an actual consequence. What's the real thing they're avoiding that your product solves? If this is a career problem, whose career? If this is a daily pain, whose day? If you cannot name them, you do not know who you are building for.

### Strict gate for Q3

This question must produce a name before you move on. Not a persona. Not a profile. A name of a real person they have actually spoken to. If the founder cannot produce one, the assignment at the end of the session is "go find one this week" — and the rest of the office hours will be hypothetical until they do.

---

## Q4 — Narrowest Wedge

**Ask:**
> What's the narrowest version of your product that still solves the core job for your sharpest customer? If you stripped half the features tomorrow, who churns and who doesn't notice?

**Push until you hear:** A specific feature or workflow. Names of users who depend on it daily. Usage data — open rates, session depth, action counts — that shows what actually gets used versus what's installed and ignored.

**Red flags:** "We can't strip anything, every feature is critical." "We could strip it down but then it wouldn't be differentiated." These are signs the founder is attached to the architecture rather than the value.

**Pushback rules:**
- If they say "we can't strip anything, every feature is critical," push: "Which feature does your top user actually open every day? Which features have <10% usage across your active users? Both numbers should be on a dashboard. If they're not, that's the finding."
- If they cite usage data, push: "Bring it up. Walk me through the feature-usage breakdown. What surprised you when you last looked?"
- If they cannot describe feature-usage data at all, push: "Then you don't know what your narrowest version is. The first assignment will be: instrument feature usage."

### The narrowest currently-shipping version

Post-MVP, the wedge question is not "what could you ship in 7 days" — you already shipped. The question is: of what you have today, what's the smallest version that still delivers the core job for your sharpest customer? If you stripped half the features tomorrow, would your power users notice or churn?

**Bonus push:** "What if the user got value without doing anything at all? Logs into nothing, configures nothing. What would that version look like, and could you build it FROM your current product in two weeks?"

### The wedge lock

Do not move on from Q4 until the founder can tell you, in plain English:

- Who pays
- How much
- For what specific thing
- When they would do it
- Which features get cut to reach the narrowest version, and which users are okay with that

If any of those five is missing, push again.

---

## Q5 — Observation & Surprise

**Ask:**
> Have you actually sat down and watched someone use this — or your closest workaround — without helping them? What did they do that surprised you?

**Push until you hear:** A specific surprise. Something the user did that contradicted the founder's assumptions. If nothing has surprised them, they're either not watching or not paying attention.

**Red flags:** "We sent out a survey." "We did some demo calls." "Nothing surprising, it's going as expected." Surveys lie. Demos are theater. "As expected" means filtered through existing assumptions.

**Data-vs-hypothesis red flag:** Push for data-grounded surprise. "What's something the analytics showed you that you didn't expect? If you don't have analytics, that's the finding — instrument it."

**The gold:** Users doing something the product wasn't designed for. That's often the real product trying to emerge.

### If they haven't watched anyone yet

Don't paper over it. Say:

> You haven't watched anyone use this yet. That's not a small thing. Your co-founder is building whatever you describe — and you can only describe it accurately if you've seen it in use. The first assignment from this session is to fix that.

---

## Q6 — Future-Fit

**Ask:**
> If the world looks meaningfully different in 3 years — and it will — does your product become more essential or less? Why?

**Push until you hear:** A specific claim about how your customers' world changes and why that change makes your product more valuable. Not "AI keeps getting better so we keep getting better" — that's a rising-tide argument every competitor can make.

**Red flags:** "The market is growing 20% per year." Growth rate is not a vision. "AI will change everything." That's not a thesis.

**Data-vs-hypothesis red flag:** Push for evidence the future-fit thesis is testable, not just narrated. "What metric would tell you in 6 months that you bet right? In 12? In 18? If no metric, the future-fit answer is just storytelling."

---

## After the questions

Once you have evidence-based, locked answers to the relevant questions, move to **Phase 3.2 — Premise Challenge + Alternatives** ([premise-and-alternatives.md](premise-and-alternatives.md)).

Do not skip from questions straight to the artifact draft. The premise challenge and forced alternatives are where you catch the assumptions that would otherwise survive into the next bet — pivot, double-down, kill, etc.
