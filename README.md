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
- OS scaling, browser zoom, accessibility settings, and `devicePixelRatio` affect effective size.
- CSS pixels (logical) are **not physical pixels**.

**Strong recommendation for researchers**
1. Treat the CSV’s **Raw Data (`px`)** as the primary ground truth.
2. Recompute metrics externally from `px` using your preferred pipeline.
3. If physical units matter, **calibrate the device** using the built-in tool and a ruler.

> Geometry is reliable (pixel-based). Physical units require calibration.

---

## ⚙ Technical Specifications

### Stimulus Sizing & Clinical Validity

The stimulus line length is defined in **logical (CSS) pixels**:

`lineLength = min(canvasWidth / 2, 600px)`

- **600px Clinical Cap**  
  Prevents the stimulus from exceeding a practical visual field on ultra-large devices (e.g., iPad Pro 12.9").

- **Relative Scaling**  
  On smaller tablets, the line is exactly **50% of the available canvas width**, maintaining a consistent relative task challenge.

- **Standardized Stroke Cap**  
  User marks are limited to **200px**. Invalid marks turn **Red** 🔴 while drawing and are **discarded** when released.

---

## 📐 Physical Units and Calibration (cm / inch)

### Why cm/in can be wrong without calibration

Browsers do not expose the true physical size of a CSS pixel. Because of this, cm/in values are only valid after calibration.

### How to calculate stimulus pixel length (px) from one edge mark

1. Start the test.
2. Go to one end of the stimulus line (left or right).
3. Draw a short vertical stroke as close to the edge as possible.
4. Read the bottom log value as **percent (%)** and **pixels (px)**.

Example:
`99.65% 299 px`

The test uses:
`Error% = (Δpx / (LineLength / 2)) × 100`

Solve for half-line:
`HalfLinePx = (Δpx × 100) / Error%`

Using the example:
`HalfLinePx = (299 × 100) / 99.65 = 300 px`

Full line:
`LineLengthPx = 2 × HalfLinePx = 600 px`

### Reference: Typical stimulus pixel lengths (px)

These are typical outputs from the test’s sizing rule (600px cap or 50% width). Always verify manually, because viewport size can change.

| Device Model         | Logical Width | Typical Stimulus Length |
|----------------------|--------------|--------------------------|
| iPad Pro 12.9"       | 1366 px      | 600 px                   |
| iPad Pro 11" / Air   | 1194 px      | 597 px                   |
| iPad Mini (8.3")     | 1133 px      | 566 px                   |
| Surface Pro 9        | 1440 px      | 600 px                   |
| MacBook Air 13"      | 1280 px      | 600 px                   |
| Std. 24" Monitor     | 1920 px      | 600 px                   |

### How to calculate PPI manually (recommended)

1. Measure the real physical length of the stimulus line on the screen with a ruler (cm).
2. Use the formula:

`PPI = (LineLengthPx × 2.54) / MeasuredLengthCm`

Example:
- `LineLengthPx = 600`
- `MeasuredLengthCm = 11.5`

`PPI = (600 × 2.54) / 11.5 = 132.5`

Enter this PPI value into the calibration field.

---

## �📊 Data Interpretation & Metrics

### Mathematical Definitions

**Pixel Displacement (`px`)**  
The signed horizontal distance between the mark and the midpoint:  
`Δpx = X_mark − X_mid`  
- Negative = left of center, Positive = right of center.

**Percentage Error (`pct`)**  
Normalized error relative to half-line length:  
`Error% = (Δpx / (LineLength / 2)) × 100`  
- Clamped to ±100%.

**Physical Units**  
Computed using the **active calibrated PPI**:  
`cm = Δpx × (2.54 / PPI)`  
`inch = Δpx / PPI`

### Aggregate Statistics
- **Directional Bias (%)**: Signed mean of `pct` values (indicates overall left/right neglect).
- **Overall Accuracy (%)**: Mean of absolute `pct` values (indicates precision regardless of direction).
- **Standard Deviation (%)**: Consistency of bisection performance.

---

## 🖼️ Understanding the Pattern Export (PNG)

The **Download Pattern** button creates a high-resolution audit image showing every trial.

- **Black Line**: The stimulus line.
- **Red Dot**: The true midpoint (`drawMidX`).
- **Blue Vertical Tick**: The participant's mark.
- **Text Label**: `±pct (cm)` based on calibrated PPI.

Placement logic:  
`drawMarkX = drawMidX + (markX − trueMidpointX)`

---

## 🧪 How to Use

- **Setup**: Enter trials (e.g., 10, 20).
- **Calibration**: Check PPI if physical units (cm) are needed.
- **Task**: Patient draws a short vertical tick at the center.
- **Drawing Feedback**:
  - **Blue**: Valid stroke length.
  - **Red**: Too long (> 200px) — discarded when released.
- **Controls**:
  - **Reset**: Restart current test.
  - **Finish**: End early and view results.
- **Export**: Enter Participant Info to unlock CSV and Pattern PNG downloads.

---

## ⚠ Ethical & Research Notice

- **Clinical Disclaimer**: This tool does not replace standardized diagnostic instruments.
- **Verification**: Researchers are encouraged to verify raw `px` data.
- **Requirement**: Cite this project if used in academic publications.

Contact: **sdswat93@gmail.com**

**Project by:** *Zengin, M.*
