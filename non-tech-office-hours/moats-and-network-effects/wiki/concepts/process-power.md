# Process Power

**Category:** Helmer Power
**Source:** raw/yc-helmer-7-powers-transcript.md

## Definition

Process power is the defensibility that comes from having built something so complex and carefully tuned over time that replication is prohibitively expensive — not because of IP protection, but because the process itself requires years of accumulated judgment. The book's canonical example is the Toyota assembly line. The AI version, per Jared Friedman: "a really complicated AI agent that's been finely honed over multiple years to work really well under real world conditions."

## Mechanism

- The gap between a demo built in a weekend and a production system handling mission-critical work is enormous — the last 10-20% of reliability is the defensible part.
- Domain-specific edge cases are invisible to outsiders: you cannot replicate a KYC compliance agent without first knowing what the edge cases in KYC are, and that knowledge only comes from operating at scale.
- The process compounds: CI/CD pipelines, evals, incident playbooks, and integration surface area accumulate into a system not replicable by hiring a handful of engineers.

## When it applies

- The product is mission-critical: failures cost the customer real money, regulatory risk, or business continuity.
- The relevant domain has a high density of edge cases that are invisible until encountered at volume.
- The operational surface area (number of integrations, failure modes, compliance requirements) is large enough that breadth itself is the moat.

## Kill-test

Could a well-funded competitor with 1,000 engineers replicate your process in 18 months by hiring 3-5 of your senior people? If yes, it's not process power, it's just hard work.

## AI-native erosion check

Process power is the most eroded Helmer power in the AI era. AI coding tools compress the 80% solution dramatically — a hackathon version of almost any agent is now fast to build. The moat survives only when the demo version would destroy customer value if deployed. Casetext (Jake Heller's original example), Greenlight's bank KYC agent, and Casa's loan origination system are the canonical cases. If a bank relies on the agent and it fails, they lose millions. That failure mode is what makes the process defensible. Garry Tan: "the version you build in a hackathon isn't useful to anyone." Process power requires real-world validation under mission-critical conditions, not code volume.

## Related concepts

- [[moats]]
- [[cornered-resource]]
- [[switching-costs]]
- [[scale-economies]]
- [[counter-positioning]]
- [[ai-native-moat-shift]]

## Case studies

- [[examples/microsoft-platform]]
