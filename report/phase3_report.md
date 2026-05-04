# Phase 3 Report

## Project Topic

This project explores whether people may be shifting some forms of help-seeking, advice-seeking, and study support from traditional human-based platforms toward AI-based alternatives.

In Phase 2, the project used exploratory data analysis and hypothesis testing to examine whether AI-related and traditional platform search terms follow different patterns over time. Phase 3 adds a machine learning layer to the project.

The main focus is not to prove that users completely stopped using traditional platforms such as Quora, Chegg, Course Hero, Yahoo Answers, or Ask.fm. Instead, this phase tests whether AI-related search trend observations and non-AI platform observations can be distinguished using machine learning models.

## Data Used in This Phase

The main dataset used in this phase is the cleaned Google Trends dataset created in `01_data_preparation.ipynb`.

This dataset includes:

- **date**
- **category**
- **keyword**
- **platform type**
- **trend score**

Google Trends was selected for the machine learning phase because it directly represents the project’s main behavioral evidence: search interest over time. It is also the most suitable dataset for this stage because it contains repeated time-based observations that can be used for classification and regression.

Other datasets, such as platform traffic data, Stack Overflow survey data, and Pew AI survey data, were used in Phase 2 as external validation and context. They were not used as direct machine learning inputs because they have different structures, time ranges, and measurement units. The machine learning phase therefore focuses mainly on Google Trends, while the other datasets support the broader interpretation of the project.

The Google Trends dataset includes AI-related terms such as:

- `ai friend`
- `chatgpt help`
- `chatgpt study`

It also includes traditional or non-AI platform terms such as:

- `Yahoo Answers`
- `Ask.fm`
- `Quora`
- `Chegg`
- `Course Hero`

After cleaning, the machine learning dataset contained **1,091 observations**.

## Machine Learning Goals

This phase included two main machine learning tasks:

- **Classification**
- **Regression**

The classification task asked whether a model could predict if a Google Trends observation belonged to an AI platform or a non-AI platform.

The regression task asked whether a model could predict the Google Trends `trend_score`, which represents the level of search interest.

These models are not used to prove individual-level replacement behavior. Google Trends is aggregate search interest data, not individual user data. Therefore, the machine learning results should be interpreted as evidence of pattern differences, not as direct proof that the same users moved from traditional platforms to AI platforms.

## Preparing the Machine Learning Dataset

Before building the models, the cleaned Google Trends dataset was prepared for machine learning.

A binary target variable called `is_ai_platform` was created:

- AI platform observations were labeled as `1`
- non-AI platform observations were labeled as `0`

After creating the `is_ai_platform` target variable inside the machine learning notebook, the Google Trends observations were distributed as follows:

- **707 non-AI platform observations**, equal to **64.8%**
- **384 AI platform observations**, equal to **35.2%**

This showed that the dataset was somewhat imbalanced, with non-AI observations forming the larger class. This was not a major problem, but it meant that accuracy alone could be misleading. For this reason, the models were evaluated with precision, recall, F1-score, and ROC-AUC in addition to accuracy.

Time-based features were also created from the date column:

- **year**
- **month**
- **quarter**
- **time_index**

The `time_index` variable represents the chronological distance from the first date in the dataset. This helped the models capture time progression in search behavior.

## Feature Sets

Two different feature sets were used for classification.

The first feature set was the **pattern-only feature set**. It included:

- `trend_score`
- `year`
- `month`
- `quarter`
- `time_index`
- `category`

This feature set did not include keyword names or platform type. It was the most important feature set because it tested whether AI-related observations could be identified from trend behavior, time, and category alone.

The second feature set was the **full feature set**. It included the same variables, but also added `keyword`.

The full feature set was useful as a practical classification check. However, it made the task much easier because keyword names strongly reveal whether an observation is AI-related. For example, `chatgpt study`, `chatgpt help`, and `ai friend` are clearly AI-related terms.

For this reason, the pattern-only models were more meaningful for interpreting the project’s main argument.

## Baseline Classification Model

A baseline classifier was created before training machine learning models. The baseline model predicted only the most frequent class, which was the non-AI platform class.

The baseline model reached:

- **accuracy:** 0.6484
- **precision:** 0.0000
- **recall:** 0.0000
- **F1-score:** 0.0000
- **ROC-AUC:** 0.5000

Although the baseline had moderate accuracy, it could not identify AI-related observations at all. Its F1-score for the AI class was 0.

