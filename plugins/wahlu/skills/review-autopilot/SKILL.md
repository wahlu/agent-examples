---
name: review-autopilot
description: Discover the current Wahlu Autopilot plan and read an existing week, then review, approve or regenerate one unused idea. Use when someone asks to find their Autopilot plan, review a week or change one topic.
---

# Review an Autopilot week

1. Call `get_context`, choose a returned brand, and read `get_brand_context`. If the person supplied an exact plan ID, preserve it. Otherwise call `get_autopilot_plan` for the brand to find its current plan ID, status and up to 100 recent available week numbers. A null plan means none exists; do not create or activate one. Use an available week or ask which one to review. Week numbers alone do not identify the current calendar week; clarify a request for "this week" or label a recap of the latest available week explicitly. This is current-plan discovery, not a complete plan-history list. If the host retains an older tool list, ask for the existing plan ID or refresh the connection.
2. Call `get_autopilot_week` for that exact plan and week. Summarise its themes, ideas and current states. Do not treat an approved idea as a published post.
3. If the person wants a different topic, show the exact unused idea and their guidance. Call `regenerate_autopilot_item` only after approval, with the matching `confirm_item_id` and a new stable `idempotency_key`. This replaces a text topic and may use the workspace's AI credits; it does not generate Studio images or videos. The response reports an ID and outcome, not the new topic: read `get_autopilot_week` again before presenting the changed idea. An uncertain result must not be retried automatically with the same key; establish the current state through that read before proposing any further change.
4. To approve an idea, show its returned topic and ask for explicit approval, then call `approve_autopilot_item` with the exact confirmation ID and a stable key. This approves the idea only; it does not start generation or publish.
5. Report the returned state. Any schedule later generated from an agent-approved idea remains held for final approval, even if Autopilot auto-approval is on. Final schedule approval needs `approve_schedule` with Publishing permission and a separate explicit user decision, or the Wahlu calendar.

Approval and regeneration require `posts:write` and an eligible paid plan. Explain entitlement refusals neutrally without subscription catalogues, prices, upgrade links or checkout. Do not change billing, start a new Autopilot plan, generate media, trigger the full week, or bypass a Free-plan refusal. Those controls remain in Wahlu.
