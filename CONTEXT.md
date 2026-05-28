# Executor Context

## Product Language

**Executor Server** is the product core. It owns scopes, sources, secrets, policies, tool execution, MCP, approvals, and the typed HTTP API. An Executor Server may run locally, inside the desktop sidecar, or behind an explicitly configured HTTP origin.

**Executor Server Connection** is a normalized pointer to an Executor Server. It contains the server origin, API base URL, display name, stable key, server kind, and optional authentication. Product surfaces should depend on this contract instead of each inventing `baseUrl` handling.

**Executor Server Profile** is a named, persisted CLI/app selection for an Executor Server Connection. Profiles choose which server a surface targets; credentials may still come from host-specific auth, such as `EXECUTOR_API_KEY` for the CLI.

**Executor App** is the reusable browser UI for working with an Executor Server. It connects to the active Executor Server Connection, offers app-side profile selection for generic HTTP servers, and avoids knowing whether the selected server came from local, desktop, or a custom remote endpoint.

**Executor CLI** is a command-line adapter over Executor Server Connections. Local server origins may auto-start a daemon; remote server origins are explicit connections and use bearer or Basic authentication from the environment/profile.

**Executor Desktop** is a platform adapter that starts a local sidecar Executor Server, manages native settings, and exposes the sidecar as an Executor Server Connection to the app. Desktop settings mutate and restart that sidecar connection inside the Electron adapter.

**Local Executor Server** is an Executor Server started by the CLI or local dev app on the user's machine.

**Remote Executor Server** is an explicitly configured HTTP(S) Executor Server reached without local daemon ownership.
