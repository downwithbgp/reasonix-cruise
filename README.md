---
name: reasonix-cruise
description: Reasonix Cruise Control — autonomous coding workflow
type: reasonix-config
system_prompt: cruise.md
---
# reasonix-cruise

"Cruise Control" mode for [Reasonix](https://reasonix.io).

A Reasonix configuration and workflow system prompt designed for autonomous, commit-to-completion coding with minimal hand-holding.

## What's inside

| File | Purpose |
|---|---|
| `cruise.md` | System prompt: Cruise Control. Teaches the agent scope assessment, commit discipline, verification gates, and self-steering. |
| `config.toml` | Reference Reasonix config. Copy to `~/.reasonix/config.toml` and customize paths / providers. |
| `skills/` | Three custom skills — `karpathy-guidelines` (coding guidelines), `prop-test` (property-based tests), `spec` (spec-driven development). Each is `skills/<name>/SKILL.md`. |

## Quick start

**Prerequisite**: [Reasonix](https://reasonix.io) installed and configured.

```bash
# 1. Clone into your Reasonix config directory
git clone https://github.com/downwithbgp/reasonix-cruise.git ~/.reasonix/cruise

# 2. Symlink or copy what you want
ln -s ~/.reasonix/cruise/cruise.md ~/.reasonix/cruise.md
ln -s ~/.reasonix/cruise/skills ~/.reasonix/skills

# 3. Merge config.toml with yours (or copy if you don't have one yet)
#    Then **uncomment** `system_prompt_file` and set the path:
#    system_prompt_file = "/home/YOU/.reasonix/cruise.md"

# 4. Set your API key
echo 'DEEPSEEK_API_KEY=sk-your-key-here' > ~/.reasonix/.env
```

## The workflow in one sentence

> Judge scope → apply right rigor → implement → verify → commit. Never leave uncommitted work.

## Usage

Give Reasonix a high-level goal. Cruise Control handles scoping, implementation, verification, and commit. No step-by-step management needed.

> **Permission mode:** The reference config defaults to `mode = "allow"` in `[permissions]`.
> This matches the system prompt's self-steering philosophy — the agent handles
> scope and tool decisions autonomously. The deny list still blocks dangerous
> operations (`rm -rf /*`, forced pushes, `curl | sh`, etc.).

## License

MIT.
