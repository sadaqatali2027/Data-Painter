<p align="center">
  <img src="assets/banner.svg" alt="Data Painter Banner" width="100%"/>
</p>

# Data Painter (By: TerraNomad)

**Data Painter** is a browser-based interactive tool that lets you *draw* scientific data directly onto professional plot canvases and export it as **CSV**, **LAS 2.0**, or **PNG**. Built for geoscientists, petrophysicists, and reservoir engineers, it requires no installation, no server, and no dependencies -- just open the HTML file in any modern browser and start painting.

Whether you need to sketch a quick GR log for a training slide, digitize a type curve from a paper figure, or mock up a Pickett plot for a proposal, Data Painter gives you an intuitive canvas-first workflow.

---

## Quick Start

1. Download or clone this repository.
2. Open **`DataPainter.html`** in any modern browser (Chrome, Edge, Firefox, Safari).
3. Select a plot type from the tab bar.
4. Configure your axis ranges and labels in the sidebar.
5. Click or drag on the canvas to paint data points.
6. Export your data as CSV, LAS 2.0, or PNG.

No build step. No `npm install`. No Python environment. Just one self-contained HTML file.

---

## Plot Types

Data Painter includes **8 specialized plot types**, each designed for a specific geoscience or engineering workflow.

### 1. 1D Well Log

A vertical depth track for painting single-curve well log data. Points are automatically connected into a continuous log trace sorted by depth.

**When to use:** Sketching synthetic well logs, digitizing curves from raster images, creating training or presentation data, or generating test data for petrophysical software.

**Capabilities:**
- Vertical depth axis (increasing downward) with configurable depth range
- Horizontal value axis with configurable min/max
- Custom curve name (GR, RHOB, NPHI, DT, etc.)
- Auto-connecting line trace sorted by depth
- Export as CSV (Depth, CurveName) or LAS 2.0

### 2. 2D Cross Plot

A standard X vs Y scatter plot for cross-plotting any two parameters.

**When to use:** Creating scatter plots of two log curves, visualizing property relationships (e.g., porosity vs permeability), or generating illustrative data for presentations and reports.

**Capabilities:**
- Fully configurable X and Y axis ranges and labels
- Individual point placement or freehand point clouds
- 10 color options for distinguishing data populations
- Export as CSV (X, Y columns)

### 3. Histogram

A frequency distribution painter where you click on bins to build up bar heights. Right-click to decrease a bar.

**When to use:** Defining cutoff values (GR sand/shale threshold, porosity cutoffs), illustrating data distributions for presentations, or creating idealized histograms for training materials.

**Capabilities:**
- Configurable value range, bin count, and max count
- Left-click to increment, right-click to decrement each bin
- Custom parameter labeling
- Count labels above each bar
- Export as CSV (BinStart, BinEnd, Count)

### 4. Multi-Track Well Log

Three side-by-side well log tracks on a shared depth axis -- the standard composite log view used across the oil and gas industry.

**When to use:** Sketching a complete well log suite (e.g., GR + RHOB + NPHI), creating composite log illustrations, generating multi-curve test data for software QA, or producing training materials.

**Capabilities:**
- Three independently configurable tracks (name, unit range)
- Shared depth axis with configurable range
- Switch between tracks to paint each curve independently
- Color-coded track headers and traces
- **Merged 4-column CSV export** (Depth, GR, RHOB, NPHI) with `-999.25` null values for missing data
- **LAS 2.0 export** with proper header sections and curve definitions

### 5. Ternary Plot

A triangular diagram for three-component compositional data with barycentric coordinate gridlines at 10% intervals.

**When to use:** Lithology classification (Sand-Silt-Clay), mineral composition analysis, fluid analysis (oil-water-gas fractions), or any three-component system visualization.

**Capabilities:**
- Equilateral triangle with customizable vertex labels
- 10% gridlines for all three axes
- Barycentric coordinate readout in the status bar
- Points automatically constrained to the triangle
- Export as CSV (A%, B%, C%)

### 6. Fence / Decline Curve

A piecewise linear plot where control points are connected by straight-line segments with a shaded area under the curve.

**When to use:** Sketching production decline curves, type curves, rate-time profiles, pressure transient shapes, or any piecewise-linear trend for forecasting or illustration.

**Capabilities:**
- Points auto-connected by straight lines (sorted by X)
- Shaded area under the curve for visual emphasis
- Configurable axis labels (e.g., Days vs Rate, or Time vs Cumulative)
- Export as CSV sorted by X coordinate

### 7. Semi-Log / Log-Log Cross Plot

A cross plot with logarithmic axis scaling -- essential for many standard oil and gas interpretation techniques.

**When to use:** Pickett plots (porosity vs resistivity), permeability transforms, pressure transient analysis, or any relationship that spans multiple orders of magnitude.

**Capabilities:**
- Three scale modes: **Semi-Log X**, **Semi-Log Y**, and **Log-Log**
- Proper logarithmic gridlines with major/minor tick marks
- Configurable axis ranges across multiple decades
- Status bar shows actual (not log-transformed) coordinate values
- Export as CSV with actual values

