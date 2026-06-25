# OctoIO LLM-Connector — Public Manifest

This repository is the **public catalog** for the OctoIO LLM Connector. It is the ONLY public surface of the
connector — it holds two small, non-secret files and nothing else:

| File | What it is |
|------|------------|
| `registry.json` | The provider catalog — the list of LLM providers, their models, endpoints, and auth info. |
| `version.json`  | A tiny version pointer (`{"version": "x.y.z"}`) so apps can cheaply check "is there anything newer?" |

## What this is for

Every OctoIO app reads this repo **once a day** to keep its provider catalog current. When a new model or
provider is added here, every app on every machine picks it up automatically within a day — no app rebuild,
no reinstall.

## What is NOT here (by design)

- ❌ **No source code** — that lives in the private repo.
- ❌ **No executable** — the connector program ships *inside* each OctoIO app's installer (private).
- ❌ **No secrets** — API keys/tokens live in each machine's OS keychain and never leave the machine.

## How updates happen

The connector's maintainer edits the catalog in the private repo and runs the publish step, which copies
`registry.json` + `version.json` here and pushes. That's the whole update — every app benefits next time it checks.

## For app developers

You do not consume this repo directly. Use the connector's client + read the integration guide
(`INTEGRATION.md` in the connector). The connector handles reading this manifest, the daily check, and caching
into the per-machine hub for you.
