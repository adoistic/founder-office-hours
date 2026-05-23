# Hub-and-Spoke Network Effects

**Category:** Hub-and-Spoke
**Source:** raw/nfx-network-effects-manual.md (line 367)

## Definition

A hub-and-spoke network effect occurs when many equal nodes submit content or goods to a central hub, and the hub selects a few for redistribution to nearly all nodes. The lottery-like chance of selection — with asymmetric, sudden rewards for winners — incentivizes every node to invest effort in high-quality contributions, generating enormous aggregate value for the hub without the hub bearing creation costs.

## Mechanism

- The hub's algorithmic selection process directs a power law: a small number of nodes receive outsized attention, which motivates all other nodes to try harder.
- Unlike broadcast (Sarnoff's Law, value scales linearly with audience), nodes also interact with each other, so value scales closer to Metcalfe's Law.
- The aspiration of selection keeps contribution volume high even for nodes that are rarely or never chosen, making the hub's supply self-sustaining.

## When it applies

- The hub controls a scarce, high-value distribution channel that individual nodes cannot replicate independently.
- The reward of being selected is large enough (traffic, revenue, status) that nodes will invest effort in quality without guaranteed return.
- Nodes can also connect with each other, creating a secondary social layer that reinforces retention beyond the selection lottery.

## Kill-test

Survey the bottom 80% of contributors (those never selected for hub distribution). If more than half report they will stop contributing within 90 days, the lottery incentive is insufficient and the hub-and-spoke effect is collapsing. Sustained contribution from perpetually-unselected nodes is the proof point.

## AI-native erosion check

AI dramatically lowers the cost of content creation, which floods hub-and-spoke platforms with low-quality submissions. This devalues the selection signal — the lottery prize shrinks if everyone can enter with zero effort. Platforms that compete on curation quality (human editors, verified creators) will maintain hub authority; platforms that rely on pure algorithmic volume will find the effect weakens as signal-to-noise collapses.

## Related concepts

- [[network-effects]]
- [[personal-network-effects]]
- [[bandwagon-network-effects]]

## Case studies

- [[examples/tiktok-hub-and-spoke]]
