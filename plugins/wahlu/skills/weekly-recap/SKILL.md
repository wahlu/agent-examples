---
name: weekly-recap
description: Summarise a Wahlu brand's social media week, covering what was published, what failed or needs attention and what's coming up next, across Instagram, Facebook, TikTok, YouTube and LinkedIn. Use when someone asks how their week went, what went out or what's scheduled.
---

# Weekly recap

A read-only summary of the past seven days and the next seven. This skill never creates, changes or publishes anything.

## Steps

1. **Pick the brand.** Call `get_context`. If there's more than one brand, ask which one, or offer a recap per brand.
2. **Check account health.** Call `list_targets` and note any account that needs reconnecting in the Wahlu app.
3. **Last week.** Call `list_schedules` with `from` seven days ago and `to` now. Group the results:
   - published
   - failed or blocked, with the reason Wahlu gives
   - still held for review (these will not publish until approved)
   - cancelled
4. **Check anything unclear.** For a schedule that ran, call `get_publish_run_receipt` to see each platform's outcome. Don't retry or clean up anything in this skill.
5. **Next week.** Call `list_schedules` with `from` now and `to` seven days ahead. List the posts by day and platform, and point out days with nothing planned.
6. **Write the recap.** Keep it short:
   - **Went out:** count by platform, with the post names
   - **Needs attention:** failures, blocked posts, accounts to reconnect, posts waiting for approval
   - **Coming up:** the next seven days
   - **Suggested next step:** for example "approve the two held posts in the Wahlu calendar" or "plan Thursday and Friday" (the `plan-a-week` skill can help)

## Rules

- Read-only: never call a create, reschedule, cancel or cleanup tool here.
- Report Wahlu's own status and reasons; don't guess why something failed.
- Wahlu's agent tools don't include engagement analytics yet, so don't report likes, reach or views.
