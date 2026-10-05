# Tool contract snapshot

Read the live tools' schemas before using them. This reference was checked
against ai-call-mcp source commit 2590dbbd1f7dfe18b26cfbbe3ce93ee57805b379
on 2026-10-04, not against an authenticated production `tools/list`.

| Tool | Inputs and role |
| --- | --- |
| `find_target` | `query` or `url`; optional ISO country, limit 1–4. Read-only lookup; registered only with research configured. Candidates can include phone, source_url, timezone, hours, callable and blocked. |
| `estimate_cost` | `country` (ISO alpha-2), `est_minutes` (1–60), optional `phone`. Pass the phone for a line-specific estimate. Does not establish destination availability. |
| `get_balance` | No arguments. Current balance, free calls/minutes remaining. |
| `place_call` | Required phone (E.164), phone_source, task (1–2000 chars), language. Consent gate via elicitation or user_confirmed. Optional max_budget_usd (0.5–50; default 5), scheduled_at (ISO instant, at most seven days ahead), target_url, conversation_language, timezone, collect (up to eight key/description pairs), outreach_confirmed. No MCP idempotency argument. |
| `get_call_status` | call_id, wait_for_change_sec (recommended 20), after_event_seq from prior last_event_seq. Returns progress/transcript tail or final report; optional costs and links. |
| `list_calls` | Optional limit (1–50, default 10). Recover IDs for this account, then verify a match before following or canceling it. |
| `cancel_call` | call_id. Idempotent cancellation request; verify termination. |
| `send_instruction` | call_id, instruction (1–500 chars). Mid-call, only when provider supports it. |
| `send_dtmf` | call_id, keys (1–32 chars from 0–9, *, #, w). Mid-call, only when supported; w inserts a pause. |
| `get_whatsapp_link` | phone, optional message (or text alias). Returns draft URL and availability=not_checked. Sends nothing. |

`phone_source`: user_message, user_screenshot, user_link, find_target,
earlier_call, user_contact. Use the actual provenance, not whichever passes.
For a number selected from Tomi lookup, use find_target.

Source language allowlist: en, ru, kk, tr, es, pt, de, fr, it, ja, ar, id.
The connected deployment and effective_language response remain authoritative.
Never hardcode callable countries or free-credit amounts from old submission docs.

`src/server.ts` also registers buy_credits, get_referral_link and
redeem_referral on commerce-enabled clients; this skill does not use them.
Pricing tools/fields depend on the client surface. Do not infer production
deployment capabilities from these source registrations.