This means that the baseline model was not useful for the project’s main goal. It only gave a minimum reference point that the actual machine learning models needed to improve on.

## Classification Models

Three main classification models were trained:

- **Logistic Regression**
- **Decision Tree Classifier**
- **Random Forest Classifier**

Each model was tested with both the pattern-only feature set and the full feature set.

The pattern-only Logistic Regression model performed better than the baseline, but its recall was lower than the tree-based models. This means that it missed more AI-related observations.

The pattern-only Decision Tree model performed better than Logistic Regression. This suggested that the relationship between time, trend score, category, and AI-related observations may not be fully linear.

The pattern-only Random Forest model performed the best among the pattern-only models. It reached:

- **accuracy:** 0.9315
- **precision:** 0.9189
- **recall:** 0.8831
- **F1-score:** 0.9007
- **ROC-AUC:** 0.9920

This was an important result because the model achieved strong performance without using keyword names. This suggests that AI-related and non-AI observations have distinguishable trend patterns.

## Full-Feature Model Results

The full-feature models reached perfect performance. Logistic Regression, Decision Tree, and Random Forest all produced scores of **1.00** for accuracy, precision, recall, F1-score, and ROC-AUC.

This happened because the full feature set included keyword names. In this dataset, each keyword is strongly connected to a platform type. For example:

- `ai friend` belongs to the AI platform class
- `chatgpt help` belongs to the AI platform class
- `chatgpt study` belongs to the AI platform class
- `Chegg`, `Course Hero`, `Quora`, `Yahoo Answers`, and `Ask.fm` belong to non-AI platform classes

Therefore, the full-feature results were interpreted carefully. They show that classification is easy when keyword names are included, but they are not the strongest evidence for the project’s main argument.

The pattern-only models are more important because they show that AI-related observations can still be identified without directly using keyword names.

## Classification Model Comparison

The classification model comparison showed a clear improvement over the baseline.

The baseline model had an F1-score of **0** because it could not identify AI-related observations.

The pattern-only Logistic Regression model reached an F1-score of **0.7059**.

The pattern-only Decision Tree model reached an F1-score of **0.8447**.

The pattern-only Random Forest model performed the best and reached an F1-score of **0.9007**.

This supports the idea that AI-related and non-AI platform observations are not random or identical in their trend behavior. Instead, the models were able to learn meaningful differences from time, category, and trend score information.

## Confusion Matrix and Error Analysis

A confusion matrix was created for the best pattern-only model, which was the Random Forest classifier.

The confusion matrix showed that the model correctly classified most observations:

- **136 non-AI observations** were correctly predicted as non-AI
- **68 AI observations** were correctly predicted as AI
- **6 non-AI observations** were incorrectly predicted as AI
- **9 AI observations** were incorrectly predicted as non-AI

Overall, the model correctly classified **204 out of 219 test observations**. Only **15 observations** were misclassified.

The error analysis showed that most of the incorrect predictions were in the study-support category. Specifically, **13 of the 15 errors** were from the study-support category.

This suggests that study-related AI and traditional platform trends are harder to separate than the other categories. Since the pattern-only model does not use keyword names, it only sees category, time, and trend score. In some periods, `chatgpt study`, `chegg`, and `course hero` can have similar trend scores, so the model may confuse them.

This does not mean that the model failed. Instead, it shows that the study-support category is more complex and that AI-based study support and traditional study platforms may overlap more than advice-seeking or general help-seeking platforms.

## Cross-Validation

Cross-validation was used to evaluate the Random Forest pattern-only model more reliably.

The 5-fold cross-validation results were:

- **Mean F1-score:** 0.7851
- **F1-score standard deviation:** 0.2672
- **Mean accuracy:** 0.8642
- **Accuracy standard deviation:** 0.1708

The mean scores were clearly better than the baseline model. This supports the idea that trend score, category, and time-based features contain useful information for distinguishing AI-related observations.

However, the standard deviation was relatively high. This means that model performance changed across different folds. This is expected because Google Trends data has a strong time-based structure, and AI-related search behavior changes significantly across years.

Therefore, cross-validation supports the usefulness of the model, but it also shows that performance depends on which time periods are included in training and testing.

## Time-Based Classification Evaluation

Since Google Trends data has a chronological structure, a time-based split was also tested.

In this evaluation, earlier observations were used for training, and later observations were used for testing. This is a stricter evaluation because it asks whether older trend patterns can help classify newer observations.

