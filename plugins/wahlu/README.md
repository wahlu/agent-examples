# Wahlu for Claude

Wahlu is social media scheduling for you and your AI agent. This plugin connects Claude to your Wahlu account so Claude can plan posts, prepare drafts, check they're ready and schedule them to Instagram, Facebook, TikTok, YouTube and LinkedIn personal profiles. Schedules are held for your review by default: nothing publishes until you approve it in the Wahlu calendar, unless you clearly tell Claude otherwise and have granted the publishing permission.

## What's included

- **The Wahlu connector**: Wahlu's hosted MCP server at `https://mcp.wahlu.com/mcp`.
- **Four skills:**
  - `plan-a-week`: proposes a week of posts that fit your connected accounts and existing calendar, then saves the ones you approve as drafts.
  - `idea-to-scheduled-post`: turns an idea, link or image into platform-ready copy, checks it and schedules it held for review.
  - `repurpose-video`: adapts one video for Reels, TikTok, YouTube Shorts, Facebook and LinkedIn with a caption for each.
  - `weekly-recap`: a read-only summary of what went out, what needs attention and what's coming up.

## Setup

1. You need a Wahlu account on a plan that includes agent access, with at least one brand and connected social accounts. Start at [wahlu.com](https://wahlu.com).
2. Install the plugin, then connect Wahlu from the plugin's **Connectors** tab (claude.ai and Cowork) or with `/mcp` (Claude Code).
3. Sign in to Wahlu in your browser, choose the workspace and brands Claude may use, and untick any permissions you don't want to grant.
4. Try: "Use Wahlu to show which brands and accounts you can see."

## What this plugin runs, sends and fetches

- **Runs:** nothing on your computer. The plugin contains only Markdown skills and a connector entry; there are no scripts, hooks or binaries.
- **Connects to:** `https://mcp.wahlu.com/mcp`, operated by Wahlu. Sign-in happens on `auth.wahlu.com` with OAuth; Claude never sees your Wahlu password and you never paste an API key.
- **Sends to Wahlu:** what the skills ask Claude to save, such as post copy, media URLs or media you share, draft settings, chosen accounts and schedule times, only for the brands and permissions you granted.
- **Fetches from Wahlu:** your workspace and brand names; each brand's context (voice, audience, content pillars, custom AI instructions, brand kit colours, fonts and logo, and Link in bio page status) and labels; connected-account status, media, drafts, schedules and publishing results for those brands.
- **Publishing:** posts go to your social accounts only through Wahlu's scheduling, and only for schedules that are approved. Approving directly from Claude needs the separate **Publish to social accounts** permission.

## Safety and control

- Every skill starts by reading and asks before it creates or changes anything.
- You can revoke access at any time at [auth.wahlu.com/connections](https://auth.wahlu.com/connections). This doesn't disconnect your social accounts.
- Wahlu's agent tools don't generate images, video or audio.

## Support

- Docs: [wahlu.com/docs/mcp-server](https://wahlu.com/docs/mcp-server)
- Privacy: [wahlu.com/privacy](https://wahlu.com/privacy)
- Terms: [wahlu.com/terms](https://wahlu.com/terms)
- Contact: [hello@wahlu.com](mailto:hello@wahlu.com)

## Licence

MIT. See [LICENSE](LICENSE).
