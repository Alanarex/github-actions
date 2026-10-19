# github-actions

> A reusable set of GitHub Actions workflows and an issue form that turn a new issue into a labelled, assigned work item with its own release branch.

![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)

**Résumé (FR)** : modèle de dépôt contenant un formulaire d'issue et 4 workflows GitHub Actions. À la création d'une issue, ils renomment le titre avec un préfixe de type (`[BUG] ...`), posent les labels de type et de version, assignent l'auteur et créent une branche `release/<version>/<type>/<titre>` si les cases correspondantes sont cochées. Aucun code applicatif : il suffit de copier le dossier `.github/` dans un autre dépôt.

## What it does

An issue created from the **Issue** form (`.github/ISSUE_TEMPLATE/issue.yml`) triggers four workflows on `opened` and `edited`:

| Workflow | Effect |
|---|---|
| `issue-title.yml` | Prefixes the title with the issue type, e.g. `[REFACTOR] ...` |
| `issue-labels.yml` | Creates the type label (red) and version label (blue) if missing, then sets exactly those two labels on the issue |
| `issue-assign.yml` | Assigns the author when "Assign to me directly" is checked |
| `issue-branch.yml` | When "Create branch automatically" is checked, creates `release/<version>/<type>/<slug>` and comments with checkout instructions |

Issues that do not come from the form are ignored. Blank issues are disabled (`config.yml`).

The form offers these types: `feature`, `bug`, `chore`, `docs`, `enhancement`, `refactor`, `test`, `perf`, `security`, plus a target version in the `vX.Y.Z` format.

## Use it in another repository

1. Copy the `.github/` folder into your repository.
2. Make sure Actions have write access: Settings → Actions → General → Workflow permissions → *Read and write permissions*.
3. Open a new issue and fill the form.

## Tests

The workflows have no automated tests; verify them by creating an issue from the form (see the open issues).

## What it demonstrates

- Event-driven automation with GitHub Actions and `actions/github-script`.
- Least-privilege `permissions` per workflow.
- Issue forms (YAML) and a branch naming convention tied to release versions.

## License

MIT, see [LICENSE](LICENSE).
