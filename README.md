# Google Calendar MCP server

Choose an accessible calendar and read upcoming events to prepare the day’s agenda.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `GOOGLE_CALENDAR_ACCESS_TOKEN`

For local OAuth, use node local-auth/cli.mjs login ./connector.json with your own provider app; see AUTH.md. Your tokens remain in the native OS credential store.

Credential help: https://www.googleapis.com/discovery/v1/apis/calendar/v3/rest

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call list_calendars '{}'
```

## Use with an MCP client

Launch `node /absolute/path/google-calendar-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| list_calendars | Read | List calendars visible to the authorized Google user. |
| list_events | Read | Read events from an authorized calendar. Use primary for the user’s primary calendar. |

## Concrete workflow

Choose an accessible calendar and read upcoming events to prepare the day’s agenda.

1. list_calendars
2. list_events

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=google-calendar&integration=google-calendar-mcp&utm_source=github&utm_campaign=github-google-calendar-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/google-calendar/).

## Provenance and maintenance

- https://developers.google.com/workspace/calendar/api/v3/reference/events/list
- https://developers.google.com/identity/protocols/oauth2/native-app
- https://developers.google.com/workspace/calendar/api/v3/reference/calendarList/list

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
