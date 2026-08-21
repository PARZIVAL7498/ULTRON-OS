# Ultron Agent ☤

<p align="center">
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/Lang-中文-red?style=for-the-badge" alt="中文"></a>
  <a href="README.ur-pk.md"><img src="https://img.shields.io/badge/Lang-اردو-green?style=for-the-badge" alt="اردو"></a>
  <a href="README.es.md"><img src="https://img.shields.io/badge/Lang-Español-orange?style=for-the-badge" alt="Español"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License: MIT"></a>
</p>

**The self-improving AI agent.** It's the only agent with a built-in learning loop — it creates skills from experience, improves them during use, nudges itself to persist knowledge, searches its own past conversations, and builds a deepening model of who you are across sessions. Run it on a $5 VPS, a GPU cluster, or serverless infrastructure that costs nearly nothing when idle. It's not tied to your laptop — talk to it from Telegram while it works on a cloud VM.

Use any model you want — OpenRouter, OpenAI, Anthropic, DeepSeek, local endpoints, and many others. Switch with `ultron model` — no code changes, no lock-in.

<table>
<tr><td><b>A real terminal interface</b></td><td>Full TUI with multiline editing, slash-command autocomplete, conversation history, interrupt-and-redirect, and streaming tool output.</td></tr>
<tr><td><b>Lives where you do</b></td><td>Telegram, Discord, Slack, WhatsApp, Signal, and CLI — all from a single gateway process. Voice memo transcription, cross-platform conversation continuity.</td></tr>
<tr><td><b>A closed learning loop</b></td><td>Agent-curated memory with periodic nudges. Autonomous skill creation after complex tasks. Skills self-improve during use. FTS5 session search with LLM summarization for cross-session recall. <a href="https://github.com/plastic-labs/honcho">Honcho</a> dialectic user modeling. Compatible with the <a href="https://agentskills.io">agentskills.io</a> open standard.</td></tr>
<tr><td><b>Scheduled automations</b></td><td>Built-in cron scheduler with delivery to any platform. Daily reports, nightly backups, weekly audits — all in natural language, running unattended.</td></tr>
<tr><td><b>Delegates and parallelizes</b></td><td>Spawn isolated subagents for parallel workstreams. Write Python scripts that call tools via RPC, collapsing multi-step pipelines into zero-context-cost turns.</td></tr>
<tr><td><b>Runs anywhere, not just your laptop</b></td><td>Seven terminal backends — local, Docker, SSH, Singularity, Modal, Daytona, and Vercel Sandbox. Daytona and Modal offer serverless persistence — your agent's environment hibernates when idle and wakes on demand, costing nearly nothing between sessions. Run it on a $5 VPS or a GPU cluster.</td></tr>
<tr><td><b>Research-ready</b></td><td>Batch trajectory generation, trajectory compression for training the next generation of tool-calling models.</td></tr>
</table>

---

## Installation & Setup

### Cloned Repository / Local Setup (From Source)

#### Linux, macOS, WSL2, Termux (Automated Script)
Run the setup script:
```bash
chmod +x setup-hermes.sh
./setup-hermes.sh
```
This script will:
1. Locate or install `uv` (or use standard `venv` + `pip` on Termux).
2. Create a Python 3.11 virtual environment (`venv`).
3. Install dependencies with hash verification via `uv.lock`.
4. Copy `.env.example` to `.env` if not already present.
5. Symlink the `ultron` CLI executable into your PATH (`~/.local/bin` or `$PREFIX/bin`).
6. Run the interactive setup wizard.

#### Windows (Native PowerShell / CMD)
```powershell
# 1. Create a virtual environment (Python 3.11 recommended)
uv venv venv --python 3.11
# Or with standard Python: python -m venv venv

# 2. Activate the virtual environment
.\venv\Scripts\activate

# 3. Install dependencies
uv sync --extra all --locked
# Or with pip: pip install -e ".[all]"

# 4. Configure environment variables
Copy-Item .env.example .env
# Edit .env and configure your API keys (e.g., OPENAI_API_KEY, OPENROUTER_API_KEY)

# 5. Launch the agent
python ultron
# or: .\ultron.cmd
# or: python cli.py setup
```

---

## Getting Started

