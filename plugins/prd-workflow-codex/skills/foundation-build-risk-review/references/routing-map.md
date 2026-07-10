<!-- PM-Skills | https://github.com/product-on-purpose/pm-skills | Apache 2.0 -->
# Routing map

The Build Risk Review is a gate that dispatches into the rest of the library. Always name a routing target so the user knows the next move.

## By verdict

| Verdict | Means | Route to |
|---|---|---|
| **Build small** | worth a narrow first version | bundled `define-problem-statement`, `define-hypothesis`, then `show-me-the-prd` |
| **Validate first** | direction plausible; demand, payment, or distribution unproven | bundled `define-hypothesis`, then run its no-code validation approach |
| **Pivot first** | the area is plausible but the current wedge is too broad, crowded, or weak | stop and document what must be reframed before PRD work |
| **Don't build yet** | too vague, no reachable user, or solved well enough already | stop and state the evidence required to reopen the decision |

## By risk type

When a specific risk dominates and warrants a deeper look, route per the "Routes to" column in `references/risk-taxonomy.md` (e.g. a `monetization` risk routes to `foundation-lean-canvas` Revenue; a `demand` risk to `discover-market-sizing`).

## Several competing requests

If the input is not one build decision but a set of requests to rank, return a constrained shortlist and suggest a prioritization skill only when one is installed. This skill judges one decision's risk of failure; it does not rank a list.

## Boundaries (NOT this skill's job)

- A launched product's pivot-or-persevere call, weighing market feedback -> `iterate-pivot-decision`.
- Framing a confirmed problem for the team or leadership -> `define-problem-statement`.
- Designing the test for a chosen assumption -> `define-hypothesis`.
- The full nine-block business model -> `foundation-lean-canvas`.
