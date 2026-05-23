# Asymptotic Marketplace

**Category:** 2-Sided
**Source:** raw/nfx-network-effects-manual.md (line 560)

## Definition

An asymptotic marketplace is a two-sided marketplace where the value delivered to the demand side increases rapidly with early supply additions but flattens sharply past a local sufficiency threshold. Adding the 100th driver in a city matters greatly; adding the 10,000th matters almost nothing to a rider who already waits under four minutes. This diminishing cross-side value makes the marketplace more vulnerable to competition than a standard marketplace with proportional value scaling.

## Mechanism

- Early supply additions produce outsized demand-side value (wait times drop from 20 to 8 minutes; the jump from 8 to 4 is significant; from 4 to 2 is near-imperceptible).
- Once the demand side reaches "good enough" service, they become indifferent to marginal supply increases, enabling a smaller competitor to match perceived quality with far less supply.
- Multi-tenanting is high on both sides because neither side pays a real penalty for switching when quality is equivalent at a lower supply level.

## When it applies

- Your supply side provides a commodity or near-commodity service where quality plateaus at a threshold (wait time, response time, selection depth past a point).
- Demand-side users have no strong identity or reputation investment in the platform — transactions are anonymous and interchangeable.
- Geographic or temporal fragmentation means your supply density advantage must be rebuilt market by market, giving competitors viable local entry points.

## Kill-test

Measure demand-side satisfaction scores at your 10th, 50th, and 90th supply-density percentile markets. If satisfaction is statistically flat across the 50th and 90th percentiles, you are past the asymptote. A competitor entering at 50th-percentile supply can match your user experience — your moat in those markets is pricing and brand, not network effect.

## AI-native erosion check

AI dispatch optimization squeezes more value from a given supply pool, accelerating the asymptote arrival — you reach "good enough" with fewer nodes. This is slightly positive for incumbents (lower supply cost) but also accelerates challenger viability (challengers can match quality with less supply). Net effect: the asymptotic vulnerability compounds in an AI-optimized world.

## Related concepts

- [[network-effects]]
- [[two-sided-marketplace]]
- [[platform-network-effects]]

## Case studies

- [[examples/uber-two-sided-marketplace]]