The time-based Random Forest model reached:

- **accuracy:** 0.5845
- **precision:** 0.3971
- **recall:** 0.3506
- **F1-score:** 0.3724
- **ROC-AUC:** 0.4153

These results were much weaker than the random split results.

This does not make the model useless. Instead, it shows that future-period classification is more difficult than random classification. The model can learn strong patterns when different time periods are mixed, but it has more difficulty generalizing from older search behavior to newer search behavior.

This supports the idea that AI-related search behavior is dynamic and changes over time.

## Feature Importance

Feature importance was calculated for the Random Forest pattern-only model.

The most important feature was `trend_score`, with an importance value of about **0.6590**. This means that the level of search interest was the strongest signal for distinguishing AI-related and non-AI observations.

Other important features included:

- `time_index`
- `year`
- `category-related features`

This shows that the model was mainly using search interest level and time progression to make predictions. This is useful for the project because the pattern-only model did not use keyword names. Instead, it relied on general trend behavior and category-level information.

## Regression Analysis

The second part of the machine learning phase focused on regression.

While classification predicted whether an observation belonged to an AI platform or not, regression predicted the Google Trends `trend_score`.

This task asked:

**Can machine learning models predict search interest level using time, category, keyword, and platform information?**

Regression added another predictive perspective to the project. It tested whether search interest levels were learnable from the available features, rather than only testing AI vs non-AI classification.

## Regression Models

Four regression models were tested:

- **Baseline Regression**
- **Linear Regression**
- **Decision Tree Regression**
- **Random Forest Regression**

The baseline regression model predicted only the average trend score. It had the weakest performance:

- **MAE:** 17.3444
- **RMSE:** 23.1602
- **R²:** -0.0160

The Linear Regression model improved over the baseline:

- **MAE:** 8.8317
- **RMSE:** 14.2841
- **R²:** 0.6135

The Decision Tree Regression model performed better than Linear Regression:

- **MAE:** 4.5103
- **RMSE:** 8.7294
- **R²:** 0.8557

The Random Forest Regression model performed the best:

- **MAE:** 2.6070
- **RMSE:** 5.3726
- **R²:** 0.9453

These results show that search interest levels can be predicted much better by flexible, non-linear models than by a simple baseline or linear model.

## Actual vs Predicted Trend Scores

An actual vs predicted plot was created for the Random Forest Regression model.

Most points were close to the diagonal line, meaning that the model predicted many trend scores accurately. The model performed especially well for low and medium trend scores.

Some higher trend-score observations were farther from the diagonal line. This suggests that sudden search interest spikes are harder to predict.

Overall, the actual vs predicted analysis supported the regression results. The Random Forest model captured the general search interest pattern well, although extreme peaks in Google Trends data were more difficult to estimate perfectly.

## Overall Machine Learning Findings

The machine learning phase produced several important findings.

First, the baseline classification model was not useful because it could not identify AI-related observations.

Second, the pattern-only classification models performed much better than the baseline. This is important because these models did not use keyword names. They showed that AI-related observations and non-AI observations have distinguishable trend patterns.

Third, the Random Forest pattern-only classifier was the strongest classification model. It achieved a high F1-score and ROC-AUC without using keyword names.

Fourth, the full-feature models reached perfect performance, but this was interpreted carefully because keyword names directly reveal platform type.

Fifth, cross-validation and time-based testing showed that AI-related search behavior changes over time. This means the shift toward AI-related search behavior is dynamic rather than fixed.

Finally, the regression models showed that trend scores can also be predicted from the available features. Random Forest Regression performed the best, suggesting that search interest patterns are not random and can be modeled effectively with non-linear methods.

## Conclusion

This phase shows that AI-related and non-AI platform observations can be meaningfully modeled using machine learning.

The strongest evidence comes from the pattern-only Random Forest classifier. It performed well without using keyword names, which suggests that trend score, time, and category information are enough to distinguish many AI-related observations from non-AI observations.

The regression results add another layer of support by showing that Google Trends search interest levels can also be predicted from the available features.

These results support the broader project argument that AI-related search behavior is distinct, measurable, and increasingly important in online help-seeking and study-support contexts.

However, the results should not be interpreted as proof that traditional human-based platforms have been fully replaced. Instead, they suggest that AI-based tools have become a significant and distinguishable part of the broader online help-seeking environment.