### 8. Zone / Fill

A dual-curve depth track for painting two boundary curves with shaded fill between them and a configurable cutoff line.

**When to use:** Defining net pay intervals, illustrating lithology zones (sand vs shale), drawing formation tops, or visualizing the difference between two curves (e.g., neutron-density crossover).

**Capabilities:**
- Two independently paintable boundary curves (Left/Right, color-coded red/blue)
- Automatic shaded fill between the two curves
- Configurable cutoff line (dashed yellow) for threshold visualization
- Visual legend and active-curve indicator
- Export as CSV with boundary labels (Upper/Lower, Depth, Value)

---

## Export Formats

### CSV Export (All Plot Types)

Every plot type supports CSV download and copy-to-clipboard. The CSV format is tailored to each plot type:

| Plot Type | CSV Columns |
|-----------|-------------|
| 1D Well Log | `Depth, CurveName` |
| 2D Cross Plot | `X, Y` |
| Histogram | `BinStart, BinEnd, Count` |
| Multi-Track | `Depth, GR, RHOB, NPHI` (merged on depth, `-999.25` for nulls) |
| Ternary | `A%, B%, C%` |
| Fence/Decline | `X, Y` (sorted by X) |
| Semi-Log | `X, Y` (actual values, not log-transformed) |
| Zone/Fill | `Boundary, Depth, Value` |

### LAS 2.0 Export (1D Well Log and Multi-Track)

Both the single-curve well log and the multi-track log support export to **LAS 2.0** (Log ASCII Standard), the industry-standard format for well log data. The exported file includes:

- **~VERSION** section (LAS 2.0, no wrap)
- **~WELL** section (start/stop depth, step, null value, company, date)
- **~CURVE** section (curve mnemonics and units: DEPT/FT, GR/GAPI, RHOB/G/CC, NPHI/V/V)
- **~PARAMETER** section
- **~A** (ASCII data) section with formatted numeric columns

LAS files can be loaded directly into industry software such as Techlog, Petrel, Interactive Petrophysics (IP), Geolog, and many open-source tools.

### PNG Export (All Plot Types)

Every plot type supports one-click PNG export that captures the current canvas exactly as rendered, including gridlines, labels, data points, and any fill or trace styling. Useful for embedding plots into presentations, reports, or publications.

---

## Drawing Tools

### Click Mode

Place individual points one at a time with precision. Best for control-point workflows like decline curves, or when digitizing specific data values. Toggle with the `C` key.

### Freehand Mode

Click and drag to paint a continuous stream of points along your cursor path. Adjustable spacing controls point density. Best for sketching smooth well log curves or dense scatter clouds. Toggle with the `D` key.

### Additional Controls

- **Point Size** -- Adjustable from 1px to 12px via slider
- **Draw Spacing** -- Controls minimum distance between freehand points (1px to 30px)
- **Color Palette** -- 10 distinct colors for differentiating data populations or lithologies
- **Undo** -- Remove the last point (`Ctrl+Z`)
- **Double-Click** -- Remove the nearest point on the canvas
- **Clear All** -- Reset all data for the current plot type

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `C` | Switch to Click mode |
| `D` | Switch to Freehand (Draw) mode |
| `Ctrl+Z` | Undo last point |

---

## Use Cases in Oil & Gas

- **Petrophysics training** -- Sketch idealized well logs to teach log interpretation concepts
- **Quick data mockups** -- Generate synthetic data for software demos or proposals
- **Curve digitization** -- Recreate data from raster images or paper logs
- **Cutoff analysis** -- Paint histograms to visualize and define GR, porosity, or saturation cutoffs
- **Decline curve analysis** -- Sketch type curves or forecast profiles for production engineering
- **Pickett plots** -- Use the log-log cross plot to illustrate porosity-resistivity relationships
- **Lithology classification** -- Use the ternary plot for sand-silt-clay or mineral composition work
- **Net pay definition** -- Use Zone/Fill to illustrate pay intervals between curve boundaries
- **Report figures** -- Export publication-ready PNG images directly from the tool

---

## Technical Details

- **Single-file application** -- One self-contained HTML file with embedded CSS and JavaScript
- **Zero dependencies** -- No external libraries, frameworks, or CDN links required
- **Offline capable** -- Works entirely in the browser with no network connection needed
- **Canvas-based rendering** -- Uses HTML5 Canvas for smooth, high-performance drawing
- **Responsive layout** -- Adapts to different window sizes; canvas resizes dynamically
- **Cross-browser** -- Compatible with Chrome, Edge, Firefox, and Safari

---

## File Structure

```
DataPainter/
  DataPainter.html    # The complete application (single file)
  assets/
    banner.svg        # Repository banner image
  README.md           # This file
```

---

## License

This project is open source. Feel free to use, modify, and distribute.

---

<p align="center">
  <b>Data Painter</b> by <b>TerraNomad</b><br/>
  <i>Paint your data. Export your science.</i>
</p>
