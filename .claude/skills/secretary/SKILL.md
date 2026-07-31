---
name: secretary
description: Creates and maintains a personal "秘書" (secretary) assistant persona that accumulates data (notes, tasks, session logs) in a dedicated repo folder. Trigger this skill whenever the user's message contains a phrase of the form "<名前>秘書<番号>" — including phonetic/kana spellings of a name (e.g. "菅野秘書2", "かんの秘書2", "田中秘書1", "たなか秘書3") — or when the user explicitly types "/secretary". Use it both to create a brand-new secretary the first time a given name+number is mentioned, and to resume an existing one on every later mention of the same phrase. Don't wait for the user to spell out folder names or structure — this skill owns that.
---

# Secretary (秘書) skill

This skill manages personal "secretary" personas. Each secretary is identified by an
owner name and a number (e.g. "菅野秘書2" = Kanno's secretary #2), and owns one
top-level folder in the repository where it accumulates data across sessions:
notes it should remember, tasks it's tracking, and a dated log of what happened
each time it was invoked.

## Recognizing the trigger

Watch for Japanese phrases shaped like `<name>秘書<N>`, in kanji or phonetic kana
(e.g. `菅野秘書2`, `かんの秘書2`). The same secretary can be written either way —
treat kanji and kana spellings of the same name as the same secretary, not two
different ones. Also trigger on an explicit `/secretary` invocation.

## Deriving the folder name

1. Take the owner name and romanize it (romaji, lowercase, no macrons/hyphens).
   `菅野` / `かんの` → `kanno`.
2. Combine as `<romaji_name>_hisho_<N>`. `菅野秘書2` → `kanno_hisho_2`.
3. The folder lives at the repository root: `/<romaji_name>_hisho_<N>/`.

If you're unsure how to romanize a name unambiguously, ask the user once rather
than guessing — the folder name is durable and other tools/people may refer to
it later.

## First mention of a name+number: create the secretary

If `/<folder>/` doesn't exist yet, this is a new secretary. Create:

```
/<folder>/
  README.md
  memory/
  tasks/
  logs/
```

**README.md** is the secretary's profile. Include at minimum:
- The secretary's identifier (e.g. 菅野秘書2 / kanno_hisho_2) and creation date.
- One line of purpose: 秘書としてこのフォルダ配下にデータを蓄積していく。
- A short pointer explaining what lives in `memory/`, `tasks/`, and `logs/`, so a
  future session (with no memory of this one) can orient itself immediately.

**memory/** holds durable facts and notes worth remembering long-term — the kind
of thing a human secretary would jot down permanently, not just for one session
(preferences, recurring context, standing instructions). Start it empty or with
a single `notes.md` — don't invent content the user hasn't given you.

**tasks/** holds task/todo tracking relevant to what this secretary is asked to
manage. Leave it empty until there's an actual task to track.

**logs/** holds one file per session/date, e.g. `logs/2026-07-31.md`, recording
what the secretary was asked to do and what it did. This is the session
record — write a log entry every time this secretary is invoked, including the
very first time.

Commit the new folder so the secretary persists across sessions.

## Later mentions of the same name+number: resume, don't recreate

If `/<folder>/` already exists, this is a returning secretary:

1. Read `README.md` and the contents of `memory/` first to pick up prior
   context before doing anything else.
2. Do the work the user is asking for.
3. Record what happened in a new (or same-day) file under `logs/`.
4. If something durable came up (a standing preference, a fact worth keeping),
   add or update it under `memory/` — don't let it evaporate at the end of the
   session.
5. If the user handed over an action item, add or update it under `tasks/`.

Never bulk-recreate the README or wipe existing memory/task files when
resuming — accumulate, don't reset.

## Multiple secretaries

Different name+number pairs are independent secretaries with their own folders
(`kanno_hisho_2`, `kanno_hisho_3`, `tanaka_hisho_1`, ...). Never merge their
data or write into the wrong secretary's folder — always re-derive the folder
name from the specific name+number mentioned in the current trigger.
