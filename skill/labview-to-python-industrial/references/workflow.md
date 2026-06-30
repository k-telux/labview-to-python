# LabVIEW To Python Migration Workflow

## 1. Intake And Freeze

- Copy or reference original LabVIEW files read-only.
- Inventory main VI, subVIs, ctl/type definitions, project files, user controls,
  indicators, property nodes, event structures, queues, timed loops, DAQ nodes,
  VISA/GPIB/serial calls, DLL calls, and vendor SDK dependencies.
- Capture front-panel screenshots and at least one known-good LabVIEW output if
  available.
- Ask which VI is canonical when folders contain versions or archives.

## 2. Extract Behavior Before UI

Document the experiment before coding:

- Initialize order and required delays
- Scan loop, nested loops, stop conditions, pause behavior
- Shutter, stage, DAQ, camera/spectrometer, source meter, and counter behavior
- Unit conversions, calibration constants, axis order, coordinate origins
- Limits and fail-safe behavior
- Save format, naming, metadata, and final screenshots
- Error handling and shutdown order

Use a parity table with columns: LabVIEW item, Python owner, simulator behavior,
test evidence, and unresolved hardware note.

## 3. Build One Workflow

Create one Python workflow used by both real and simulated hardware. Keep UI
callbacks thin:

1. Parse and validate parameters.
2. Initialize adapters.
3. Run the scan loop.
4. Emit progress and result events.
5. Save raw data, metadata, plots, and logs.
6. Close hardware in a finally/fail-closed path.

Do not create separate "UI measurement logic" and "headless measurement logic".

## 4. Simulate Like The Instrument

The simulator should be deterministic enough for tests and realistic enough for
UI review:

- Use configurable profiles and seeds.
- Return arrays with the same shape, axis order, units, and metadata as real
  adapters.
- Cover normal, boundary, slow, timeout, failed init, failed command, and
  interrupted scan cases.
- Write a `simulation_profile.json` or equivalent in run artifacts.

Simulator success proves software flow, not real hardware compatibility.

## 5. Test The Migration

Use the smallest checks that catch real breakage:

- Unit/shape checks for scan plans and saved outputs
- Adapter contract tests with simulated devices
- Extreme parameter checks: zero steps, one step, max/min limits, bad unit,
  bad device name, stopped scan, paused scan
- Screenshot UI checks with real interaction
- Packaged EXE smoke checks

Manual visual review remains required for typography, layout, and plot quality.

## 6. Report Evidence

Use a verification matrix:

| Gate | Evidence | Status |
| --- | --- | --- |
| LabVIEW parity inventory | table/report | pass/block |
| Simulator workflow | tests, run artifacts | pass/block |
| Source UI | screenshots, interaction log | pass/block |
| Packaged EXE | EXE screenshot, hash/timestamp | pass/block |
| Real hardware | dry-run log | pass/block/unvalidated |

Never collapse `unvalidated` into `pass`.
