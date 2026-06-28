# A suggested workflow

Here's an example workflow that worked well for me on a past project — from a rough idea all the way to a shipped product.

## 1. Draft a rough PRD (/kickstart-ai-project)

- Run `/kickstart-ai-project` and follow it with a prompt describing your project — the more detail, the better.
- You don't need to know 100% of what the project will look like; this step (and the next) will help shape it.
- Ask Claude Code to write the result out to a `PRD.md` file — a first, rough draft of the requirements.

## 2. Refine the PRD (/grill-me)

- Use `/grill-me` to stress-test the rough PRD. The grill session forces you to resolve every branch of the decision tree *before* writing any code.
- It even surfaces important questions I hadn't thought to consider, and gets the agent and me on the same page about what I'm actually building.
- Once done, ask Claude to update the PRD with the locked decisions (a new revision).

> **Lesson:** don't skip the grill. Every "we'll decide later" turns into a rewrite.

## 3. Break the work into vertical slices (/to-issues)

- Split the PRD into independently-grabbable GitHub issues.
- Slice **vertically** along the product (tracer-bullet slices), not horizontally by layer. This way each issue ships something end-to-end and the build gets more feedback along the way.
- Review and approve the issues as they're generated.

## 4. Prove the setup works before any real logic

- Write a tiny smoke test first — e.g. a single API call that proves your key and environment actually work — before writing any business logic.
- Scaffold the repo with stubs so the tests pass *before* there's any real logic to break.

## 5. Build in a locked order

- Follow the build order from the PRD. Each step = one PR = one closed issue.
- **One constraint per file.** Keep each part responsible for one thing (e.g. core engine stays pure, the provider talks to the API, the CLI does the file I/O). When responsibilities don't leak across files, the code stays easy to test and cross-file mistakes become obvious.
- Make commits map to build steps (`build step N: <thing>`) so `git log --oneline` reads like the table of contents of the PRD.

## 6. Expect to re-grill when reality hits

- Once the first version runs against real inputs, real bugs show up.
- When a design assumption breaks, re-grill the design and write a new PRD revision rather than patching blindly. Treat the spec as a living document.

## Conventions that held the project together

Codify these in `CLAUDE.md` so future agents and humans follow the same rules:

- **Change-log every behavior-affecting edit** to a `progress.txt` (append-only, dated), each entry with *What / Why it works / Verification / Caveats*. This becomes the project's narrative memory — read it top to bottom and you see exactly how the codebase evolved. (Pure refactors are exempt.)
- **Commits map to build steps**, so the git history mirrors the PRD.
- Keep a consistent convention for docstrings and comments so the codebase reads the same everywhere.

## The skills I leaned on most

- `/grill-me` — turn vague intent into locked decisions before coding.
- `/to-issues` — turn the PRD into vertical-slice GitHub issues.
- `/loop` — when iterating on prompts against tests.
- `/review` and `/security-review` — before merging each PR.
- Sub-agents (Explore, Plan) — for cross-file research instead of polluting the main context.

## The three rules that made this work

1. **Lock the design before you code** (PRD + grill).
2. **One constraint per file** — cross-file leaks become obvious.
3. **Every behavior change goes in the change-log the same day**, with *why* it works, not just *what* changed. This is what lets a new contributor walk in cold and ship a fix the same week.
