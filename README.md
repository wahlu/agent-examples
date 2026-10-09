# Wahlu agent examples

Wahlu is social media scheduling for you and your AI agent. Connect Claude, ChatGPT, Codex, Cursor, Gemini CLI or OpenClaw to Wahlu, and your agent can plan posts, prepare drafts, check they're ready and schedule them to **Instagram, Facebook, TikTok, YouTube, LinkedIn** personal profiles and **X**. Schedules are held for your review by default, so nothing publishes until you approve it.

This repository holds the connect guides, example prompts, a portable ChatGPT/Codex plugin with Claude compatibility and six skills, and the OpenClaw skill. Everything here is Markdown and JSON; there's no code to build or run.

## Connect

|                       |                                                                                         |
| --------------------- | --------------------------------------------------------------------------------------- |
| MCP server (hosted)   | `https://mcp.wahlu.com/mcp`: Streamable HTTP, OAuth sign-in in your browser, no API key |
| MCP server (local)    | `npx -y @wahlu/mcp-server` with a Wahlu API key; adds uploads from your computer        |
| CLI                   | `npx -y @wahlu/cli`                                                                     |
| REST API              | `https://api.wahlu.com/v1` ([docs](https://wahlu.com/docs))                             |
| Official MCP registry | `com.wahlu/mcp-server`                                                                  |

Guides for each client:

- [Claude](connect/claude.md): claude.ai, Claude Desktop and Claude Code
- [ChatGPT](connect/chatgpt.md)
- [Codex](connect/codex.md)
- [Cursor](connect/cursor.md)
- [Gemini CLI](connect/gemini-cli.md)
- OpenClaw: install the [Wahlu skill](openclaw/wahlu/SKILL.md) from ClawHub

Or give your agent [wahlu.com/connect.md](https://wahlu.com/connect.md). It's written for agents: it sets up what it can and tells you when it needs you.

## Wahlu plugin

[`plugins/wahlu`](plugins/wahlu) bundles the Wahlu connector with six skills:

| Skill                    | What it does                                                                                                      |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------- |
| `plan-a-week`            | Proposes a week of posts that fit your connected accounts and calendar, then saves the ones you approve as drafts |
| `idea-to-scheduled-post` | Turns an idea, link or image into platform-ready copy, checks it and schedules it held for review                 |
| `repurpose-video`        | Adapts one video for Reels, TikTok, YouTube Shorts, Facebook and LinkedIn with a caption for each                 |
| `weekly-recap`           | Read-only summary of what went out, what needs attention and what's coming up                                     |
| `manage-posts`           | Edits unused drafts and manages exact unsent schedules, with separate publishing approval                         |
| `review-autopilot`       | Finds the current plan and available weeks, then reviews one unused text idea without starting generation         |

Install it in Claude Code:

```text
/plugin marketplace add wahlu/agent-examples
/plugin install wahlu@wahlu
```

Then run `/mcp`, select **wahlu** and sign in.

The 0.4.4 package describes 38 hosted tools, 39 generic tools and 40 local stdio tools, with six workflows. It adds Pinterest, including listing an account's boards. `npx -y @wahlu/mcp-server` installs the published 0.17.0 local server, which supports X, Bluesky, Telegram, Discord, Tumblr, Pinterest and X/Bluesky threads. Use the actual connected tool schema and preserve permission refusals. Source publication and local validation do not establish authenticated ChatGPT/Claude execution or a directory listing.

## Example prompts

See [prompts](prompts/README.md) for first-connection checks, planning a week, an idea to a held post, one video for every platform, moving and cancelling posts, and a weekly recap.

## What your agent can do

| Area           | Tools                                                                                                                                                                                                                                      |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Discovery      | `get_context`, `get_brand_context`, `list_labels`, `list_targets`, `get_platform_capabilities`, `refresh_target_dynamic_options`                                                                                                           |
| Media          | `list_media`, `get_media`, `import_media_from_url`, `upload_media`, `create_media_repair_derivative`, `upload_media_from_file` (local server only)                                                                                         |
| Content        | `list_content_items`, `get_content_item`, `list_drafts`, `create_draft`, `update_draft`, `delete_draft`, `update_draft_tiktok_privacy`, `preflight_draft`                                                                                  |
| Schedules      | `list_schedules`, `get_schedule`, `create_schedule`, `reschedule_schedule`, `cancel_schedule`, `approve_schedule`, `move_schedule_to_draft`, `delete_schedule`, `get_publish_run_receipt`, `cleanup_provider_publications`, `list_history` |
| Brand surfaces | `get_bio_page`, `get_bio_stats`, `get_autopilot_plan`, `get_autopilot_week`, `approve_autopilot_item`, `regenerate_autopilot_item`, `list_notifications`                                                                                   |

Connecting social accounts, queue configuration, Insights, reply automations, Link in bio editing, billing and account management stay in the [Wahlu app](https://app.wahlu.com). Final schedule approval from an agent requires Publishing permission and explicit approval. Existing draft editing is limited to unused draft names and shared captions; separate platform captions stay in Wahlu. History and notifications require their separate OAuth scopes; the ordinary API-key selector does not offer those two scopes. See the [plugin README](plugins/wahlu/README.md) for current access limits.

## Safety

- You choose the workspace, brands and permissions at sign-in, and can untick any permission.
- Scheduling and publishing are separate permissions. Held schedules can't publish until someone approves them in Wahlu.
- Revoke access at [auth.wahlu.com/connections](https://auth.wahlu.com/connections).

## Links

[Website](https://wahlu.com) · [MCP docs](https://wahlu.com/docs/mcp-server) · [Privacy](https://wahlu.com/privacy) · [Terms](https://wahlu.com/terms) · [hello@wahlu.com](mailto:hello@wahlu.com)

## Licence

MIT. See [LICENSE](LICENSE).
