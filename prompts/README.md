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

Tools: `list_schedules`, `reschedule_schedule`, `cancel_schedule`. The agent should confirm both changes with you first.

## Weekly recap

> What went out on my brand's accounts this week, what failed, and what's coming up next week?

Tools: `list_schedules`, `get_publish_run_receipt`, `list_targets`. Read-only. Skill: `weekly-recap`.

## Upload from your computer (local server only)

> Upload ~/Desktop/launch.mp4 to Wahlu for my main brand, then tell me when it's ready.

Tools: `upload_media_from_file`, `get_media`. Needs the local server (`npx -y @wahlu/mcp-server`); the hosted server can't read your files.
