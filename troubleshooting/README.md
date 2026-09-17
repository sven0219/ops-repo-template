# Troubleshooting

Troubleshooting cases: root-cause analysis and reusable debugging notes for resolved investigations. One case per file.

## Relationship With Other Directories

| Directory | Purpose |
|-----------|---------|
| `../worklog/` | Raw investigation stream, by date (the daily log) |
| `troubleshooting/` | This directory — distilled case write-ups with root cause per incident |
| `../knowledge/` | Reusable knowledge and runbooks (stable, cross-incident conclusions) |
| `../incidents/` | Major incident retrospectives (production/customer impact) |

## Usage

- Copy `_template.md` for a new case.
- File naming: `YYYY-MM-DD-<short-slug>.md` (e.g. `2026-09-17-rds-connectivity-timeout.md`).
- Link the case back to the raw process in `../worklog/YYYY-MM-DD.md`.
- If the case yields a stable, reusable conclusion, also create a `../knowledge/` entry.

## Cases

| Date | Topic |
|------|-------|
| _no cases yet_ |