# Credit-Risk Analysis with LoanTap
<div align="left">
   <a href="https://colab.research.google.com/drive/1ZR31o9dIztLcxZvJPKTgwxL2fw5UfK0b?usp=sharing">
    <img src="https://github.com/ultralytics/yolov5/releases/download/v1.0/logo-colab-small.png" width="10%" /></a>
    <img src="https://github.com/ultralytics/assets/raw/main/social/logo-transparent.png" width="5%" alt="" />
</div>

### Analysis
---
**Customer Credit Health Analysis:**

1. Credit Maturity:  A majority of customers have a credit history between 100-400 months.  A lower proportion of younger customers suggests a bias towards more established borrowers.  Further analysis could explore if this impacts loan default rates.

2. Open Credit Lines:  While the distribution of open credit lines is relatively balanced, a significant portion (51%) of customers possess a high number of open accounts, potentially indicating increased risk. This warrants closer scrutiny regarding default probability.

3. Debt-to-Income Ratio (DTI):  DTI follows a near-normal distribution, but the higher end of the spectrum needs monitoring, as these customers present a greater risk of default.  Further segmentation by DTI risk level could reveal valuable insights.

4. Revolving Line Utilization Rate (Revol_Util): The distribution is nearly normal, with some extreme values possibly due to outlier capping. A peak around 50% suggests moderate credit utilization but those with higher values deserve attention due to higher risk.  Visualization with "eyes" added a playful touch, but its real impact is minimal. The key is the distribution itself.

5. Interest Rate:  The interest rate distribution is slightly left-skewed, implying a higher concentration of lower interest rate loans.  Analysis of interest rates in relation to loan default risk and customer segment is crucial.

**Correlation Analysis:**

- Loan amount and installment amount show strong positive correlation, as expected.
- Annual income is left-skewed, indicating more borrowers in lower income brackets.
- Loan term moderately correlates with loan amount and interest rates, despite the lack of direct correlation between the latter two.  This could indicate different loan product types affecting these variables.

**Time Series Analysis of Loan Characteristics (2016):**

1. Loan Amount Trends:
   - Increased lending to younger customers (credit maturity < 100 months) in the last few months of 2016.
   - High loan disbursement to customers with many open credit lines.
   - Shift in lending to customers with low-moderate DTI risk, with a reduction in high DTI borrowers.  This is potentially a positive risk management shift.
   - Increased loan disbursement to high revol_util customers.  This warrants further monitoring.

2. NPA Loan Trends:
   - A drop in extremely high interest rates and NPAs (1500 basis points drop) between March and July.
   - Significant decrease in "very low" interest rate loan volumes, with a shift towards moderate interest rates.  This suggests a changing lending strategy or market dynamics.

3. Loan Amount and Interest Rate Interaction:
   - Loans below 15k initially saw a larger proportion at lower interest rates, but this shifted to moderate/high rates later in the year.
   - 25k-30k bucket shows no clear trend in interest rate over time.
   - Loans over 35k consist primarily of ultra-high and low-moderate interest rates.

**Business Recommendations:**

1. Deeper Dive into Risk Factors:  Analyze the relationship between customer segments (defined by open accounts, DTI, credit maturity, revol_util) and loan defaults.  Are the increased lending to high-risk groups truly profitable given potential defaults?
2. Monitor Lending Trends:  Continue to track loan disbursal and NPA trends over time.  Changes in lending behavior can be positive but require careful observation. Are the interest rate shifts helping profitability or increasing risk?
3. Model Refinement:  Develop predictive models to assess credit risk based on these characteristics, focusing on those identified as high risk.
4. Segment Analysis: Focus on customer segments with potentially different risk profiles to refine risk assessment and optimize lending strategies for each group.  Understand what drives shifts in these segments and their corresponding interest rates.

### Data Modelling
---


1. Feature Selection and Hyperparameter Tuning:
   - Recursive Feature Elimination (RFE) and GridSearchCV were used with Logistic Regression to find the best features and hyperparameters.
   - The best F1 score achieved was 42% for class 0, indicating poor performance with this model and feature set.

