---
name: idea-to-scheduled-post
description: Turn an idea, article link or image into a platform-ready social post in Wahlu, check it's ready, and schedule it held for review. Use when someone asks to post, schedule or queue something on Instagram, Facebook, TikTok, YouTube or LinkedIn through Wahlu.
---

# Idea to scheduled post

Take one idea from conversation to a Wahlu schedule. By default the schedule is **held for review**: it sits in the Wahlu calendar and can't publish until a person approves it there.

## Steps

1. **Pick the brand.** Call `get_context`. If there's more than one brand, ask which one. Call `get_brand_context` and write the copy in the brand's voice, following its custom instructions and default call to action.
2. **Pick the accounts.** Call `list_targets` for the brand and confirm which connected accounts the post should go to. Only use accounts marked schedulable.
3. **Check the format.** Call `get_platform_capabilities` and choose a post type each platform supports for this media (for example an Instagram grid post for an image, a Reel or TikTok video for a clip).
4. **Get the media into Wahlu.**
   - A public image or video URL: call `import_media_from_url` with a stable `idempotency_key`.
   - A file you hold as data: call `upload_media` (small files inline, larger ones through the returned upload URL).
   - A file on the person's computer with the local server: call `upload_media_from_file`.
   - Existing Wahlu media: call `list_media` and let the person choose.
   Then call `get_media` once to check it's ready. If it's still processing, say so and check again later; don't loop.
5. **Write the copy.** Draft a caption per platform in the brand's voice. Keep it true to what the person told you. Show it to them and make their edits.
6. **Save the draft.** Call `create_draft` with the copy, media and intended accounts, and a stable `idempotency_key`.
7. **Check it's ready.** Call `preflight_draft` with the accounts and the planned time. It changes nothing. Explain any blockers and fix them before going on.
8. **Schedule it.** Call `create_schedule` with `approval_status: "pending_review"` and a stable `idempotency_key`. Only use `approved` when the person has clearly said to publish without review, and the connection has the **Publish to social accounts** permission.
9. **Confirm.** Call `get_schedule` once and report the time, the accounts and the status. Tell the person where to approve it: the Wahlu calendar.

## Rules

- Confirm the brand, accounts, copy and time before you schedule.
- Never guess IDs. Use the `brand_id`, `integration_id`, media and content IDs returned by earlier calls.
- Reuse the same `idempotency_key` when retrying the same request.
- To move or cancel a schedule later, use `reschedule_schedule` or `cancel_schedule`, and only after the person asks.
