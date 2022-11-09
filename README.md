### Research Title: Predicting Corporate Distress for Small and Medium-sized Enterprises (SMEs) in Hong Kong, Singapore, and South Korea
#
### Project Structure

1.	[Abstract](#1-abstract)
2.	[Data Collection](#2-data-collection)
3.	[Data Pre-processing (1)](#3-data-pre-processing-1)
4.	[Exploratory Data Analysis](#4-exploratory-data-analysis)
5.	[Data Pre-processing (2)](#5-data-pre-processing-2)
6.	[Encoding](#6-encoding)
7.	[Train and Test Partition](#7-train-and-test-partition)
8.	[Feature Scaling](#8-feature-scaling)
9.	[Feature Selection](#9-feature-selection)
10.	[Handling Imbalanced Dataset](#10-handling-imbalanced-dataset)
11.	[Modelling](#11-modelling)
12.	[Results and Evaluation](#12-results-and-evaluation)
13.	[Conclusion](#13-conclusion)

#
### 1. Abstract
In the banking industry, the topic of modelling distress prediction for small and medium-sized enterprises (“SMEs”) has been a fundamental challenge for financial institutions and banks. One of the key issues is the inability of traditional models to efficiently predict corporate distress. In an evolving business landscape, their reliance on accounting-based indicators is reactive rather than predictive. As a result of late detection associated with traditional models, banks unintentionally extend credit to highly risky borrowers who are almost in default, costing banks substantial credit losses.
\
\
This project aims to develop a market-responsive model for predicting SMEs distress, enabling financial institutions to predict SMEs distress in a timely manner, thereby minimising credit losses. This research improves existing traditional models by introducing a hybrid distress prediction model that combines accounting-based and market-based measures to enhance the predictive ability of models.
\
\
The dataset consists of 3,972 SMEs from Hong Kong, Singapore, and South Korea. Using eight predictive features, three different classification models are constructed: Logistic Regression, Artificial Neural Network, and Decision Tree, and their classification performance are compared.
\
\
The experimental results demonstrate that logistic regression performs the best in predicting distressed SMEs, as it collectively possesses a relatively high AUC value (0.82), accuracy rate (88.19%), specificity (88.91%), and sensitivity (75.65%). Its type I (11.09%) and type II (24.35%) errors are also fairly low. Our findings suggest that the incorporation of valuation ratios in the models can address inefficiencies present in traditional algorithms, thereby indicating the potential of our approach in improving corporate distress prediction. 

&nbsp;

### 2. Data Collection
Our research collected a total of 26 Excel documents containing financial information covering a time period of 2011 to 2021 (11 years). All financial data have been gathered in Euro dollars.
\
\
The dataset is taken from FactSet, a company that consolidates and provide firm-level financial statement data gathered from publicly available sources, such as regulatory filings and corporate websites.
\
\
Our dataset contains the category of ratios reported by Altman and Sabato (2007): liquidity, profitability, leverage, coverage, and activity. As extension of this approach, we added valuation ratio and rearranged some of the categories, resulting in – liquidity, profitability, leverage, activity, and valuation categories – used in our research.

&nbsp;

### 3. Data Pre-processing (1)
The data preparation process entails:
- Retaining rows relevant to research focus:
    - Countries: Hong Kong, Singapore, and South Korea
    - Industries: Companies in all sectors, except of those in the ‘Finance’ industry
    - SMEs, defined as companies with annual sales less than or equal to EUR 50 million
- Missing values:
    - In target (Removed)
    - In independent variables (Filling in missing values using linear interpolation to preserve the relationship between the attributes)
- Removing rows with missing data for the whole 11-year period
- Encoding target variable: 
    - Positive equity replaced by 0 (denoting non-distress)
    - Negative equity replaced by 1 (denoting distress)


&nbsp;

### 4. Exploratory Data Analysis

Dataset consists of 3,972 rows and 292 columns.

Table below shows a summary of the dataset used.

*Data Information*

| **Variables**                         | 292 columns
:--------------------------------------:|:-------------------------:
| **Time Period**                       | 2011 to 2021 (11 years)
| **Number of distressed companies**    | 293 companies 
| **Number of observations**            | 3972 companies


&nbsp;

### 4.1 Descriptive Statistics, Figures, and Charts
\
**4.1.1 Overall Percentage Distress**

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200688161-959c43c6-7a0a-4629-859f-5ab1e37e44de.png" width="380" height="55"/>
</p>

Across 2011 to 2021, there are a total of 3972 companies, of which 293 companies experienced distress while 3679 companies did not experience distress. The **overall percentage distress is 7.38%.**

&nbsp;

**4.1.2 Percentage Distress by Year**


<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696374-f8c0dc85-0da6-475c-a68b-84e0fe7df8e6.png" width="700" height="370"/>
</p>


There is **a trend of increasing percentage distress across the years.** The percentage distress remains relatively stable from 2011 to 2018 and peaked from 2019 to 2021. The highest percentage of distress is recorded is in 2021, at 2.24%, while the lowest percentage distress is recorded is in 2014, at 1.04%.
\
\
A possible explanation for the rise in percentage distress, notably between 2019 to 2021, could an **implication of COVID-19 on the credit market, where many lenders are facing increasing breach of loan commitments by their borrowers due to deteriorating credit conditions.**

&nbsp;

**4.1.3 Percentage Distress by Country**


<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696322-ba68a425-a3d4-4331-95c9-cdff3051adfc.png" width="450" height="400"/>
</p>

**Singapore has the highest percentage distress (10.71%)**, followed by Hong Kong (9.27%), and South Korea (5.33%). 

&nbsp;

**4.1.4 Percentage Distress by Industry**

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696233-cad7666a-61bd-47e5-aaa9-23c5b3b5ea26.png" width="800" height="430"/>
</p>


The **top 3 industries with the highest percentage distress are Energy (21.05%), followed by Consumer Services (11.98%), and Business Services (10.53%).** On the other hand, the bottom 3 industries with the lowest percentage distress are Telecommunications (0%), followed by Consumer Non-Cyclicals (4.67%), and Consumer Cyclicals/Non-Energy Materials (5.45%).


&nbsp;

**4.1.5 Market Value**


<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696432-1c6580fa-4fce-4f49-880a-b803ebd334f0.png" width="750" height="400"/>
</p>


<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696437-dafd0b9c-6355-41f2-bbcc-9af7777139dc.png" width="750" height="250"/>
</p>


From the histogram, the overall distribution of the sample is observed to be **positively skewed, which means that most companies fall in the lower range of the market value group.** A similar distribution is observed for both distress and non-distress charts individually.


&nbsp;

### 4.2 Univariate Analysis for Financial Ratios
Univariate analysis serves as a precursor to feature selection. 
\
\
A histogram is plotted for all 25 ratios. It aims to evaluate the significance of a ratio, by assessing its ability to distinguish between distress and non-distress firms, while holding other attributes constant.
\
\
In sum, three main patterns can be observed from the univariate analysis:
1.	**Pattern 1:** There is evident overlap between the two classes which indicates that the stipulated ratio ineffectively distinguishes between the distress and non-distress group, suggesting that it has a weak predictive power.
2.	**Pattern 2:** There is slight separation between the two classes indicates that the stipulated ratio fairly distinguishes between the distress and non-distress group, suggesting that it has some predictive power.
3.	**Pattern 3:** There is apparent separation between the two classes indicates that the stipulated ratio effectively distinguishes between the distress and non-distress group, suggesting that it has a high predictive power.



Out of the 25 histograms plotted, 3 of them are presented below as examples.

&nbsp;

**4.2.1 Dividend Yield Ratio Histogram**

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696625-60379478-07bd-4635-a1f6-64ee53eb04b0.png" width="600" height="400"/>
</p>

Dividend yield ratio constitutes part of the valuation category. Dividend yield ratio illustrates the distribution of Pattern 1, where there is an **evident overlap between the distress and non-distress classes.** This indicates that **dividend yield ratio has a low predictive power.**

&nbsp;

**4.2.2 Return on Assets Histogram**

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696619-300e1f0c-26ae-40ea-a8df-f7e7b0c0b529.png" width="600" height="400"/>
</p>

Return on assets constitutes part of the Profitability category. Return on assets illustrates the distribution of Pattern 2, where there is a **slight separation between the distress and non-distress classes.** This indicates that the **return on assets ratio has some predictive power.**

&nbsp;

**4.2.3 Debt-to-Asset Histogram**

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696604-f0888033-c565-4449-9957-169367225c8b.png" width="600" height="400"/>
</p>


Debt-to-asset constitutes part of the leverage category. Debt-to-Asset ratio illustrates the distribution of Pattern 3, where there is **distinct separation between the distress and non-distress classes.** This indicates that the **debt-to-asset ratio has a high predictive power.**


&nbsp;

### 5. Data Pre-processing (2)

Attributes are selected based on a **time interval of 3 years.**
\
\
Dataset is partitioned into two categories: <br />
(1) For non-distress companies, the study period used is between 2019 to the latest year, 2021. <br />
(2) For distress companies, the years of financial ratios taken for each company differs depending on the year when they faced a negative equity circumstance. The data used in the model are the financial ratios 3 years prior to their first year of distress.
\
\
The preparation process for distress companies entails:
- First identify the year that the company experienced distress for the first time <br />
- Pivoting on that year, take the data 3 years prior to distress <br />
Companies with ‘2011’ and ‘2012’ first year distress are excluded from the dataset because inputs require a minimum of a 3-year time frame.

&nbsp;

After data preparation, the dataset used for modelling contains 11736 rows and 28 columns – where 27 of the columns serves as inputs (i.e., 25 financial ratios, country, and industry columns) and the remaining column as target:
- **Target:** ‘Distress’ or ‘Non-distress’ (represented by Equity)
- **Predictors:** Country, Industry, 25 Financial Ratios that are categorised in 5 groups: Activity, Leverage, Liquidity, Profitability, Valuation


&nbsp;

### 6. Encoding
- Dummy encoding is performed for **categorical predictors** in our dataset.

&nbsp;

### 7. Train and Test Partition 
- **70/30 train-test split** is adopted.

&nbsp;

### 8. Feature Scaling
- **Standardisation** is performed for numeric predictors in our dataset.
- Features are rescaled so that their values have a **mean of 0 and a standard deviation of 1.**

&nbsp;

### 9. Feature Selection

3 methods of feature selection are employed: (1) Variance Inflation Factor (VIF), (2) Recursive Feature Elimination with Cross-Validation (RFECV), and (3) P-Value

&nbsp;

### 9.1 Variance Inflation Factor (VIF)
- VIF measures the degree of multicollinearity in a set of predictor variables
- Perform VIF selection process by removing features with a VIF threshold of more than 5 from the training dataset in a stepwise manner
- Removed 6 features

&nbsp;

### 9.2 Recursive Feature Elimination with Cross-Validation (RFECV)
- RFECV is an automated feature elimination method which aims to find best performing subset of features 
- Learning estimator: 'Random Forest Classifier'
- Metric: 'Accuracy’
- Removed 10 features

&nbsp;

### 9.3 P-Value
- Run the logistic regression to manually filter features that are insignificant in predicting the target variable.
- Features with a p-value of more than 0.05 are removed in a stepwise fashion.
- Removed 13 features

&nbsp;

### 9.4 Analysis of Features after Feature Selection
Out of the 37 features (before feature selection), 8 of them are considered to be significant predictors after undergoing the feature selection process. These **8 predictors (i.e., 6 numeric financial ratios and 2 categorical variables) will be used as inputs in the final models.**

&nbsp;

*Features selected in the model*

| No.   | Ratio Category        | Features Selected                 | Formula
:------:|:---------------------:|:---------------------------------:|:-------------------------:
| 1     | Profitability         | EBITDA-to-Assets                  | EBITDA/Total Assets
| 2     | -                     | Industry Energy                   | -
| 3     | Leverage              | Debt-to-Assets                    | Total Debt/Total Asset
| 4     | Activity              | Inventory Turnover                | Cost of Goods Sold/Average Inventory
| 5     | Liquidity             | Working Capital over Total Assets | Working Capital/Total Assets
| 6     | Profitability         | Return on Assets                  | Net Income/Average Total Assets
| 7     | Valuation             | Dividend Yield Ratio              | Dividend per Share/ Market price per share
| 8     | -                     | Country South Korea               | - 

&nbsp;

**Correlation**

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696723-8f48c6a9-dd76-4cf3-9c0b-a3a2e76aeb3c.png" width="650" height="650"/>
</p>

Figure above shows a **low pairwise correlation among the 8 selected features in the training sample.**

&nbsp;

### 10. Handling Imbalanced Dataset

Our dataset showed signs of imbalanced characteristics, with just **6.16% of the dataset belonging to the 'distress' class.**
\
\
To alleviate the issue of an imbalance class distribution in our dataset, we opted for **Synthetic Minority Oversampling Technique (“SMOTE”) algorithm.**
\
\
*Distribution of y_train set*

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200696971-6bfca171-0326-4996-a1df-743517e62362.png" width="700" height="350"/>
</p>

With SMOTE, the proportion of minority class (i.e., distress class) **increased from 6.16% to 23.07% in the train set.**

&nbsp;

### 11. Modelling

The three proposed models build in our study are: (1) Logistic Regression, (2) Decision Tree, and (3) Artificial Neural Network.

&nbsp;

### 11.1 Logistic Regression

*Logistic Regression Summary Table*

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200698033-ce612650-bf29-407f-846c-b048bb91b542.png" width="600" height="300"/>
</p>


We can observe that **all 8 features are statistically significant because their p-values are less than the level of significance of 0.05.**

&nbsp;

### 11.2 Decision Tree

Two parameters are adjusted: (1) Setting the maximum depth as 3 to control the tree size and prevent the model from overfitting, and (2) Appointing ‘Gini’ as the criterion to measure the quality of a split.
\
\
As a result, the decision tree is generated.

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200698273-7ef19828-0555-4059-9e24-90cc60c8fb95.png" width="900" height="400"/>
</p>

The three main splitting features of the tree are: (1) Debt-to-Asset, (2) Return on Assets, and (3) Working Capital over Total Assets.

&nbsp;

### 11.3 Artificial Neural Network
Three layers of architecture are constructed – 1 input layer with 8 nodes, which represents the 8 features, 1 hidden layer with 5 nodes, and an output layer, which represents the prediction. 
\
\
Two types of activation function are implemented in the neural network: Rectified Linear Unit ("ReLU"), and sigmoid. The ReLU activation function is applied on the input and hidden layer, while the sigmoid activation function is applied on the output layer.
\
\
Multiple parameters are calibrated to optimise the performance of the neural network. Examples of these configurations include:
- Number of nodes in the hidden layer,
- Activation function,
- Number of hidden layers,
- Initialiser,
- Learning rate,
- Batch size,
- Epochs,
- Optimiser, and
- Early stop is also implemented in the model iteration to prevent overfitting

&nbsp;

### 11.3.1 Sensitivity Analysis

A **major shortcoming of artificial neural network is challenge of interpreting or logically explaining the behaviour of the features on the target, which gives rise to the term 'black box'.** This concern of model interpretability is important for any decision-makers to justify specific conclusions as well as to mitigate risks such as bias and discrimination. Despite being widely perceived as opaque or 'black box' models, it is possible to uncover the underlying process hidden in artificial neural network.
\
\
**By running sensitivity analysis, the readability of artificial neural network can be improved.** Sensitivity analysis is the process of understanding the strength of relationship between a given predictor and the model output, thereby addressing the problem of interpretability associated with artificial neural network.
\
\
To investigate how the predictor affects the target, we vary one input at a time at multiple steps ***(by their standard deviation away from the mean across intervals of 1)***, while holding all other attributes constant ***(at their mean value of 0).***
\
\
Through the process of sensitivity analysis, the two features: **EBITDA-to-Assets and Return on Assets Ratio are removed from the neural network model** because they do not display intuitive results.

&nbsp;

<p align="center">
  <img src="https://user-images.githubusercontent.com/79804641/200698548-c3795e65-8acf-44ef-a17a-c132f2e2d228.png" width="700" height="700"/>
</p>

&nbsp;

The figure above illustrates the remaining features in the neural network that display the anticipated output.
\
\
After verifying the relationships between the predictors and the target, the final six features constitute: (1) Debt-to-Asset, (2) Inventory Turnover, (3) Working Capital over Total Assets, (4) Dividend Yield Ratio, (5) Industry – Energy, and (6) Country – South Korea. They comprise of four continuous attributes and two dummy variables.
\
\
The artificial neural network architecture for the 6 features is presented in the figure below.

&nbsp;

<p align="left">
  <img src="https://user-images.githubusercontent.com/79804641/200698927-214f1236-c5db-4e0c-8b50-23f4675c1769.png" width="450" height="400"/>
</p>

&nbsp;

### 11.4 Assessing Model Stability
Additionally, we assessed the stability of all three models by using a stratified 10-fold cross validation. The mean accuracy score derived from 10-fold cross-validation is approximately the same as the training accuracy across all three models. Correspondingly, all models have low 10-fold cross-validation standard deviations. This implies that all three models produce stable results.

&nbsp;

### 12. Results and Evaluation
The output (i.e., probability of distress) generated by the models will be passed through a cut-off point to classify an observation belonging to ‘distress’ or ‘non-distress’ class.
\
\
The selection of this cut-off value is dependent on the goal of our research.
\
\
The goal of our research focuses on identifying event (i.e., distress) than non-event (i.e., ‘non-distress’). Therefore, we will set a lower cut-off point (<0.5) to give greater preference for classifying ‘distress’ firms (rare events) than ‘non-distress’ firms (common events). This also means that the model becomes more conservative, whereby prediction model will advise the decision-maker not to issue the loan to a specific company unless there is a high probability that the loans can be repaid. The **cut-off value is set as 0.3** after testing several thresholds.
\
\
Next, we assess the implications of committing Type I and Type II error in order to understand the commercial implications in the standpoint of a financial provider.
\
\
Committing Type I error means that the bank rejects loans from non-distress applicants. Since the non-distress applicant is wrongly classified as distress, the bank loses some valuable customers as well as profit. Conversely, committing Type II error indicates that the bank approves loan for applicants in distress. Therefore, the bank may extend loans to a large number of borrowers who eventually will not pay back the loan. This is potentially risky and could cause the bank to sustain substantial losses on a large-scale basis.
\
\
When comparing between Type I and Type II, Type II error is more serious for a loan provider or bank. Hence, we **place greater emphasis on the model with a lower Type II error than Type I error because the cost of misclassifying an actual distress applicant as non-distress (Type II Error) is considerably higher than the cost of misclassifying an actual non-distress applicant as distress (Type I Error).**

&nbsp;

*Model Performance*

| Models                                            | Overall Accuracy  | Specificity   | Type I Error  | Sensitivity   | Type II Error | AUC
:--------------------------------------------------:|:-----------------:|:-------------:|:-------------:|:-------------:|:-------------:|:-----:
| Logistic Regression                               | 88.19%            | 88.91%        | 11.09%        | 75.65%        | 24.35%        | 0.82
| Decision Tree (CART)                              | 86.48%            | 87.2%         | 12.8%	        | 74.09%        | 25.91%        | 0.81
| Artificial Neural Network (Before Sensitivity)    | 86.54%            | 86.78%        | 13.22%        | **82.38%**    | **17.62%**    | **0.85**
| Artificial Neural Network (After Sensitivity)     | **88.5%**         | **89.63%**    | **10.37%**    | 68.91%        | 31.09%        | 0.79

&nbsp;

To increase the performance of the model, the overall aim of the research is to increase specificity and sensitivity while reducing type I and type II error. The table above summarises the classification results for each model. *(The models that excelled at each metric are those in bold)*
\
\
From the table above, we can observe that all three models performed reasonably well. To ascertain which is the best model, we adopt a process of elimination by analysing both quantitative and qualitative characteristics of the models as a whole:
- Artificial neural network (Before Sensitivity) possesses the highest AUC (0.85). But after removing incoherent features through sensitivity analysis, the **AUC for artificial neural network dropped to 0.79, rendering logistic regression and decision tree as better models.** This leaves us to choose the best model between logistic regression and decision tree. 
- We conclude that **logistic regression is the superior model** when comparing between logistic regression and decision tree. Logistic regression is preferred over decision tree because it **collectively possess a higher AUC (0.82), with a higher accuracy rate (88.19%), specificity (88.91%), and sensitivity (75.65%) compared to decision tree. Its Type I (11.09%) and Type II (24.35%) errors are also lower.**
- Additionally, logistic regression offers capabilities that are suitable for application in real-world scenario. The value of θ coefficients in logistic regression explains the direction and degree of significance of the independent variables over the dependent variable. Therefore, logistic regression **provides interpretability benefits for internal bank managers to understand the impact of predictors on the target variable.**
- Furthermore, when we examine the features that were incorporated in the model, logistic regression had a **better selection of features because it included valuation ratio, notably dividend yield ratio.** By integrating valuation ratio, the logistic regression model is better equipped to respond to market fluctuations and predict corporate distress efficiently, which aids in addressing the business problem of our study. <br />

Based on the composite of factors, we arrive at the conclusion that the **logistic regression is the best model for our research.**

&nbsp;

Figures below present the ROC curve for each model.

| ROC Curve – Logistic Regression                               | ROC Curve – Decision Tree (CART)
:--------------------------------------------------------------:|:-------------------------:
<img src="https://user-images.githubusercontent.com/79804641/200700302-5e3472ee-b18f-4317-8291-d25b0c517fb6.png" width="370" height="300"/> | <img src="https://user-images.githubusercontent.com/79804641/200700301-17a9d1c8-8fb0-4927-8b5a-22f75ee5a472.png" width="370" height="300"/>
| **ROC Curve – Artificial Neural Network (Before Sensitivity)**     | **ROC Curve – Artificial Neural Network (After Sensitivity)**
<img src="https://user-images.githubusercontent.com/79804641/200700288-1c1c7cdb-fb26-4a99-a282-d7b9776bcd9b.png" width="370" height="300"/> | <img src="https://user-images.githubusercontent.com/79804641/200700299-0bd7d98c-af61-4ac8-8717-b944996683f5.png" width="370" height="300"/>

&nbsp;

### 13. Conclusion
This paper aims to develop a **market-responsive model for predicting SMEs distress** based on financial ratios, country, and industry-specific characteristics. The dataset consists of 3,972 SMEs in Hong Kong, Singapore, and South Korea spanning the years 2011 to 2021. After applying data pre-processing techniques and feature selection, eight features were determined to be predictive indicators of corporate distress.
\
\
We performed a comparative analysis between three different classification methodologies: logistic regression, decision tree, and artificial neural network. From the empirical results, **logistic regression is observed to be the best performing model** as it collectively possesses a high AUC (0.82), accuracy (88.19%), specificity (88.91%), and sensitivity (75.65%). Its type I (11.09%) and type II (24.35%) errors are also fairly low. Furthermore, logistic regression exhibits high degree of interpretability.
\
\
By pairing dynamic ratios alongside accounting-based metrics, the models developed in this research are more forward-looking and can more efficiently facilitate early detection of distressed firms. Correspondingly, this proposed distress prediction methodology can **aid lending institutions in deciding whether to approve or reject loan requests from SMEs. By granting credit to credit-worthy candidates and denying credit to distressed applicants, banks can minimise unnecessary losses, and increase profit.**

[(Go to the top)](#research-title-predicting-corporate-distress-for-small-and-medium-sized-enterprises-smes-in-hong-kong-singapore-and-south-korea)

&nbsp;

## Reference
- Altman, E. I., & Sabato, G. (2007). Modelling credit risk for SMEs: Evidence from the U.S. Market. Abacus, 43(3), 332–357. https://doi.org/10.1111/j.1467-6281.2007.00234.x
