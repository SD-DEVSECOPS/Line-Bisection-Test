# Line Bisection Test (LBT)

This repository contains the **Computerized Line Bisection Test (cLBT)** — a browser-based assessment tool used to measure visuospatial attention and motor accuracy. 

> [!CAUTION]
> **CRITICAL SCIENTIFIC DISCLAIMER**  
> All calculations (cm, inch, averages, SD) provided by this tool are **CONVENIENCE ESTIMATIONS** and may be **INACCURATE** due to screen scaling, uncalibrated PPI, or software edge cases. 
> 
> **Researchers are strongly advised to:**
> 1. **Do not rely** on the on-screen summary for final clinical conclusions.
> 2. **Recompute all metrics** independently using the **Raw Data (px)** columns in the exported CSV.
> 3. **Independently validate** the internal logic against your specific research protocol.

---

## 🚀 [CLICK HERE TO START TEST](https://sd-devsecops.github.io/Line-Bisection-Test/index.html)

---

## 📐 Mathematical Calculations & Formulas

The system records the interaction between a user stroke (vector $\vec{U}$) and the stimulus line (vector $\vec{S}$).

### 1. Raw Pixel Displacement (`px`)
Calculated by finding the intersection point $I(x, y)$ of the user's mark and the horizontal stimulus.
$$\Delta px = I_x - X_{midpoint}$$
- **Negative (-)**: Leftward error (Mark is to the left of true center).
- **Positive (+)**: Rightward error (Mark is to the right of true center).

### 2. Percentage Error (`pct`)
Normalizes the error relative to the stimulus size. $R$ is the radius (half-length) of the line.
$$Error\% = \left( \frac{\Delta px}{R} \right) \times 100$$
- *Clamped at $\pm 100\%$ if the mark is outside the line.*

### 3. Estimated Physical Units (`cm` / `inch`)
**WARNING:** These assume a standard browser density of **96 DPI**.
- **Inches**: $inch = \Delta px / 96$
- **Centimeters**: $cm = \Delta px / 37.795$
- *Physical accuracy varies by device. Use a physical ruler for calibration.*

### 4. Aggregate Statistics (Session Summary)
- **Signed Avg % (Directional Bias)**: $\frac{1}{N} \sum_{i=1}^N Error\%_i$. (Note: Left/Right errors can cancel out).
- **Absolute Avg % (Overall Accuracy)**: $\frac{1}{N} \sum_{i=1}^N |Error\%_i|$. Measures total precision.
- **Standard Deviation (Consistency)**: $\sigma = \sqrt{\frac{\sum (x_i - \bar{x})^2}{N}}$. Higher SD = higher variability/inattention.

---

## ⚙ Validation Logic (What makes a "Good Mark"?)

To maintain data integrity, a mark is only recorded if it passes these three filters:

1.  **Stroke Length Cap (200px)**: If a mark exceeds **200px**, it turns **Red** 🔴 and is discarded. This filters out random large swipes.
2.  **Intersection Check**: The user's stroke must physically cross the stimulus line.
3.  **Y-Tolerance (< 1.5px)**: The intersection must occur precisely on the line. Marks that are too high or too low are ignored.

---

## 📱 Technical Specifications & Scaling

The app uses **Smart Scaling** to ensure continuity if a tablet is rotated or resized.

| Device Model | Logical Width ($W_{px}$) | Hits 1200px Cap? | Est. Line Length ($L_{phys}$) |
| :--- | :--- | :--- | :--- |
| **iPad Pro 12.9"** | 1366 px | **YES** | **12.32 cm** |
| **iPad Air / Pro 11"** | ~1180 px | NO | **11.76 cm** |
| **iPad (10.2")** | 1080 px | NO | **11.90 cm** |
| **iPad Mini (8.3")** | 1133 px | NO | **9.28 cm** |

> *Scaling Formula: New $X = Old X \times (New Canvas W / Old Canvas W)$*

---

## 🧪 Usage & Export

1. **Setup**: Enter trials (e.g., 20). Randomized horizontal/vertical positioning.
2. **Task**: Instruct participant to mark the center with a short vertical tick.
3. **Export**: 
   - **Download CSV**: Full experimental data for external re-calculation.
   - **Download Pattern**: Visual audit PNG showing true center vs. user mark.

---

## ⚖ Ethical & Usage Notice
- **Clinical Use**: Must be supervised by a **licensed specialist**. This is a screening tool, not a diagnostic finality.
- **Required Citation**: If used in research or publication, you are **required** to cite this project.
- **Commercial Use**: Prohibited without written consent.

📧 **Contact**: [sdswat93@gmail.com](mailto:sdswat93@gmail.com)

---
**Project by:** *Zengin, M.*
