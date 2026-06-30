# Contributing

Contributions should make the skill more reliable for real LabVIEW-to-Python
measurement migrations.

## Good Changes

- Clearer migration gates
- Better hardware safety checks
- Better screenshot UI QA checks
- More precise simulator versus real-hardware language
- Small reference updates backed by real project evidence

## Before A Pull Request

Run:

```powershell
py $env:USERPROFILE\.codex\skills\.system\skill-creator\scripts\quick_validate.py .\skill\labview-to-python-industrial
```

Keep `SKILL.md` concise. Put long checklists in `references/`.

## Do Not Add

- Secrets, credentials, private lab paths, or proprietary driver files
- One-off project output logs
- Large vendor documentation dumps
- Safety claims that are not backed by hardware evidence
