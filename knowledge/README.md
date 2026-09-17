# Knowledge

Reusable knowledge base: environment facts, access permissions, operational runbooks, and reference resources. Distilled automatically once an investigation reaches a stable conclusion.

## Usage

- Copy `_template.md` for new entries; fill in the YAML frontmatter and body.
- Every document carries YAML frontmatter metadata: type, status, environment.
- Put executable operational steps in `runbooks/`; put external links and resource lists in `reference/`.
- Put environment facts (clusters, accounts, endpoints) here, not in `AGENTS.md`.

## Entries

| Document | Type | Description |
|----------|------|-------------|
| _no entries yet_ |

## Notes

- This directory holds only stable conclusions; raw investigation process stays in `../worklog/`.
- Never commit sensitive information — use placeholders (e.g. `<ask-devops>`).
- Entries marked `UNVERIFIED` are drafts, not verified state.