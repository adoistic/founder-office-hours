# Platform Network Effects

**Category:** 2-Sided
**Source:** raw/nfx-network-effects-manual.md (line 510)

## Definition

A platform network effect is a two-sided effect where the supply side (developers, game studios) engineers products that exist only because of and within the platform. Supply-side contributors must integrate deeply to participate — they are not merely listing inventory, they are building assets that are a function of the platform itself. This deep integration makes both sides more expensive to leave than in a standard marketplace.

## Mechanism

- More developers build on the platform; more apps or games increase value for users; more users attract more developers — a cross-side flywheel.
- Developer investment (porting, API integration, certification) creates sunk costs that discourage multi-tenanting more effectively than marketplace listings where the same item ships anywhere.
- The platform's own features (hardware, SDK, performance) add direct value independent of the network, making the product defensible even before the network effect is fully formed.

## When it applies

- Third-party developers must build a distinct version of their product for your platform — porting is non-trivial.
- Your platform controls critical distribution (app store, console shelf, OS runtime) so developers cannot reach your users without going through you.
- User switching cost includes losing access to platform-specific apps, saves, achievements, or integrations, not just a new login.

## Kill-test

Count your top 20 third-party developers. How many of them are exclusive to your platform? If all 20 also ship on competitor platforms with minimal modification, multi-tenanting is unconstrained and your platform effect is weaker than claimed. Exclusivity — even partial — is the measurable signal of genuine platform lock-in.

## AI-native erosion check

AI lowers the cost of cross-platform porting (code generation, automated API adapters), which weakens the integration-cost moat on the supply side. Platforms that depend primarily on developer lock-in face real erosion; platforms that also control hardware, identity, or payment rails (iOS, Android) remain structurally defended because AI cannot replicate hardware distribution.

## Related concepts

- [[network-effects]]
- [[two-sided-marketplace]]
- [[asymptotic-marketplace]]
- [[tech-performance-network-effects]]

## Case studies

- [[examples/microsoft-platform]]
