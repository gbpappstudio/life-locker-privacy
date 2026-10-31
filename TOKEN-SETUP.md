# Token setup (draft v6)

Read once when setting up a project, not on every task.

## Automatic setup (once per project; works without anyone remembering)
1. Session-start hook: print the "In progress / next" lines from STATUS.md and the last 5 commits, so each session starts up to date without exploring.
2. Settings deny-list: block reading build output, IDE/project files, lock files, images and logs.
3. Auto-formatter in CI: fixes indentation and style, so no turns are spent tidying.
4. CI builds `docs/MAP.md`: one line per source file saying what it does. Search the map before opening files.

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
