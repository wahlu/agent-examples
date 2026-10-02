---
name: plan-a-week
description: Plan a week of social media posts for a Wahlu brand across Instagram, Facebook, TikTok, YouTube and LinkedIn, then save the approved ideas as Wahlu drafts. Use when someone asks to plan, map out or fill next week's content calendar with Wahlu.
---

# Plan a week of posts

Use the Wahlu MCP tools to propose seven days of posts that fit the brand's connected accounts and existing calendar. Nothing is scheduled or published in this skill; the output is a plan and, once the person agrees, drafts in Wahlu.

## Steps

1. **Read the context.** Call `get_context`. Tell the person which workspace, brands and permissions you can see. If there's more than one brand, ask which one to plan for. Then call `get_brand_context` for that brand and follow its voice, audience, content pillars and custom instructions.
2. **Check where posts can go.** Call `list_targets` with the `brand_id`. Only plan for accounts marked schedulable. Mention any account that needs reconnecting in the Wahlu app.
3. **Check the calendar.** Call `list_schedules` for the brand with `from` set to the start of the week and `to` set to the end. Don't plan on top of posts that are already there, and point out gaps.
   Call `list_drafts` to reuse unused drafts, and `list_labels` when the plan needs existing labels. The current source supports an exact `label` ID filter on both draft and schedule lists; use it when the connected tool schema exposes it, without inventing saved or multiple-label filters. If the person has a named Autopilot plan, `get_autopilot_week` can read its existing week; creating or running an Autopilot plan remains in Wahlu.
4. **Check the formats.** Call `get_platform_capabilities` once, so each idea uses a post type the platform supports (for example an Instagram Reel needs a video).
5. **Ask for the brief if you don't have one.** Useful inputs: the week's theme or launches (use the brand's content pillars as a starting point), how many posts per platform, and any media the person already has. Don't invent product claims, prices or dates.
6. **Propose the plan as a table:** day, time (in the person's time zone), platform, post type, hook, caption outline and the media it needs. Keep it realistic: one to two posts a day is plenty for most brands.
7. **Wait for approval.** Ask which rows to keep or change. Don't create anything yet.
8. **Create drafts for the approved rows.** For each one, call `create_draft` with a stable `idempotency_key` (for example `plan-2026-w40-mon-instagram`), then `preflight_draft` for the intended accounts and time. Report any blockers in plain English, such as missing media or a caption that's too long.
9. **Hand over.** Summarise what you saved and what still needs media. If the person wants the drafts scheduled, use the `idea-to-scheduled-post` skill, which holds schedules for review by default.

## Rules

- Start read-only. Never create, schedule or publish without the person's clear go-ahead.
- Reuse the same `idempotency_key` when retrying the same draft, so nothing is duplicated.
- If a tool returns an authorisation or permission error, ask the person to reconnect Wahlu and check the brands and permissions they chose.
- Wahlu publishes to Instagram, Facebook, TikTok, YouTube and LinkedIn personal profiles. Don't plan posts for other networks in Wahlu.
- Facebook targets are Pages. Read current format and multi-photo limits from `get_platform_capabilities` and use only connected accounts marked schedulable.
- Explain an entitlement refusal neutrally. Do not show subscription catalogues, prices, upgrade links or checkout. Planning in conversation does not create an Autopilot plan or change billing.
