# Line Bisection Test (LBT)

This repository contains the **Computerized Line Bisection Test (cLBT)** — a high-precision, browser-based assessment tool used to measure visuospatial attention, perceptual biases, and motor accuracy. It is designed for neurological research, including studies involving stroke, unilateral spatial neglect, and related cognitive conditions.

<div align="center">

## 🚀 [CLICK HERE TO START TEST](https://sd-devsecops.github.io/Line-Bisection-Test/line-bisection-test.html)
**https://sd-devsecops.github.io/Line-Bisection-Test/line-bisection-test.html**

</div>

---

## 📌 Overview

The test displays horizontal lines on an interactive canvas. For each trial, the participant marks what they believe is the **center** of the line.

The system provides immediate feedback and structured exports:
- **Core Statistics**: Signed bisection error (%), absolute error, and standard deviation.
- **Physical Estimation**: Estimated displacement in **Pixels (px)**, **Centimeters (cm)**, and **Inches (in)**.
- **Visual Auditing**: High-resolution PNG export of the patient's bisection pattern with errors mapped.
- **Longitudinal Export**: Structured CSV for statistical analysis (SPSS, R, Python).

---

## [!CAUTION] Scientific & Measurement Disclaimer (Read First)

Even if this tool is implemented carefully, **screen-based measurement has unavoidable sources of error**.  
All on-screen summaries (averages, SD, cm/in conversion) should be treated as **convenience estimates**, not final truth.

**Why this matters**
- Browsers do not guarantee true physical DPI/PPI.
- OS scaling, browser zoom, accessibility settings, and devicePixelRatio can change effective measurement.
- Converting pixels → cm/in assumes a display density that may not match the real device.

**Strong recommendation for researchers**
1. Treat the CSV’s **Raw Data (`px`)** as the primary ground truth.
2. Recompute your own metrics externally from `px` (and/or `pct`) using your preferred pipeline.
3. If physical units matter, calibrate the device with a ruler and your protocol (or store a calibration factor per device/session).

> In short: this tool produces reliable **geometry** (pixel-based), while **physical units and derived stats should be independently verified**.

---

## ⚙ Technical Specifications

### Stimulus Sizing & Clinical Validity
To ensure clinical validity across different screen sizes, the tool uses a dynamic rendering engine:

