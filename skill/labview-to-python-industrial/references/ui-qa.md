# Industrial Lab UI And Visual QA

## Design Principles

- Use Apple-like clarity: hierarchy, alignment, spacing, and restrained surfaces.
  Do not translate this into decoration.
- Use an industrial dark theme with high contrast and low saturation. Avoid
  bright AI-like blue/purple gradients and noisy color ramps.
- Keep cards and panels shallow. Avoid nested cards unless the inner element is
  a true repeated item or modal.
- Put common operating parameters on the main page. Move rare, advanced, and
  simulator-only parameters into tabs.
- Size command buttons for repeated lab use. Button text must be readable and
  vertically centered.
- Represent hardware status as `device name + LED`: green connected, red
  error/fail-closed, gray simulation/optional/unconnected.
- Shutter controls must reflect the real or simulated shutter state with text
  and color.
- Logs need scannable structure: timestamp, severity, point/step, message, and
  separators. Highlight `Result` without overusing saturated colors.

## Visual Checklist

Check every page and every interactive state:

- Main tabs, lower tabs, advanced tabs, save tabs, simulation tabs
- QLineEdit, QComboBox, spin boxes, checkboxes, buttons, progress bars, logs
- Text baseline, vertical centering, clipping, long path fields, and combo arrows
- Empty first rows inside panels
- Field labels and input left edges
- Progress percent not overlapping the bar
- Hardware LED alignment and state color
- Plot titles, axis labels, units, tick labels, line width, point markers
- Plot hover readout text left aligned and showing reduced x/y coordinates
- Heatmap cell aspect ratio, matrix shape, extent, colorbar spacing, and no
  cropped edge cells
- Small and normal resolution screenshots

Automated OpenCV checks can catch nonblank windows and obvious overlap. They do
not replace human review of baseline, clipping, color, and plot meaning.

## Required Screenshot Evidence

For a serious UI claim, collect:

- Complete screenshot of every main tab
- Local crop of dense controls such as scan timing
- True/False or equivalent combo states
- Open/closed shutter states
- Run status crop with progress, result, and log
- Hardware status crop with LEDs
- Acquisition display with hover over each plot
- Heatmap full screenshot and edge crop
- Save page with long paths
- Packaged EXE screenshots matching the source UI checks

Do not accept JSON alone as UI proof.
