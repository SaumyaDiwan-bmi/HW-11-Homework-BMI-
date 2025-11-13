# BMI HW 11
Model Based Machine Learning
- Saumya Diwan
- Email: saumya.diwan@emory.edu
- Question Number 3: Model-based Bias Removal in Machine Learning using Synthetic Blood Pressure Data

**Disclaimer:** **ChatGPT 5.1** was used to complete **HW3 [A ii]** to identify the library and function used for general curve fitting, its syntax, generating initial parameter estimates, and checking convergence and in **HW 3 [Bi]** to outline the steps used to generate data when given the mean, standard deviation, and correlation of variables and in **HW 3 [Bii.ii]** to generate an ROC curve with inset (since originally plots were unclear as they got superimposed due to similar performance) and line graph for performance drop accross different MF ratios It was further used to convert some results to tables in Markdown Format here

All codes for the assignment can be found here ([https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/BMI_Week_11_notebook_Saumya_Diwan_final.ipynb])

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
- For the polynomial model,
- - c1 and d1 (curvature coefficients) reflects the rate of change of slope with age (Physical dimension:mmHg/year^2) 
- c2 and d2 (linear coefficients) reflect the linear change of slope with age (Physical dimension:mmHg/year)
- c3 and d3 (intercept terms) reflect the baseline BP at age = 0 (Physical dimension:mmHg) 
For the sigmoidal-Gaussian model
– Smax reflects the Maximum Systolic Blood Pressure which would be the upper plateau (Physical dimension:mmHg)
– a0: reflects the age at which SBP reaches half-maximum which would be Smax/2.(Physical dimension: year)
– Dmax reflects the maximum Diastolic Blood Pressure around middle age.(Physical dimension:mmHg)
– apeak reflects the age of peak DBP which would be at Dmax.(Physical dimension: year)
– σ reflects the spread of the Gaussian curve for DBP.(Physical dimension:year)
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
For SBP, both Polynomial and Sigmoid models perform extremely well MSE = 0.065030,0.065419 , and R^2 = 0.998764,0.998757 respectively. The polynomical model performing seems to perform slightly better. Physiologcially sigmoid makes more sense as it shows slight curvature and which leads to a plateau, which is what is noted in SBP trends where it intially increases but stabilizes in adults. For DBP, both Polynomial and Gaussian models perform extremely well MSE = 0.897586,0.800747 , and R^2 = 0.926137,0.934106 respectively. The Gaussian model performing seems to perform better. This shows that a gaussian distribution suits DBP trends more where it first increases till around around the 55 years of age and then decrease after as one ages further

- ii. How do model parameters reflect physiological blood pressure changes with age?
- Physiological Interpretation of Model Parameters: 
- For the polynomial model, 
- c1 and d1 (curvature coefficients): here low negative c1 shows increase of BP with age with slight curvature as it gradually increases with age and negative d1 shows similar increase and then decrease later. The increase and decrease are gradual and curve is concave
- c2 and d2 (linear coefficients) reflect the linear change of slope with age and are postive here showing the postive change in BP initially
- c3 and d3 (intercept terms) reflect the baseline BP at age = 0. These seem to be extrapolated backward values. However might not be the best estimate 
For the sigmoidal-Gaussian model
– Smax reflects the Maximum Systolic Blood Pressure which would be the upper plateau. This is the SBP (Here 148.910538 mmHg) one has around mid life around 55 years of age after which it plateaus
– a0: reflects the age at which SBP reaches half-maximum which would be Smax/2. After this the increase would slow down and move towards plateauing 
– Dmax reflects the maximum Diastolic Blood Pressure around middle age.This is the BBP one has around mid life around 55 years of age after which it starts decreases 
– apeak reflects the age of peak DBP which would be at Dmax.This is the age where DBP is maximum after which it wouls start decreasing
– σ reflects the how the distribution of DBP is across the ages. If this value is large here 85.573570 years it would signify slow increase and decrease in the DBP
- iii. Discuss limitations in capturing demographic nuances.
- Here in the Gaussian model a0 parameter is getting pushed towards high negative value. More parameters seem to be required for a more accurate fit.
- Here I used class marks of the age brackets which reduces the nuances of the values in teh distributions
- The functions are not fully generalizable
- No subgroup analysis has been performed to capture nuances based on sex, race, ethnicity, BMI, comorbidities as well as external exposure factors



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

