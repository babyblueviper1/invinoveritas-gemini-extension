# invinoveritas for Gemini CLI

An independent check before your agent does something it can't undo, from a party that is neither the agent nor you.

```sh
gemini extensions install https://github.com/babyblueviper1/invinoveritas-gemini-extension
```

The extension connects Gemini CLI to the invinoveritas MCP server (`https://api.babyblueviper.com/mcp/verify`, streamable
HTTP) and adds a short context file so the model knows when to use it.

| Tool | What it does | Cost |
|---|---|---|
| `review` | Verdict on an exact action (command, diff, transaction, plan): approve, approve_with_concerns or reject, with concerns and an optional signed proof | paid; first use opens an OAuth sign-in |
| `verify_proof` | Checks a signed verdict someone else attached (BIP-340 over a Nostr event), offline-verifiable against the published key | free |
| `payment_receipt` | Signed receipt for one verdict-governed EIP-3009 payment: whether it settled and whether a retry is safe | free |
| `ledger` | The public record of past verdicts and their outcomes | free |

Free tools need no account. For paid tools Gemini CLI follows the server's OAuth discovery the first time; if you
already have an API key, add `"headers": {"Authorization": "Bearer <key>"}` to the server entry in your own
settings instead.

Every proof can be checked without trusting us: `POST https://api.babyblueviper.com/verify-proof`, or offline against
the key published at `https://api.babyblueviper.com/.well-known/agent-handshake`.

More: https://invinoveritas.dev · public record: https://invinoveritas.dev/ledger

License: Apache-2.0
