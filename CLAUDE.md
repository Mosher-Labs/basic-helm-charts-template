# Mosher Labs Basic Helm Charts Template - Project Memory

This file contains persistent context for Claude Code sessions on this project.
It will be automatically loaded at the start of every session.

## Project Overview

This is a template repository for creating new Helm chart projects. It provides
a standardized starting point with pre-configured tooling, workflows, and a
sample hello-world chart following Helm best practices.

**Key Details:**

- **Purpose:** Template for Helm chart repositories
- **CI/CD:** GitHub Actions with release workflow
- **Linting:** helm lint, yamllint, pre-commit hooks
- **Pattern:** Fork or use as template, then customize

## Repository Structure

```text
basic-helm-charts-template/
├── .github/workflows/     # CI/CD workflows
│   └── release.yml        # Semantic versioning & releases
├── charts/                # Helm charts
│   └── hello-world/       # Example chart
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
├── .pre-commit-config.yaml
├── .helmignore
├── README.md
└── CLAUDE.md
```

## Using This Template

### Creating a New Helm Chart Repo

1. **Use as template:** Click "Use this template" on GitHub
1. **Clone locally:** `git clone <your-new-repo>`
1. **Update README.md:** Replace template content with project description
1. **Customize hello-world chart:** Rename and modify for your application
1. **Test locally:** `helm lint charts/your-chart`
1. **Install pre-commit:** `pre-commit install`
1. **Create project CLAUDE.md:** Document chart-specific context

### Pre-configured Features

- **Release workflow:** Automatic semantic versioning
- **Pre-commit hooks:** helm lint, yamllint, markdown, commit messages
- **Example chart:** hello-world chart demonstrating best practices
- **Helm ignore:** Proper `.helmignore` file

## Helm Best Practices

### Chart Structure

- Use semantic versioning (major.minor.patch)
- Document all values with comments in `values.yaml`
- Include resource limits/requests
- Add labels: app.kubernetes.io/name, app.kubernetes.io/instance
- Use `_helpers.tpl` for common template functions

### Testing Charts

```bash
# Lint the chart
helm lint charts/your-chart

# Dry-run to see generated YAML
helm install --dry-run --debug my-release charts/your-chart

# Template with custom values
helm template my-release charts/your-chart -f custom-values.yaml

# Install to cluster
helm upgrade --install my-release charts/your-chart
```

## Git Workflow

1. **Create feature branch:** `git checkout -b feature/description`
1. **Make changes** to charts, templates, or documentation
1. **ALWAYS run pre-commit BEFORE committing:** `pre-commit run --all-files`
   - Fix ALL errors (especially helm lint, yamllint, and markdown)
   - Do NOT commit with `--no-verify` unless absolutely necessary
1. **Commit with conventional format:** `git commit -m "type: description"`
1. **Push and create PR:** `gh pr create --title "feat: description"`
1. **Test changes:** If your changes reference shared workflows that were also updated,
   temporarily change the reference from `@main` to `@your-branch` to test, verify
   the PR passes, then change back to `@main` before merging
1. **Merge to main:** Automatic release created based on commits

**Commit Format:** Conventional Commits (enforced by pre-commit hook)

- `feat:` - New feature or chart
- `fix:` - Bug fix
- `docs:` - Documentation changes
- `chore:` - Maintenance
- `refactor:` - Code refactoring
- `test:` - Temporary test changes (like branch references)

## Pre-commit Hooks

**Installed hooks:**

- Helm lint (chart validation)
- YAML linting (yamllint)
- Markdown linting (markdownlint)
- Conventional commit format
- File hygiene (trailing whitespace, EOF, etc.)

**Setup:**

```bash
pre-commit install              # One-time setup
pre-commit run --all-files      # Run manually
pre-commit autoupdate           # Update hook versions
```

## Important Notes

### Code Quality Standards

**CRITICAL:** All code must adhere to linter rules from the start. Do NOT write
code that needs fixing after running pre-commit hooks.

**Markdown (markdownlint):**

Configuration: `.markdownlint.yaml` (allows 2-space indent, 120 char lines)

- Nested lists under unordered items: Use 2-space indentation
- Nested lists under ordered items: Use 2-space indentation
- Inline format for simple nested items: `**Item:** Detail 1, Detail 2`
- Line length: 120 characters max (code/tables excluded)
- Bare URLs: Allowed in reference sections
- Bold for emphasis: Allowed in lists

**YAML (yamllint):**

- Maximum line length: 80 characters
- Use 2-space indentation
- No trailing whitespace
- Proper quoting for strings containing special characters

**Helm (helm lint):**

- Valid Chart.yaml with proper semantic version
- All values used in templates must be defined in values.yaml
- Proper indentation in templates (2 spaces)
- No hardcoded values (use values.yaml or _helpers.tpl)
- Include resource limits and requests

### When Working on This Repo

1. **Write linter-compliant code from the start** - Don't fix after the fact
1. **Test charts locally** before committing
1. **Run pre-commit hooks** BEFORE committing (fix all errors!)
1. **Use helm lint** to validate charts
1. **Document values** with comments in values.yaml
1. **Test shared workflow changes** - Use branch references before merging

## References

- @README.md - Repository overview
- Shared Workflows: <https://github.com/Mosher-Labs/.github>
- Helm Docs: <https://helm.sh/docs/>
- Helm Best Practices: <https://helm.sh/docs/chart_best_practices/>

---

**Last Updated:** 2025-11-18

This file should be updated whenever:

- Project patterns change
- Important Helm context is discovered
- Charts are added or modified
