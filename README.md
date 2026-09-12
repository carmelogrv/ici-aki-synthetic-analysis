# ici-aki-synthetic-analysis
Python pipeline to generate synthetic clinical data and model the long-term effects of AKI on ICI-treated cancer patients in terms of survival and eGFR trajectories. 

## Data generation and Privacy
No real patient records are included in this repository. To ensure data privacy while maintaining a realistic clinical and demographic profile, the synthetic cohort is built entirely from scratch based on aggregated summary statistics extracted from the original cohort. Before extracting any percentages, data entry errors - in terms of registration dates or unrealistic clinical parameter values - were identified and corrected. 

## Clinical problem description
* **Context**: Immune checkpoint inhibitors (ICIs) have revolutionized the treatment of several types of solid malignancies, but they can trigger immune-related adverse events, including acute kidney injury (AKI).
* **Objective**: This pipeline evaluates the long-term prognostic impact of a single AKI episode on mortality and kidney function on a cohort of ICI-treated patients.

## Synthetic data generation 
**File**: `01_data_generation.ipynb`

This notebook generates a synthetic cohort mimicking the clinical features of 752 adult cancer patients. Specifically, the generated variables are:
* Baseline demographics (age, gender)
* Malignancy types (Melanoma, Lung, Urogenital, Other)
* Immunotherapy regimens (anti-CTLA-4, anti-PD-1, anti-PD-L1, dual blockade)
* Baseline serum creatinine (sCr) and AKI occurrence
* sCr values at discrete timestamps 

## Data analysis steps 
**File**: `02_data_analysis.ipynb`

1. **Exploratory Data Analysis**: visualization of variable distributions, along with sCr trends and statistical testing to compare the mortality/survival groups and the AKI/No AKI groups.
2. **Cox Model**: evaluation of the risk factors for AKI occurrence, the mortality risk associated with it, and the use of a time-varying Cox model to address immortal time bias and treat AKI as a dynamic covariate.
3. **Longitudinal Kidney Function Modeling**: after estimating the glomerular filtration rate through the CKD-EPI 2021 equation, the trajectories are analyzed using Linear Mixed-Effects Models (LMM) to account for both population-level trends and individual patient variability.
