---
name: jobspipe-setup
description: Use when the JobsPipe connector is not authenticated, when a JobsPipe tool returns a 401 or an "Access token is invalid or expired" error, or when the user asks how to connect, sign in to, or set up JobsPipe.
---

# Connecting JobsPipe

The JobsPipe MCP server is remote and authenticated. Every request is billed to
a JobsPipe account, so the user must connect one before any tool will return
data. There is nothing to install and no local server to run.

## Two ways to authenticate

**OAuth (default).** The server advertises OAuth 2.1 with dynamic client
registration and PKCE. Claude discovers this automatically and prompts the user
to sign in the first time a JobsPipe tool is called. The user signs in at
jobspipe.dev and approves; no credential is ever pasted into the client.

**API key.** A JobsPipe API key can be sent instead, as an
`Authorization: Bearer` header. Keys are created at
https://jobspipe.dev/dashboard and start with `jp_live_`. Use this when the
connector runs somewhere non-interactive.

Both paths resolve to the same account and draw down the same credit balance. A
user who has an API key and connects with OAuth is not billed twice.

## If the user has no account

Direct them to https://jobspipe.dev/signup to sign up. A free account starts
with 1,000 credits that never expire, which is enough to evaluate the tools.
Do not attempt to create an account on their behalf.

## Diagnosing failures

| Symptom | Cause | Action |
| --- | --- | --- |
| `401` with a `WWW-Authenticate` header | No credential, or the token expired | Have the user reconnect; the header points at the discovery document |
| `Access token is invalid or expired. Reconnect to continue.` | The OAuth grant was revoked or aged out | Reconnect through the same sign-in flow |
| `402`, or a result carrying `low_balance` | The account's credits are used up or nearly so | Call `get_account_info` to confirm, then `list_pricing_plans`; `upgrade_plan` returns a checkout link to show the user and never charges by itself |

Report an exhausted balance plainly rather than retrying. Retrying a credit
failure burns nothing but wall-clock time and hides the real cause from the user.
