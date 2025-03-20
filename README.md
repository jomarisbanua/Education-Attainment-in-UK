# Education-Attainment-in-UK
Data: https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2024/2024-01-23/english_education.csv

## I. Project Goals and Tasks
This repository contains an analysis of how growing up in a small town versus a large city influences educational success. The study explores the relationship between students' educational attainment—measured by high school and college graduation rates—and the demographics of their hometowns.

I was responsible for performing exploratory data analysis (EDA) to uncover key trends, conducting power analysis to ensure the reliability of statistical tests, and developing regression model to evaluate the predictive relationship between high school performance and college graduation rates.

The investigation was inspired by findings from the UK’s Office for National Statistics (ONS), which suggest that smaller towns may foster better academic outcomes. The dataset used in this study is derived from the Longitudinal Education Outcomes (LEO) database, containing anonymized information on students who completed their GCSEs in the 2012-2013 academic year. Ethical considerations were strictly followed to ensure privacy protection.

Key Research Areas:
- The impact of town size on high school and college graduation rates.
- The influence of income and demographic factors on educational outcomes.
- Statistical hypothesis testing to evaluate differences in graduation rates.

This repository includes data preprocessing scripts, statistical analysis, and visualization outputs used to assess the impact of hometown demographics on student success.

📌 Contributions and discussions are welcome!

## Data Cleaning and Preparation

**Variable Selection and Renaming:**  
- **Key Variables:** The dataset was refined to include important factors: `town11nm` (geographical identifier), `size_flag`, `income_flag`, `university_flag`, along with measures for high school graduation (GCSEs) and college graduation (`college_grad`).
- **Renaming and Format Adjustments:** Variables were renamed for clarity, and categorical variables (e.g., town size and income status) were converted into factors using **dplyr** and **forcats**.

**Collapsing Town Size Categories:**  
- The detailed town size classifications were consolidated into two categories: **Large** (comprising urban centers such as cities, large towns, and various London BUAs) and **Small** (small towns and similar areas). This decision was made to reduce noise and highlight key contrasts in urban versus rural-like environments.

**Exclusion of Irrelevant Variables:**  
- Non-essential variables, including those with incomplete or redundant information, were removed to maintain focus on the determinants of educational attainment.

## Exploratory Data Analysis (EDA)

The EDA phase involved creating a series of visualizations to explore data distributions and potential relationships:

- Town Size Distribution: Bar charts indicated a clear split between Large and Small towns. The frequency distribution confirmed that both categories were well-represented, ensuring reliable comparisons between urban centers and smaller communities. This balanced distribution supports further analyses by providing a robust grouping for evaluating differences in educational outcomes.

- Income Status Distribution: Visualizing income levels with a pastel color palette revealed varied socioeconomic profiles across the towns. The charts highlighted that many Large towns tend to have a higher proportion of lower-income areas, whereas Small towns showed a more diverse income status mix. This observation hints at an underlying association between town size and economic factors, which may influence educational performance.

- Graduation Rates Distributions: Histograms for both high school (GCSE) and college graduation rates uncovered important distribution characteristics. The high school graduation data appeared approximately normally distributed with only moderate skewness, suggesting consistency across towns. In contrast, the college graduation rates demonstrated a wider range and a greater spread, indicating more variability that might be linked to other socioeconomic or regional factors. Notable outliers in both distributions were flagged for further investigation, as they could represent exceptional cases or data quality issues.

- Summary Statistics: Grouped summary tables produced using gtsummary provided a concise quantitative comparison between Large and Small towns. The tables showed that while the average high school graduation rate was slightly higher in Small towns, the difference in college graduation rates was more pronounced. These differences, along with the corresponding standard deviations, provide a quantitative basis for further hypothesis testing and suggest that town size might be an influential factor in educational outcomes.

## Data Analysis and Hypothesis Testing

Four main tests were performed to address the research questions:

