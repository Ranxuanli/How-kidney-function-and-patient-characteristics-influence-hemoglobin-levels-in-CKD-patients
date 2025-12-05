# How Kidney Function and Patient Characteristics Influence Hemoglobin Levels in CKD Patients

> Course project – Weill Cornell Medicine, Biostatistics & Data Science  
> Group 4: Ranxuan Li, Sinuo Lu, Yongxian Zhang

---

## 📌 Project Overview

This project investigates how kidney function, age, and hypertension influence hemoglobin levels among patients with chronic kidney disease (CKD).

Hemoglobin is a key indicator of CKD-related anemia, while serum creatinine is a core marker of renal dysfunction. Older adults tend to have both poorer kidney function and a higher prevalence of comorbidities such as hypertension, which complicates the interpretation of age–hemoglobin relationships.

**Main questions:**

1. Is kidney function significantly associated with hemoglobin?
2. Does age still matter after adjusting for kidney function?
3. Does hypertension modify this relationship and create a Simpson’s paradox?

---

## 📂 Repository Contents

| File | Description |
|------|-------------|
| `Complete R code.Rmd` | Full workflow: data cleaning, EDA, modeling, and plots |
| `EDA.Rmd` | Exploratory data analysis of kidney function and anemia markers |
| `linear Regression.Rmd` | Crude and adjusted linear regression models |
| `kidney_clean.csv` | Cleaned analysis dataset (∼400 patients, 24 variables) |
| `Final-ppt-pre-1201-final.pdf` | Final presentation slides |
| `How-kidney-function-and-patient-characteristics-influence-hemoglobin-levels-in-CKD-patients.Rproj` | RStudio project file |
| `.gitignore` | Git ignore rules for R / RStudio projects |

You can open the `.Rproj` file in RStudio to reproduce the analysis.

---

## 🧪 Data & Methods

### Data

- ~400 patient records with 24 demographic, laboratory, and clinical variables
- Key variables:
  - Kidney function: serum creatinine, blood urea, urine abnormalities
  - Hematology: hemoglobin, packed cell volume (PCV), anemia status
  - Comorbidities: hypertension, diabetes
  - Demographics: age, sex

### Cleaning steps (implemented in `Complete R code.Rmd`)

- Trim hidden spaces and convert blanks to `NA`
- Convert fake character numerics to proper numeric or factor types
- Impute:
  - Numeric variables → median
  - Categorical variables → mode
- Construct analysis dataset with age, kidney markers, hemoglobin, PCV, hypertension, diabetes, anemia, and CKD classification

### Statistical methods

- Exploratory data analysis (EDA)
  - Histograms, boxplots, and summary tables
  - Wilcoxon rank-sum tests for non-normal numeric variables
  - Chi-square tests for categorical variables (hypertension, diabetes, anemia, CKD)
- Correlation analysis
  - Correlation heatmap identifying clusters:
    - Renal dysfunction (creatinine, urea)
    - Anemia (hemoglobin, PCV)
    - Metabolic/diabetes-related markers
- Regression modeling
  - Crude model: `Hemoglobin ~ Age`
  - Adjusted model: `Hemoglobin ~ log(Creatinine) + Age`
  - Stratified models by hypertension status to illustrate Simpson’s paradox

---

## 🔍 Key Findings

### 1️⃣ Kidney function is the primary driver of hemoglobin

- Higher serum creatinine is strongly associated with lower hemoglobin.
- CKD patients show:
  - Higher creatinine and urea
  - Lower hemoglobin and PCV
- This pattern is consistent with impaired erythropoietin production in CKD.

### 2️⃣ The age effect is washed out after adjustment

- Crude model:  
  - Age has a small negative slope and a statistically significant p-value.
- Adjusted model:  
  - After controlling for log-creatinine, the age coefficient is near zero and non-significant.
  - Model fit is driven almost entirely by kidney function.

> Interpretation: the apparent effect of age on hemoglobin is largely explained by declining kidney function rather than age itself.

### 3️⃣ Hypertension creates a Simpson’s paradox

- In the crude analysis, older age appears associated with lower hemoglobin.
- After stratifying by hypertension:
  - Both hypertensive and non-hypertensive groups show a **positive** association between age and hemoglobin.
- The reversal occurs because:
  - Older patients are much more likely to have hypertension.
  - Hypertension itself is associated with lower hemoglobin.

> Hypertension both **confounds** and **modifies** the age–hemoglobin relationship, generating a Simpson’s paradox.

---

## 🩺 Clinical Interpretation

- Kidney dysfunction is the dominant determinant of anemia severity in CKD.
- Age-related declines in hemoglobin are mostly indirect, operating through poorer renal function and a higher burden of comorbidities.
- Hypertension must be accounted for when evaluating age-related anemia in CKD patients; otherwise, crude analyses can be misleading.

---

## 🔁 Reproducibility

To reproduce the analysis:

1. Open the `.Rproj` file in RStudio.
2. Install required R packages (e.g. `tidyverse`, `dplyr`, `ggplot2`, etc.).
3. Knit `Complete R code.Rmd` to generate the full report.

---


If you are working on CKD, anemia, or clinical modeling and would like to discuss methods or collaborate, feel free to reach out or open an issue.
