# Framingham-Dataset-Analysis-in-Stata
Framingham Dataset Analysis
Author: Rudolph Mensah, assisted by Grok, created by xAI

Date: June 11, 2025

Overview
This repository contains the code, data, and results for a comprehensive analysis of the Framingham Heart Study dataset, focusing on cardiovascular risk factors and their association with cardiovascular disease (CVD) and mortality. The analysis was conducted using Stata, with descriptive statistics, visualizations, and regression models to identify key risk factors.

Dataset Description
The dataset (Frammingham heart study_CSV.csv) includes 95 observations and 17 variables related to cardiovascular health:

Continuous Variables: age (years), bmi (Body Mass Index), diabp (diastolic blood pressure, mmHg), glucose (mg/dL), heartrte (heart rate, bpm), sysbp (systolic blood pressure, mmHg), totchol (total cholesterol, mg/dL).
Categorical/Binary Variables: cursmoke (0=No, 1=Yes), cvd (0=No, 1=Yes), death (0=No, 1=Yes), diabetes (0=No, 1=Yes), educ (education level, 1–4), hyperten (0=No, 1=Yes), sex (1=Female, 2=Male), stroke (0=No, 1=Yes).
Other Variables: period (study period, constant at 1), randid (unique identifier).
Missing Data:

educ: 2 missing values.
glucose: 9 missing values.
totchol: 4 missing values.
Analysis
The analysis was performed using the Stata script Frammingham Heart Study.do and includes:

Data Management: Labeling variables and checking for missing data.
Descriptive Statistics: Summary statistics for continuous variables and frequency tables for categorical variables.
Visualizations:
Histogram of age (age_histogram.gph).
Box plot of systolic BP by sex (sysbp_sex_boxplot.gph).
Scatter plot of BMI vs. total cholesterol (bmi_totchol_scatter.gph).
Regression Analysis:
Logistic regression to model CVD risk.
Cox proportional hazards model for mortality (noted issue: period is constant, invalidating the model).
Output: Results are logged in Framingham_Analysis.log.
Key Findings
Descriptive Statistics:
Mean age: 51.0 years (SD = 9.2, range: 35–69).
Mean BMI: 25.7 (SD = 3.3), near overweight threshold.
Mean systolic BP: 133.7 mmHg (SD = 22.5), indicating elevated BP.
Mean cholesterol: 241.5 mg/dL (SD = 44.9), suggesting high cholesterol levels.
Prevalence: 31.6% with CVD, 40.0% mortality, 69.5% with hypertension, 45.3% smokers, 5.3% with diabetes, 10.5% with stroke.
Sex: 52.6% male, 47.4% female.
Logistic Regression (CVD):
Significant predictors:
Total cholesterol (OR = 1.017, p = 0.016): Each 1 mg/dL increase raises CVD odds by 1.7%.
Sex (Male vs. Female, OR = 0.166, p = 0.007): Males have 83% lower odds of CVD, which is unexpected and may indicate coding issues or confounding.
Non-significant: Age, BMI, smoking, diabetes, hypertension, systolic BP, education.
Model fit: Pseudo R² = 0.2326, p = 0.0062 (n=89).
Cox Regression (Mortality):
Significant predictor: Age (HR = 1.074, p = 0.001), each year increases mortality hazard by 7.4%.
Non-significant: BMI, smoking, diabetes, hypertension, systolic BP, cholesterol, sex, education.
Issue: period = 1 for all observations, invalidating the Cox model. A logistic regression for death is recommended.
Visualizations:
Age histogram shows a slightly right-skewed distribution.
Systolic BP box plot likely indicates higher BP in males.
BMI vs. cholesterol scatter plot suggests a weak positive correlation.
Issues and Recommendations
Missing outreg2: The outreg2 command failed due to the package not being installed. Run ssc install outreg2 in Stata to generate cvd_logistic_results.txt and death_cox_results.txt.
Cox Model Issue: The period variable is constant (1), making the Cox regression inappropriate. Consider replacing with logistic regression for death:
stata
