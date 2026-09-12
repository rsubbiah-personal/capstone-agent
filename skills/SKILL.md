---
name: customer-support-resolution
description: Resolve a customer support request using the knowledge base, escalating when policy requires it. Use when handling a customer question about products, policies, or order issues.
---

# Customer Support Resolution

## When to use
A customer asks a question that may be answerable from the indexed knowledge base
(product catalog, company policy, FAQ, escalation guidelines).

## Procedure

1. Redact PII from the incoming message before anything else.
2. Retrieve the top-k relevant chunks with the knowledge search tool.
3. If no chunk clears the minimum retrieval score, say the answer is not in the
   knowledge base — do not improvise.
4. Draft an answer grounded strictly in the retrieved context, citing the source
   document for each claim.
5. Run the policy checker. If a rule with severity `escalate` fires, call the
   escalation tool instead of answering.
6. Return the answer along with its sources and the feedback prompt.

## Constraints
- Never state a refund, warranty, or entitlement that is not in the retrieved context.
- Never echo customer PII back in the response.
- Prefer escalation over guessing when confidence is below the configured threshold.
