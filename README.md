# Line Bisection Test (LBT)

This repository contains the **Computerized Line Bisection Test (cLBT)** — a browser-based assessment tool used to measure visuospatial attention, perceptual biases, and motor accuracy.  
It is commonly used in neurological and neuropsychological research, including studies involving stroke, spatial neglect, and related conditions.

<div align="center">

## 🚀 [CLICK HERE TO START TEST](https://sd-devsecops.github.io/Line-Bisection-Test/cblt.html)
**https://sd-devsecops.github.io/Line-Bisection-Test/cblt.html**

</div>

---

## 📌 Overview

The test displays horizontal lines on an interactive canvas.  
For each trial, the participant marks what they believe is the **center** of the line.

The system automatically records:

- Signed bisection error (negative = leftward bias, positive = rightward bias)  
- Absolute error  
- Standard deviation  
- Closest and farthest marks  
- Summary statistics across all trials  
- CSV export including full data and participant demographics

A researcher can **set the number of lines at the beginning**, allowing flexibility for different study protocols.

---

## ⚙ Technical Specifications

### Stimulus Sizing
To ensuring clinical validity across different screen sizes, the tool uses a dynamic rendering engine:

- **1200px Clinical Cap**: On large devices (like the iPad Pro 12.9"), the canvas scales up to 1200 logical pixels, creating a stimulus line >12cm.
- **Universal Scaling**: On smaller devices, the stimulus adheres to a standard visual angle (approx 47.5% of the physical screen width).

### Mobile Data Safety
The tool features **Smart Resize Protection**. If a patient rotates the tablet or the browser address bar toggles during active testing:
- The test does **NOT** reset.
- The stimulus line and all user marks are **mathematically scaled** to the new dimensions accurately.
- This prevents "moving goalposts" and ensures no data is lost during handling.

### Device Sizing Reference Table

| Device Model | Logical Width ($W_{px}$) | Physical Width ($W_{phys}$) | Hits 1200px Cap? | Line Length ($L_{phys}$) |
| :--- | :--- | :--- | :--- | :--- |
| **iPad Pro 12.9"** | 1366 px | 28.06 cm | **YES** | **12.32 cm** |
| **iPad Pro 11"** | 1194 px | 24.76 cm | NO | **11.76 cm** |
| **iPad Air (10.9")** | 1180 px | 24.76 cm | NO | **11.76 cm** |
| **iPad (10.2")** | 1080 px | 25.06 cm | NO | **11.90 cm** |
| **iPad Mini (8.3")** | 1133 px | 19.54 cm | NO | **9.28 cm** |

> *Note: The iPad Mini is the only modern Apple tablet that falls slightly below the 10cm threshold using this formula.*

---

## 🌐 Cross-Platform Use

The cLBT runs entirely in a web browser — no installation required.

- **Desktop:** use mouse clicks  
- **Mobile / iPad:** use touchscreen taps (native scrolling is blocked for precision)
- Fully responsive layout  
- Live errors/stats are placed far below the test area to avoid influencing performance

---

## 🧪 How to Use

1. **Setup**: Enter the desired number of trials (e.g., 20, 50, 100).
2. **Controls**:
   - **Reset**: Restart the current session with fresh random seed.
   - **Finish**: End test early and calculate results instantly.
   - **Main Menu**: Return to setup screen.
3. **Task**: Tap/Click the perceived midpoint of the line.
4. **Export**: 
   - Enter Name/Surname/Age.
   - Press **Download CSV** to analyze the full dataset.

---

## ⚠ Research Validity Notice

The built-in statistical calculations (mean, SD, etc.) are **not independently validated**.  
**Do not rely solely on internal calculations for clinical or research conclusions.**  
Always verify results using your own analysis pipeline.

---

## 📁 Repository Contents

- **`cblt.html`** (or `line_bisection.html`) – Full test interface + JavaScript logic  
- **`README.md`** – Documentation

---

## ⚖ License
This project is open-source for **research**, **educational**, and **clinical development** purposes.

---

## 📚 **Required Citation**

If you use this tool in **research**, **clinical evaluation**, **academic studies**, or **publications**,  
you are **required to cite** the project to acknowledge its use and support continued development.

Please use the following provisional citation:
> For citation inquiries or academic use, contact: **sdswat93@gmail.com**

---

## ⚠ Ethical & Usage Disclaimer

To ensure responsible and ethical use, the following conditions apply:

### 🏥 Clinical Use
- This tool **does not replace** standardized or professionally validated diagnostic instruments.  
- Interpretation must only be performed by a **licensed clinician**, **neuropsychologist**, or a **qualified specialist**.  
- All assessment outcomes must be **independently verified** before being used in any clinical or medical decision-making.  
- Users must obtain **informed consent** from participants and appropriate **ethical approval** for all human-subject testing.

### 🔬 Research Use
Researchers using this tool must:
- Obtain **IRB / Ethics Committee approval** where required  
- Follow local and international data protection regulations (e.g., **GDPR**, **HIPAA**)  
- Properly **cite this project** in publications  

### 💼 Commercial Use
Commercial use of this software is **not permitted** without **explicit written authorization** from the project author.

For licensing discussions, institutional deployment, or collaboration requests, contact:
📧 **sdswat93@gmail.com**

---

### ✅ User Agreement
By using this tool, you agree to:
- Follow all ethical guidelines listed above  
- Obtain all required permissions  
- Use the results responsibly within the limits of the tool  

Failure to follow these terms may result in misuse and invalidation of collected data.

---

**Project by:** *Zengin, M.*
