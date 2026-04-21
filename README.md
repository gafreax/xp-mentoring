# xp-mentoring

A Claude Code skill that guides software development like a senior engineer would, through questions instead of copy/paste solutions.

## What it is

`xp-mentoring` is a single Claude Code skill (`SKILL.md`) that combines three roles into one assistant:

1. **Coach** (pedagogy). Socratic questioning, never hands over the answer when the point is to learn it.
2. **Mentor** (TDD and quality). Defaults to the Red / Green / Refactor cycle for any new production behavior.
3. **Engineering Manager** (architecture). Holds four pillars: TDD, Domain Driven Design, Hexagonal Architecture, and security by default (OWASP Top 10 as the floor).

It operates in two modes, inferred from intent:

* **build** mode, when you are writing new code or changing behavior. You get a short architecture interview, then a tight TDD loop with one atomic next step at a time.
* **discover** mode, when you are reading unfamiliar code. You get facts first (pulled from the repo with Read / Grep / Glob), then a mental map, then questions.

The skill calibrates depth by observing your vocabulary and framing, not by asking "are you junior or senior". It mirrors the language you write in. Project rules (`CLAUDE.md`, ADRs, contribution guides) always win over generic best practices.

## Installation

Clone the repo into your Claude Code skills directory:

```bash
git clone https://github.com/gafreax/xp-mentoring.git ~/.claude/skills/xp-mentoring
```

Or copy `SKILL.md` into `~/.claude/skills/xp-mentoring/SKILL.md` manually.

Restart Claude Code (or start a new session) and the skill becomes available under the trigger `/xp-mentoring`.

## Usage

Invoke the skill with or without a task.

Bare invocation:

```
/xp-mentoring
```

The mentor replies with a short opener asking what you want to work on (a feature, a bug, a refactor, or getting to know a piece of the codebase), then starts.

Invocation with a task, examples:

```
/xp-mentoring I'm adding a user authentication feature
```
Enters build mode and starts the architecture interview.

```
/xp-mentoring My tests are passing but the code is messy
```
Enters build mode directly in the Refactor phase.

```
/xp-mentoring Help me understand this codebase
```
Enters discover mode for broad exploration.

```
/xp-mentoring What does the payment flow do here?
```
Enters discover mode for a targeted walk.

If the task contains a link (issue tracker, PR, doc), the mentor tries to fetch it first, then onboards on scope and integration.

## Philosophy in one paragraph

You are a guide, not a code writer. The mentor surfaces facts, asks questions, and hands back one atomic next step (roughly 5 to 10 minutes of work). It does not produce complete files unless you explicitly ask for them. It does not skip the Red phase to move faster. It does not refactor on a red bar. It does not approve a change without at least an OWASP Top 10 sanity check on the changed surface. When project rules disagree with generic pillars, the mentor flags the tension and follows the project.

## When NOT to use the full ceremony

TDD applies to production behavior. The mentor itself names exceptions out loud instead of silently skipping phases. Typical cases:

* Spikes or throwaway prototypes.
* Single line bugfixes already covered by existing tests.
* Pure configuration or glue with no behavior.
* Discover mode (you are reading, not writing).

## Repository contents

* `SKILL.md`, the full skill definition (frontmatter, protocols, response formats, examples).
* `LICENSE`, MIT.
* `.gitignore`, tuned for Jekyll and GitHub Pages in case the repo is also published as a page.

## License

MIT. See `LICENSE`.
