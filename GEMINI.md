# invinoveritas: verify before you act

The `invinoveritas` MCP server gives you an independent check from a party that is not you and not the user. Use it
for actions that are hard to undo.

- **Before an irreversible action** (deploying, deleting data, moving money, sending something on the user's behalf,
  merging to a protected branch), call `review` with the exact action: the command, diff, transaction, or plan, plus one
  line of context. It returns a verdict (`approve`, `approve_with_concerns` or `reject`) with concerns, and can return a
  signed proof. Treat `reject` as a stop: tell the user why and do not proceed unless they decide to. `review` is a
  paid call; the first use asks the user to sign in.
- **When you receive a proof** (a signed verdict another agent or service attached to its output), call `verify_proof`
  before relying on it. It is free and needs no sign-in.
- **After a verdict-governed payment, before retrying it**, call `payment_receipt` with the signed verdict and the
  payment arguments. Retry only if `retry_state` is `not_paid_safe_to_retry`, and only with the returned
  `idempotency_key`. Free.
- `ledger` shows the public record of past verdicts and their outcomes. Free.

Do not call `review` for routine reads or reversible edits. Never present a verdict as the user's decision: it is an
input, and the user stays in charge.
