# Two-Sided Marketplace

**Category:** 2-Sided
**Source:** raw/nfx-network-effects-manual.md (line 464)

## Definition

A two-sided marketplace connects buyers and sellers through a platform that serves as intermediary. Each additional seller increases value for buyers (more choice, better prices); each additional buyer increases value for sellers (more demand). The network — not the app's features — provides the majority of the value. This cross-side reinforcement makes successful marketplaces extremely difficult to disrupt because you must offer a better deal to both sides simultaneously.

## Mechanism

- Cross-side effect: more sellers attract more buyers attract more sellers, compounding with each cycle.
- Same-side competition is usually negative — more sellers compete with each other — but the indirect benefit of attracting more buyers typically outweighs this cost, keeping sellers on the platform.
- Multi-tenanting (sellers listing on multiple platforms simultaneously) is the primary structural weakness; lock-in must come from tools, reputation, or liquidity that competitors cannot match.

## When it applies

- You have two distinct user populations with complementary needs where each side's value is directly proportional to the size of the other side.
- Your platform achieves a liquidity threshold: enough supply that demand-side users reliably find what they need without searching elsewhere.
- The switching cost for at least one side is high enough to resist multi-tenanting (exclusive inventory, embedded tools, reputation system).

## Kill-test

Pull cohort data for buyers who joined in months when seller supply was low versus high. If buyer retention rates are indistinguishable across those cohorts, buyers are returning for price, habit, or trust — not because the network grew. You do not have evidence of a marketplace network effect without that retention differential.

## AI-native erosion check

AI lowers discovery friction (better search, automated matching), which can accelerate marketplace liquidity formation — helpful for incumbents and attackers alike. The moat itself (cross-side network density) is unchanged by AI, but AI-powered vertical competitors can achieve liquidity faster in narrow niches, making horizontal incumbents more vulnerable to specialist challengers.

## Related concepts

- [[network-effects]]
- [[platform-network-effects]]
- [[asymptotic-marketplace]]
- [[market-network-effects]]

## Case studies

- [[examples/ebay-two-sided-marketplace]]
- [[examples/craigslist-two-sided-marketplace]]
- [[examples/uber-two-sided-marketplace]]
- [[examples/airbnb-two-sided-marketplace]]
