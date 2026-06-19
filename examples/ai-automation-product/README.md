# Example: AI Automation Product

This example shows how Agent Execution OS can be adapted for an AI-powered product with prompts, background workers, provider costs, evaluations, and user-facing outputs.

## Project type

AI automation product.

## Risk profile

High when AI outputs affect user decisions, cost money, touch private data, or trigger actions automatically.

## Example sections

```text
Section 1: Foundation, Environments & Provider Boundaries
Section 2: Prompt Contracts & Versioning
Section 3: Worker/Queue Reliability
Section 4: Cost Controls, Quotas & Rate Limits
Section 5: Evaluation Dataset & Quality Scoring
Section 6: User Feedback & Human Review
Section 7: Observability, Logging & Redaction
Section 8: Billing and Plan Gates
```

## AI-specific quality extensions

- Prompts that affect product behavior must be versioned.
- Provider calls must have timeout/retry behavior.
- Expensive routes must have quota or rate limits.
- User data sent to AI providers must be intentional and documented.
- AI outputs persisted to DB must be validated where possible.
- Evaluation cases must be updated when scoring/routing logic changes.
- Logs must redact private user content unless explicitly approved.

## Example task names

```text
01_audit-ai-provider-usage.md
02_define-prompt-versioning-contract.md
03_add-cost-ledger-for-model-calls.md
04_create-evaluation-fixture-set.md
05_add-provider-failure-fallbacks.md
```

## Example user request

```text
I need the AI provider test API key so the staging worker can run model calls without using production credentials.

How to get it:
1. Open the AI provider dashboard.
2. Create a new project or key named `[project]-staging`.
3. Set usage limits if the provider supports it.
4. Copy the key.
5. Add it to Vercel/CI staging secrets as `AI_PROVIDER_API_KEY`.

Safety: do not commit the key. Use a staging-specific key with a spending limit.

Next: after the key is added, the provider boundary task can verify model calls, timeouts, and failure handling in staging.
```
