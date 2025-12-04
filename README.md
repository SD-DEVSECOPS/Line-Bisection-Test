# Line Bisection Test (cLBT)

This repository contains the **Computerized Line Bisection Test (cLBT)** — a web-based tool designed to assess visuospatial attention and motor function. The test is commonly used in clinical research and neurology, including studies related to Parkinson’s disease and other neurological conditions.

---

## Overview

The Line Bisection Test presents users with horizontal lines on a canvas. The participant's task is to mark the **perceived midpoint** of each line. The software records:

- The **bisection errors** for each trial (positive or negative deviation from the true midpoint).  
- **Detailed statistics** including average error, standard deviation, closest mark, and biggest miss.  
- Final results can be downloaded as a **CSV file** for further analysis, including user demographics and error breakdown.

**Important:** The built-in statistics have **not been independently validated**. Do **not** rely solely on them for research conclusions — always verify calculations independently.

This tool is designed to be **cross-platform**:

- **Desktop**: Use a mouse to mark the line.  
- **Mobile/iPad**: Use touch gestures to mark the line.

---

## How to Use

1. Open the test in a modern browser:  
   [https://sd-devsecops.github.io/Line-Bisection-Test/cblt.html](https://sd-devsecops.github.io/Line-Bisection-Test/cblt.html)  

2. Draw a line to indicate the midpoint of the horizontal line.  

3. After completing the predefined number of trials (default: 100), a form will appear to enter:
   - Name
   - Surname
   - Age
   - Years with Parkinson's (if applicable)

4. Click **Download CSV** to save the results for analysis. The file name will automatically include the user’s details.  

---

## Features

- Responsive design for both desktop and mobile devices.  
- Tracks per-draw errors and calculates summary statistics.  
- Exports results in CSV format, including user info and detailed statistics.  
- Prevents invalid input and ensures accurate recording of user responses.  

---

## Repository Structure

- `cblt.html` – The main HTML/JS file containing the test interface and logic.  
- `README.md` – Project documentation.  

---

## License

This project is open-source and available for research and educational purposes.  

---

**Caution:** Always verify the recorded errors and statistics independently before using them in any clinical or research context.

**Note:** For clinical studies, ensure proper ethical approvals and patient consent before data collection.

