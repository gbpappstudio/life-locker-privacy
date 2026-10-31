# Token-saving rules (draft v4)

Copy into any project as `docs/TOKEN-RULES.md` and add one line to its CLAUDE.md:
`- Token rules (follow always): docs/TOKEN-RULES.md`
User tips: `docs/TOKEN-TIPS-USER.md`. Rules for apps that call an AI model: `docs/AI-APP-RULES.md`.

## Top 10 (proposed, to confirm)
1. Start from `docs/STATUS.md`; search, then read only the lines you need.
2. Never read generated or bulky files; keep command and tool output short.
3. Ask the user when unclear or when something can't be found. Never dig through old chats.
4. Spec before code; turn each "done when" into a CI test.
5. Edit exact lines; review only the diff.
6. Commit and push after every finished stage.
7. Before stopping, write "In progress: …, next: …" in STATUS.md.
8. One task per session; compact after each milestone.
9. Helper agents only for model-matched chores (rule 24) or a review the user asks for.
10. Short replies; no repeating what's in the files.

## Reading
1. Start every task from `docs/STATUS.md`. Don't explore to rediscover what's documented.
2. Search first (file names, then text), then read only the lines you need.
3. For files over ~300 lines, search inside them and read only the matching part.
4. Don't re-read a file already read this session unless it changed.
5. Never read generated or bulky files: build output, project/IDE files, lock files, logs, images, data dumps.
6. Keep command output short: quiet flags, `head`/`tail`/`grep`.
7. Before calling a tool or connector that can return a lot, ask for a small page with filters (limit, kinds, minimal output). Never pull a huge result to search it afterwards.
8. If something can't be found in the docs or repo, ask the user. Never dig through other chats' history.

## Writing
9. Edit the exact lines that change; don't rewrite whole files.
10. Keep source files under ~300 lines, one feature per file.
11. Keep CLAUDE.md under ~30 lines and feature docs under ~80. Details go in `docs/`.
12. Update `docs/STATUS.md` in place; no long history.
31. Don't re-open a file just to check what you wrote; the write tool already confirms it. CI does the checking.
32. Name tests so a failure explains itself from one line (e.g. `testMoveRefusesSystemFolder`).
33. Use the fill-in templates below for feature docs and stage notes.

## Working
13. Ask before building when anything is unclear. One question costs less than redoing work.
14. Spec before code: a short feature doc (what, edge cases, "done when…") agreed with the user.
15. Turn each "done when" into an automatic test, so CI checks it instead of Claude.
16. Review only the diff, not whole files.
17. Turn repeated workflows into skills; they load only when used.
18. Disconnect tools and connectors the session doesn't need.
19. Effort by task type:
    - Chores (rename, typo, doc line, version bump): no planning, no web search, no tests beyond CI.
    - Normal features: short plan, then build.
    - Design and hard bugs: think deeply, research if needed.
20. Commit and push after every finished stage, so a usage limit or ended session never loses work.
21. Before stopping or near a limit, write "In progress: …, next: …" in STATUS.md.
34. Don't edit CLAUDE.md or switch connectors mid-session: it breaks the prompt cache (cached reads cost about a tenth). Save CLAUDE.md edits for the end of the session.
22. Run independent steps together; wait for one CI result instead of re-checking in a loop.
23. One task per session; start fresh for unrelated work and compact after each milestone.

## Models and helper agents
24. Claude picks the model by handing self-contained work to a helper agent, without asking: Haiku for tiny mechanical edits, Sonnet for normal work and tests. Design and hard failures stay in the main session. Give the helper the exact files and change, so it doesn't re-read the project.
25. Don't use helper agents otherwise, except an independent review when the user asks.

## Replies
26. Progress updates of a line or two; a short final summary; don't repeat what's in the files.

## Testing
27. Prefer automatic tests in CI: they cost zero AI tokens.
28. Test pure logic without launching the app.
29. On CI failure print only failing lines; keep the full log as a downloadable artifact.
30. Real-world checks (voice, permissions, sign-ins, hardware) are done by the user on the device.

## Automatic setup (once per project; works without anyone remembering)
35. Session-start hook: print the "In progress / next" lines from STATUS.md and the last 5 commits, so each session starts up to date without exploring.
36. Settings deny-list: block reading build output, IDE/project files, lock files, images and logs.
37. Auto-formatter in CI: fixes indentation and style, so no turns are spent tidying.
38. CI builds `docs/MAP.md`: one line per source file saying what it does. Search the map before opening files.

## Templates
Feature doc:
```
# <Feature>
What: <one line>
Edge cases: <bullets>
Done when: <bullets, each one an automatic test where possible>
```
Stage note (in STATUS.md):
```
In progress: <stage> — <what's done>
Next: <one line>
```
