# ops-repo-template

A ready-to-use repository template for **troubleshooting, knowledge base and worklog records** for any project. Clone it (Use this template) and start recording — no setup required.

## Directory Structure

```
<repo>/
├── AGENTS.md            # Repository rules for agents and contributors
├── README.md            # Entry point / navigation
├── worklog/             # Daily troubleshooting stream, one file per date
│   └── YYYY-MM-DD.md
├── troubleshooting/     # Distilled troubleshooting cases with root cause
│   └── YYYY-MM-DD-<slug>.md
├── knowledge/           # Reusable knowledge: environment facts, runbooks, references
│   ├── _template.md     # Template for new knowledge entries
│   ├── runbooks/        # Executable operational procedures
│   └── reference/       # External links and lookup material
└── incidents/           # Major incident retrospectives
    └── YYYY-MM-DD-<slug>.md
```

## How To Use

1. Click **Use this template** on GitHub to create a new repository, or copy the files into your project.
2. Update this README to describe your project.
3. Start troubleshooting. Each investigation is recorded in `worklog/YYYY-MM-DD.md`.
4. Resolved cases are distilled into `troubleshooting/` write-ups with root cause.
5. Stable conclusions are distilled into `knowledge/` entries.
6. Major incidents get a full retrospective under `incidents/`.

### One-Command Setup (GitHub CLI)

Because this template is **public**, anyone can spin up a new project repo in one command:

```bash
# Create a private project repo from this template
gh repo create <project>-ops --template sven0219/ops-repo-template --private

# ...or a public one, and clone it locally right away
gh repo create <project>-ops --template sven0219/ops-repo-template --public --clone
```

Example:

```bash
gh repo create cybex-ops --template sven0219/ops-repo-template --private --clone
```

For an AI agent (e.g. opencode), the same intent works as a single instruction:

> Create a repo named `<project>-ops` from `sven0219/ops-repo-template` (private), and push it.

The agent will run the `gh repo create --template` flow automatically. A ready-to-follow procedure is documented in [knowledge/runbooks/create-repo-from-template.md](knowledge/runbooks/create-repo-from-template.md) — any agent or contributor can pick it up and execute it step by step.

## Rules

See [AGENTS.md](AGENTS.md). Core conventions:

1. Record every investigation into `worklog/YYYY-MM-DD.md` immediately after it completes.
2. Distill stable conclusions into `knowledge/` entries automatically.
3. Major incidents get a separate retrospective in `incidents/`.
4. Never commit secrets, tokens, passwords, or certificates.
5. Every change is committed and pushed automatically.