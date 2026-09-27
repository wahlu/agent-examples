# Wahlu agent examples

Wahlu is social media scheduling for you and your AI agent. Connect Claude, ChatGPT, Codex, Cursor, Gemini CLI or OpenClaw to Wahlu, and your agent can plan posts, prepare drafts, check they're ready and schedule them to **Instagram, Facebook, TikTok, YouTube and LinkedIn** personal profiles. Schedules are held for your review by default, so nothing publishes until you approve it.

This repository holds the connect guides, example prompts, a Claude plugin with four skills and the OpenClaw skill. Everything here is Markdown and JSON; there's no code to build or run.

## Connect

| | |
|---|---|
| MCP server (hosted) | `https://mcp.wahlu.com/mcp`: Streamable HTTP, OAuth sign-in in your browser, no API key |
| MCP server (local) | `npx -y @wahlu/mcp-server` with a Wahlu API key; adds uploads from your computer |
| CLI | `npx -y @wahlu/cli` |
| REST API | `https://api.wahlu.com/v1` ([docs](https://wahlu.com/docs)) |
| Official MCP registry | `com.wahlu/mcp-server` |

Guides for each client:

- [Claude](connect/claude.md): claude.ai, Claude Desktop and Claude Code
- [ChatGPT](connect/chatgpt.md)
- [Codex](connect/codex.md)
- [Cursor](connect/cursor.md)
- [Gemini CLI](connect/gemini-cli.md)
- OpenClaw: install the [Wahlu skill](openclaw/wahlu/SKILL.md) from ClawHub

Or give your agent [wahlu.com/connect.md](https://wahlu.com/connect.md). It's written for agents: it sets up what it can and tells you when it needs you.

## Claude plugin

[`plugins/wahlu`](plugins/wahlu) bundles the Wahlu connector with four skills:

| Skill | What it does |
|---|---|
| `plan-a-week` | Proposes a week of posts that fit your connected accounts and calendar, then saves the ones you approve as drafts |
| `idea-to-scheduled-post` | Turns an idea, link or image into platform-ready copy, checks it and schedules it held for review |
| `repurpose-video` | Adapts one video for Reels, TikTok, YouTube Shorts, Facebook and LinkedIn with a caption for each |
| `weekly-recap` | Read-only summary of what went out, what needs attention and what's coming up |

Install it in Claude Code:

```text
/plugin marketplace add wahlu/agent-examples
/plugin install wahlu@wahlu
```

Then run `/mcp`, select **wahlu** and sign in.

## Example prompts

See [prompts](prompts/README.md) for first-connection checks, planning a week, an idea to a held post, one video for every platform, moving and cancelling posts, and a weekly recap.

## What your agent can do

| Area | Tools |
|---|---|
| Discovery | `get_context`, `list_targets`, `get_platform_capabilities`, `refresh_target_dynamic_options` |
| Media | `list_media`, `get_media`, `import_media_from_url`, `upload_media`, `create_media_repair_derivative`, `upload_media_from_file` (local server only) |
| Content | `list_content_items`, `get_content_item`, `create_draft`, `update_draft_tiktok_privacy`, `preflight_draft` |
| Schedules | `list_schedules`, `get_schedule`, `create_schedule`, `reschedule_schedule`, `cancel_schedule`, `get_publish_run_receipt`, `cleanup_provider_publications` |

Connecting social accounts, approving held schedules, general draft edits and queues stay in the [Wahlu app](https://app.wahlu.com).

## Safety

- You choose the workspace, brands and permissions at sign-in, and can untick any permission.
- Scheduling and publishing are separate permissions. Held schedules can't publish until someone approves them in Wahlu.
- Revoke access at [auth.wahlu.com/connections](https://auth.wahlu.com/connections).

## Links

[Website](https://wahlu.com) · [MCP docs](https://wahlu.com/docs/mcp-server) · [Privacy](https://wahlu.com/privacy) · [Terms](https://wahlu.com/terms) · [hello@wahlu.com](mailto:hello@wahlu.com)

## Licence

MIT. See [LICENSE](LICENSE).
