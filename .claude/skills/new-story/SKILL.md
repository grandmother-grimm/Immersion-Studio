---
name: new-story
description: Scaffold a new story folder from the studio templates and fill its bible from whatever Victoria provides.
argument-hint: <story-slug>
disable-model-invocation: true
---

New story slug: $ARGUMENTS

1. The slug must be lowercase letters, digits and hyphens. If it is missing, ask for one. If `stories/$ARGUMENTS/` already exists, stop and say so.
2. Create the folder and copy the templates:

   ```
   mkdir -p "stories/$ARGUMENTS/transcript" "stories/$ARGUMENTS/notes"
   cp studio/templates/bible.md "stories/$ARGUMENTS/bible.md"
   cp studio/templates/state.md "stories/$ARGUMENTS/state.md"
   touch "stories/$ARGUMENTS/transcript/.gitkeep"
   ```

3. Ask Victoria for the bible: a pasted Playground system prompt, notes, or a conversation. Then fill `bible.md`:
   - Keep her wording. Reorganise into the template's sections; do not rewrite her canon.
   - Anything that duplicates `studio/voice.md` (Valen's identity, the universal protocols, the universal directives) stays out of the bible. Only story-specific material goes in.
   - If something she gives you conflicts with `studio/voice.md`, put it in the bible's **Story directives** (the bible wins for that story) and tell her you did.
   - Mark the female lead's profile as hers.
4. Fill `state.md` with "Not started in the studio" under **Where we are**, and the date.
5. Commit and push: `git add -A && git commit -m "$ARGUMENTS: new story scaffolded" && git push -u origin "$(git branch --show-current)"`.
6. Tell her what was created and that the story opens with `/open $ARGUMENTS` from the next session, or in this one once the bible is in.
