# Data Network Effects

**Category:** Data
**Source:** raw/nfx-network-effects-manual.md (line 659)

## Definition

A data network effect exists when a product becomes more valuable as more users generate more useful data, and when that improved product in turn attracts more users. Usage feeds data; data feeds product quality; quality feeds usage. Most products collect data, but few have genuine data network effects — the data must be central to the product's value delivery, and usage must be the primary driver of new data collection.

## Mechanism

- Each new user session generates data that measurably improves predictions, recommendations, or personalization for existing users.
- The improvement loop is tight: the product gets better fast enough that users notice the difference, reinforcing engagement.
- The dataset is proprietary and grows with usage — a competitor starting from zero cannot buy their way to equivalent coverage quickly.

## When it applies

- Data is the core value mechanism of the product, not a marginal feature (navigation accuracy for Waze, route prediction; recommendation relevance for a streaming service where the algorithm is the product).
- Most users both consume and produce useful data passively through normal usage — you are not dependent on a small minority of active contributors.
- The dataset requires continuous real-time updating, so recency gives incumbents a compounding advantage that cannot be bridged with a historical data dump.

## Kill-test

Does each new data point measurably improve the product for existing users? Not "will" — has it measurably in the last 30 days? Pull your model performance metrics before and after a 20% user base growth event. If the metrics are flat, you have a data scale advantage, not a data network effect.

## AI-native erosion check

Foundation models trained on internet-scale data partly commoditize proprietary datasets, because general-purpose reasoning can substitute for narrow behavioral data in some use cases. However, real-time, domain-specific, or behavioral data that does not exist in public training sets remains a genuine advantage. The moat narrows for historical or static datasets and holds for continuously-updated, usage-generated behavioral signal.

## Related concepts

- [[network-effects]]
- [[tech-performance-network-effects]]
- [[expertise-network-effects]]

## Case studies

- [[examples/google-data]]
