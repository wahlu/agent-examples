---
name: wahlu
description: Social media scheduling for you and your AI agent. Plan, draft, check and schedule posts to Instagram, Facebook, TikTok, YouTube, LinkedIn, X and Bluesky with Wahlu, held for your review by default. Uses the Wahlu MCP server or the Wahlu CLI.
homepage: https://wahlu.com/openclaw
metadata: {"openclaw":{"emoji":"🐦","requires":{"env":["WAHLU_API_KEY"],"anyBins":["npx","wahlu"]},"homepage":"https://wahlu.com/openclaw","primaryEnv":"WAHLU_API_KEY","install":[{"id":"npm","kind":"node","pkg":"@wahlu/cli","bins":["wahlu"],"label":"Install the Wahlu CLI"}]}}
---

# Wahlu: social media scheduling for you and your AI agent

Wahlu holds a person's brands, media, drafts and publishing calendar for **Instagram, Facebook, TikTok, YouTube, LinkedIn personal profiles, X and Bluesky**. With this skill you can read that context, bring in media, save drafts, check they're ready and schedule them. Schedules are **held for review** by default: they sit in the Wahlu calendar and can't publish until a person approves them.

- Website: [wahlu.com](https://wahlu.com)
- Agent setup guide: [wahlu.com/connect.md](https://wahlu.com/connect.md)
- MCP docs: [wahlu.com/docs/mcp-server](https://wahlu.com/docs/mcp-server)
- CLI on npm: [@wahlu/cli](https://www.npmjs.com/package/@wahlu/cli)

## Setup

1. The person needs a Wahlu account on a plan that includes agent access, with at least one brand and connected social accounts.
2. They create an API key in the Wahlu app under **Settings → API Keys**, with only the permissions and brands you need, and store it as `WAHLU_API_KEY` in OpenClaw's secret environment. Never ask them to paste the key into the chat.
3. Choose how to connect:
   - **MCP (preferred when your runtime supports MCP servers):** run Wahlu's local MCP server with `npx -y @wahlu/mcp-server` and `WAHLU_API_KEY` in its environment. It has every Wahlu tool, including `upload_media_from_file` for files on this machine.
   - **CLI:** use `npx -y @wahlu/cli` (Node.js 20 or later). It reads `WAHLU_API_KEY` from the environment; there is no `--api-key` flag.
4. Check the connection: call `get_context`, or run `npx -y @wahlu/cli auth status`. Tell the person which workspace, brands and permissions you can see.

## Workflow

Always work in this order, carrying the IDs each step returns into the next. Never guess IDs.

| Step | MCP tool | CLI command |
|---|---|---|
| 1. Context and brands | `get_context` | `wahlu auth status --json` |
| 2. Connected accounts | `list_targets` | `wahlu targets list --brand BRAND_ID --json` |
| 3. Platform rules | `get_platform_capabilities` | `wahlu platforms capabilities --json` |
| 4. Media from a URL | `import_media_from_url` | `wahlu media import --brand BRAND_ID --url URL --idempotency-key KEY --json` |
| 5. Media readiness (read once) | `get_media` | `wahlu media get --brand BRAND_ID --media MEDIA_ID --json` |
| 6. Save a draft | `create_draft` | `wahlu drafts create --brand BRAND_ID --input-file draft.json --idempotency-key KEY --json` |
| 7. Check readiness (changes nothing) | `preflight_draft` | `wahlu drafts preflight --brand BRAND_ID --content-item ID --integration ID --scheduled-at TIME --json` |
| 8. Schedule, held for review | `create_schedule` | `wahlu schedules create --brand BRAND_ID --content-item ID --integration ID --scheduled-at TIME --approval-status pending_review --idempotency-key KEY --json` |
| 9. Check the schedule | `get_schedule` | `wahlu schedules get --brand BRAND_ID --schedule SCHEDULE_ID --json` |

The MCP server also has `list_media`, `upload_media`, `list_content_items`, `get_content_item`, `list_schedules`, `reschedule_schedule`, `cancel_schedule` and `get_publish_run_receipt`. The CLI covers the steps in the table.

### Draft input for the CLI

`draft.json` is the public draft body. For an Instagram image post:

```json
{
  "name": "Autumn menu launch",
  "copy_mode": "single",
  "single_copy": { "caption": "Our autumn menu starts Monday.", "hashtags": ["autumn"] },
  "instagram_settings": { "media_ids": ["MEDIA_ID"], "post_type": "GRID_POST", "collaborators": [] },
  "intended_integration_ids": ["INTEGRATION_ID"]
}
```

For a text post on X, use `"x_settings": { "media_ids": [], "post_type": "X_TEXT" }` instead. X takes 280 characters, and up to 4 images (`X_IMAGE`) or one video (`X_VIDEO`); it needs CLI 0.7.0 or MCP server 0.14.0 or later.

For a text post on Bluesky, use `"bluesky_settings": { "media_ids": [], "post_type": "BSKY_TEXT" }`. Bluesky takes 300 characters, and up to 4 images (`BSKY_IMAGE`) or one video (`BSKY_VIDEO`); put alt text in `alt_text`, keyed by media ID. It needs CLI 0.8.0 or MCP server 0.15.0 or later.

Run `wahlu platforms capabilities --json` for every platform's post types and settings.

## Examples

- "Plan three Instagram posts and two TikToks for next week about our autumn menu. Show me a table first."
- "Import this image, write a LinkedIn post about our launch and schedule it for Tuesday 9am, held for review."
- "Check my Spring sale draft for Instagram at 10am Friday and tell me what needs fixing. Don't schedule it."
- "What's scheduled for my brand this week, and is anything blocked?"

## Rules

- Start read-only. Confirm the brand, accounts, copy and time with the person before any write.
- Use `approval_status: pending_review` unless the person has clearly said to publish without review. An `approved` schedule needs the **Publishing** (`publish:execute`) permission and can go out at its time with no further review.
- Reuse the same `idempotency_key` when retrying the same request, so nothing is duplicated.
- Read media and schedule status once per request; don't write polling loops.
- Connecting social accounts, approving held schedules, editing existing drafts and managing queues happen in the Wahlu app. Tell the person when they need to go there.
- Wahlu publishes to Instagram, Facebook, TikTok, YouTube, LinkedIn personal profiles, X and Bluesky only.
