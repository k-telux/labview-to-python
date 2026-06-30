# LabVIEW to Python Industrial Skill

Reusable Codex skill for migrating laboratory and industrial LabVIEW measurement
software into Python applications with hardware adapters, simulator parity,
industrial UI review, screenshot validation, and EXE packaging gates.

Author: telux

## Why

LabVIEW-to-Python projects fail most often at the edges: hidden subVI behavior,
hardware fail-safe paths, simulator claims being confused with real hardware,
UI defects visible only in screenshots, and packaged EXEs that do not match the
source application. This skill turns those lessons into a repeatable workflow.

## What It Covers

- LabVIEW VI and subVI behavior inventory
- Python workflow, hardware adapter, simulator, UI, tests, and packaging layout
- Industrial dark UI rules and screenshot-based QA
- Hardware status, fail-closed controls, and simulator/real-hardware boundaries
- Packaged EXE verification with hashes, timestamps, and runtime screenshots

## Install

Copy the skill folder into your Codex skills directory:

```powershell
Copy-Item -Recurse -Force .\skill\labview-to-python-industrial $env:USERPROFILE\.codex\skills\
```

Restart Codex or reload skills if your client requires it.

## Usage

Example prompt:

```text
Use $labview-to-python-industrial to convert this LabVIEW pump-probe VI into a
Python app with simulator, hardware adapters, screenshot UI QA, and EXE delivery.
```

The skill can also trigger implicitly for requests mentioning LabVIEW to Python,
VI migration, industrial measurement UI, hardware driver migration, simulator
parity, or packaged EXE verification.

## Repository Layout

```text
skill/
  labview-to-python-industrial/
    SKILL.md
    agents/openai.yaml
    references/
      workflow.md
      ui-qa.md
      hardware-packaging.md
```

## Validation

Validate the skill with the OpenAI skill creator validator:

```powershell
py $env:USERPROFILE\.codex\skills\.system\skill-creator\scripts\quick_validate.py .\skill\labview-to-python-industrial
```

For real LabVIEW projects, a final claim should include:

- LabVIEW parity inventory
- simulator run artifacts
- source UI screenshots
- packaged EXE screenshots
- real hardware status as verified or unvalidated

## Security

This repository contains instructions only. It should not include secrets,
driver license files, vendor credentials, or private lab paths. Real hardware
actions should stay fail-closed until the operator explicitly approves the dry
run.

## Credits

The README structure follows common mature open-source patterns from GitHub's
README guidance, Standard Readme, Best-README-Template, and the Agent Skills
progressive disclosure model.

## License

MIT License. See [LICENSE](LICENSE).
