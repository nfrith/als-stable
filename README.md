# als-stable

The **stable distribution channel** for the ALS plugin.

This repository exists for one reason: to declare harness-native marketplaces whose plugin source is pinned to the `stable` branch of [`nfrith/als`](https://github.com/nfrith/als). Edgerunners install ALS through this channel; the architect ships through it.

## What this repository is not

- **Not the source of ALS.** The plugin code lives at [`nfrith/als`](https://github.com/nfrith/als). PRs and issues belong there.
- **Not actively developed.** This repo holds two marketplace catalog files plus this README. The `stable` branch on `nfrith/als` is what advances when a release ships; this repo's catalog files don't change.

## How it works

ALS uses a harness × channel release model. Two harnesses (Claude Code, Codex), each with an RC and a Stable channel:

| Harness | Channel | Marketplace name | Source | Audience |
|---------|---------|------------------|--------|----------|
| Claude Code | **Stable** | `als-marketplace-stable` | This repo → `.claude-plugin/marketplace.json` → `nfrith/als@stable` | Edgerunners (production use) |
| Claude Code | RC | `als-marketplace` | `nfrith/als` repo → `.claude-plugin/marketplace.json` on `main` | Architects (pre-release testing) |
| Codex | **Stable** | `als-codex-marketplace-stable` | This repo → `.agents/plugins/marketplace.json` → `nfrith/als@stable` | Edgerunners (production use) |
| Codex | RC | `als-codex-marketplace` | `nfrith/als` repo → `.agents/plugins/marketplace.json` on `main` | Architects (pre-release testing) |

When the architect bumps a version on `nfrith/als@main`, only the two RC channels receive it. After the architect validates the bump on a pre-release test fixture, they fast-forward the `stable` branch on `nfrith/als` to the new commit. Both Stable channels then expose the validated version. Bad bumps never reach edgerunners because they never make it past the `stable` advance.

## How to install ALS as an edgerunner

### Claude Code

1. Open Claude Code Desktop.
2. Customize → Plugins → Add plugin → Add marketplace.
3. Enter the source: `nfrith/als-stable` (this repo).
4. Find ALS in the plugins directory; click Install.
5. In the chat, type `/install` to bootstrap your first ALS system.

### Codex

Add this repo as a Codex marketplace, then install the `als` plugin from it. The exact `codex plugin marketplace add` invocation depends on your Codex version — see [`nfrith/als`](https://github.com/nfrith/als) docs for the current canonical command. Once installed, the plugin's install-surface metadata is what's portable to Codex today; skill / hook portability is tracked as follow-up work.

## Updates

**Claude Code:** Run `/update` from any Claude Code session. The skill detects which channel the install came from and updates within that channel.

**Codex:** No ALS-managed update flow yet. Re-add or refresh the marketplace through Codex's own plugin tooling when a new stable release ships. Tracked as follow-up work in [`nfrith/als`](https://github.com/nfrith/als).

## License

The plugin itself is licensed Elastic-2.0 — see [`nfrith/als`](https://github.com/nfrith/als).
