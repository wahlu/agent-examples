---
name: manage-posts
description: Find, edit or delete an unused Wahlu draft, or inspect, move, cancel, delete or approve an exact Wahlu schedule. Use when a person asks to change an existing social post in Wahlu.
---

# Manage existing posts

Read `get_context` and choose a returned brand. Its permission list reports already-held public scopes; it grants no extra access. Use `list_drafts` or `list_content_items` and `get_content_item` for drafts; use `list_schedules` and `get_schedule` for schedules. Use an exact `label` ID filter when useful and exposed by the connected schema. Show the exact post, accounts, time and status before acting. Use IDs returned by these reads.

## Drafts

- `update_draft` changes the name or shared caption of one unused draft. Caption changes require `copy_mode: "single"`; separate per-platform captions must be edited in Wahlu, while name changes remain supported. It cannot edit content already scheduled, queued or published. Supply the matching `confirm_draft_id` and a stable `idempotency_key` after the person approves the change.
- `delete_draft` deletes one unused draft after exact confirmation. It keeps media and published posts. Use the matching confirmation ID and a stable key.
- `list_labels` returns existing labels; `list_drafts` accepts an exact label filter. Changing platform settings or media on existing drafts beyond the exposed tools stays in Wahlu.

## Schedules

- Read the exact schedule before using `reschedule_schedule` or `cancel_schedule`. Confirm the new time and time zone for a move. Rescheduling requires both `schedule:write` and `publish:execute`, including for held schedules; cancellation needs `schedule:write`. Cancellation keeps the stored content; it does not remove a published social post.
- `move_schedule_to_draft` returns an unsent schedule's content to Drafts. It requires both `schedule:write` and `posts:write` and the exact `confirm_schedule_id`.
- `delete_schedule` deletes one unsent schedule after exact confirmation and keeps its content and media. It cannot delete a published provider post.
- `approve_schedule` releases one held schedule for publishing at its scheduled time. Show the copy, selected accounts and time, and obtain explicit approval. It requires both `schedule:write` and `publish:execute` (Publishing). A connection without Publishing cannot approve it; direct the person to the Wahlu calendar or reconnection instead. Do not grant permissions or create an approved replacement to bypass a refusal. If it refuses because the post has lines to check, show the person the lines it names; pass `acknowledge_fact_flags` only after they have seen them and still want the post approved.

Use `preflight_draft` to resolve readiness blockers before scheduling or approval. Keep `pending_review` as the default for new schedules. Report the returned final state after a successful change. Use a stable key for each distinct write, and preserve it for supported retries.

## Published results and limits

`get_publish_run_receipt` reads one schedule's latest platform outcomes. `cleanup_provider_publications` is a separate destructive action: it requires the exact `cleanup_authority` returned by that receipt, explicit confirmation and the required permissions. It cannot search for posts or broadly delete history. Never infer cleanup authority from a provider ID or link.

Queue configuration, adding a post to a queue, connecting accounts, workspace ownership, billing and account deletion stay in the Wahlu app. Do not invent tools for them.
