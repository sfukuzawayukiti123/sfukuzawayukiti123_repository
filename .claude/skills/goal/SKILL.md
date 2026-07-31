---
name: goal
description: Checks whether current work is actually on track toward a stated goal — reviews recent progress, flags drift or blockers, and reports a concrete status. Trigger this whenever the user explicitly types "/goal", or asks things like "am I on track", "are we making progress", "check my progress", or "did we drift off the goal". Use it to audit against an existing goal, not to define a new one from scratch (use /grill-me for that).
---

# Goal Check

This skill is a progress audit, not a pep talk. When invoked, figure out
whether recent work is actually converging on the stated goal, and say so
plainly — including when it isn't.

## How to run it

1. **Find the goal.** Look for it in the conversation first. If a secretary
   folder (`<name>_hisho_<N>/`) is active, also check its `tasks/` (open
   items) and `memory/` (standing goals/priorities) for the goal as recorded
   there. If no goal is clearly stated anywhere, say so and suggest running
   `/grill-me` first instead of inventing one.

2. **Gather the evidence.** Look at what's actually happened since the goal
   was set — recent commits/diffs, files changed, a secretary's `logs/`
   entries, completed vs. still-open items in `tasks/`. Don't rely on
   the user's self-report alone; check the actual state (git log, file
   contents, test results) where you can.

3. **Report status plainly.** Structure the answer as:
   - **On track / partially on track / off track** — a direct call, not hedging.
   - **What's actually been done** toward the goal, briefly.
   - **What's missing or drifted** — scope creep, stalled steps, work that
     doesn't serve the stated goal even if it's real work.
   - **The next concrete step**, not a general suggestion.

4. **If a secretary is active, log it.** Append a short status note to the
   secretary's `logs/` (and update `tasks/` if items were completed or new
   ones surfaced) so the next check has a trail to compare against.

Keep the tone honest rather than encouraging — the value of this skill is
catching drift early, so soft-pedaling a real problem defeats the point.
