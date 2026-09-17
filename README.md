# ops-repo-template

A ready-to-use repository template for **troubleshooting, knowledge base and worklog records** for any project. Clone it (Use this template) and start recording — no setup required.

## Directory Structure

```
<repo>/
├── AGENTS.md            # Repository rules for agents and contributors
├── README.md            # Entry point / navigation
├── worklog/             # Daily troubleshooting stream, one file per date
│   └── YYYY-MM-DD.md
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
4. Stable conclusions are distilled into `knowledge/` entries.
5. Major incidents get a full retrospective under `incidents/`.

## Rules

See [AGENTS.md](AGENTS.md). Core conventions:

1. Record every investigation into `worklog/YYYY-MM-DD.md` immediately after it completes.
2. Distill stable conclusions into `knowledge/` entries automatically.
3. Major incidents get a separate retrospective in `incidents/`.
4. Never commit secrets, tokens, passwords, or certificates.
5. Every change is committed and pushed automatically.