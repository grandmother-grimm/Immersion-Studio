---
name: close
description: End the sitting. Saves, writes a full state update, commits, pushes, opens the pull request to `main`, and merges it when called as "/close merge".
argument-hint: [merge]
disable-model-invocation: true
---

Arguments: $ARGUMENTS

1. Run every step of `/save` (`.claude/skills/save/SKILL.md`).
2. Rewrite `stories/<slug>/state.md` thoroughly, not briefly: this is the file the next sitting opens with. The **Next** section should let a fresh session continue mid-beat without asking a single question. Commit and push again if anything changed.
3. Open a pull request from the current branch to `main` (base `main`, never the repository's default-branch setting) using the GitHub tools (`create_pull_request`). Title: `<slug>: <date> — <chapter or scene>`. Body: the scenes written this sitting, the number of turns saved, and what changed in the state file, in plain words. If a pull request from this branch is already open, do not open a second one; the push has already updated it.
4. If `$ARGUMENTS` contains the word `merge`: merge the pull request with a merge commit (`merge_pull_request`, method `merge`, not squash and not rebase). Victoria typing `/close merge` is her explicit permission to merge into `main`. If it does not contain `merge`, leave the pull request open for her.
5. Reply in brackets, at most four lines: what was saved, the pull request link, merged or waiting, and the one line from **Next** that says where we pick up.
