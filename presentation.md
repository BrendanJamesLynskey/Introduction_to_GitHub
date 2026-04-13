# Introduction to GitHub

**Git Hosting, Collaboration & Automation**

*From repositories and pull requests to CI/CD pipelines and the GitHub CLI*

```
Repo -> Branch -> PR -> Review -> Merge -> Deploy
```

Code  |  Collaborate  |  Automate  |  Ship

---

## Table of Contents

1. [Topics](#slide-01--topics)
2. [What Is GitHub?](#slide-02--what-is-github)
3. [Repositories & the GitHub Interface](#slide-03--repositories--the-github-interface)
4. [Markdown on GitHub](#slide-04--markdown-on-github)
5. [Branching & Pull Requests](#slide-05--branching--pull-requests)
6. [Code Review on GitHub](#slide-06--code-review-on-github)
7. [GitHub Issues & Projects](#slide-07--github-issues--projects)
8. [GitHub Actions — Foundations](#slide-08--github-actions--foundations)
9. [GitHub Actions — Workflow Syntax](#slide-09--github-actions--workflow-syntax)
10. [GitHub Actions — Advanced Patterns](#slide-10--github-actions--advanced-patterns)
11. [GitHub CLI (gh)](#slide-11--github-cli-gh)
12. [GitHub CLI — Workflow Examples](#slide-12--github-cli--workflow-examples)
13. [GitHub Pages & Releases](#slide-13--github-pages--releases)
14. [GitHub Packages & Container Registry](#slide-14--github-packages--container-registry)
15. [GitHub Security Features](#slide-15--github-security-features)
16. [GitHub Copilot & AI Features](#slide-16--github-copilot--ai-features)
17. [GitLab — Platform Overview](#slide-17--gitlab--platform-overview)
18. [GitLab CI/CD](#slide-18--gitlab-cicd)
19. [GitHub vs GitLab — Detailed Comparison](#slide-19--github-vs-gitlab--detailed-comparison)
20. [Other Git Platforms](#slide-20--other-git-platforms)
21. [Summary & Next Steps](#slide-21--summary--next-steps)

---

## Slide 01 — Topics

### Foundations

- What GitHub is and why it matters
- Repositories, branches, and pull requests
- Markdown for docs, READMEs, and wikis
- Code review workflows

### Automation & Tooling

- GitHub Actions — workflows, jobs, and steps
- GitHub CLI (`gh`) for terminal-driven workflows
- GitHub Pages, Releases, and Packages

### Security & AI

- Dependabot, code scanning, secret scanning
- GitHub Copilot and AI-assisted development

### GitLab & Alternatives

- GitLab platform and CI/CD
- GitHub vs GitLab — feature-by-feature comparison
- Bitbucket, Gitea, and self-hosted options

---

## Slide 02 — What Is GitHub?

GitHub is the world's largest **source code hosting platform**, built on top of Git. It adds collaboration, code review, project management, CI/CD, and security tooling around Git's distributed version control.

### Key facts

- Founded 2008, acquired by Microsoft in 2018 for $7.5 billion
- 100+ million developers, 420+ million repositories (2024)
- Free for public and private repos (with limits on Actions minutes)
- Available as SaaS (github.com) or self-hosted (GitHub Enterprise Server)

### What GitHub adds to Git

Git is a distributed version control system — it tracks changes, branches, and merges. GitHub layers on:

- **Pull requests** — structured code review before merging
- **Issues & Projects** — lightweight project management
- **Actions** — CI/CD pipelines defined as YAML
- **Packages** — host npm, Docker, Maven, NuGet packages
- **Security** — dependency scanning, secret detection, code analysis
- **Pages** — free static site hosting from a repo
- **Copilot** — AI pair programming in the editor

GitHub is not Git. You can use Git without GitHub, and GitHub without the command line (though you shouldn't).

---

## Slide 03 — Repositories & the GitHub Interface

A **repository** (repo) is a project — source code, history, branches, issues, and settings in one place.

### Anatomy of a GitHub repo

- **Code tab** — file browser, branch selector, commit history
- **Issues tab** — bug reports, feature requests, discussions
- **Pull requests tab** — proposed changes awaiting review
- **Actions tab** — CI/CD workflow runs
- **Settings** — branch protection, secrets, webhooks, collaborators

### Key files

| File | Purpose |
|------|---------|
| `README.md` | Project overview — rendered on the repo homepage |
| `LICENSE` | Legal terms for using the code |
| `.gitignore` | Patterns for files Git should not track |
| `CONTRIBUTING.md` | Guidelines for contributors |
| `CODEOWNERS` | Auto-assign reviewers based on file paths |
| `.github/` | Directory for Actions workflows, issue templates, PR templates |

### Visibility

- **Public** — anyone can see and fork; free
- **Private** — only invited collaborators; free (with limits)
- **Internal** — visible to all org members (Enterprise only)

---

## Slide 04 — Markdown on GitHub

GitHub uses **GitHub Flavoured Markdown (GFM)** — standard Markdown extended with tables, task lists, syntax-highlighted code blocks, and auto-linked references.

### Essential syntax

```markdown
# Heading 1
## Heading 2
### Heading 3

**bold** and *italic* and `inline code`

- bullet list
- [ ] task list (unchecked)
- [x] task list (checked)

[Link text](https://example.com)
![Alt text](image.png)

> Blockquote

| Column A | Column B |
|----------|----------|
| cell     | cell     |
```

### Code blocks with syntax highlighting

````markdown
```python
def hello(name: str) -> str:
    return f"Hello, {name}!"
```
````

GitHub detects the language and applies highlighting. Supported languages include Python, JavaScript, TypeScript, Go, Rust, YAML, Bash, SQL, and hundreds more.

### GitHub-specific extensions

- `#123` — auto-links to issue or PR number 123
- `@username` — mentions a user (sends notification)
- `:emoji_name:` — renders emoji (e.g. `:rocket:` → 🚀)
- `<details><summary>Toggle</summary>Hidden content</details>` — collapsible sections
- Mermaid diagrams in fenced code blocks (```mermaid)

### Where Markdown is used

READMEs, issues, PRs, comments, wikis, GitHub Pages, release notes, discussion posts, and profile READMEs (`username/username` repo).

---

## Slide 05 — Branching & Pull Requests

A **pull request** (PR) is GitHub's mechanism for proposing, reviewing, and merging changes. It is the central unit of collaboration.

### The PR workflow

```
1. Create a branch from main
2. Make commits on the branch
3. Open a pull request
4. Automated checks run (CI)
5. Reviewers comment and approve
6. Merge the PR into main
7. Delete the branch
```

### Branch protection rules

Protect `main` by requiring:

- At least one (or two) approving reviews
- All CI status checks to pass
- No force pushes or deletions
- Linear history (squash or rebase merges only)
- Signed commits
- Up-to-date branch before merging

### Merge strategies

| Strategy | Result | When to use |
|----------|--------|-------------|
| **Merge commit** | Preserves all branch commits + creates a merge commit | When full commit history matters |
| **Squash and merge** | Combines all branch commits into one commit on main | Default for most teams — clean history |
| **Rebase and merge** | Replays branch commits onto main without a merge commit | Linear history purists |

### Draft pull requests

Open a PR as **Draft** to signal work-in-progress. CI still runs, but reviewers know it is not ready. Convert to "Ready for review" when done.

---

## Slide 06 — Code Review on GitHub

Code review is the highest-leverage quality practice a team can adopt. GitHub's review tools make it structured and asynchronous.

### Review actions

- **Comment** — feedback without explicit approval or rejection
- **Approve** — "this is good to merge"
- **Request changes** — "fix these issues before merging"

### Inline comments

Click any line in the diff to leave a comment. Use **suggestions** to propose exact code changes that the author can accept with one click:

````markdown
```suggestion
const result = items.filter(Boolean);
```
````

### Review best practices

- Review within 24 hours — blocked PRs kill velocity
- Focus on correctness, security, and maintainability — not style (use linters for that)
- Explain *why*, not just *what* — "this could deadlock under concurrent access because…"
- Keep PRs small (< 400 lines) — large PRs get rubber-stamped
- Use CODEOWNERS to auto-assign domain experts

### CODEOWNERS file

```
# .github/CODEOWNERS
*.js        @frontend-team
*.py        @backend-team
docs/       @tech-writers
*.tf        @infra-team
```

When a PR modifies matching files, the listed team is automatically requested as reviewer.

---

## Slide 07 — GitHub Issues & Projects

**Issues** are GitHub's built-in issue tracker. **Projects** (v2) add Kanban boards, tables, and custom fields for project management.

### Issues

- Title, description (Markdown), labels, assignees, milestone
- Templates: `.github/ISSUE_TEMPLATE/bug_report.md` or YAML forms
- Close issues automatically from PRs: `Fixes #42` in the PR description
- Pin up to 3 issues to the top of the Issues tab
- Transfer issues between repos in the same org

### Labels

Use labels to categorise: `bug`, `enhancement`, `documentation`, `good first issue`, `priority:high`. Consistent labelling enables filtering and triage.

### Milestones

Group issues into milestones with a due date and progress bar. Useful for release planning.

### GitHub Projects (v2)

- **Board view** — Kanban columns (To Do, In Progress, Done)
- **Table view** — spreadsheet-style with custom fields (priority, estimate, sprint)
- **Roadmap view** — timeline with date ranges
- **Automation** — auto-move items when PRs are merged, issues are closed, etc.
- Scoped to an organisation or a user — can span multiple repos

### Issue forms (YAML)

```yaml
# .github/ISSUE_TEMPLATE/bug_report.yml
name: Bug Report
description: Report a bug
body:
  - type: input
    id: version
    attributes:
      label: Version
    validations:
      required: true
  - type: textarea
    id: steps
    attributes:
      label: Steps to reproduce
```

---

## Slide 08 — GitHub Actions — Foundations

**GitHub Actions** is GitHub's built-in CI/CD and automation platform. Workflows are YAML files in `.github/workflows/`.

### Core concepts

| Concept | Description |
|---------|-------------|
| **Workflow** | A YAML file defining an automated process |
| **Event / Trigger** | What starts the workflow (`push`, `pull_request`, `schedule`, `workflow_dispatch`) |
| **Job** | A set of steps that run on a single runner |
| **Step** | A single task — a shell command or a reusable Action |
| **Runner** | The VM or container executing the job |
| **Action** | A reusable, packaged step from the Marketplace or your own repo |

### Trigger examples

```yaml
on:
  push:
    branches: [main]
  pull_request:
  schedule:
    - cron: '0 6 * * 1'      # every Monday at 06:00 UTC
  workflow_dispatch:           # manual trigger from the UI
  release:
    types: [published]
```

### Runner options

- **GitHub-hosted** — `ubuntu-latest`, `windows-latest`, `macos-latest`. Pre-installed tools. Ephemeral (fresh VM every run).
- **Self-hosted** — your own machines. Needed for GPU workloads, on-prem access, or cost control at scale.
- **Larger runners** — GitHub-managed runners with more CPU/RAM (paid).

### Free tier (public repos)

Unlimited Actions minutes for public repositories. Private repos get 2,000 minutes/month on the Free plan.

---

## Slide 09 — GitHub Actions — Workflow Syntax

### Complete workflow example

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:

permissions:
  contents: read

jobs:
  lint-and-test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [18, 20, 22]
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Lint
        run: npm run lint

      - name: Test
        run: npm test -- --coverage

      - name: Upload coverage
        if: matrix.node-version == 22
        uses: actions/upload-artifact@v4
        with:
          name: coverage-report
          path: coverage/

  build:
    needs: lint-and-test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: 'npm'
      - run: npm ci
      - run: npm run build
      - uses: actions/upload-artifact@v4
        with:
          name: dist
          path: dist/
```

### Key syntax elements

- `needs:` — declare job dependencies (otherwise jobs run in parallel)
- `strategy.matrix` — run the same job across multiple configurations
- `if:` — conditionally run a step or job
- `env:` — set environment variables at workflow, job, or step level
- `secrets.*` — access encrypted secrets stored in repo settings
- `${{ github.sha }}` — expression context for git SHA, branch, actor, etc.

---

## Slide 10 — GitHub Actions — Advanced Patterns

### Reusable workflows

Define a workflow in one repo, call it from others. DRY for organisation-wide CI standards.

```yaml
# In the calling workflow
jobs:
  deploy:
    uses: my-org/shared-workflows/.github/workflows/deploy.yml@main
    with:
      environment: production
    secrets: inherit
```

### Composite Actions

Bundle multiple steps into a single reusable Action with its own `action.yml`.

### Caching

```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: npm-${{ hashFiles('**/package-lock.json') }}
    restore-keys: npm-
```

Cache dependencies to avoid re-downloading on every run. Key on the lockfile hash for automatic invalidation.

### Concurrency control

```yaml
concurrency:
  group: deploy-${{ github.ref }}
  cancel-in-progress: true
```

Prevents duplicate runs — if a new commit arrives while CI is running, cancel the old run.

### Environment protection rules

- Define environments (`staging`, `production`) in repo settings
- Require manual approval before deploying to production
- Limit which branches can deploy to an environment
- Add wait timers between deployments

### Secrets and OIDC

- Store secrets in repo or org settings — never in YAML
- Use OIDC federation with AWS, GCP, Azure — no long-lived credentials
- Pin third-party Actions to full SHA, not tags

---

## Slide 11 — GitHub CLI (gh)

The **GitHub CLI** (`gh`) brings GitHub to the terminal. It replaces switching to the browser for PRs, issues, Actions, and more.

### Installation

```bash
# macOS
brew install gh

# Ubuntu / Debian
sudo apt install gh

# Windows
winget install GitHub.cli
```

### Authentication

```bash
gh auth login          # interactive — browser or token
gh auth status         # check current auth
gh auth switch         # switch between accounts
```

### Repository operations

```bash
gh repo create my-app --public --clone
gh repo clone owner/repo
gh repo fork owner/repo --clone
gh repo view owner/repo --web     # open in browser
gh repo list my-org --limit 50
```

### Pull request operations

```bash
gh pr create --title "Add feature" --body "Description"
gh pr list --state open
gh pr view 42
gh pr checkout 42        # fetch and switch to PR branch
gh pr review 42 --approve
gh pr merge 42 --squash --delete-branch
gh pr diff 42
gh pr checks 42          # view CI status
```

### Issue operations

```bash
gh issue create --title "Bug" --label bug
gh issue list --assignee @me
gh issue view 99
gh issue close 99 --reason completed
gh issue edit 99 --add-label priority:high
```

---

## Slide 12 — GitHub CLI — Workflow Examples

### Actions from the terminal

```bash
gh run list                         # list recent workflow runs
gh run view 123456                  # details of a specific run
gh run watch 123456                 # live-stream a running workflow
gh run rerun 123456                 # re-trigger a failed run
gh workflow list                    # list all workflows
gh workflow run deploy.yml          # trigger a workflow_dispatch
gh workflow run deploy.yml -f env=staging
```

### GitHub API via `gh api`

```bash
# Get repo info
gh api repos/owner/repo

# List PR comments
gh api repos/owner/repo/pulls/42/comments

# Create a label
gh api repos/owner/repo/labels \
  -f name="priority:critical" \
  -f color="d73a4a"

# Pagination
gh api repos/owner/repo/issues --paginate
```

`gh api` handles authentication, pagination, and JSON output. Pipe to `jq` for filtering.

### Aliases and extensions

```bash
# Create a custom alias
gh alias set prs 'pr list --state open --assignee @me'
gh prs    # now works

# Install community extensions
gh extension install dlvhdr/gh-dash     # terminal dashboard
gh extension install github/gh-copilot  # Copilot in the CLI
```

### Scripting with `gh`

```bash
# Close all issues with a specific label
gh issue list --label "wontfix" --json number --jq '.[].number' \
  | xargs -I {} gh issue close {}

# Create PRs across multiple repos
for repo in app-api app-web app-worker; do
  gh pr create --repo "my-org/$repo" \
    --title "Bump dependency" --body "Automated update"
done
```

---

## Slide 13 — GitHub Pages & Releases

### GitHub Pages

Free static site hosting directly from a repository.

- Serve from `main` branch, `gh-pages` branch, or `/docs` folder
- Custom domains with HTTPS (free Let's Encrypt certificate)
- Built-in Jekyll support, or deploy any static site via Actions
- URL: `username.github.io/repo-name`

```yaml
# .github/workflows/pages.yml — deploy with Actions
name: Deploy to Pages
on:
  push:
    branches: [main]
permissions:
  pages: write
  id-token: write
jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: './dist'
      - id: deployment
        uses: actions/deploy-pages@v4
```

### Releases

- Tag a commit with a version (`v1.2.0`)
- Attach compiled binaries, installers, or archives
- Auto-generate release notes from merged PRs
- Mark as pre-release or latest

```bash
# Create a release with the CLI
gh release create v1.2.0 \
  --title "v1.2.0" \
  --generate-notes \
  ./dist/app-linux ./dist/app-macos ./dist/app-windows.exe
```

---

## Slide 14 — GitHub Packages & Container Registry

**GitHub Packages** is a package registry integrated with GitHub. Host packages alongside your source code with unified permissions.

### Supported registries

| Registry | Package type | URL |
|----------|-------------|-----|
| **Container** (GHCR) | Docker / OCI images | `ghcr.io/owner/image` |
| **npm** | Node.js packages | `npm.pkg.github.com` |
| **Maven** | Java / Kotlin | `maven.pkg.github.com` |
| **NuGet** | .NET | `nuget.pkg.github.com` |
| **RubyGems** | Ruby | `rubygems.pkg.github.com` |

### Publishing a Docker image

```yaml
# In a GitHub Actions workflow
- name: Log in to GHCR
  uses: docker/login-action@v3
  with:
    registry: ghcr.io
    username: ${{ github.actor }}
    password: ${{ secrets.GITHUB_TOKEN }}

- name: Build and push
  uses: docker/build-push-action@v5
  with:
    push: true
    tags: ghcr.io/${{ github.repository }}:${{ github.sha }}
```

### Visibility and access

- Packages inherit repo visibility by default
- Public packages are free; private packages count toward storage quota
- Fine-grained permissions — grant read/write per package
- `GITHUB_TOKEN` provides automatic authentication in Actions

---

## Slide 15 — GitHub Security Features

GitHub provides multiple layers of **supply chain and code security** — most are free for public repos and included in GitHub Advanced Security for private repos.

### Dependabot

- **Alerts** — notifies when dependencies have known CVEs
- **Security updates** — auto-opens PRs to bump vulnerable dependencies
- **Version updates** — keeps dependencies fresh on a schedule

```yaml
# .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: "npm"
    directory: "/"
    schedule:
      interval: "weekly"
    open-pull-requests-limit: 10
```

### Code scanning (CodeQL)

GitHub's static analysis engine. Finds security vulnerabilities (SQL injection, XSS, command injection, etc.) by analysing data flow through your code.

```yaml
# Enable via Actions
- uses: github/codeql-action/init@v3
  with:
    languages: javascript, python
- uses: github/codeql-action/analyze@v3
```

### Secret scanning

Automatically detects committed secrets — API keys, tokens, passwords. Over 200 partner patterns (AWS, Stripe, Slack, etc.). Push protection can **block the push** before the secret reaches the remote.

### Security advisories

- Private vulnerability reporting — external reporters submit vulnerabilities without public disclosure
- Create advisories with CVE IDs
- Coordinate patches before public announcement

---

## Slide 16 — GitHub Copilot & AI Features

**GitHub Copilot** is an AI pair programmer powered by large language models. It integrates into editors and the CLI to suggest code, explain code, and generate tests.

### Copilot products

| Product | Description |
|---------|-------------|
| **Copilot Individual** | AI completions in VS Code, JetBrains, Neovim |
| **Copilot Business** | Organisation-managed, policy controls, audit logs |
| **Copilot Enterprise** | Fine-tuned on your codebase, knowledge bases, Bing search |
| **Copilot Chat** | Conversational AI in the editor and on github.com |
| **Copilot CLI** | Explain and suggest terminal commands |
| **Copilot in PRs** | Auto-generated PR summaries and review comments |

### Copilot Chat in the editor

- Explain selected code: "What does this function do?"
- Generate tests: "/tests for this function"
- Fix errors: "/fix this error"
- Refactor: "Rewrite this using async/await"
- Workspace-aware: understands project context

### Copilot in the CLI

```bash
gh copilot explain "awk '{print $2}' file.txt"
gh copilot suggest "find all .log files older than 30 days"
```

### Other AI features on GitHub

- **Copilot Autofix** — suggests fixes for code scanning alerts
- **Copilot for PRs** — generates PR descriptions and review summaries
- **Copilot Workspace** — plan and implement changes from an issue (preview)

---

## Slide 17 — GitLab — Platform Overview

**GitLab** is an all-in-one DevSecOps platform. Where GitHub is a code host with bolted-on features, GitLab was designed as a **single application** covering the entire software development lifecycle.

### GitLab editions

| Edition | Hosting | Cost |
|---------|---------|------|
| **Community Edition (CE)** | Self-hosted only | Free, open-source (MIT) |
| **Enterprise Edition (EE)** | Self-hosted | Paid tiers (Premium, Ultimate) |
| **GitLab.com** | SaaS | Free tier + paid plans |

### GitLab's "single application" philosophy

GitLab bundles features that GitHub requires third-party tools or marketplace Actions for:

- **Built-in CI/CD** — `.gitlab-ci.yml`, no marketplace needed
- **Built-in container registry** — every project gets one
- **Built-in package registry** — npm, Maven, PyPI, NuGet, etc.
- **Built-in wiki** — per-project, Git-backed
- **Built-in SAST/DAST/SCA** — security scanning in the pipeline
- **Built-in infrastructure management** — Terraform state, Kubernetes agent
- **Review apps** — deploy a live preview for every merge request

### Key terminology differences

| GitHub | GitLab |
|--------|--------|
| Repository | Project |
| Pull request | Merge request (MR) |
| GitHub Actions | GitLab CI/CD |
| Organisation | Group |
| GitHub Pages | GitLab Pages |
| CODEOWNERS | CODEOWNERS (same concept) |
| Gist | Snippet |

---

## Slide 18 — GitLab CI/CD

GitLab CI/CD is configured via a single `.gitlab-ci.yml` file in the repo root. No marketplace — pipelines are built from shell commands and Docker images.

### Example pipeline

```yaml
# .gitlab-ci.yml
stages:
  - build
  - test
  - deploy

variables:
  NODE_ENV: production

build:
  stage: build
  image: node:22-alpine
  script:
    - npm ci
    - npm run build
  artifacts:
    paths:
      - dist/
    expire_in: 1 week

test:
  stage: test
  image: node:22-alpine
  script:
    - npm ci
    - npm test -- --coverage
  coverage: '/Statements\s*:\s*(\d+\.?\d*)%/'

deploy_staging:
  stage: deploy
  environment:
    name: staging
    url: https://staging.example.com
  script:
    - ./deploy.sh staging
  only:
    - main

deploy_production:
  stage: deploy
  environment:
    name: production
    url: https://example.com
  script:
    - ./deploy.sh production
  when: manual
  only:
    - tags
```

### GitLab CI vs GitHub Actions

| Aspect | GitLab CI | GitHub Actions |
|--------|-----------|----------------|
| Config location | `.gitlab-ci.yml` (single file) | `.github/workflows/*.yml` (multiple files) |
| Reusability | `include:` templates, `extends:` | Reusable workflows, composite Actions, Marketplace |
| Runners | Self-hosted or shared (GitLab.com) | GitHub-hosted, self-hosted, or larger runners |
| Container registry | Built-in, one per project | GHCR (separate service) |
| Environments | First-class with review apps | Environments with protection rules |
| DAG pipelines | `needs:` keyword for directed acyclic graph | `needs:` keyword (similar) |
| Auto DevOps | Automatic CI/CD with zero config | No equivalent |
| Parent-child pipelines | Native support | Reusable workflows (similar) |

### GitLab-unique features

- **Auto DevOps** — zero-config pipeline that builds, tests, scans, and deploys
- **Review apps** — automatically deploy every MR to a temporary environment
- **Multi-project pipelines** — trigger pipelines across multiple projects
- **Merge trains** — queue MRs and test them in sequence to prevent broken main

---

## Slide 19 — GitHub vs GitLab — Detailed Comparison

### Philosophy

- **GitHub** — best-of-breed code hosting with a rich ecosystem of integrations and Marketplace Actions
- **GitLab** — single-application platform aiming to replace your entire DevOps toolchain

### Feature comparison

| Feature | GitHub | GitLab |
|---------|--------|--------|
| **Source code hosting** | Excellent | Excellent |
| **Pull / Merge requests** | Pull requests | Merge requests — largely equivalent |
| **CI/CD** | GitHub Actions (YAML, Marketplace) | Built-in CI/CD (YAML, templates) |
| **Package registry** | GitHub Packages (npm, Docker, Maven, etc.) | Built-in (npm, PyPI, Maven, Docker, etc.) |
| **Container registry** | GHCR (`ghcr.io`) | Built-in (one per project) |
| **Static analysis** | CodeQL (GitHub Advanced Security) | Built-in SAST, DAST, SCA, fuzzing |
| **Secret scanning** | Built-in with push protection | Built-in secret detection |
| **Dependency scanning** | Dependabot | Built-in dependency scanning |
| **Wiki** | GitHub Wiki (Git-backed) | GitLab Wiki (Git-backed) |
| **Project management** | Issues + Projects (v2) | Issues + Boards + Epics + Roadmaps |
| **Pages** | GitHub Pages | GitLab Pages |
| **Self-hosted** | GitHub Enterprise Server (paid) | GitLab CE (free) or EE (paid) |
| **AI features** | Copilot (paid) | Duo (paid) |
| **Marketplace / ecosystem** | Huge — 20,000+ Actions | Smaller — template-based |
| **Community size** | 100M+ developers | Smaller but significant |

### When to choose GitHub

- Open-source projects — largest community, discoverability, and contributor base
- Teams already using the GitHub ecosystem (Actions, Copilot, GHCR)
- Projects that benefit from the Marketplace and third-party integrations
- When Copilot and AI-assisted development are priorities

### When to choose GitLab

- Organisations wanting a single platform for the entire DevOps lifecycle
- Self-hosted requirement with a free option (GitLab CE)
- Teams needing built-in security scanning without additional licensing
- Regulated industries requiring comprehensive audit trails and compliance
- When review apps and Auto DevOps are valuable

---

## Slide 20 — Other Git Platforms

### Bitbucket (Atlassian)

- Tight integration with Jira and Confluence
- Bitbucket Pipelines for CI/CD
- Free for up to 5 users on private repos
- Best for teams already invested in the Atlassian ecosystem

### Gitea

- Lightweight, self-hosted Git server written in Go
- Single binary — runs on minimal hardware (Raspberry Pi)
- GitHub-like interface, MIT-licensed
- No built-in CI/CD — pair with Woodpecker CI or Drone

### Forgejo

- Community fork of Gitea (post-governance dispute)
- Identical feature set, different governance model
- Backed by Codeberg (non-profit hosting)

### Azure DevOps

- Microsoft's enterprise DevOps platform
- Azure Repos (Git hosting) + Azure Pipelines (CI/CD)
- Deep Azure cloud integration
- Being succeeded by GitHub for many Microsoft-ecosystem teams

### Comparison summary

| Platform | Best for | CI/CD | Self-host | Free tier |
|----------|----------|-------|-----------|-----------|
| **GitHub** | Open source, community | Actions | Enterprise (paid) | Generous |
| **GitLab** | Full DevOps lifecycle | Built-in | CE (free) | Generous |
| **Bitbucket** | Atlassian shops | Pipelines | Data Center (paid) | 5 users |
| **Gitea** | Lightweight self-host | External | Yes (free) | N/A |
| **Azure DevOps** | Azure-heavy enterprises | Pipelines | Server (paid) | 5 users |

---

## Slide 21 — Summary & Next Steps

### What we covered

- GitHub as a platform — repos, branches, pull requests, and code review
- Markdown on GitHub — formatting, GFM extensions, and where it is used
- Issues and Projects — lightweight project management
- GitHub Actions — workflows, syntax, advanced patterns
- GitHub CLI — terminal-driven GitHub workflows with `gh`
- Pages, Releases, and Packages — hosting and distribution
- Security — Dependabot, CodeQL, secret scanning
- Copilot — AI-assisted development
- GitLab — platform overview, CI/CD, and unique features
- GitHub vs GitLab — when to choose each

### Recommended next steps

1. Set up `gh` CLI and authenticate — replace browser-based GitHub workflows
2. Add branch protection rules to your main branch
3. Create a `.github/workflows/ci.yml` for your next project
4. Configure Dependabot for automated dependency updates
5. Try GitHub Projects (v2) for your next sprint or milestone
6. If evaluating platforms, spin up a GitLab CE instance and compare workflows

### Further reading

- GitHub Docs — docs.github.com
- GitHub CLI Manual — cli.github.com/manual
- GitHub Skills — skills.github.com (interactive courses)
- GitLab Docs — docs.gitlab.com
- GitLab CI/CD Tutorial — docs.gitlab.com/ee/ci/quick_start
- Pro Git (2nd ed.) — git-scm.com/book (free)
