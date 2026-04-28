# als-stable

The **stable distribution channel** for the ALS plugin.

This repository exists for one reason: to declare a Claude Code marketplace named `als-marketplace-stable` whose plugin source is pinned to the `stable` branch of [`nfrith/als`](https://github.com/nfrith/als). Edgerunners install ALS through this channel; the architect ships through it.

## What this repository is not

- **Not the source of ALS.** The plugin code lives at [`nfrith/als`](https://github.com/nfrith/als). PRs and issues belong there.
- **Not actively developed.** This repo holds one file (`.claude-plugin/marketplace.json`) plus this README. The `stable` branch on `nfrith/als` is what advances when a release ships; this repo's marketplace.json doesn't change.

## How it works

ALS uses a two-channel release model:

| Channel | Marketplace name | Source repo + ref | Audience |
|---------|------------------|-------------------|----------|
| **Stable** | `als-marketplace-stable` | This repo → `nfrith/als@stable` | Edgerunners (production use) |
| **RC** | `als-marketplace` | `nfrith/als` at default ref (`main`) | Architects (pre-release testing) |

When the architect bumps a version on `nfrith/als@main`, only the RC channel receives it. After the architect validates the bump on a pre-release test fixture, they fast-forward the `stable` branch on `nfrith/als` to the new commit. Edgerunners' next `/update` pulls the new version through this channel. Bad bumps never reach edgerunners because they never make it past the `stable` advance.

## How to install ALS as an edgerunner

1. Open Claude Code Desktop.
2. Customize → Plugins → Add plugin → Add marketplace.
3. Enter the source: `nfrith/als-stable` (this repo).
4. Find ALS in the plugins directory; click Install.
5. In the chat, type `/install` to bootstrap your first ALS system.

## Updates

Run `/update` from any Claude Code session. The skill detects which channel the install came from and updates within that channel. See [`nfrith/als`](https://github.com/nfrith/als) for the skill source.

## License

The plugin itself is licensed Elastic-2.0 — see [`nfrith/als`](https://github.com/nfrith/als).
