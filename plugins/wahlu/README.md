# Wahlu for ChatGPT, Codex and Claude

Plan, draft, review and schedule social posts through your Wahlu account. Use your brand's voice, existing media and connected Instagram, Facebook Pages, TikTok, YouTube and LinkedIn personal accounts. New schedules are held for review by default. Publishing requires a separate permission and your explicit approval.

## Included workflows

| Skill | What it does |
|---|---|
| `plan-a-week` | Plans around your existing calendar and saves approved ideas as drafts |
| `idea-to-scheduled-post` | Prepares captions, media and labels, checks readiness and creates a held schedule |
| `repurpose-video` | Reuses one video across suitable connected platforms with their own settings |
| `weekly-recap` | Reads calendar outcomes, available History links, Link in bio stats and upcoming posts |
| `manage-posts` | Edits or deletes unused drafts and manages exact unsent schedules, including permitted approval |
| `review-autopilot` | Reads a named plan's week and reviews, regenerates or approves one unused text idea |

The package includes the hosted HTTPS MCP configuration and both portable OpenAI and Claude-compatible manifests. It runs no scripts, hooks or binaries on your computer. Public directory submission and publication are separate from this source package.

## Connect

1. Create or use a Wahlu workspace with at least one brand. Agent access follows the current plan's limits, including eligible free accounts; do not assume a paid subscription is always required.
2. Install the plugin in a supported host. For direct testing, add `https://mcp.wahlu.com/mcp` as a custom remote MCP connection. In Claude Code, use `/mcp` after plugin installation.
3. Complete Wahlu OAuth in your browser. Choose the workspace, brands and permissions the assistant can use. Your password stays in the Wahlu login flow.
4. Try: "Use Wahlu to show my brands, connected accounts and social content calendar."

## Available tools

The hosted server has 36 tools. A host may retain an older imported tool list until the connection is refreshed. Local stdio has 38 tools, with separate catalogue discovery and local-file upload; those two tools are not part of the hosted directory package.

| Area | Hosted tools |
|---|---|
| Context | `get_context`, `get_brand_context`, `list_labels`, `list_targets`, `refresh_target_dynamic_options`, `get_platform_capabilities` |
| Media | `import_media_from_url`, `list_media`, `get_media`, `create_media_repair_derivative`, `upload_media` |
| Content | `create_draft`, `update_draft_tiktok_privacy`, `preflight_draft`, `list_content_items`, `get_content_item`, `list_drafts`, `update_draft`, `delete_draft` |
| Calendar and outcomes | `create_schedule`, `list_schedules`, `get_schedule`, `get_publish_run_receipt`, `cleanup_provider_publications`, `reschedule_schedule`, `cancel_schedule`, `approve_schedule`, `move_schedule_to_draft`, `delete_schedule`, `list_history` |
| Brand surfaces | `get_bio_page`, `get_bio_stats`, `get_autopilot_week`, `approve_autopilot_item`, `regenerate_autopilot_item`, `list_notifications` |

Read current platform media limits before creating multi-photo posts. Facebook multi-photo posts go to Pages; LinkedIn targets are personal profiles. Draft editing changes only an unused draft's name or caption. Autopilot review needs an existing plan ID; approving an idea does not start generation, and any later schedule remains held for final approval.

History needs `publications:read`; notifications need `notifications:read`. These are additional OAuth scopes and are not newly available through the ordinary API-key selector. Existing grants may lack them. Explain unavailable access and use schedule receipts for outcomes where possible. Link in bio stats describe page visits and link clicks, not social engagement Insights.

## Data, permissions and control

- The assistant sends the content and selected records needed for the requested workflow: captions, media bytes or URLs, labels, account selections, draft settings and times. It reads only the granted workspace, brands and permissions.
- Media uploads create private media; a URL import fetches the supplied public URL. Processing may continue after the call. A repair derivative preserves the source and requires an explicitly chosen repair option.
- Unused draft and unsent schedule deletion require exact confirmation. Published social posts are not deleted by those tools. Provider cleanup needs separate exact receipt authority and permission.
- Final schedule approval and rescheduling need `schedule:write` and `publish:execute` (Publishing). Approval requires an explicit decision about that post, accounts and time. New held schedules and cancellation need scheduling permission only. Permission refusals cannot be bypassed by creating an approved replacement.
- Text-topic regeneration requires an eligible plan and may use AI credits. Wahlu's agent tools do not generate Studio images, videos or audio.
- Revoke this connection at [Connected agents](https://auth.wahlu.com/connections). Connect social accounts, configure queues or automations, view social Insights, edit Link in bio, manage billing and membership, or delete your account in the [Wahlu app](https://app.wahlu.com). Administrator controls and native-app distribution are outside this plugin.

## Support

[MCP docs](https://wahlu.com/docs/mcp-server) · [Help](https://wahlu.com/help) · [Privacy](https://wahlu.com/privacy) · [Terms](https://wahlu.com/terms) · [hello@wahlu.com](mailto:hello@wahlu.com)

MIT. See [LICENSE](LICENSE).

Hosted directory tools exclude the public subscription catalogue under [OpenAI commerce policy](https://developers.openai.com/plugins/plugin-guidelines). Local stdio keeps its 38-tool inventory, including `get_plans` and `upload_media_from_file`; the generic SDK and CLI catalogue remain separate from directory use.
