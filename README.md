# Line Bisection Test (LBT)

This repository contains the **Computerized Line Bisection Test (cLBT)** — a browser-based assessment tool used to measure visuospatial attention, perceptual biases, and motor accuracy.  
It is commonly used in neurological and neuropsychological research, including studies involving stroke, spatial neglect, and related conditions.

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

A researcher can **set the number of trials at the beginning**, allowing flexibility for different study protocols.

---

## ⚠ Research Validity Notice

The built-in statistical calculations (mean, SD, etc.) are **not independently validated**.  
**Do not rely solely on internal calculations for clinical or research conclusions.**  
Always verify results using your own analysis pipeline.

---

## 🌐 Cross-Platform Use

The cLBT runs entirely in a web browser — no installation required.

- **Desktop:** use mouse clicks  
- **Mobile / iPad:** use touchscreen taps  
- Fully responsive layout  
- Canvas area enlarged for better visibility on phones and tablets  
- Live errors/stats are placed far below the test area to avoid influencing performance

---

## 🧪 How to Use

1. Open the test at:

   **https://sd-devsecops.github.io/Line-Bisection-Test/cblt.html**

2. When prompted, enter the number of trials (e.g., 50, 100, 150).

3. For each line:
   - Tap or click the perceived midpoint.

4. When all trials are completed:
   - A form will appear requesting:
     - Name  
     - Surname  
     - Age

5. Press **Download CSV** to save results.  
   The file includes:
   - All trial errors  
   - Signed/absolute deviations  
   - Mean error  
   - Standard deviation  
   - Positive/negative error counts  
   - Closest mark  
   - Biggest miss  
   - Demographic metadata

---

## ✨ Features

- Researcher-defined number of trials  
- Automatically disables drawing after the final trial  
- Large responsive canvas for mobile/iPad usability  
- Statistics displayed far below test area (reduces user influence)  
- CSV export with all metrics and demographic info  
- No external libraries required  
- Fully offline capable (works without internet once loaded)

---

## 📁 Repository Contents

- **`cblt.html`** – Full test interface + JavaScript logic  
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

This software is provided for **research**, **educational**, and **clinical development** purposes.  
To ensure responsible and ethical use, the following conditions apply:

---

### 🏥 Clinical Use

- This tool **does not replace** standardized or professionally validated diagnostic instruments.  
- Interpretation must only be performed by a **licensed clinician**, **neuropsychologist**, or a **qualified specialist**.  
- All assessment outcomes must be **independently verified** before being used in any clinical or medical decision-making.  
- Users must obtain **informed consent** from participants and appropriate **ethical approval** for all human-subject testing.

---

### 🔬 Research Use

Researchers using this tool must:

- Obtain **IRB / Ethics Committee approval** where required  
- Follow local and international data protection regulations (e.g., **GDPR**, **HIPAA**)  
- Properly **cite this project** in publications, reports, or presentations  
- Ensure that data collection and storage follow recognized scientific and ethical standards  

---

### 💼 Commercial Use

Commercial use of this software is **not permitted** without **explicit written authorization** from the project author.

For licensing discussions, institutional deployment, or collaboration requests, contact:

📧 **sdswat93@gmail.com**

---

### ⚖ Liability

This software is provided **“as is”**, without any warranties, guarantees, or certifications.  
The authors and contributors assume **no responsibility** for:

- Misuse or misinterpretation  
- Diagnostic mistakes  
- Data corruption or loss  
- Any direct or indirect damages arising from its use  

---

### ✅ User Agreement

By using this tool, you agree to:

- Follow all ethical guidelines listed above  
- Obtain all required permissions  
- Properly cite the software where relevant  
- Use the results responsibly within the limits of the tool  

Failure to follow these terms may result in misuse and invalidation of collected data.

---


---


**Project by:** *Zengin, M.*  
**Enhanced by:** *ChatGPT*

