# <p align="center">Hospital Readmission Risk Analysis</p>
# <p align="center">![Pic](https://cdn-icons-png.flaticon.com/512/1802/1802511.png)</p>

## Business Problem: 
Hospitals face financial penalties when patients are readmitted within 30 days of leaving the hospital. This project looks at 10 years of data from 130 U.S. hospitals to find which patients, diagnoses, and care patterns are linked to a higher risk of readmission. The goal is to help care teams identify high-risk patients, focus follow-up resources, and prevent avoidable readmissions.


## Data & Tools:
- **Dataset**: Diabetes 130-US Hospitals for Years 1999-2008 (UCI Machine Learning Repository, CC BY 4.0). ~100,000 patient encounters across 130 hospitals, 1999-2008
- **Database**: MySQL Workbench
- **Techniques Used**: CTEs, Window Functions (RANK, NTILE), CASE-based risk tiering, correlated subqueries, and multi-table joins

## Approach/Methodology
- **Cleaning**: Replaced placeholder missing values with NULLS, removed a column with about 97% missing data, kept only one encounter per patient to avoid duplicate bias, and removed patients who were inactive or were discharged to hospice
- **Exploratory analysis**: Established baseline readmission rates by age, admission type, and diagnosis category.
- **Advanced analysis**: Built a reusable high-risk patient group with a CTE, applied window function to rank patients by risk, grouped them by medication use and number of diagnoses, and found diagnosis categories with above average readmission rates.
- **Findings**: Summarized the results into four key findings that connect back to the main business problem.

## Key SQL Techniques Used
- CTEs to stage a clean, reusable risk cohort across multiple queries
- Window functions: RANK() OVER (PARTITION BY) to rank medication burden within age groups, NTILE(4) to build risk quartiles
- CASE-based tiering to convert continuous variables into business-readable risk categories
- Correlated subqueries with HAVING to isolate diagnosis categories performing above the population-wide average
- Multi-table joins against ID-mapping reference tables to convert numeric codes into readable labels

## Findings
1. **Circulatory and diabetes diagnoses** had the **highest readmission rates** among all diagnosis categories, and both exceeded the average readmission rate.
2. Patients with **more prior inpatient visits** in the prior year showed a substantially elevated readmission risk, supporting prior-utilization as a strong predictive signal.
3. **Discharge disposition mattered significantly**. Patients discharged to certain facility types showed measurably different readmission rates than those discharged home.
4. Findings around **medication changes at discharge and A1C testing** during the stay both align with the original clinical research question this dataset was collected to investigate.

## Recommendations
- Focus discharge planning and follow-up on patients with the highest risk based on past hospital visits.
- Give extra care coordination to patients with heart/circulatory conditions and diabetes, given they have higher readmission rates.
- Review discharge processes at facilities with high readmission rates to find areas that could be improved.
