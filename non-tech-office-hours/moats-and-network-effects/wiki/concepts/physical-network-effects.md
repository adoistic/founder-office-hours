# Physical Network Effects

**Category:** Direct
**Source:** raw/nfx-network-effects-manual.md (line 189)

## Definition

Physical network effects arise when the nodes and links of a network are physical objects — telephone cables, rail tracks, water pipes, power lines. Each new physical node (a home connected to the grid, a station on a rail line) increases the value of every existing node. The network literally cannot be replicated without rebuilding the physical infrastructure.

## Mechanism

- Every new physical node added (house wired for cable, car added to a fleet) raises the total number of reachable endpoints for every other node.
- Capital intensity locks out competition: a rival must fund the same civil engineering before it can offer comparable coverage.
- Physical networks layer naturally with scale economies and embedding, compounding the defensibility beyond the network effect alone.

## When it applies

- Your product's core value depends on physical infrastructure you own or control (wires in the ground, cell towers, rails).
- Each new installation adds direct utility to all existing installations, not just to the new user.
- Switching requires customers to abandon their physical endpoint, not just a software account.

## Kill-test

Pull your coverage map and churn data by geographic cluster. If users in dense, mature clusters churn at the same rate as users in sparse, new clusters, the physical network is not producing the value gain you claim — something else is retaining them.

## AI-native erosion check

Physical network effects are the most AI-resistant of all 16 types. Software factories and LLM agents can replicate code in weeks; they cannot lay fiber or build cell towers. If anything, AI-driven logistics optimization strengthens physical networks by squeezing more value from existing infrastructure. The moat is intact.

## Related concepts

- [[network-effects]]
- [[protocol-network-effects]]
- [[tech-performance-network-effects]]

## Case studies

- [[examples/att-physical-network]]
