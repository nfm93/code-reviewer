# Code Reviewer

Code Reviewer is a reusable Codex plugin that adds a read-only reviewer skill for codebases, diffs, and app-specific project reviews.

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
  .codex-plugin/
    plugin.json
  skills/
    code-reviewer/
      SKILL.md
```

## Installation

This repository contains a Codex plugin. Install it through the Codex plugin flow from the repository or add it to a local/personal plugin marketplace.

For local development, keep the plugin folder available to Codex and register it in your personal marketplace.

## License

No license has been selected yet.
