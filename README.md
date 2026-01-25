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

## 📐 Why 600px ≠ 16cm on iPad (Important)

A common misconception is assuming the generic browser standard:  
`1 inch = 96 CSS pixels`

On high-density "Retina" displays, this assumption is physically incorrect.

**Example: iPad Pro 12.9"**
- Physical width ≈ **28.16 cm**
- Logical width = **1366 CSS px**
- **Actual Reality**: 1366px / 28.16cm ≈ **48.5 px/cm** (or ~123.7 PPI)

**Real conversion logic used in cLBT**:  
`600px × (2.54 / 123.7) ≈ 12.3 cm`  
*(The common mistake of using 96 DPI would report ~15.9 cm for the same 600px).*

---

## ⚖️ Hardware Calibration (Correct Solution)

Because browsers do not expose physical dimensions, cLBT uses a **Device-Aware Calibration Model**.

### Auto-Detection (Best-Effort)
The system identifies the device class and applies known PPI values:
- **iPad Pro 12.9"** → ~123.7 PPI
- **iPad Pro 11" / iPad Air** → ~122.5 PPI
- **iPad Mini** → ~163 PPI
- **Desktop** → 96 PPI (Standard W3C)

### Manual Calibration (Recommended)
Before a clinical session:
1. Hold a **physical ruler** to the stimulus line on the screen.
2. Adjust the **Calibration PPI** value in the Hardware Calibration box until the reported **cm** matches your ruler.
3. Calibration is applied per session.

**Tip**: Real PPI ≈ `Logical Pixels / Physical Inches`.

---

## � Device Reference Table (Comparative)

The following table shows how the same **600px (or 50%)** stimulus scales across different hardware using cLBT's calibration engine.

| Device Model | Logical Width | Calibrated PPI | Line Length | Physical Length (cm) |
| :--- | :--- | :--- | :--- | :--- |
| **iPad Pro 12.9"** | 1366 px | 123.7 | 600 px | **12.32 cm** |
| **iPad Pro 11" / Air** | 1194 px | 122.5 | 597 px | **12.38 cm** |
| **iPad Mini (8.3")** | 1133 px | 163.0 | 566 px | **8.82 cm** |
| **Surface Pro 9** | 1440 px | 120.0 | 600 px | **12.70 cm** |
| **MacBook Air 13"** | 1280 px | 113.0 | 600 px | **13.48 cm** |
| **Std. 24" Monitor** | 1920 px | 96.0 | 600 px | **15.88 cm** |

> **Note**: Values marked in **bold** are calibrated for the iPad Pro 12.9" form factor. Desktop values follow the W3C standard (96 DPI). Smaller devices use 50% width instead of the 600px cap.

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
- **Red Dot**: The **true midpoint** (`drawMidX`).
- **Blue Vertical Tick**: The participant's mark.
- **Text Label**: `±pct (cm)` based on calibrated PPI.

Placement logic:  
`drawMarkX = drawMidX + (markX − trueMidpointX)`

---

## 🧪 How to Use

1. **Setup**: Enter trials (e.g., 10, 20).
2. **Calibration**: Check PPI if physical units (cm) are needed.
3. **Task**: Patient draws a short vertical lick at the center.
4. **Drawing Feedback**:
   - **Blue**: Valid stroke length.
   - **Red**: Too long (> 200px) — discarded when released.
5. **Controls**:
   - **Reset**: Restart current test.
   - **Finish**: End early and view results.
6. **Export**: Enter Participant Info to unlock CSV and Pattern PNG downloads.

---

## ⚠ Ethical & Research Notice

- **Clinical Disclaimer**: This tool **does not replace** standardized diagnostic instruments.
- **Verification**: Researchers are encouraged to verify raw `px` data.
- **Requirement**: Cite this project if used in academic publications.

Contact: **sdswat93@gmail.com**

---

**Project by:** *Zengin, M.*
