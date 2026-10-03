---
name: repurpose-video
description: Adapt one video into platform-specific posts for Instagram Reels, TikTok, YouTube Shorts, Facebook and LinkedIn in Wahlu, with a caption and settings for each, held for review. Use when someone has a video and wants it posted across several platforms.
---

# Repurpose one video

Take one video and prepare a version for each connected platform, with its own caption, post type and settings. Schedules are held for review unless the person says otherwise.

## Steps

1. **Pick the brand and accounts.** Call `get_context`, `get_brand_context` (for the brand's voice) and `list_targets`. Agree which platforms to use; only schedulable accounts count.
2. **Get the video into Wahlu.** Reuse an existing video with `list_media` when appropriate. If further browsing is needed and the connected schema exposes it, use `pagination: "cursor"` and the returned `next_cursor` with the same brand until the video is found or the cursor is null; an empty page may still advance. Otherwise use `import_media_from_url` for a public URL, `upload_media` for bytes you hold, or `upload_media_from_file` with the local server. Call `get_media` once to confirm it's ready; if it's still processing, tell the person and check later.
3. **Check each platform's rules.** Call `get_platform_capabilities`. Note the post type for each platform (Reel, TikTok video, YouTube Short or video, Facebook Reel or post, LinkedIn video) and any length, size or aspect-ratio limits.
4. **Fix media that doesn't fit.** If preflight later reports that the video doesn't fit a format, Wahlu may offer a repair option (such as a crop). Show it to the person and only call `create_media_repair_derivative` with the option they choose.
5. **Write per-platform copy.**
   - Instagram and Facebook: a hook in the first line, then context and a few relevant hashtags.
   - TikTok: short and conversational.
   - YouTube: a clear title plus a description.
   - LinkedIn: a professional angle and the takeaway.
     Show the set to the person and make their edits.
6. **TikTok privacy.** For TikTok, explain that `refresh_target_dynamic_options` queries the account live and can update connection state, then obtain permission to refresh that exact account before choosing a privacy level. After the draft exists, set it with `update_draft_tiktok_privacy` using one of the returned values.
7. **Save and check.** Call `create_draft` with each platform's settings and a stable `idempotency_key`, then `preflight_draft` for all chosen accounts and the planned time. Resolve blockers.
8. **Schedule held for review.** Call `create_schedule` with `approval_status: "pending_review"`, then `get_schedule` once and report the result.

## Rules

- One video, one draft with per-platform settings, unless the person wants separate posts at different times.
- Don't generate or alter the video itself beyond the repair options Wahlu offers.
- Confirm before every write, and reuse `idempotency_key` values on retries.
- This workflow reuses an existing video; it does not edit clips, generate media, run Studio or promise engagement analytics.
