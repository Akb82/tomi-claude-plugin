# Tomi — phone calls from Claude

Tomi gives Claude access to an AI phone agent for errands such as checking
opening hours, confirming a hotel arrival, or arranging a reservation in the
recipient's language. The plugin combines Tomi's existing remote connector
with one skill, `make-call`, covering preparation, confirmation, progress,
and the final report. Calls are real and can cost credits.

## Connect and use

Upload the plugin zip through **Customize → Plugins → Add → Upload plugin**
in Claude. Open its **Connectors** tab, connect Tomi, and complete the server's
OAuth sign-in. No API key or local server is required. On Team/Enterprise,
an Owner may need to add the connector before members connect their accounts.

Ask: “Help me call my hotel to confirm late check-in” or select
`/tomi:make-call` where the slash menu supports it. Give the recipient or
number, the task, and the call language. Claude prepares the call and asks
you to approve the exact number, task, language, time, and budget before
dialing. A new call or retry requires a new approval. Scheduled calls require
approval when they are scheduled. Unattended call campaigns are unsupported.

Tomi announces that it is an AI assistant. Calls are recorded and transcribed;
confirm recording is permitted for your destination. Availability, language
support, free allowance, and pricing depend on the connected service. The
plugin follows its current tool responses rather than promising worldwide
coverage or fixed prices. It returns the outcome, blockers, and next steps;
phone completion alone does not mean the errand succeeded.

## Local review in Claude Code

From this repository root:

```sh
claude plugin validate .
claude --plugin-dir .
```

In the session, inspect `/mcp`, authenticate Tomi, and invoke
`/tomi:make-call`. Do not approve a real call during a preparation-only test.
This package has no agents, hooks, executables, or bundled backend. Its
remote MCP URL is the same one used by the existing connector.

## Status and support

Version 0.1.0 is the initial plugin package. Its manifest has passed local
Claude Code validation. Upload, OAuth compatibility, and call behavior on
each Claude surface still need end-to-end verification; manifest validation
does not establish them. Calls require approval even during testing.

- Documentation: https://tomi.tel
- Support: https://tomi.tel/support — support@tomi.tel
- Privacy and data handling: https://tomi.tel/privacy

## License

MIT applies only to the plugin files in this repository. The remote Tomi
service, backend software, user data, and service terms are not licensed
under MIT by this package. Using the connector requires a Tomi account and
is governed by the service terms at https://tomi.tel/terms.