```bash
ultron              # Interactive CLI — start a conversation
ultron model        # Choose your LLM provider and model
ultron tools        # Configure which tools are enabled
ultron config set   # Set individual config values
ultron config get   # Print individual config values
ultron gateway      # Start the messaging gateway (Telegram, Discord, etc.)
ultron setup        # Run the full setup wizard (configures everything at once)
ultron claw migrate # Migrate from OpenClaw (if coming from OpenClaw)
ultron update       # Update to the latest version
ultron doctor       # Diagnose any issues
```

---

## CLI vs Messaging Quick Reference

Ultron has two entry points: start the terminal UI with `ultron`, or run the gateway and talk to it from Telegram, Discord, Slack, WhatsApp, Signal, or Email. Once you're in a conversation, many slash commands are shared across both interfaces.

| Action                         | CLI                                           | Messaging platforms                                                              |
| ------------------------------ | --------------------------------------------- | -------------------------------------------------------------------------------- |
| Start chatting                 | `ultron`                                      | Run `ultron gateway setup` + `ultron gateway start`, then send the bot a message |
| Start fresh conversation       | `/new` or `/reset`                            | `/new` or `/reset`                                                               |
| Change model                   | `/model [provider:model]`                     | `/model [provider:model]`                                                        |
| Set a personality              | `/personality [name]`                         | `/personality [name]`                                                            |
| Retry or undo the last turn    | `/retry`, `/undo`                             | `/retry`, `/undo`                                                                |
| Compress context / check usage | `/compress`, `/usage`, `/insights [--days N]` | `/compress`, `/usage`, `/insights [days]`                                        |
| Browse skills                  | `/skills` or `/<skill-name>`                  | `/<skill-name>`                                                                  |
| Interrupt current work         | `Ctrl+C` or send a new message                | `/stop` or send a new message                                                    |
| Platform-specific status       | `/platforms`                                  | `/status`, `/sethome`                                                            |

---

## Documentation Overview

| Section                 | What's Covered                                             |
| ----------------------- | ---------------------------------------------------------- |
| **Quickstart**          | Install → setup → first conversation in 2 minutes          |
| **CLI Usage**           | Commands, keybindings, personalities, sessions             |
| **Configuration**       | Config file, providers, models, all options                |
| **Messaging Gateway**   | Telegram, Discord, Slack, WhatsApp, Signal, Home Assistant |
| **Security**            | Command approval, DM pairing, container isolation          |
| **Tools & Toolsets**    | 40+ tools, toolset system, terminal backends               |
| **Skills System**       | Procedural memory, Skills Hub, creating skills             |
| **Memory**              | Persistent memory, user profiles, best practices           |
| **MCP Integration**     | Connect any MCP server for extended capabilities           |
| **Cron Scheduling**     | Scheduled tasks with platform delivery                     |
| **Context Files**       | Project context that shapes every conversation             |
| **Architecture**        | Project structure, agent loop, key classes                 |
| **Contributing**        | Development setup, PR process, code style                  |
| **CLI Reference**       | All commands and flags                                     |
| **Environment Variables** | Complete env var reference                               |

---

## Migrating from OpenClaw

If you're coming from OpenClaw, Ultron can automatically import your settings, memories, skills, and API keys.

**During first-time setup:** The setup wizard (`ultron setup`) automatically detects `~/.openclaw` and offers to migrate before configuration begins.

**Anytime after install:**

```bash
ultron claw migrate              # Interactive migration (full preset)
ultron claw migrate --dry-run    # Preview what would be migrated
ultron claw migrate --preset user-data   # Migrate without secrets
ultron claw migrate --overwrite  # Overwrite existing conflicts
```

What gets imported:

- **SOUL.md** — persona file
- **Memories** — MEMORY.md and USER.md entries
- **Skills** — user-created skills → `~/.ultron/skills/openclaw-imports/`
- **Command allowlist** — approval patterns
- **Messaging settings** — platform configs, allowed users, working directory
- **API keys** — allowlisted secrets (Telegram, OpenRouter, OpenAI, Anthropic, ElevenLabs)
- **TTS assets** — workspace audio files
- **Workspace instructions** — AGENTS.md (with `--workspace-target`)

See `ultron claw migrate --help` for all options, or use the `openclaw-migration` skill for an interactive agent-guided migration with dry-run previews.

---

## Contributing

We welcome contributions!

### Developer Setup:

```bash
# Setup development virtual environment
uv venv .venv --python 3.11
source .venv/bin/activate  # or: .venv\Scripts\activate on Windows

# Install all development dependencies
uv pip install -e ".[all,dev]"

# Run test suite
pytest
```

---

## License

MIT — see [LICENSE](LICENSE).
