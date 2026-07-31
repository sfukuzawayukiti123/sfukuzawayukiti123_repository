---
name: grill-me
description: Interviews the user with pointed follow-up questions to surface what they actually want to do, before any work starts. Trigger this whenever the user explicitly types "/grill-me", or asks to be "grilled"/questioned/pressed about a vague idea, goal, or request that hasn't been pinned down yet. Use it when a request is underspecified and guessing would waste work — this skill's job is to ask, not to assume.
---

# Grill Me

The point of this skill is to replace guessing with asking. When invoked, do not
start doing the task yet — first ask the user a focused round of questions to
turn a vague idea into something concrete enough to act on.

## How to run it

1. **Start from what's already known.** Skim the conversation (and, if a
   secretary folder like `<name>_hisho_<N>/memory/` is active in this session,
   its notes) for context you already have. Don't ask for things you can
   already infer — ask about the gaps.

2. **Ask real questions, not a form.** Use `AskUserQuestion` where the answers
   are genuinely a handful of concrete options (recommended option first), and
   plain follow-up text when the answer space is open-ended. Good questions to
   reach for:
   - What does "done" look like? How will you know this worked?
   - Who/what is this for — just you, or does someone else see the output?
   - What's the actual constraint — time, format, a specific tool, a deadline?
   - What have you already tried or ruled out?
   - Is there a version of this that's smaller/faster that would still count?

3. **Go one or two rounds, not twenty.** Ask 2-4 questions at a time, wait for
   answers, then ask a tighter follow-up round only if something's still
   unclear. The goal is a request you could hand to someone else and have them
   build the right thing — stop as soon as you're there, don't keep grilling
   for its own sake.

4. **Close the loop.** Once it's clear, restate the concretized goal back in
   1-3 sentences ("So: you want X, by Y, measured by Z — right?") and get a
   yes before starting real work. If a secretary folder is active, this is a
   good moment to jot the concretized goal into its `tasks/` or `memory/`.

Don't use this skill as a delay tactic on requests that are already clear —
if the user's ask is specific and actionable, just do it instead of grilling
them for sport.
