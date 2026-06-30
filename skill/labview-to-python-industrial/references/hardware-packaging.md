# Hardware, Simulator, And Packaging Gates

## Hardware Adapter Contract

Each instrument adapter should expose the smallest stable surface:

- `status()` with connected, simulated, optional, failed, and message fields
- `initialize(config)`
- Core commands used by the workflow
- `close()` and fail-closed cleanup
- Clear exceptions or result objects for timeouts, limit errors, and driver
  failures

Adapters should hide vendor SDK details from workflow and UI code.

## Hardware Safety

- Stage/motion devices need limits and a checked zero/reference path.
- Shutters should default to closed on init failure, scan failure, stop, and app
  exit.
- DAQ outputs should return to safe values on failure.
- Source meters and lasers need ramping and explicit user approval before real
  output.
- Real hardware not connected means `blocked/unvalidated`, not `ready`.

## Simulator Requirements

- Same adapter contract as hardware.
- Same units, shapes, metadata, and save formats.
- Configurable profiles for normal and failure cases.
- Deterministic seeds for tests.
- Artifacts that state simulation settings.

## EXE Packaging Gates

Before claiming packaged delivery:

1. Build from the current source after the last UI or workflow edit.
2. Verify the intended deliverable path, timestamp, and hash.
3. Avoid mixing old nested `dist/<app>/<app>.exe` outputs with the current
   top-level deliverable.
4. Launch the final EXE and repeat critical UI checks with screenshots.
5. Confirm runtime assets, SDK DLLs, icons, config files, and output folders are
   present.
6. Record any antivirus, permission, or working-directory assumptions.

Report source and EXE verification separately.
