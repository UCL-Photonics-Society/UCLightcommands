# UCLightcommands

<div align="center">
  <img src="docs/resources/logos/logo_purple.png" alt="UCL Photonics Society" height="100">
  &nbsp;&nbsp;&nbsp;
  <img src="docs/resources/logos/thorlabs-logo.webp" alt="Thorlabs" height="65">
  &nbsp;&nbsp;&nbsp;
  <img src="docs/resources/logos/lightcommands_bottom_text.png" alt="LightCommands" height="100">
</div>

<br>

Repository for the UCL Photonics Society × Thorlabs UK LightCommands Hackathon.

The `docs/` folder contains an MkDocs site where participants document their work. It is published automatically to GitHub Pages on every merge to `main`:

**https://ucl-photonics-society.github.io/UCLightcommands/**

---

## Contributing

### Prerequisites

Before contributing, make sure you have:

- **[Git](https://git-scm.com/downloads)** installed and configured ([first-time setup guide](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)). Windows users should install [Git for Windows](https://gitforwindows.org/) to get Git Bash.
- **[VS Code](https://code.visualstudio.com/download)** or another editor with Markdown support ([VS Code Git integration guide](https://code.visualstudio.com/docs/sourcecontrol/overview)).
- A **[GitHub account](https://github.com/signup)** with Write access to this repository (ask the organiser).

See the [Prerequisites page](https://ucl-photonics-society.github.io/UCLightcommands/phase1/prerequisites/) on the hackathon site for detailed setup instructions.

### Protected branch

[`main` is a protected branch](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) — direct pushes are disabled. All changes must go through a [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) and require organiser approval before merging.

### Workflow

1. **[Create a branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-and-deleting-branches-within-your-repository)** on GitHub: open the branch dropdown, type your branch name (e.g. `phase1-task1-tx`), and click **Create branch from 'main'**.

2. **Fetch and checkout** your branch locally:
   ```bash
   git fetch origin
   git checkout phase1-task1-tx
   ```

3. **Edit** the relevant file in `docs/` and save.

4. **[Commit](https://github.com/git-guides/git-commit) and [push](https://github.com/git-guides/git-push)**:
   ```bash
   git add docs/phase1/tasks.md
   git commit -m "Add Tx answers for Phase 1 Task 1"
   git push
   ```

5. **Open a [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)** on GitHub from your branch into `main`. The organiser will review and merge it.

### If main has moved on since you branched

Bring your branch up to date with a [rebase](https://git-scm.com/docs/git-rebase) before pushing:

```bash
git fetch origin
git rebase origin/main
```

If there are [conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line), resolve them, then:

```bash
git add <resolved-file>
git rebase --continue
git push --force-with-lease
```

---

## Local development

The site is built with **[MkDocs](https://www.mkdocs.org/)** using the **[Material theme](https://squidfunk.github.io/mkdocs-material/)**. Dependencies are managed with **[uv](https://docs.astral.sh/uv/)**.

### Clone

[Clone the repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) to your local machine:

```bash
git clone https://github.com/UCL-Photonics-Society/UCLightcommands.git
cd UCLightcommands
```

### Setup

Install `uv` ([installation guide](https://docs.astral.sh/uv/getting-started/installation/)), then sync the project environment:

```bash
pip install uv
uv sync
```

### Preview

Serves the site locally with live reload at [http://127.0.0.1:8000](http://127.0.0.1:8000) ([MkDocs docs](https://www.mkdocs.org/getting-started/#creating-a-new-project)):

```bash
uv run mkdocs serve
```

### Build

Builds the static site into `site/` and fails on any warning ([`--strict` flag docs](https://www.mkdocs.org/user-guide/cli/#mkdocs-build)):

```bash
uv run mkdocs build --strict
```

---

## Contributors

<a href="https://github.com/UCL-Photonics-Society/UCLightcommands/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=UCL-Photonics-Society/UCLightcommands" />
</a>
