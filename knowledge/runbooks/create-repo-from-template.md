---
type: runbook
status: current
environment: shared
---

# Create a New Project Ops Repo From Template

One-command workflow for an AI agent: a user asks to create a project ops repo from `sven0219/ops-repo-template` and the agent does it end to end.

## Trigger Phrase (what the user says)

> Create a repo named `<project>-ops` from `sven0219/ops-repo-template` (private), and push it.

Or: "用 sven0219/ops-repo-template 给 xxx 项目创建一个 ops repo"

## Agent Steps

1. **Verify GitHub CLI and auth**
   ```bash
   gh auth status
   ```

2. **Create the repo from the template** (`-p` / `--template` copies the template files)
   ```bash
   gh repo create <owner>/<project>-ops --template sven0219/ops-repo-template --private
   ```
   - Use `--private` unless the user asks for `--public`.
   - If the user did not specify a repo name, derive one from the project name, e.g. `cybex` → `cybex-ops`.

3. **Clone locally**
   ```bash
   gh repo clone <owner>/<project>-ops
   ```

4. **Confirm the template content was copied** (files should include `AGENTS.md`, `worklog/`, `knowledge/`, `incidents/`, `.gitignore`)
   ```bash
   ls <project>-ops
   ```

5. **Customize the repo for the project** (as requested):
   - Update `README.md` title/description to the project.
   - Update `AGENTS.md` with the project name in the header.
   - Reset `worklog/` date example files; keep the structure.
   - If the user asked to link real infrastructure (clusters, accounts), add `knowledge/` entries for them.

6. **Commit and push**
   ```bash
   cd <project>-ops
   git add -A
   git status && git diff --cached
   git commit -m "feat: scaffold <project> ops repo from ops-repo-template"
   git push -u origin main
   ```

## Security Checks (mandatory)

- Never generate or commit real credentials, tokens, or connection strings in the scaffolded repo.
- Do not copy `.env`, kubeconfigs, or key material from the user's machine into the new repo.
- Before `git commit`, run `git diff --cached` and scan for secrets; if anything is found, stop and report.

## Post-Creation

- Report the repo URL to the user: `https://github.com/<owner>/<project>-ops`
- Remind the user that the repo inherits the template rules in `AGENTS.md` (worklog / knowledge / incidents / auto commit-push).