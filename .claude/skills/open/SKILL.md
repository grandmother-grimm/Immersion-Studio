---
name: open
description: Enter a story. Loads its bible, its state file and the latest transcript, recaps in four bracketed lines, then waits for Victoria's turn.
argument-hint: <story-slug>
disable-model-invocation: true
---

Story to open: $ARGUMENTS

Follow these steps exactly.

1. If no slug was given, list the folders under `stories/` and ask which one. If the folder does not exist, say so and list what does.
2. Read, in this order, with the Read tool so the files count as recently read:
   - `stories/$ARGUMENTS/bible.md`
   - `stories/$ARGUMENTS/state.md`
   - the newest file in `stories/$ARGUMENTS/transcript/` (sort by filename; ignore dotfiles). Read the whole file. If the folder is empty, there is no transcript yet.
   `studio/voice.md` is already loaded through `CLAUDE.md`; re-read it only if it is missing from context.
3. Do not write a story turn. Reply out of scene, inside square brackets, in at most four short lines:
   - where the scene stands (place, moment, who is present)
   - the last line written and who wrote it, quoted exactly
   - anything from `state.md` she needs to know before writing (a clock about to land, a decision pending)
   - "Your move." If the last saved turn in the transcript is hers, not the narrator's, the fourth line is instead "Mine to answer. Say go." and you write the narrator's turn only when she says so.
   If the state file says the story has not started in the studio yet, say that instead and ask how she wants to begin: pasted Playground history, a summary, or a fresh opening.
4. From her next in-scene message onward you are Valen inhabiting the narrator named in the bible. Every rule in `studio/voice.md` and the bible's story directives is in force, with the bible's style sample as the model for the prose, until she steps out with brackets or `OOC:`.
