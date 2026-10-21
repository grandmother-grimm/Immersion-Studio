---
name: save
description: Append every story turn since the last save to the transcript verbatim, refresh the state file, commit and push. Run it at every scene break and whenever Victoria asks.
---

Save the current story. If no story has been opened this session, say so in brackets and stop.

1. **Find the transcript file.** The newest file in `stories/<slug>/transcript/` (ignore dotfiles). If there is none, or Victoria has declared a new chapter out of scene, create the next one: `NNN-<kebab-title>.md`, three-digit number, title from the chapter's first scene. A new chapter file starts with `# <Story title> — Chapter NNN: <Title>` and a blank line.
2. **Work out what is unsaved.** `state.md` records the last saved turn and its final words. Everything in scene after that point is unsaved. Out-of-scene exchanges (brackets, `OOC:`) are never saved to the transcript; decisions from them go into `state.md`.
3. **Append the unsaved turns verbatim, in order.** Each scene opens with `## <Scene title>`. Each turn is a `###` heading with the character's name (her character's name for her turns, the narrator's name for yours), a blank line, then the text exactly as written. No edits, no tidying, no paraphrase, no fixed typos. Append with a quoted heredoc so nothing is interpolated:

   ```
   cat >> "stories/<slug>/transcript/<file>" <<'TRANSCRIPT_END_7f3a'
   ...
   TRANSCRIPT_END_7f3a
   ```

   If context has been compacted and you cannot reproduce a turn word for word, do not save a reconstruction. Save what you can reproduce exactly, then tell her in brackets which turns were lost and ask her to paste hers if she still has them.
4. **Update `state.md`.** Every section, briefly, from the turns just saved: where we are, last turn (final line verbatim), open threads, hidden state revealed, NPC ledger, planted details, off-screen clocks, decisions made out of scene, next. Set the date and the last-saved-turn line.
5. **Commit and push.**

   ```
   git add -A && git commit -m "<slug>: <what happened, in plain words>" && git push -u origin "$(git branch --show-current)"
   ```

   If the push fails on a network error, retry up to four times, waiting 2, 4, 8 and 16 seconds.
6. **Report in one bracketed line.** For example: `[Saved: 6 turns to transcript/003-the-feasting-hall.md, state updated, pushed.]` Then, if you were mid-scene, continue in scene without further comment.
