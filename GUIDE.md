# How to use the studio

This is the plain-words guide to writing with Claude in this repository. Read it once, keep it open for the first few sittings, and then you will not need it.

## The one-minute version

1. Start a session on this repository at claude.ai/code.
2. Type `/open <story>` to step into a story.
3. Write your turns. Claude writes the world.
4. Type `/save` whenever you want the story on disk. Claude also saves at every scene break on its own.
5. Type `/close merge` when you are done for the night. Always.

Everything below explains those five lines.

## Cheat sheet

| You type | What happens |
|---|---|
| `/open thornwood` | Claude loads that story's bible, state file and latest transcript, gives you a four-line recap, and waits for your turn. |
| `/open` | Claude lists the stories and asks which one. |
| `/save` | Every turn since the last save is copied into the transcript word for word, the state file is updated, everything is committed and pushed. |
| `/close merge` | Saves, writes a full state update, pushes, opens the pull request and merges it, so the next session can see tonight's work. |
| `/close` | Same, but leaves the pull request open for you to merge yourself on GitHub. |
| `/new-story <slug>` | Creates a new story folder from the templates and asks you for its bible. |
| `[anything in square brackets]` | Out of scene. Claude answers as itself, briefly, in brackets. |
| `OOC: anything` | Same as brackets. |
| `/context` | Shows how full the conversation's memory is. |
| `/compact keep the last scene verbatim` | Summarises the older conversation to free space. Save first. |

## The words

- **Repository** (repo): this folder of files, kept on GitHub. The studio.
- **Session**: one conversation with Claude. Each session gets a fresh copy of the repo.
- **Branch**: a private copy of the files that one session works on. Every session gets its own.
- **Commit**: a saved snapshot of the files, with a short note.
- **Push**: send commits from the session up to GitHub so they are safe.
- **Pull request** (PR): a request to copy one branch's changes into main.
- **Merge**: accepting that request. After a merge, main has the new files.
- **Main**: the main branch. New sessions start from here. If tonight's work is not on main, tomorrow's session cannot see it.

## Starting a sitting

1. Go to claude.ai/code in a browser, or Code in the Claude app. Start a new session and choose the Immersion-Studio repository. Leave the branch at the default, which is main.
2. Wait for the session to open. The first message box is yours.
3. Type `/open` and the story's slug, for example `/open thornwood`. Send it.
4. Claude replies out of scene, in brackets, with four lines: where the scene stands, the last line written and who wrote it, anything you need to know, and "Your move."
5. Write your turn as prose, exactly as in the Playground. Claude answers in scene.

If you do not remember the slug, type `/open` alone and Claude lists the stories.

## Writing

- **In scene:** write your character. Claude writes the narrator and everyone else, and never writes your character's thoughts or consequential decisions.
- **Out of scene:** put it in square brackets, or start a line with `OOC:`. Claude drops character and answers as itself. Then write your next turn and the scene resumes.
- **Directions:** a bracketed note before your prose is an instruction, not a conversation. `[Skip to the morning. She wakes alone.]` followed by your turn is followed as written.
- **Decisions** made out of scene (a new fact, a change of plan) go into the story's state file at the next save, not into the transcript.

## Saving

Nothing in a session is safe until it is saved and pushed. The conversation is not the manuscript; the transcript files are.

- Claude saves on its own at every scene break.
- Type `/save` any time you want to be sure: before a break, after a turn you love, when the sitting has run long.
- The reply is one bracketed line, for example `[Saved: 6 turns to transcript/003-the-feasting-hall.md, state updated, pushed.]`
- Saved turns are copied word for word, yours and Claude's, typos included. Edits happen later, out of scene, if you ask for an edit pass.

## Ending a sitting

Type `/close merge`. That is the whole ritual.

What happens: Claude saves, rewrites the state file in full so the next session can pick up mid-beat, pushes, opens a pull request from this session's branch to main, merges it, and replies with four lines including the pull request link and where you pick up next time.

If you only type `/close`, the pull request stays open and you merge it yourself: open the link, press "Merge pull request", then "Confirm merge". Until that happens the next session cannot see tonight's work.

If you forgot to close: open the old session from the sidebar at claude.ai/code and type `/close merge` there. It still works days later.

## Starting a new story

1. Pick a slug: lowercase, hyphens, no spaces. `thornwood`, `salt-and-iron`.
2. In any session, type `/new-story thornwood`.
3. Claude creates the folder and asks for the bible. Paste your Playground system prompt for that story, or notes, or talk it through. Claude files it into `stories/thornwood/bible.md` in your words, reorganised into the template's sections, leaving out anything the studio voice already covers.
4. Read the bible file once, in the session or on GitHub, and correct anything.
5. `/close merge`, then `/open thornwood` in the next session, or straight away in this one.

The first `/open` of a new story asks how to begin: paste the Playground history so far, give a summary, or start fresh.

## Bringing in a story that already has history

If a story was running in the Playground before it came to the studio, the earlier turns belong in the transcript so Claude can read them and continue from the last line. Two ways to get them in; pick whichever is easier.

**Paste in chunks.** In a session where the story's folder exists, paste the history in order, in as many messages as the message box needs, each one starting with a bracketed label like `[history, part 1 of 4]`. Keep whatever speaker labels the paste carries. Claude appends each part to the transcript word for word as it arrives, so nothing is lost if the session dies in the middle. When the last part is in, say `[history complete]` and Claude writes the state file from it. Then `/close merge`.

**Upload a file on GitHub.** Open the repository on GitHub, go into `stories/<slug>/notes/`, choose "Add file" then "Upload files", drop in a text or markdown file of the history, and commit it to main. In the next session, type `[OOC: the Playground history is in notes/<filename>, bring it into the transcript.]` and Claude converts it into chapter files and writes the state file. Better for anything long.

Either way, the next `/open` recaps from the last imported line and says whose move it is.

## Editing the bible or the state file

Say it in brackets: `[OOC: add to the bible, Caius's brother is dead, killed in the spring.]` Claude edits the file and confirms. Or edit the file on GitHub yourself and have Claude re-read it with `/open`.

## When something feels wrong

- **Claude seems to have forgotten the story.** Type `/open <slug>` again. It re-reads everything from disk.
- **You want more than a four-line recap.** `[OOC: give me the full state of play.]`
- **Claude says it cannot reproduce a turn word for word.** The conversation was compacted before a save. Paste your turn if you still have it; Claude's own lost turn is rewritten, and it will say so. Save more often in long sittings.
- **The slash command is not recognised.** Type the words instead: "open thornwood", "save", "close and merge". Claude knows what they mean.
- **A message is blocked by a safety classifier.** This happened while setting up the studio, each time on a message that carried the raw Playground directive. The directive now lives in `studio/voice.md` and loads on its own; it never needs to be pasted into chat again. If it happens on an ordinary message, re-send it with less instruction and more story, or in two halves.
- **Something went to the wrong branch, or the merge failed.** `[OOC: what branch are we on and what is unmerged?]` Claude will sort it out and say what it did.

## Where things are

```
CLAUDE.md                     the studio rules, loaded every session
GUIDE.md                      this file
studio/voice.md               Valen, the universal protocols and directives
studio/templates/             blank bible and state files
.claude/skills/               the commands
stories/<slug>/bible.md       canon and story-specific directives
stories/<slug>/state.md       the save file
stories/<slug>/transcript/    the manuscript, one file per chapter
stories/<slug>/notes/         anything else
```