### Test 1: High School Graduation Rates (Small vs. Large Towns)
- **Objective:** To determine whether a statistically significant difference exists between the high school graduation rates of small and large towns.
- **Method:** A two-sample t-test was conducted after checking assumptions of independence, normality, and adequate sample size.  
- **Results:**  
  - A statistically significant difference was observed (p-value < 0.05).
  - The effect size (Cohen's d) was relatively small, suggesting that while differences exist, they may be subtle.
  - Power analysis indicated a sufficient sample size to detect this difference.

### Test 2: College Graduation Rates (Small vs. Large Towns)
- **Objective:** To evaluate whether college graduation rates differ significantly between small and large towns.
- **Method:** A similar two-sample t-test was used along with effect size estimation and power analysis.
- **Results:**  
  - The t-test revealed a highly significant difference (p-value < 0.05).
  - A larger effect size was found compared to high school graduation, indicating a more pronounced difference in college graduation rates.
  - The power analysis confirmed that the test was well-powered.

### Test 3: Association Between Income and Town Size
- **Objective:** To assess whether income levels and town size are associated.
- **Method:** A Chi-squared test of independence was applied to the contingency table of income status and town size, and Cramér's V was calculated to measure effect size.
- **Results:**  
  - The Chi-squared test produced a significant result (p-value < 2.2e-16), leading to the rejection of the null hypothesis of independence.
  - The computed Cramér's V indicates a moderate association between income levels and town size.

### Test 4: Predictive Relationship Between High School and College Graduation Rates
- **Objective:** To investigate if high school graduation rates (GCSEs) can predict college graduation rates.
- **Method:** Linear regression was used, and assumptions (linearity, independence, constant variance, and normality of residuals) were validated.  
- **Results:**  
  - The model showed a strong linear relationship, with an R-squared of approximately 0.598. This indicates that nearly 60% of the variation in college graduation rates can be explained by high school performance.
  - The regression coefficients were statistically significant, and the overall model was robust, as confirmed by power analysis.

## Power Analysis Discussion

Power analysis was conducted to ensure that statistical tests had sufficient sensitivity to detect meaningful differences in educational outcomes. Given the structured comparisons between town sizes and graduation rates, as well as the association between income levels and town size, the power analysis helped confirm that the sample size was adequate for drawing reliable conclusions.

### **1. Power Analysis for High School Graduation Rate Differences (Small vs. Large Towns)**
- A two-sample t-test was planned to compare mean GCSE scores between Small and Large towns.
- To assess the **effect size**, Cohen’s *d* was calculated using the pooled standard deviation of both groups.
- The power of the test was computed using `pwr.t.test()`, ensuring that the sample size was large enough to detect a true difference if one existed.
- **Findings:**  
  - The observed effect size was small but statistically significant.
  - The computed power was **above 0.78**, suggesting a reasonable probability of detecting a real effect.

### **2. Power Analysis for College Graduation Rate Differences**
- Given the observed variability in college graduation rates, another power analysis was performed for this comparison.
- The effect size was larger than that of high school graduation rates, indicating a stronger difference between Small and Large towns.
- The power was computed similarly using `pwr.t.test()`, and results showed **power > 0.99**, meaning a very high likelihood of correctly rejecting the null hypothesis if a true difference existed.

### **3. Power Analysis for Chi-Square Test (Income vs. Town Size)**
- Since income levels were categorized, a **Chi-squared test of independence** was conducted to examine whether income status was associated with town size.
- Power analysis for the Chi-squared test was performed using `pwr.chisq.test()`, leveraging **Cramér’s V** as a measure of effect size.
- **Findings:**
  - The observed effect size was moderate.
  - The computed power was **near 1**, confirming that the dataset had more than enough observations to detect an association if one was present.

### **4. Power Analysis for Regression: GCSEs as a Predictor of College Graduation Rates**
- For the linear regression model predicting college graduation rates from high school graduation rates, **Cohen’s f²** was used to assess effect size.
- The power of the regression model was calculated using `pwr.f2.test()`, based on the R-squared value from the fitted model.
- **Findings:**
  - With an R-squared of **0.598**, the effect size was strong.
  - The computed power was **1.00**, confirming that the model was well-powered to detect a relationship.

### **Overall Implications**
The power analysis results supported the robustness of the statistical tests, ensuring that the study’s conclusions were not driven by chance or inadequate sample sizes. The findings indicated that:
- The t-tests were sufficiently powered, particularly for college graduation rates.
- The chi-squared test was highly reliable in detecting associations.
- The regression model was well-calibrated with strong predictive power.
- 
## Technical Details

**Languages and Tools:**  
- **R:** The entire analysis was conducted using R.
- **Key Libraries:**  
  - **dplyr:** For data manipulation and cleaning.
  - **forcats:** For handling factor levels and collapsing categories.
  - **ggplot2:** For creating visualizations.
  - **gtsummary:** For generating summary tables.
  - **pwr:** For performing power analyses.
  - **scales:** For formatting visualizations.

**Project Execution:**  
- The interactive visualizations and analyses were compiled into an HTML dashboard for easy dissemination and stakeholder engagement.  
- The code is well-documented, ensuring that the decisions made during data preparation and analysis are clear and reproducible.

## Conclusion

The analysis revealed significant differences in educational outcomes between small and large towns. Specifically:
- High school graduation rates differ modestly between town types, while college graduation rates show a more marked difference.
- There is a moderate association between town size and income status, underlining the influence of socioeconomic factors.
- High school performance is a strong predictor of college graduation rates, highlighting the importance of early educational achievement.

These insights provide a foundation for further research and may inform targeted interventions to address educational disparities across different regions.

## Future Directions

- **Granular Analysis:** Future work may incorporate more detailed, school-level data.
- **Longitudinal Study:** Extending the analysis over multiple years to observe trends.
- **Additional Variables:** Including other socioeconomic indicators to further understand their impact on educational outcomes.

---

This documentation aims to provide a clear, methodical account of the analytical process, decisions, and results for the project on educational attainment in the UK.
