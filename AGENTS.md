# Repository Rules

This repository is a **troubleshooting, knowledge base and worklog** repository for the <PROJECT> project. Keep it safe, traceable, and easy to navigate.

## Directory Structure

```
<repo>/
├── AGENTS.md            # This rules file
├── README.md            # Entry point navigation
├── worklog/             # Daily troubleshooting stream, by date
│   └── YYYY-MM-DD.md
├── knowledge/           # Reusable knowledge: environment facts, access, runbooks, references
│   ├── _template.md     # Template for new entries
│   ├── runbooks/        # Executable operational procedures
│   └── reference/       # External links and resource lists
└── incidents/           # Major incident retrospectives
    └── YYYY-MM-DD-<slug>.md
```

## Worklog Rules

1. Worklog is organized by date, file name `worklog/YYYY-MM-DD.md`.
2. All issues on the same day are appended to that day's file in chronological order; create the file if it does not exist.
3. Write an entry **immediately** after finishing each investigation, not at the end of the task.
4. Each entry must include at least: time, problem, investigation steps, root cause, resolution, follow-up (optional).
5. Separate entries with `## <Title>` headings.
6. Distill stable conclusions into `knowledge/` entries within the same task; the worklog keeps the raw process.

## Knowledge Rules

1. After each investigation produces a stable conclusion, **automatically** evaluate whether it should be distilled into a knowledge entry, and do it immediately if needed.
2. Copy `knowledge/_template.md` for new entries and fill in the YAML frontmatter (type / status / environment).
3. Put changing environment facts (clusters, accounts, endpoints) in `knowledge/`, not in this file.
4. Put executable operational steps in `knowledge/runbooks/`; put external links in `knowledge/reference/`.
5. Entries link back to the corresponding worklog record via relative Markdown links.
6. Entries marked `UNVERIFIED` are drafts and do not represent verified state.

## Incidents Rules

1. Major incidents (affecting production/customers) get a standalone retrospective in `incidents/YYYY-MM-DD-<slug>.md`.
2. Copy `incidents/_template.md` for new retrospectives; include timeline, root cause, impact, resolution, and improvement actions.
3. Link retrospectives back to the corresponding worklog record.

## Security Rules (Mandatory)

These rules are **non-negotiable**. Violating them leaks credentials into a public repository.

- **Never** commit or push any of the following: passwords, access keys, secret keys, tokens, API keys, certificates, private keys, `.kube/config` or kubeconfig content, decoded Kubernetes Secret values, `.env` files, or database connection strings containing credentials.
- When writing documentation that must reference a sensitive value, use a placeholder such as `<ask-devops>` or `<redacted>` — never the real value.
- If a file containing secrets is found in the working tree, do not stage it; if it is already tracked, remove it from staging with `git rm --cached <file>` and add it to `.gitignore`.
- Before every commit, run `git status` and `git diff --cached` and manually scan the staged diff for any of the patterns above. If anything suspicious is found, do **not** commit — stop and report to the user.
- Do not echo, print, or write secrets into terminal output, logs, or any file in the repository.
- If a secret is ever pushed, it must be rotated immediately, not just deleted from history.

## Automatic Commit and Push

1. After every change (worklog record, knowledge entry, code change, config change), commit and push automatically — do not wait for the user to ask.
2. Before committing, check `git status` / `git diff`; stage only files related to this change, not unrelated files.
3. Use a concise one-line English or Chinese summary as the commit message.

## Example Record

```markdown
# Worklog 2026-09-17

## Grant EKS access to a new user

- **Time**: 10:30
- **Problem**: New teammate cannot access the cybex-prod / cybex-nonprod clusters
- **Investigation**: Checked IAM users and groups in both accounts; confirmed cluster auth mode is CONFIG_MAP; inspected aws-auth mapUsers
- **Root cause**: User was not present in aws-auth
- **Resolution**: Added the userarn to aws-auth of both clusters with group system:masters
- **Follow-up**: Remind the user to configure a local AWS profile
```