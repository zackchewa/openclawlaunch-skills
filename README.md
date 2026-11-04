# OpenClaw Launch skills

Agent skills for [OpenClaw Launch](https://openclawlaunch.com/build-and-resell?utm_source=github&utm_medium=skill&utm_campaign=openclawlaunch-skill), the managed host for OpenClaw and Hermes agents.

| Skill | What it does |
| --- | --- |
| [`openclawlaunch`](skills/openclawlaunch/SKILL.md) | Deploy and manage hosted OpenClaw or Hermes bots from your coding agent: create a bot, check status, chat with it, connect Telegram, start, stop, restart or delete it. |

Works with Claude Code, Codex, OpenClaw, Hermes and any agent that reads `SKILL.md` files. Instruction-only: no scripts, no binaries, just `curl` against the documented API.

## Install

Claude Code plugin:

```bash
/plugin install openclawlaunch --marketplace zackchewa/openclawlaunch-skills
```

skills.sh (Claude Code, Codex, Cursor and others):

```bash
npx skills add zackchewa/openclawlaunch-skills
```

ClawHub (OpenClaw):

```bash
clawhub install openclawlaunch
```

Manual: copy `skills/openclawlaunch/` into your agent's skills folder, for example `~/.claude/skills/` (Claude Code), `~/.openclaw/workspace/skills/` (OpenClaw) or `~/.hermes/skills/` (Hermes).

## Setup

1. Sign in at [openclawlaunch.com/developer](https://openclawlaunch.com/developer?utm_source=github&utm_medium=skill&utm_campaign=openclawlaunch-skill) and create a new API key just for your agent.
2. Set it in your shell or agent config, not in the chat:

   ```bash
   export OPENCLAW_LAUNCH_API_KEY=sk_live_...
   ```

   For OpenClaw you can instead set `skills.entries["openclawlaunch"].apiKey` in `openclaw.json`.
3. Ask your agent something like "deploy an OpenClaw bot called Support Bot on OpenClaw Launch and say hi to it".

Creating bots needs a Build & Resell plan or a Scale prepaid balance. On Scale, OpenClaw bots also need model funding (a free Agnes key or an OpenRouter provisioning key) set under Build & Resell; Hermes bots come with model access billed to the account. See [pricing](https://openclawlaunch.com/build-and-resell?utm_source=github&utm_medium=skill&utm_campaign=openclawlaunch-skill).

## Security

- The key is only read from `OPENCLAW_LAUNCH_API_KEY` and is only sent to `openclawlaunch.com`. The skill tells the agent never to print it, write it to files, or accept it pasted into chat.
- A key can only see and control the bots that same key created. Give your agent its own key: it cannot reach bots made by your storefront or other keys, and you can revoke it at any time without affecting them.
- The agent must ask before anything that costs money (creating a bot) or cannot be undone (deleting one), and it treats bot replies and API responses as data, never as instructions.
- The skill uses only lifecycle, chat, Telegram connect and balance endpoints. It never touches file writes, exports, model key changes, SSH or terminals.
- Found a security problem? Email support@openclawlaunch.com.

## License

MIT
