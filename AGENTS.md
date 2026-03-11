<!-- This is a prefered structure of AGENTS.md file -->

<!-- Short overview of current project (up to 5 sentences) -->
# Overview

OpenCode is an open-source AI coding agent that runs locally and supports multiple LLM providers (Claude, OpenAI, Google, local models).
It uses a client/server architecture — the server exposes an HTTP + WebSocket API, and clients (TUI, web app, desktop app) connect to it via a generated TypeScript SDK.
The project includes a cloud console (auth, sync, billing), a VS Code extension, a plugin system, and an Astro docs site.

<!-- High-level Architecture (main components, integrations, DB + ORM, infra) -->
# Architecture

- **`packages/opencode`** — core: CLI, Hono server (:4096), AI agent, tools, LSP, SQLite (Drizzle). Entry: `src/index.ts`.
- **`packages/app`** — SolidJS web UI, connects to server via `@opencode-ai/sdk`.
- **`packages/desktop`** — Tauri 2 wrapper around the web app.
- **`packages/ui`** — shared SolidJS + Tailwind + Kobalte components.
- **`packages/sdk/js`** — TypeScript SDK auto-generated from OpenAPI. Rebuild: `./packages/sdk/js/script/build.ts`.
- **`packages/plugin`** — plugin API for extending OpenCode.
- **`packages/web`** — docs site (Astro + Starlight).
- **`packages/function`** — Cloudflare Worker API for cloud features.
- **`packages/console/*`** — cloud backend: PlanetScale, Stripe, auth.
- **`sdks/vscode`** — VS Code extension.

Runtime: Bun. Infra: SST (Cloudflare Workers, R2, KV).

<!-- List of main commands -->
# Commands

Dev mode - `...`
Build - `...`
Run unit tests - `...`
Run e2e tests - `...`
Lint - `...`
Typecheck - `...`

<!-- Preferable code style - list only those not obvious from the code -->
# Code style

* Avoid using classes. Use functions and objects instead.
* Prefer types over interfaces.
* Each file with an entity should contain a type of an entity, factory function that starts with `init...`.
* Each function should accept a typed params object. Type lives in the same file.
* Use named exports.
* Never use `any` type.

<!-- List common mistakes agent makes -->
# Rules / restrictions

* Be extremely concise in non-code texts (except planning phase).
* Never do the whole implementation in a single run. Make a pause after each step for my review. Proceed to a next step only after my approval.
* Never do DB reset except when I directly tell you to do it