Here only a marginal drop in performance (in all metrics) was noted. Further on different Male: Female ratios (0.1,0.2,0.3,0.4,0.5,0.6,0.7,0.8,0.9) were tested (Results in the following table). The strategy followed here was that to keep the test set unchanged to prevent data leakge and just subsampling the train dataset with different ratios for M:F. Also we used stratification while the initial split the test set is balanced so we can note the change in performance when training set is skewed. The ROC curves can be found here ([https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/ROC%20Curves%20for%20different%20ratios.png]). 

|   Male-Female Ratio |   Accuracy |   F1 score |     AUC |
|--------------------:|-----------:|-----------:|--------:|
|                 0.1 |    0.5     | 0          | 0.5     |
|                 0.2 |    0.50005 | 0.00039988 | 0.50005 |
|                 0.3 |    0.50645 | 0.0476604  | 0.50645 |
|                 0.4 |    0.5485  | 0.319107   | 0.5485  |
|                 0.5 |    0.58275 | 0.585012   | 0.58275 |
|                 0.6 |    0.5542  | 0.665441   | 0.5542  |
|                 0.7 |    0.5131  | 0.670368   | 0.5131  |
|                 0.8 |    0.50045 | 0.666867   | 0.50045 |
|                 0.9 |    0.5     | 0.666667   | 0.5     |

- The line graph ([https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/Performance%20drift%20with%20differetn%20MF%20ratios.png]) showcases that at ratios closer to 0.1 ie where males less represented the F1 score is very low. Accuracy and AUC are also around chance or 0.5. However as the data balances out ie ratio closer to F1 score starts increasing and so do Accuracy and AUC after 0.3 upto 0.5 after which they both drop. The F1 score seems to keep increasing ever after that (that seems to showcase increase in confident false positives). The major potential bias is that model only trains to recognize one sex over the other. So while its performance to identify once sex might be high it isnt generalizable. Here it is just sex identification however in cases where other clinical endpoints are being looked at, model might only be able to perform well for one sex which was prevalent in the training set
### iii
-Balanced datasets are extremeley important

### iv
-Added in bias mitigation by using class weight as balanced in the model so that the model doesnt get influenced by the prevalence of one sex over the other. This was chosen as it allows the model to optimize for bias by assigning weights to the under represented class. It stabilizes the model performance in skewed datasets. It also improved the AUC, Accuracy and F1 score significantly here (table below shows results over differnt ratios). The line graph here ([https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/Performance%20drift%20with%20differetn%20MF%20ratios%20after%20bias%20mitigation.png]) shows much less drift in metrics over the ratios while the ROC curve shows similar trend as before with improved AUC ([https://github.com/SaumyaDiwan-bmi/HW-11-Homework-BMI-/blob/main/ROC%20Curves%20for%20different%20ratios%20after%20bias%20mitigation.png])
|   Male-Female Ratio |   Accuracy |   F1 score |     AUC |
|--------------------:|-----------:|-----------:|--------:|
|                 0.1 |    0.582   |   0.583665 | 0.582   |
|                 0.2 |    0.5827  |   0.585683 | 0.5827  |
|                 0.3 |    0.58255 |   0.585102 | 0.58255 |
|                 0.4 |    0.58255 |   0.584771 | 0.58255 |
|                 0.5 |    0.58275 |   0.585012 | 0.58275 |
|                 0.6 |    0.58265 |   0.584912 | 0.58265 |
|                 0.7 |    0.5828  |   0.585329 | 0.5828  |
|                 0.8 |    0.58215 |   0.585034 | 0.58215 |
|                 0.9 |    0.58255 |   0.584854 | 0.58255 |


# References and further reading:
1. https://arxiv.org/pdf/2306.08451.pdf
2. https://arxiv.org/pdf/2402.01598
3. https://doi.org/10.1016/j.jelectrocard.2022.07.007

