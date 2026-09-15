---
name: globai-catalog
description: Query the public Glob.AI AI Pods catalog — groups, offerings, capabilities, and per-token pricing — via an unauthenticated JSON endpoint.
---

# Glob.AI catalog

## When to use this skill

Use it to answer questions about what Glob.AI sells: AI Pods (managed AI delivery pods), their capability groups, what each offering includes, what it is and is not a fit for, and per-token pricing where visible.

## How to fetch the catalog

```
GET https://glob.ai/api/catalog
Accept: application/json
```

No authentication is required. The response is cached server-side; expect it to be up to ~10 minutes stale.

## Response shape

```
{
  "version": string,
  "groups": [
    {
      "name": string,
      "description": string,
      "offerings": [Offering]
    }
  ],
  "offerings": [Offering]   // flat list, ordered by sort_order
}
```

Each `Offering` has: `name`, `sku_id`, `problem_statement`, `outcome_statement`, `what_you_get[]`, `capabilities_included[]`, `best_for[]`, `not_a_fit_for[]`, `notes`, `group_name`, `price_per_unit_usd`, `unit_price_usd`, `price_unit` (`"price_per_100k_tokens"`, `"price_per_million_tokens"`, or `""` when unpriced), and optionally `sort_order` and `partner`.

## Pricing caveat

The endpoint renders the catalog for the anonymous audience. When the platform hides prices for anonymous viewers, `price_unit` is `""` and the price fields are not meaningful — do not quote prices in that case; link to https://glob.ai/en/catalog instead.

## Related resources

- Machine-readable API description: https://glob.ai/openapi.json
- API documentation: https://glob.ai/docs/api.md
- Full site content for agents: https://glob.ai/llms-full.txt