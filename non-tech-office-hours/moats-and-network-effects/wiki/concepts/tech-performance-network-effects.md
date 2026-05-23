# Tech Performance Network Effects

**Category:** Tech Performance
**Source:** raw/nfx-network-effects-manual.md (line 731)

## Definition

Tech performance network effects occur when the technical performance of a product — speed, accuracy, cost, reliability — improves directly as a function of more users or devices on the network. More nodes make the network technically better for every existing node, not just larger. This is distinct from revenue-funded R&D: the performance improvement must be a direct mechanical consequence of network scale, not a downstream result of the revenue scale generates.

## Mechanism

- Each additional node contributes computational capacity, bandwidth, or sensing coverage that every other node can consume (BitTorrent seeders, Tile's Bluetooth mesh, Waze's GPS feeds).
- Performance improvement is automatic and continuous — no engineering work required to capture the benefit of a new node joining.
- A competitor starting from zero not only lacks the features but operates at a mechanically inferior performance level until it closes the node-count gap.

## When it applies

- The product's core technical output (latency, coverage density, prediction accuracy) scales as a direct function of node count, not revenue or dataset size.
- Users or devices contribute resources to the network passively — no active contribution is required to participate in the performance improvement loop.
- The performance difference between a small and large node-count deployment is perceptible to users and affects their primary reason for using the product.

## Kill-test

Partition your user base: compare product performance metrics (latency, accuracy, coverage) in your top 10% densest markets versus your bottom 10% sparsest markets. If performance is statistically identical, node count is not driving performance — you have marketing language, not a tech performance network effect.

## AI-native erosion check

AI inference at the edge and model distillation can partly replicate what peer-to-peer performance networks do — LLM agents can coordinate, route, and optimize without requiring physical node density. This is a genuine threat: AI closes the performance gap between large and small networks faster than in 2023. Tech performance network effects for purely software-based tasks face real erosion. Physical-layer networks (mesh radio, Bluetooth proximity) remain more durable.

## Related concepts

- [[network-effects]]
- [[data-network-effects]]
- [[physical-network-effects]]

## Case studies

- [[examples/bittorrent-tech-performance]]
