# Line Bisection Test (LBT)

This repository contains the **Computerized Line Bisection Test (cLBT)** — a high-precision, browser-based assessment tool used to measure visuospatial attention, perceptual biases, and motor accuracy. It is designed for neurological research, including studies involving stroke, unilateral spatial neglect, and related cognitive conditions.

<div align="center">

## 🚀 [CLICK HERE TO START TEST](https://sd-devsecops.github.io/Line-Bisection-Test/index.html)
**https://sd-devsecops.github.io/Line-Bisection-Test/index.html**

</div>

---

## 📌 Overview

The test displays horizontal lines on an interactive canvas. For each trial, the participant marks what they believe is the **center** of the line. 

The system provides immediate clinical feedback and professional data exports:
- **Core Statistics**: Signed bisection error (%), absolute error, and standard deviation.
- **Physical Estimation**: Estimated displacement in **Pixels (px)**, **Centimeters (cm)**, and **Inches (in)**.
- **Visual Auditing**: High-resolution PNG export of the patient's bisection pattern with errors mapped.
- **Longitudinal Export**: Structured CSV for statistical analysis (SPSS, R, Python).

---

## ⚙ Technical Specifications

### Stimulus Sizing & Clinical Validity
To ensure clinical validity across different screen sizes, the tool uses a dynamic rendering engine:

- **1200px Clinical Cap**: On ultra-large devices (like the iPad Pro 12.9"), the stimulus line is capped at 1200 logical pixels. This ensures the line doesn't exceed a practical visual field (approx. 12cm physically).
- **Universal Scaling**: On small-to-medium tablets, the stimulus length is exactly **50% of the available canvas width**, maintaining a consistent relative challenge regardless of hardware.
- **Standardized Stroke Cap**: User marks are limited to **200px**. If a mark exceeds this, it turns **Red** 🔴 and is silently cleared. This prevents "slashing" and ensures marks are intentional "midpoint ticks."

### Device Sizing Reference Table
| Device Model | Logical Width ($W_{px}$) | Physical Width ($W_{phys}$) | Hits 1200px Cap? | Line Length ($L_{phys}$) |
| :--- | :--- | :--- | :--- | :--- |
| **iPad Pro 12.9"** | 1366 px | 28.06 cm | **YES** | **12.32 cm** |
| **iPad Pro 11"** | 1194 px | 24.76 cm | NO | **11.76 cm** |
| **iPad Air (10.9")** | 1180 px | 24.76 cm | NO | **11.76 cm** |
| **iPad (10.2")** | 1080 px | 25.06 cm | NO | **11.90 cm** |
| **iPad Mini (8.3")** | 1133 px | 19.54 cm | NO | **9.28 cm** |

> *Note: Estimated using standard browser PPI (96). Screen-specific physical line length should be verified with a ruler if 100% precision is required.*

### Mobile Data Safety
The tool features **Smart Resize Protection**. If a patient rotates the tablet or the browser UI changes during a session:
- The test does **NOT** reset.
- The stimulus line and all previous marks are **mathematically scaled** to the new dimensions instantly.
- Coordinates are recalculated using relative ratios, preserving the clinical integrity of the session.

---

## 📊 Data Interpretation & Metrics

### Directional Bias (The "Neglect" Metric)
The primary clinical indicator is the **Signed Average Error (%)**:
- **Negative Value (-)**: Indicates a **Leftward Bias**. In neglect patients, this often suggests right-hemisphere damage affecting the left visual field (marking "center" too far to the left).
- **Positive Value (+)**: Indicates a **Rightward Bias**.
- **Percentage Calculation**: Error is calculated as a percentage of the line's half-length. `(Error_px / (Line_Length / 2)) * 100`.

### Accuracy & Consistency
- **Overall Accuracy (Abs Avg %)**: The average distance from the center, ignoring direction. Useful for measuring general motor precision or "coarseness" of response.
- **Standard Deviation (SD %)**: Measures consistency. A high SD indicates highly variable performance, which can be a marker for fluctuating attention or severe coordination deficit.

### Calculations for Research
The app calculates the intersection between the user's stroke and the stimulus line using a **parametric dot-product**.
**Researchers can verify data manually using the Raw CSV columns:**
- `pct`: Percentage error (relative).
- `px`: Raw pixel displacement from center.
- `cm / inch`: Estimated physical displacement.

---

## 🧪 How to Use

1. **Setup**: Enter the trials (e.g., 10, 20). Trials are randomized in position and Y-offset.
2. **Task**: Instruct the patient to draw a short vertical tick at the center of the line.
3. **Controls**:
   - **Reset**: Restarts the current test (clears all current session data).
   - **Finish**: End early to see results for the markers placed so far.
   - **Main Menu**: Clears data and returns to the trials screen.
4. **Export**: 
   - Fill in Participant Name, Surname, and Age (Required for export safety).
   - Press **Download CSV** for numerical analysis.
   - Press **Download Pattern** for a visual PDF-ready report showing every mark.

---

## ⚠ Ethical & Research Notice

- **Clinical Disclaimer**: This tool **does not replace** standardized diagnostic instruments. Interpretation must only be performed by a **licensed clinician**.
- **Verification**: Built-in calculations are for convenience. Researchers are encouraged to verify raw data against their specific study protocols.
- **Required Citation**: If you use this tool in publications, it is **required** to cite the project.
> For citation inquiries or institutional use, contact: **sdswat93@gmail.com**

---
**Project by:** *Zengin, M.*