2. Addressing Class Imbalance:
   - SMOTE (Synthetic Minority Over-sampling Technique) was applied to oversample the minority class in the training data to address data imbalance.

3. Model Training and Evaluation (after SMOTE):
   - Logistic Regression, RandomForest, and XGBoost classifiers were trained on the resampled data.
   - Performance metrics were not explicitly stated in the code.

4. XGBoost Hyperparameter Tuning:
   - A manual grid search with stratified K-fold cross-validation was performed to find the optimal hyperparameters for the XGBoost model.
   - The best hyperparameters were found to be: *{'n_estimators': 200, 'max_depth': 7, 'learning_rate': 0.2, 'subsample': 1.0, 'colsample_bytree': 1.0}*
   - The best F1 score achieved was 0.86 for class 0.

5. Data Normalization:
   - StandardScaler was used to normalize features for model improvement.
   - XGBoost was tested again with best hyperparameters found earlier.

6. Feature Scaling and Pipeline:
   - A ColumnTransformer was used for scaling specific features ('int_rate', 'annual_inc', 'loan_amnt')
   - A pipeline was created to incorporate scaling in model training for streamlined workflow.
   - Logistic Regression, RandomForest, and XGBoost models used again

7. Stacking Classifier:
   - Logistic Regression, RandomForest, and potentially XGBoost, were combined using StackingClassifier with Logistic Regression as the final estimator.
   - The predictions of these base models were stacked as meta features for the final model.
   - The meta-model (Logistic Regression) was trained to produce predictions on the stacked features.

8. Neural Network:
   - A neural network using Keras was implemented.
   - The model was trained with epochs and a custom f1_class_0 metric.
   - The model's performance was evaluated and additional epochs were added to potentially improve results.
   - Model architecture with several dense layers and dropout was tested.

9. Prediction Pipeline:
   - A comprehensive prediction pipeline was built combining preprocessing steps including feature engineering, feature scaling and feature selection.
   - The prediction_pipeline was saved with pickle and loaded later for further predictions.

**General Notes:**
  - The code focuses on model selection for imbalanced data. 
  - The analysis has some focus on finding the best metrics for evaluation.
  - There are several model versions that are being compared, and XGBoost consistently seems to yield the best results.

<div align="left">
  <a href="https://gitpod.io/#https://github.com/lunaSnowflake/Credit-Risk">
    <img src="https://gitpod.io/button/open-in-gitpod.svg" alt="Open in Gitpod">
  </a>
</div>

### Languages
<img src="https://user-images.githubusercontent.com/25181517/183423507-c056a6f9-1ba8-4312-a350-19bcbc5a8697.png" width="50"> <!--Python-->

## <img width="48" height="48" src="https://img.icons8.com/pulsar-color/48/about-me-male.png" alt="about-me-male"/> About Me

<font color="orange">Imagine a curious soul frolicking in the realm of Data Science and Development – that's me! With a heart brimming with joy, I dance through projects ranging from coding escapades to the magic of AI and DevOps. Technology isn't just my playground; it's my vibrant canvas where every line of code is a brushstroke of pure delight! <br/> I am open to any suggestions, connect with me anywhere! Also, I would appreciate it if I could get a 🌟</font> 
<br/>

![Dev Gif](https://media.giphy.com/media/f3iwJFOVOwuy7K6FFw/giphy.gif) <br/>

## 🌐 Socials
[![Github](https://img.icons8.com/ios-filled/50/github.png)](https://github.com/lunaSnowflake)
[![linkedin](https://img.icons8.com/fluency/48/linkedin.png)](https://www.linkedin.com/in/hussainkhatumdi/)
[<img src="https://i.ibb.co/5MsxX1w/kaggle-icon-512x512-ubnqei0x.png" width="48px">](https://www.kaggle.com/lunaticsain)
[![Medium](https://img.icons8.com/sf-regular-filled/48/medium-logo.png)](https://medium.com/@hussainkhatumadi53) 
[![Twitter](https://img.icons8.com/color/48/twitter--v1.png)](https://twitter.com/lunatic_sain) 
<br/>
<br/>
