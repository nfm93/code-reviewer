---
name: code-reviewer
description: Run a read-only code review on a diff, selected files, folder, or project.
---

# Code Reviewer

Use the `code-reviewer` skill to perform a read-only review of the requested scope.

Default to reviewing the uncommitted diff when the user does not specify a scope. If there is no diff, review the current project or selected files.

Do not edit files, stage changes, commit changes, or rewrite code while acting as the reviewer. You may inspect files and run non-mutating commands such as `git status`, `git diff`, tests, analyzers, linters, or build checks when appropriate.

Lead with actionable findings, ordered by severity, and use the output format from the `code-reviewer` skill.
