# Switching Costs

**Category:** Helmer Power
**Source:** raw/yc-helmer-7-powers-transcript.md

## Definition

Switching costs exist when changing to a competitor becomes so expensive (financially, operationally, or in time) that a customer stays even if the alternative is modestly better. As Garry Tan puts it: "you get a moat when your customers are kind of trapped because it becomes very expensive for them to find another solution." Classic SaaS examples are Oracle (data migration too painful) and Salesforce (workflow rebuilds, retraining, and data migration can cost a year of productivity).

## Mechanism

- Deep integration into customer workflows means switching requires rebuilding processes, retraining staff, and migrating data. These costs far exceed the value of any marginal improvement by a competitor.
- Long pilot periods (six months to a year) with forward-deployed engineers create custom logic specific to one customer's operations, making the AI agent functionally irreplaceable.
- AI-era memory and personalization accumulate over time: the longer a customer uses the product, the more the agent understands their context, raising the cost to restart with a competitor.

## When it applies

- Customer workflows are deeply customized around the product's logic, not just its data.
- Switching would require rebuilding integrations with internal systems (banks, logistics platforms, ERP).
- Consumer personalization (memory, preferences, learned behavior) has accumulated to the point that starting over costs the user significant context.

## Kill-test

If your top customer got a six-month free trial from your best competitor tomorrow, what would they have to rebuild, retrain, and re-integrate before going live? If the answer is "nothing material," you have vendor preference, not switching costs.

## AI-native erosion check

Mixed picture. Old-school data-migration switching costs (the Oracle and Salesforce flavor) are eroded by LLMs: language models can morph data from one schema to another and browser automation can extract data from systems that block export. But the AI-native form is genuinely new and harder to erode: deep agent customization of workflow logic (not just data) did not exist in the SaaS era. Happy Robot's DHL integration and Salient's bank-specific loan consultation flows are not migratable by an LLM, because the logic was built collaboratively over months.

## Related concepts

- [[moats]]
- [[process-power]]
- [[cornered-resource]]
- [[counter-positioning]]
- [[network-economies]]
- [[ai-native-moat-shift]]

## Case studies

- [[examples/salesforce-expertise]]
- [[examples/microsoft-platform]]
