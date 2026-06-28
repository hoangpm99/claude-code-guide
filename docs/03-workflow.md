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

## Anatomy of a good `CLAUDE.md`

`CLAUDE.md` is the file every agent reads first — it's where the conventions above actually live. A good one is short and high-signal; the agent re-reads it every session, so it pays rent forever. The structure that worked for me:

- **What this project does** — two or three sentences at the top so the agent orients before reading any code.
- **Layout** — a small `tree` of the important directories with a one-line "owns X" note each. This is what stops the agent guessing where things go.
- **Commands** — the exact, copy-pasteable commands to install, run, and test (including how to run a *single* test). Saves the agent from inventing them.
- **Hard Constraints** — the single most valuable section. Name the invariants the agent must never cross, each with its *why*. For example:
  > **Engine never touches the filesystem.** All disk I/O belongs in the CLI or the UI layer. This boundary must not be crossed.

  These are the rules that, if broken, quietly rot the design. Stating them up front (with the reason) means the agent defends them instead of you re-explaining every time.
- **Conventions** — spell out docstring and comment style *concretely*, with a tiny example. "Use Google-style docstrings; comment only when the *why* is non-obvious, never narrate what the code already says." Vague guidance gets ignored; a worked example gets followed.
- **Change-logging rule** — the instruction to append every behavior-affecting change to `progress.txt` lives here too, so the agent does it without being asked.

> **Lesson:** put the *why* next to every constraint. "Backend has no UI imports" gets bent the first time it's inconvenient; "Backend has no UI imports *so it stays testable without the UI installed*" survives.

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
