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

### Protected branch

`main` is a protected branch — direct pushes are disabled. All changes must go through a Pull Request and require organiser approval before merging.

### Workflow

1. **Create a branch** on GitHub: open the branch dropdown, type your branch name (e.g. `phase1-task1-tx`), and click **Create branch from 'main'**.

2. **Fetch and checkout** your branch locally:
   ```bash
   git fetch origin
   git checkout phase1-task1-tx
   ```

3. **Edit** the relevant file in `docs/` and save.

4. **Commit and push**:
   ```bash
   git add docs/phase1/tasks.md
   git commit -m "Add Tx answers for Phase 1 Task 1"
   git push
   ```

5. **Open a Pull Request** on GitHub from your branch into `main`. The organiser will review and merge it.

### If main has moved on since you branched

Bring your branch up to date before pushing:

```bash
git fetch origin
git rebase origin/main
```

If there are conflicts, resolve them, then:

```bash
git add <resolved-file>
git rebase --continue
git push --force-with-lease
```

---

## Local development

### Setup

```bash
pip install uv
uv sync
```

### Preview

```bash
uv run mkdocs serve
```

### Build

```bash
uv run mkdocs build --strict
```
