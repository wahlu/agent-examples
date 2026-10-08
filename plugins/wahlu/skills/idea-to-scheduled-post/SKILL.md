---
name: idea-to-scheduled-post
description: Turn an idea, article link or image into a platform-ready social post in Wahlu, check it's ready, and schedule it held for review. Use when someone asks to post, schedule or queue something on Instagram, Facebook, TikTok, YouTube, LinkedIn, X, Bluesky, Telegram, Discord or Tumblr through Wahlu.
---

# Idea to scheduled post

Take one idea from conversation to a Wahlu schedule. By default the schedule is **held for review**: it sits in the Wahlu calendar and can't publish until a person approves it there.

## Steps

1. **Pick the brand.** Call `get_context`. If there's more than one brand, ask which one. Call `get_brand_context` and write the copy in the brand's voice, following its custom instructions and default call to action.
2. **Pick the accounts.** Call `list_targets` for the brand and confirm which connected accounts the post should go to. Only use accounts marked schedulable.
3. **Check the format.** Call `get_platform_capabilities` and choose a supported post type and media count for each account. Multi-photo posts are supported on Instagram, TikTok, Facebook Pages, LinkedIn personal profiles, X and Bluesky (up to 4 images each), Telegram, Discord and Tumblr (up to 10 each); use the current returned rules rather than copying one platform's limit to another. Facebook Reels and Stories still use one item.
4. **Get the media into Wahlu.**
   - A public image or video URL: call `import_media_from_url` with a stable `idempotency_key`.
   - A file you hold as data: call `upload_media` (small files inline, larger ones through the returned upload URL).
   - A file on the person's computer with the local server: call `upload_media_from_file`.
   - Existing Wahlu media: call `list_media` and let the person choose. To browse further, use `pagination: "cursor"` and the returned `next_cursor` with the same brand. Stop when the item is found or the cursor is null; an empty page may still advance. Use pagination only when the connected schema exposes it.
     Then call `get_media` once to check it's ready. If it's still processing, say so and check again later; don't loop.
5. **Write the copy.** Draft a caption per platform in the brand's voice. Keep it true to what the person told you. Show it to them and make their edits.
6. **Save the draft.** Call `list_labels` if the person wants an existing label. Call `create_draft` with the copy, media, labels and intended accounts, and a stable `idempotency_key`. Use `update_draft` for approved name changes while it is still unused, or a shared caption change when `copy_mode` is `single`. Separate per-platform captions must be edited in Wahlu; do not retry a refused caption update as an arbitrary settings patch.
7. **Check it's ready.** Call `preflight_draft` with the accounts and the planned time. It changes nothing. Explain any blockers and fix them before going on.
8. **Schedule it.** Call `create_schedule` with `approval_status: "pending_review"` and a stable `idempotency_key`. Only use `approved` when the person has clearly said to publish without review, and the connection has the **Publishing** permission.
9. **Confirm.** Call `get_schedule` once and report the time, the accounts and the status. It can be approved in the Wahlu calendar, or with `approve_schedule` after a separate explicit decision when the connection has Publishing permission.

## Rules

- Confirm the brand, accounts, copy and time before you schedule.
- Never guess IDs. Use the `brand_id`, `integration_id`, media and content IDs returned by earlier calls.
- Reuse the same `idempotency_key` when retrying the same request.
- To move or cancel a schedule later, use `reschedule_schedule` or `cancel_schedule`, and only after the person asks.
- A request to "queue" means a held schedule at an agreed time here. Queue configuration and automatic queue slots are managed in the Wahlu app; do not claim to add a post to a queue.
- Explain plan or credit refusals using the returned feature and usage limits. Do not show subscription catalogues, prices, upgrade links or checkout, and do not promise access that the workspace lacks.
- TikTok privacy must use live values from `refresh_target_dynamic_options` for the exact account; changing it on an existing draft uses `update_draft_tiktok_privacy`. Explain that the refresh can change stored connection state before requesting it.
