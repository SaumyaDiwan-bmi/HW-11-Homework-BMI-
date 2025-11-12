# BMI HW 11
Model Based Machine Learning
- Saumya Diwan
- Email: saumya.diwan@emory.edu
- Question Number 3: Model-based Bias Removal in Machine Learning using Synthetic Blood Pressure Data

**Disclaimer:** **ChatGPT 5.1** was used to complete **HW3 [A ii]** to identify the library and function used for general curve fitting, its syntax, generating initial parameter estimates, and checking convergence and in **HW 3 [Bi]** to outline the steps used to generate data when given the mean, standard deviation, and correlation of variables. It was further used to convert results to tables in Markdown Format here

# Key Insights
## A 
### ii 
Data from the reference preprint ([https://arxiv.org/pdf/2402.01598]) was taken class marks for the Age brackets were generated in a separate column (Age_class_mark))
| Age   | Number    | %    | mean_SBP | std_SBP | mean_DBP | std_DBP | rho_SBP_DBP | Age_class_mark |
| ----- | --------- | ---- | -------- | ------- | -------- | ------- | ----------- | -------------- |
| <20   | 193631    | 3.6  | 115.05   | 13.65   | 69.80    | 8.90    | 0.61        | 10.0           |
| 20–29 | 547023    | 10.3 | 121.27   | 14.19   | 74.27    | 9.60    | 0.66        | 24.5           |
| 30–39 | 674798    | 12.7 | 123.79   | 15.91   | 77.31    | 10.48   | 0.74        | 34.5           |
| 40–49 | 806952    | 15.2 | 127.32   | 16.93   | 79.36    | 10.46   | 0.73        | 44.5           |
| 50–59 | 984094    | 18.5 | 129.98   | 17.19   | 79.05    | 9.88    | 0.67        | 54.5           |
| 60–69 | 1,012,979 | 19.1 | 132.42   | 17.13   | 76.71    | 9.38    | 0.58        | 64.5           |
| 70–79 | 732,165   | 13.8 | 134.62   | 17.36   | 74.06    | 9.11    | 0.52        | 74.5           |
| 80–89 | 305,157   | 5.7  | 136.89   | 18.35   | 71.56    | 9.22    | 0.49        | 84.5           |
| ≥90   | 60,637    | 1.1  | 138.11   | 19.59   | 69.86    | 9.44    | 0.50        | 95.0           |

### iii
Quantitative Evaluation of Model Fit: The Mean Squared Error (MSE) and R-squared (R^2) metrics were computed and are displayed in the table below. The model curves for SBP and DBP can be found here ([https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/SBP_DBP_model_comparision.png])

| Model          | MSE      | R²       |
| -------------- | -------- | -------- |
| Polynomial SBP | 0.065030 | 0.998764 |
| Polynomial DBP | 0.897586 | 0.926137 |
| Sigmoid SBP    | 0.065419 | 0.998757 |
| Gaussian DBP   | 0.800747 | 0.934106 |
### iv
Interpretation of Model Parameters: 
For the polynomial model, 
-c1 and d1 (curvature coefficients) reflect the rate of change of slope with age (Physical dimension:mmHg/year^2). Both neagtive with 
-c2 and d2 (linear coefficients) reflect the linear change of slope with age (Physical dimension:mmHg/year)
-c3 and d3 (intercept terms) reflect the baseline BP at age = 0 (Physical dimension:mmHg) 
For the sigmoidal-Gaussian model
–Smax reflects the Maximum Systolic Blood Pressure which would be the upper plateau (Physical dimension:mmHg/year^2)
–a0: reflects the age at which SBP reaches half-maximum.(Physical dimension: year)
–Dmax reflects the maximum Diastolic Blood Pressure around middle age.(Physical dimension:mmHg)
–apeak reflects the age of peak DBP.(Physical dimension: year)
–σ reflects the spread of the Gaussian curve for DBP.(Physical dimension:year)
The Coefficient Values are displayed in the Table below for the polynomial, sigmoid and gaussian model functions. 

| Coefficient | Value      |
| ----------- | ---------- |
| **c1**      | -0.001532  |
| **c2**      | 0.431291   |
| **c3**      | 111.083788 |
| **d1**      | -0.004983  |
| **d2**      | 0.505025   |
| **d3**      | 65.479662  |
| **Smax**    | 148.910538 |
| **k**       | 0.015761   |
| **a0**      | -67.937007 |
| **Dmax**    | 78.372481  |
| **apeak**   | 50.569448  |
| **sigma**   | 85.573570  |

### v 
Discussion and Analysis 
i. Which model captures age trends in SBP and DBP better? 
ii. How do model parameters reflect physiological blood pressure changes with age?
iii. Discuss limitations in capturing demographic nuances.


## B
### i:
- Synthetic Data Generated for Systolic Blood Pressure colored by Male and Female labels ([HW-11-Homework-BMI-/Synthetic SBP data generated.png](https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/Synthetic%20SBP%20data%20generated.png)) 
- Synthetic Data Generated for Diastolic Blood Pressure colored by Male and Female labels ([HW-11-Homework-BMI-/Synthetic DBP data generated.png](https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/Synthetic%20DBP%20data%20generated.png))
- Note: The mean SBP is centered around 130 mmHg and mean DBP is centered around 75 mmHg
ii:
-Data was split into training (80%) and testing (20%)
-Logistic Regression Model was chosen 
-Initially experimentation was done with (https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/ROC%20curve%20initial%20with%20sex%20stratification.png) and without (https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/ROC%20curve%20initial%20without%20sex%20stratification.png ) stratification based on sex while data was split to note if there is affect in performance

| Metric               | **Without Stratification**       | **With Stratification**          |
| -------------------- | -------------------------------- | -------------------------------- |
| **Accuracy**         | 0.58675                          | 0.58085                          |
| **F1 Score**         | 0.58603                          | 0.58296                          |
| **ROC AUC**          | 0.62262                          | 0.61276                          |
| **Confusion Matrix** | [[5885, 4193],<br> [4072, 5850]] | [[5758, 4242],<br> [4141, 5859]] |

Here only a marginal drop in performance (in all metrics) was noted. Further  

- 



# References and further reading:
1. https://arxiv.org/pdf/2306.08451.pdf
2. https://arxiv.org/pdf/2402.01598
3. https://doi.org/10.1016/j.jelectrocard.2022.07.007

