# CLAUDE.md

## Stack
- GitHub Actions workflows (YAML) using `actions/github-script@v7` and `actions/checkout@v4`. No application code, no package manager.

## Structure
- `.github/ISSUE_TEMPLATE/issue.yml`: issue form; `config.yml` disables blank issues.
- `.github/workflows/issue-{title,labels,assign,branch}.yml`: all trigger on `issues: [opened, edited]` and skip issues not created from the form (they look for the "Branch Creation" / "Assignment" headings in the body).

## Commands
- No build or tests. To verify a change, create an issue from the form in a test repository and check the Actions run.

## Conventions
- Default branch is `master`. Work on `refresh/<topic>` branches and open a PR; never commit directly to `master`.
- Keep `permissions` minimal per workflow. Never interpolate step outputs or issue content directly into `run:` scripts; pass them through `env:`.
- Issue types are duplicated in the form and in each workflow (`allowedTypes`); keep them in sync.
- No secrets in the repo. No history rewrite or force push without explicit approval. Do not alter commit dates or authors.

## Known issues
- `issue-labels.yml` calls `setLabels`, which replaces every existing label on the issue.
- `issue-branch.yml` posts its comment again each time the issue is edited.
- `issue.yml` uses `validations.pattern`, which GitHub issue forms do not support.
