---
name: labview-to-python-industrial
description: Industrial workflow for converting or reviewing LabVIEW measurement VIs into Python applications. Use when the user asks for LabVIEW to Python, LabVIEW-to-Python, LabVIEW转Python, VI migration, PyQt/PySide lab UI, hardware driver migration, simulator parity, screenshot UI review, or EXE packaging for laboratory or industrial measurement software.
---

# LabVIEW To Python Industrial

Use this as the default operating procedure for LabVIEW VI migrations, reviews,
and packaging audits. Keep the implementation boring: one measured workflow,
thin hardware adapters, simulator adapters that run through the same workflow,
and a UI that controls and observes the workflow instead of duplicating it.

## Start Here

1. Confirm the role: implement, review/supervise, or package/verify only. If the
   user asks for review or supervision only, do not edit code.
2. Freeze the LabVIEW sources: main VI, subVIs, ctl/type definitions, project
   files, front-panel screenshots, sample outputs, experiment notes, vendor SDKs,
   and driver versions.
3. Keep validation labels separate: `source UI`, `simulator`, `packaged EXE`,
   and `real hardware`. Never describe simulator success as real hardware
   success.
4. Read the relevant reference before acting:
   - New migration or audit: `references/workflow.md`
   - UI or visual feedback: `references/ui-qa.md`
   - Hardware, simulator, or EXE delivery: `references/hardware-packaging.md`

## Architecture

Use these modules unless the existing project already has better names:

- `workflow`: initialization, scan loop, pause/stop/shutter, saving, cleanup
- `hardware`: one adapter per instrument, with status, init, command, close
- `simulation`: fake adapters and signal generators using the same workflow
- `ui`: PyQt/PySide or local framework view/controller only
- `packaging`: PyInstaller or installer configuration and runtime assets
- `tests` or `scripts`: deterministic checks and screenshot verification
- `docs`: migration report, verification matrix, known hardware gaps

Do not put measurement state machines inside UI callbacks. The UI should call
the workflow and render state.

## Migration Gates

Pass gates in order and report the evidence for each gate:

1. LabVIEW parity inventory: all controls, default values, units, limits,
   scan grammar, saved outputs, error paths, and shutdown paths are accounted for.
2. Simulator parity: simulated hardware produces realistic dimensions, units,
   files, plots, and extreme-case behavior through the real workflow.
3. UI runtime: run the app, click buttons, type inputs, open combos, switch tabs,
   execute a simulated scan, and inspect screenshots.
4. Packaged EXE: launch the final deliverable EXE, not only source code, and
   repeat critical UI and simulator checks.
5. Real hardware: perform a fail-closed dry run only when hardware is present
   and the user approved safe instrument interaction.

## UI Rules

Industrial lab UI is not a landing page. Favor dense, stable, readable controls.
Use quiet dark surfaces, clear contrast, restrained colors, large enough command
buttons, LabVIEW-style hardware LEDs, readable logs, and charts that expose
coordinates and units. Validate typography with screenshots: baseline, clipping,
overlap, blank rows, hidden layers, combo arrows, and long-path fields matter.

For detailed UI checks, read `references/ui-qa.md`.

## Output Contract

For implementation tasks, finish with changed files, commands run, screenshots,
EXE path when applicable, and remaining hardware gaps. For reviews, lead with
blocking findings and evidence. For final claims, use precise labels:

- `source UI verified`
- `simulator verified`
- `packaged EXE verified`
- `real hardware unvalidated` or `real hardware verified`

If a screenshot or hardware gate is missing, say it is incomplete instead of
rounding up.
