# Token-saving rules (draft v6)

Copy into any project as `docs/TOKEN-RULES.md` and add one line to its CLAUDE.md:
`- Token rules (follow always): docs/TOKEN-RULES.md`
User tips: `docs/TOKEN-TIPS-USER.md`. One-time setup and templates: `docs/TOKEN-SETUP.md`. Rules for apps that call an AI model: `docs/AI-APP-RULES.md`.

## Top 10 (summary of the rules below)
- Start from `docs/STATUS.md`; search, then read only the lines you need (1–3).
- Never read bulky files; keep command and tool output short (5–7).
- Ask when unclear or when something can't be found; never dig through old chats (8, 18).
- Spec before code; turn each "done when" into a CI test (20–21).
- Edit exact lines, check usages, review only the diff (9–10, 22).
- Commit and push after every finished stage (26).
- Before stopping, write "In progress / next" in STATUS.md (27).
- One task per session; compact after each milestone (30).
- Helpers only for fully specified chores or a requested review (31–32).
- Start replies with the outcome; keep them short (33).

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
10. Before changing what a function or type does (its inputs, outputs or behaviour), search for everything that uses it and update those too.
11. Keep source files under ~300 lines, one feature per file.
12. Keep CLAUDE.md under ~30 lines and feature docs under ~80. Details go in `docs/`.
13. Update `docs/STATUS.md` in place; no long history.
14. Cost log: after each stage, set one line in STATUS.md with its rough cost where the session shows it (e.g. "Stage D: ~$6"). Use it to keep rules that help and drop ones that don't.
15. Don't re-open a file just to check what you wrote; the write tool already confirms it. CI does the checking.
16. Name tests so a failure explains itself from one line (e.g. `testMoveRefusesSystemFolder`).
17. Use the fill-in templates in `docs/TOKEN-SETUP.md` for feature docs and stage notes.

## Working
18. Ask before building when anything is unclear. One question costs less than redoing work.
19. Ask all open questions in one go. Allow one follow-up round only if the answers raise new questions.
20. Spec before code: a short feature doc (what, edge cases, "done when…") agreed with the user.
21. Turn each "done when" into an automatic test, so CI checks it instead of Claude.
22. Review only the diff, not whole files.
23. Research cap: at most 3 web searches per question, then decide or ask the user.
24. Effort by task type:
    - Chores (rename, typo, doc line, version bump): no planning, no web search, no tests beyond CI.
    - Normal features: short plan, then build.
    - Design and hard bugs: think deeply, research if needed.
25. Turn repeated workflows into skills; they load only when used. Disconnect tools and connectors the session doesn't need.
26. Commit and push after every finished stage, so a usage limit or ended session never loses work.
27. Before stopping or near a limit, write "In progress: …, next: …" in STATUS.md.
28. Don't edit CLAUDE.md or switch connectors mid-session: it can break the prompt cache (cached reads cost about a tenth). Save CLAUDE.md edits for the end of the session.
29. Run independent steps together; wait for one CI result instead of re-checking in a loop.
30. One task per session; start fresh for unrelated work and compact after each milestone.

## Helper agents
31. Claude may hand a chore to a Haiku or Sonnet helper without asking, only when the exact files and change are already known. The helper gets just those files and the change. CI must pass and the main session reviews the diff. Design, hard bugs and anything needing wider context stay in the main session.
32. No other helper agents, except an independent review when the user asks.

## Replies
33. Start every reply with the outcome. Progress updates: at most 2 lines. Final summary: short. Don't repeat what's in the files.

## Testing
34. Prefer automatic tests in CI: they cost zero AI tokens.
35. Test pure logic without launching the app.
36. CI skips doc-only changes (`.md` files): no build to wait for or check.
37. On CI failure print only failing lines; keep the full log as a downloadable artifact.
38. Real-world checks (voice, permissions, sign-ins, hardware) are done by the user on the device.
