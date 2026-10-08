# Code Reviewer

Code Reviewer is a reusable read-only reviewer skill for codebases, diffs, and app-specific project reviews.

It can be installed as a Codex plugin, Claude Code plugin, or standalone Agent Skill.

It is designed to inspect code with fresh context, report actionable findings, and avoid editing files directly.

## What It Reviews

- Uncommitted diffs and staged changes
- Current code in selected files, folders, or whole projects
- Flutter and Dart projects
- Native iOS and Swift projects
- Native Android, Kotlin, and Java projects
- Web, Node, frontend, backend, and API projects
- Targeted areas such as security, tests, architecture, performance, accessibility, and release readiness

## Behavior

The reviewer is read-only by default.

It can inspect files, review diffs, and run non-mutating checks when appropriate. It should not edit files, stage changes, commit changes, or rewrite code while acting as the reviewer.

Findings are reported with priorities:

- `P0 blocker`: release-blocking bugs, crashes, security issues, data loss, or broken builds
- `P1 should-fix`: likely user-visible bugs, important regressions, or meaningful maintainability risks
- `P2 nit`: small but actionable correctness, clarity, test, or maintainability issues

If no actionable issues are found, the reviewer reports `Status: CLEAN`.

## Example Prompts

```text
review the uncommitted diff with code-reviewer
review current code in src/
review the whole project for bugs and test gaps
review native app code
review Flutter app code
review auth for security issues
loop review/fix until clean, max 3 rounds
```

## Review Modes

### Diff Review

Reviews uncommitted changes, staged changes, or a branch comparison. This mode focuses on regressions introduced by the diff.

### Current Code Review

Reviews the selected files, folder, feature area, or whole project as it exists now. This mode is useful even when there are no pending changes.

### Targeted Review

Reviews only the requested concern, such as security, tests, performance, accessibility, architecture, release readiness, Flutter, iOS, Android, backend, or frontend.

### Loop Review

Reports findings for the main agent to fix, then re-reviews after fixes until the code is clean or the requested maximum number of rounds is reached.

The reviewer remains read-only during the loop.

## Project Detection

The reviewer infers project type from common files:

- Flutter/Dart: `pubspec.yaml`, `lib/`, `analysis_options.yaml`, `.dart`
- iOS/Swift: `.xcodeproj`, `.xcworkspace`, `Package.swift`, `Podfile`, `.swift`
- Android/Kotlin/Java: `settings.gradle`, `build.gradle`, `build.gradle.kts`, `AndroidManifest.xml`, `.kt`, `.java`
- Web/Node: `package.json`, framework config files, `.ts`, `.tsx`, `.js`, `.jsx`
- Backend/API: route handlers, server config, migrations, database access, auth/session files, infrastructure config

## Plugin Structure

```text
code-reviewer/
  .claude-plugin/
    marketplace.json
    plugin.json
  .codex-plugin/
    plugin.json
  agents/
    code-reviewer.md
  skills/
    code-reviewer/
      SKILL.md
```

## Installation

### Codex

Add this repository as a plugin marketplace:

```bash
codex plugin marketplace add nfm93/code-reviewer
```

Then open Codex and run:

```text
/plugins
```

Install **Code Reviewer**, enable it, and start a new chat.

Use it with prompts like:

```text
review the uncommitted diff with code-reviewer
review the whole project for bugs and test gaps
review auth for security issues
```

For local development, clone this repository and add the local marketplace root instead:

```bash
codex plugin marketplace add /absolute/path/to/code-reviewer
```

After changing plugin files locally, restart the ChatGPT desktop app or refresh the marketplace so Codex picks up the latest plugin contents.

### Claude Code

This repository also contains a Claude Code plugin manifest at `.claude-plugin/plugin.json`, a marketplace manifest at `.claude-plugin/marketplace.json`, and a `code-reviewer` subagent at `agents/code-reviewer.md`.

Claude Code auto-discovers the subagent from `agents/code-reviewer.md` and the skill from `skills/code-reviewer/SKILL.md`.

Install from a Git repository with Claude Code's plugin flow after publishing or pushing this repository:

```text
/plugin marketplace add <path-or-git-url-of-this-repo>
/plugin install code-reviewer@code-reviewer-tools
```

For local testing without installation:

```bash
claude --plugin-dir ./
```

For local/manual use without a marketplace, install only the skill:

```bash
mkdir -p ~/.claude/skills/code-reviewer
cp skills/code-reviewer/SKILL.md ~/.claude/skills/code-reviewer/SKILL.md
```

Then use:

```text
Delegate the review to code-reviewer:code-reviewer.
```

or:

```text
Delegate the review to the code-reviewer subagent.
```

### Claude.ai

Zip the skill folder and upload it from Claude.ai's skill settings:

```bash
cd skills
zip -r code-reviewer.zip code-reviewer
```

Upload `code-reviewer.zip` in Claude.ai under **Customize > Skills > Create skill > Upload a skill**.

## License

No license has been selected yet.
