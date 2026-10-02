# Example prompts and workflows

These prompts work in any client connected to Wahlu (Claude, ChatGPT, Codex, Cursor, Gemini CLI or OpenClaw). They're illustrations, not recorded conversations: your agent's wording will differ, but the Wahlu tools it calls should match.

Every workflow starts by reading, and schedules are **held for review** unless you say otherwise. A held schedule sits in your Wahlu calendar and can't publish until you approve it there.

## First connection

> Use Wahlu to tell me which workspace, brands and permissions you can see, and which social accounts are connected for my main brand.

Tools: `get_context`, `list_targets`. Read-only.

## Plan next week

> Plan next week for my bakery brand: three Instagram posts, two TikToks and one LinkedIn post. The theme is our new autumn menu. Check what's already scheduled, show me a table first, and only save drafts for the rows I approve.

Tools: `get_context`, `list_targets`, `list_schedules`, `get_platform_capabilities`, then `create_draft` and `preflight_draft` after you approve. Skill: `plan-a-week`.

## From an idea to a held post

> Turn this article into a LinkedIn post and an Instagram caption: https://example.com/our-launch. Use the hero image from the article. Schedule both for Tuesday at 9am my time, held for review.

Tools: `import_media_from_url`, `get_media`, `create_draft`, `preflight_draft`, `create_schedule` with `pending_review`, `get_schedule`. Skill: `idea-to-scheduled-post`.

## One video, every platform

> Here's our new product video: https://example.com/video.mp4. Prepare it as an Instagram Reel, a TikTok, a YouTube Short and a LinkedIn video, each with its own caption. Set TikTok to public if that's allowed. Hold everything for review on Thursday at 6pm.

Tools: `import_media_from_url`, `get_platform_capabilities`, `refresh_target_dynamic_options`, `create_draft`, `update_draft_tiktok_privacy`, `preflight_draft`, `create_schedule`. Skill: `repurpose-video`.

## Check a draft before scheduling

> Check my "Spring sale" draft for Instagram and Facebook at 10am Friday. Don't schedule anything; just tell me what needs fixing.

Tools: `list_content_items`, `preflight_draft`. Read-only; preflight changes nothing.

## Move or cancel a post

> Move Thursday's Instagram post to Friday at 8am. Then cancel the Saturday TikTok.

Tools: `list_schedules`, `reschedule_schedule`, `cancel_schedule`. The agent should confirm both changes with you first. Rescheduling needs both scheduling and Publishing permissions, even for a held post; cancellation needs scheduling permission.

## Weekly recap

> What went out on my brand's accounts this week, what failed, and what's coming up next week?

Tools: `list_schedules`, `get_publish_run_receipt`, `list_targets`. Read-only. Skill: `weekly-recap`.

## Labelled drafts and calendar

> Show my Launch drafts and the next month's Launch calendar. Read only; do not schedule anything.

Tools: `list_labels`, `list_drafts`, `list_schedules` with one exact returned label ID. Use the calendar filter only when the connected tool schema exposes `label`; older imported tool lists may need refreshing.

## Several photos across platforms

> Use these three ready Wahlu photos for an Instagram carousel, Facebook Page post and LinkedIn profile post. Show each caption, check the current photo limits, and save drafts and schedule them held for review on Tuesday at 9am.

Tools: `get_context`, `list_targets`, `get_platform_capabilities`, `list_media`, `get_media`, `create_draft`, `preflight_draft`, `create_schedule`. Skill: `idea-to-scheduled-post`. Select only schedulable targets and use each platform's own media rules; Facebook videos go on their own.

## Manage one unused draft

> Change only my unused Spring launch draft's caption to the wording I just approved. Keep its media and don't schedule it.

Tools: `list_drafts`, `get_content_item`, `update_draft` with matching exact confirmation and a stable key. Skill: `manage-posts`. Already queued, scheduled or published drafts cannot be edited this way.

## Review a named Autopilot week

> Read week 1 of my Autopilot plan PLAN_ID. Show the unused ideas and replace only the one I choose with a coffee-brewing topic. Show the new topic before I approve it; don't generate or publish posts.

Tools: `get_autopilot_week`, then `regenerate_autopilot_item` for an explicitly chosen unused idea and a new week read. Skill: `review-autopilot`. Replace PLAN_ID with the actual existing plan. Regeneration requires an eligible paid plan and may use AI credits.

## Upload from your computer (local server only)

> Upload ~/Desktop/launch.mp4 to Wahlu for my main brand, then tell me when it's ready.

Tools: `upload_media_from_file`, `get_media`. Needs the local server (`npx -y @wahlu/mcp-server`); the hosted server can't read your files.