- **600px Clinical Cap**: On ultra-large devices (like the iPad Pro 12.9"), the stimulus line length is capped at 600 logical pixels. This ensures the line doesn't exceed a practical visual field (approx. 15.8cm physically at 96 DPI).
- **Universal Scaling**: On small-to-medium tablets, the stimulus length is exactly **50% of the available canvas width**, maintaining a consistent relative challenge regardless of hardware.
- **Standardized Stroke Cap**: User marks are limited to **200px**. If a mark exceeds this, it turns **Red** 🔴 while drawing and is **discarded** when released (the stroke is cleared and the trial is not recorded).  
  *Note: Discarding is currently silent (no popup); the red visual is the feedback.*

### Device Sizing Reference Table

All physical length estimates below follow the **same assumption used in code**:

- 1 inch = 96 CSS pixels  
- 1 cm ≈ 37.795 px  

The stimulus line length is computed as:

lineLength = min(canvasWidth / 2, 600px)

| Device Model | Logical Width (px) | Canvas Width Used (px) | Line Length (px) | Estimated Line Length (cm) |
|-------------|--------------------|------------------------|------------------|----------------------------|
| **iPad Pro 12.9"** | 1366 | 1200 (capped) | 600 | **15.88 cm** |
| **iPad Pro 11"** | 1194 | 1194 | 597 | 15.80 cm |
| **iPad Air (10.9")** | 1180 | 1180 | 590 | 15.61 cm |
| **iPad (10.2")** | 1080 | 1080 | 540 | 14.29 cm |
| **iPad Mini (8.3")** | 1133 | 1133 | 566.5 | 14.99 cm |

> Note: These values are **estimates**, not guaranteed physical measurements.  
> Actual physical size depends on browser scaling and device calibration.


> *Note: Physical size estimates above assume a standard browser PPI (96). Screen-specific physical line length should be verified with a ruler if 100% precision is required.*

### Mobile Data Safety
The tool features **Smart Resize Protection**. If a patient rotates the tablet or the browser UI changes during a session:
- The test does **NOT** reset.
- The stimulus line and all previous marks are **mathematically scaled** to the new dimensions instantly.
- Coordinates are recalculated using relative ratios, preserving the clinical integrity of the session.

---

## 📊 Data Interpretation & Metrics

### Mathematical Formulas & Logic
The system generates the data columns seen in the **Raw Data** export as follows:

1. **Pixel Displacement (`px`)**
   - The signed horizontal distance between the user’s mark intersection and the true midpoint:
   - `Δpx = X_mark − X_mid`
   - Negative = left of center, Positive = right of center.

2. **Percentage Error (`pct`)**
   - Normalized error relative to half-line length:
   - `Error% = (Δpx / (LineLength / 2)) × 100`
   - This normalizes performance across different line lengths.
   - Values are clamped to ±100%.

3. **Physical Units (`cm` & `inch`)**
   - Based on a **fixed assumption** (96 DPI):
   - `cm = Δpx / 37.795`
   - `inch = Δpx / 96`
   - ⚠️ These are estimates; use calibration if physical units matter.

### Aggregate Clinical Statistics
At the end of a session, the following aggregates are calculated:

- **Directional Bias (Signed Avg %)**: mean of all `pct` values (left/right can cancel).
- **Overall Accuracy (Abs Avg %)**: mean of absolute `pct` values (direction ignored).
- **Standard Deviation (SD %)**: population SD of `pct` values (higher = less consistent).

### Clinical Thresholds (Guide)
In many clinical studies (e.g., *Schenkenberg et al.*), a **signed displacement > 0.6 cm (6mm)** or a **percentage error > 5–10%** is often considered a positive screening for Unilateral Spatial Neglect.

> **Important:** Thresholds vary by protocol; do not apply these without matching your study design and validation.

---

## 🖼️ Understanding the Pattern Export (PNG)

The **Download Pattern** button creates a high-resolution audit image showing every trial in a standardized layout.

For each row (trial):

- **`L#` label (left)**  
  The trial index (e.g., `L1`, `L2`, ...).

- **Black horizontal line**  
  The stimulus line that was shown during the trial (recentered on the export image for readability).

- **Red dot at the center**  
  The **true midpoint** of the line:
  - In the export code, this is `drawMidX`.

- **Blue vertical tick**  
  The participant’s mark position:
  - The system computes the trial’s intersection point with the stimulus line (`markX`).
  - Then it places the mark relative to the midpoint using:
    - `(markX − trueMidpointX)` = signed displacement in pixels
    - `drawMarkX = drawMidX + (markX − trueMidpointX)`

- **Right-side text label: `±pct (cm)`**  
  Example: `+3.25% (0.42cm)`
  - `pct` is computed from pixel displacement:
    - `pct = (Δpx / (LineLength/2)) × 100`
  - `cm` is computed using:
    - `cm = Δpx / 37.795`
  - The sign (`+` or `-`) matches the direction (right vs left of midpoint).

**How to debug errors using the Pattern PNG**
- If `pct` looks wrong:
  1. Check if the blue tick is visually right/left of the red dot (direction).
  2. Compare the signed value in the CSV (`px`) to the label.
  3. Recompute `pct` externally from `px` + `lineLength` if needed.
- If cm/in seems off:
  - That’s expected on many devices unless calibrated; treat cm/in as estimate.

---

## 🧪 How to Use

1. **Setup**: Enter the trials (e.g., 10, 20). Trials are randomized in position and Y-offset.
2. **Task**: Instruct the patient to draw a short vertical tick at the center of the line.
3. **Drawing Feedback**:
   - **Blue Stroke**: Valid stroke length (≤ 200px).
   - **Red Stroke** 🔴: Too long (> 200px) — will be discarded when released.
4. **Controls**:
   - **Reset**: Restarts the current test (clears all current session data).
   - **Finish**: End early to see results for the markers placed so far.
   - **Main Menu**: Clears data and returns to the trials screen.
5. **Export**:
   - Fill in Participant Name, Surname, and Age (required for download buttons).
   - Press **Download CSV** for numerical analysis.
   - Press **Download Pattern** for a visual report of marks vs true midpoints.

---

## ⚠ Ethical & Research Notice

- **Clinical Disclaimer**: This tool **does not replace** standardized diagnostic instruments. Interpretation must only be performed by a **licensed clinician**.
- **Verification**: Built-in calculations are for convenience. Researchers are encouraged to verify raw data against their specific study protocols.
- **Required Citation**: If you use this tool in publications, it is **required** to cite the project.

> For citation inquiries or institutional use, contact: **sdswat93@gmail.com**

---

**Project by:** *Zengin, M.*
