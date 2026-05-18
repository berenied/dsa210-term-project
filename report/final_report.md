# DSA210 Final Report
## Human-to-AI Interaction Shift Analysis

**Student:** Ela Beren Yücel  
**Student ID:** 34155  
**Course:** DSA 210 – Introduction to Data Science  
**Project Website:** https://berenied-dsa210-human-ai-shift.lovable.app  
**GitHub Repository:** https://github.com/berenied/dsa210-term-project  

---

## Abstract

This project investigates whether online help-seeking behavior is shifting from traditional human-based platforms toward AI-based alternatives. The main research question is: **To what extent are people shifting from traditional human-based help-seeking platforms toward AI-based alternatives?** To study this question, the project combines four layers of evidence: Google Trends search behavior, platform traffic context, survey evidence from Stack Overflow and Pew, and machine learning models.

Google Trends is used as the main behavioral evidence because it shows how public search interest changes over time. AI-related search terms are compared with traditional platform-related terms across three contexts: advice and interaction, general help-seeking, and study support. The analysis also includes platform traffic data to avoid relying only on search-interest proxies. Survey data is used as external validation, especially to show whether AI usage and awareness are increasing outside the Google Trends data. Finally, machine learning models are used to test whether AI-related and non-AI observations can be distinguished from trend behavior.

The results show statistically significant differences between AI-related and traditional platform search patterns in all three selected contexts. Because the paired differences were not normally distributed, Wilcoxon signed-rank tests were also used as non-parametric robustness checks, and these tests also showed significant differences. Platform traffic data provides supporting context: Claude and Character AI increased during the observed traffic window, while selected study-support platforms decreased on average. Stack Overflow survey results show that AI tool usage among valid respondents increased from **44.38% in 2023** to **78.50% in 2025**. Machine learning results also support the idea that AI-related and non-AI observations can be distinguished: the best pattern-only Random Forest classifier achieved an **F1-score of 0.9007**.

Overall, the project supports the conclusion that AI-related tools are becoming a measurable part of online help-seeking behavior. However, the findings should not be interpreted as proof of complete replacement or direct individual-level migration. The safest interpretation is that there is a measurable shift in online attention and search behavior toward AI-based tools.

---

## 1. Introduction

AI tools such as ChatGPT have become increasingly common in everyday online activity. People now use AI tools to ask questions, receive explanations, get study support, and sometimes even seek advice or interaction. Before the widespread use of such tools, many of these needs were met through traditional online platforms such as Quora, Yahoo Answers, Ask.fm, Chegg, Course Hero, and other human-based or community-based help sources.

This project studies whether there is evidence that some online attention is moving from traditional human-based help-seeking platforms toward AI-based alternatives. The purpose is not to claim that traditional platforms have disappeared. It is also not to claim that the same individual users definitely moved from one platform to another. Instead, the project asks whether search behavior, platform traffic, survey evidence, and machine learning results together suggest a broader shift in online help-seeking behavior.

The project is important because AI tools are not only technological products; they also change how people access information, explanations, advice, and learning support. If people increasingly search for AI-related help instead of traditional platform-based help, this may indicate a change in online behavior and digital interaction patterns.

---

## 2. Research Question and Scope

The central research question is:

> **To what extent are people shifting from traditional human-based help-seeking platforms toward AI-based alternatives?**

To make this broad question measurable, the project focuses on three online help-seeking contexts:

| Context | What It Represents | Traditional / Non-AI Side | AI-Related Side |
|---|---|---|---|
| Advice and interaction | Advice, conversation, or social-style support | Yahoo Answers, Ask.fm | ai friend |
| General help-seeking | Questions, explanations, and practical help | Quora | chatgpt help |
| Study support | Homework help, learning resources, and student support | Chegg, Course Hero | chatgpt study |

These comparisons do not cover every possible form of online help-seeking. They are used as operational examples that allow the broader research question to be studied using real data.

---

## 3. Data Sources

The project uses multiple data sources so that the final interpretation does not rely on only one type of evidence.

| Data Source | Role in the Project | Why It Was Used |
|---|---|---|
| Google Trends | Main behavioral evidence | Measures public search interest over time for AI-related and traditional platform-related terms. |
| Platform traffic context | External grounding | Adds recent platform-level activity and helps avoid relying only on search-interest proxies. |
| Stack Overflow survey | AI adoption validation | Shows whether AI tool usage increased among survey respondents across years. |
| Pew AI survey | Public awareness and attitude context | Provides broader context about AI awareness and public concern/excitement toward AI. |

Google Trends is the central dataset because the project’s main question is about search behavior and online attention. The other sources are used to strengthen and contextualize the findings.

---

## 4. Data Preparation

The first notebook, `01_data_preparation.ipynb`, prepares the raw datasets and converts them into cleaned files used in later analysis. The preparation process includes cleaning Google Trends files, organizing platform traffic data, and summarizing survey datasets.

### 4.1 Google Trends Preparation

The Google Trends files required several cleaning steps before they could be used for analysis:

| Step | Purpose |
|---|---|
| Date conversion | Converts time values into a consistent datetime format. |
| Keyword standardization | Makes keyword names consistent across files. |
| Numeric conversion | Converts Google Trends scores into numeric values. |
| Low-value handling | Treats values such as `<1` as `0.5` so they can be analyzed numerically. |
| Long-format restructuring | Converts the data into a clean structure with date, category, keyword, platform type, and trend score. |
| Platform labeling | Labels observations as AI platform, forum/Q&A platform, or study-support platform. |

The final cleaned Google Trends dataset contains **1,091 observations**. These observations are used for exploratory data analysis, hypothesis testing, and machine learning.

### 4.2 Platform Traffic Preparation

The platform traffic dataset includes recent traffic estimates for platforms such as ChatGPT, Claude, Character AI, Quora, WikiHow, Chegg, Course Hero, Khan Academy, and Quizlet. The traffic values were cleaned and converted into numeric form. Platforms were grouped into broader types such as AI platform, forum Q&A platform, general help platform, and study-support platform.

This dataset is not used as the main evidence because it covers only a short time window. Instead, it is used as supporting context to compare whether platforms gained or lost traffic during the observed period.

### 4.3 Survey Preparation

The Stack Overflow survey data was summarized into AI adoption groups:

- uses AI
- plans to use AI
- does not plan to use AI

The Pew survey data was summarized to describe public AI awareness and attitudes toward AI. These survey datasets are not used to prove direct replacement behavior, but they provide useful external context.

---

## 5. Exploratory Data Analysis

The exploratory data analysis examines whether AI-related search terms and traditional platform-related search terms show different patterns over time. The EDA focuses on three main areas: advice and interaction, general help-seeking, and study support.

### 5.1 Advice and Interaction

![Figure 1. Advice-seeking and AI interaction trends](../figures/01_advice_seeking_trends.png)

**Figure 1** compares the AI-related term `ai friend` with traditional advice or interaction platforms such as Yahoo Answers and Ask.fm. The AI-related term becomes much more visible in the later period, while the older advice/community platforms remain lower. This suggests that AI-based interaction is becoming more noticeable in online search behavior.

This result does not prove that users directly moved from Yahoo Answers or Ask.fm to AI tools. However, it shows that search interest related to AI-style interaction has become more visible in the same general context.

### 5.2 General Help-Seeking

![Figure 2. General help-seeking trends](../figures/02_general_help_seeking_trends.png)

**Figure 2** compares `chatgpt help` with Quora. Quora still has higher overall search interest, but `chatgpt help` begins to appear more clearly in the later period. This suggests that AI-based help-seeking is forming its own visible search pattern rather than completely replacing Quora.

This is an important finding because it avoids an overly simple conclusion. The evidence does not show that Quora disappeared. Instead, it shows that AI-based help search has become visible alongside traditional Q&A search behavior.

### 5.3 Study Support

![Figure 3. Study-support trends](../figures/03_study_support_trends.png)

**Figure 3** compares `chatgpt study` with Chegg and Course Hero. The AI-related study-support term becomes more visible over time. Traditional study-support platforms still appear in the data, but their later patterns are weaker compared with earlier periods.

This supports the idea that AI tools are becoming more relevant in learning and student-support contexts. However, as with the other Google Trends results, this should be interpreted as a shift in search attention rather than proof that individual students directly replaced one platform with another.

---

## 6. Comparison Metrics

After reshaping the Google Trends data into category-level wide formats, the analysis calculates comparison metrics between AI-related and traditional search interest.

The main comparison metrics are:

| Metric | Meaning |
|---|---|
| Traditional average | Average search interest of selected traditional platforms in the same context. |
| Difference | AI-related search interest minus traditional average search interest. |
| Ratio | AI-related search interest divided by traditional average search interest, with a small adjustment to avoid division problems. |

The comparison summary shows different patterns across categories:

| Category | Mean Difference | Median Difference | Mean Ratio | Median Ratio |
|---|---:|---:|---:|---:|
| Advice-seeking | 14.2787 | 7.5 | 4.1526 | 2.1818 |
| General help-seeking | -61.6393 | -67.0 | 0.1117 | 0.0411 |
| Study support | -15.5878 | -20.5 | 0.8098 | 0.1538 |

The advice-seeking category shows a positive mean difference, meaning that the AI-related term is higher than the traditional average on average. General help-seeking and study support show negative mean differences, meaning that traditional platforms remain stronger in absolute Google Trends search interest. However, the time patterns still show AI-related visibility increasing or becoming more distinct.

This distinction matters because a shift does not always mean that AI search interest is already higher in every category. It can also mean that AI-related terms are developing visible and statistically different patterns.

---

## 7. Correlation Analysis

Correlation analysis was used to examine whether AI-related and traditional search terms move together or in opposite directions. Several correlations between AI-related and traditional terms are negative. For example, `chatgpt help` and Quora show a strong negative correlation, and `chatgpt study` has negative correlations with traditional study-support terms.

The correlation results support the idea that AI-related and traditional platform search patterns do not always move together. However, correlation alone does not prove causation or direct user migration. Therefore, correlation is used only as an exploratory signal, not as final proof.

---

## 8. Hypothesis Testing and Robustness Checks

Hypothesis testing was used to evaluate whether the differences between AI-related and traditional platform search interest are statistically significant.

### 8.1 Test Choice

A paired t-test was used because each AI-related trend value is compared with a traditional platform value from the same time period. This pairing is important because search interest can change over time due to general external factors. Comparing observations within the same time period makes the test more appropriate than treating the samples as completely independent.

### 8.2 Normality Check

Before interpreting the paired t-tests, the paired differences were checked using the Shapiro-Wilk normality test. The results showed that the paired differences were not normally distributed:

| Comparison | Shapiro-Wilk Interpretation |
|---|---|
| AI interaction vs traditional advice average | Not normally distributed |
| AI help search vs Quora | Not normally distributed |
| AI study support vs traditional study average | Not normally distributed |

Because the normality assumption was not satisfied, the paired t-test results needed to be interpreted carefully. To address this, the Wilcoxon signed-rank test was added as a non-parametric robustness check.

### 8.3 Hypothesis Test Results

| Comparison | Paired t-test p-value | Wilcoxon p-value | Result |
|---|---:|---:|---|
| AI interaction vs traditional advice average | 2.1694e-04 | 8.0002e-05 | Significant difference |
| AI help search vs Q&A platform search | 8.1217e-27 | 1.1054e-11 | Significant difference |
| AI study support vs traditional study average | 6.4909e-24 | 2.1152e-20 | Significant difference |

All three paired t-tests show statistically significant differences. The Wilcoxon signed-rank tests also show significant differences. This means that the conclusion does not rely only on the paired t-test assumption.

### 8.4 Interpretation

The hypothesis tests support the conclusion that AI-related and traditional platform search patterns differ in a statistically meaningful way. However, these tests do not prove direct replacement. They show that the overall search interest patterns are different, not that the same individuals moved from traditional platforms to AI tools.

---

## 9. Platform Traffic Context

Platform traffic data was added to provide external grounding beyond Google Trends. This was important because Google Trends alone compares search-interest proxies. Traffic data helps show whether selected platforms are also gaining or losing recent platform-level activity.

### 9.1 Relative Traffic Change

![Figure 4. Relative traffic change by platform](../figures/04_relative_traffic_change_by_platform.png)

**Figure 4** shows how each platform’s traffic changed relative to its first observed month. A value above 1 means the platform increased compared with the first month, while a value below 1 means the platform decreased.

The traffic-change results show:

| Platform | Percentage Change | Interpretation |
|---|---:|---|
| Claude | +57.36% | Strong positive change in the short window |
| Character AI | +4.88% | Small positive change |
| ChatGPT | -7.13% | Slight decline, but still very large in traffic scale |
| Quora | -5.43% | Slight decline |
| WikiHow | -6.38% | Slight decline |
| Chegg | -61.81% | Strong decline |
| Course Hero | -46.39% | Strong decline |
| Khan Academy | -19.46% | Decline |
| Quizlet | -32.74% | Decline |

Two of the three AI platforms increased during the observed period, while all selected study-support platforms decreased. This pattern supports the broader project argument, but the short time window means it should be treated as supporting context rather than long-term proof.

### 9.2 Traffic Scale Context

![Figure 5. Monthly platform traffic on log scale](../figures/14_monthly_platform_traffic_log_scale.png)

**Figure 5** adds scale context. This is important because percentage change alone can be misleading. ChatGPT shows a small negative percentage change in the short traffic window, but it still has much higher total monthly traffic than the other selected platforms.

This is one of the key interpretive points of the project: change and scale should be interpreted together. A small percentage decline for a very large platform does not mean the platform is unimportant.

### 9.3 Platform-Type Summary

| Platform Type | Average Percentage Change | Positive Platforms | Negative Platforms |
|---|---:|---:|---:|
| AI platform | 18.37% | 2 | 1 |
| Forum Q&A platform | -5.43% | 0 | 1 |
| General help platform | -6.38% | 0 | 1 |
| Study support platform | -40.10% | 0 | 4 |

The platform-type summary shows that AI platforms had a positive average traffic change, while the selected traditional and study-support groups showed negative average changes in this short window.

---

## 10. Survey Evidence

Survey data was used to validate whether AI adoption and awareness patterns also appear outside Google Trends.

### 10.1 Stack Overflow AI Adoption

![Figure 6. Stack Overflow AI adoption by year](../figures/06_stackoverflow_ai_adoption.png)

The Stack Overflow survey results show a clear increase in AI tool usage among valid respondents:

| Year | Does Not Plan to Use AI | Plans to Use AI | Uses AI |
|---|---:|---:|---:|
| 2023 | 29.81% | 25.81% | 44.38% |
| 2024 | 24.36% | 13.80% | 61.84% |
| 2025 | 16.17% | 5.33% | 78.50% |

The share of respondents using AI tools increased by **34.12 percentage points** from 2023 to 2025. At the same time, the share of respondents who do not plan to use AI decreased. The “plans to use AI” category also decreased, which may suggest that some respondents moved from planning to active use.

This survey is not representative of the entire population because it focuses on Stack Overflow respondents. However, it provides useful external validation for the idea that AI tools are becoming more common in online problem-solving and technical help contexts.

### 10.2 Pew AI Awareness and Attitudes

The Pew survey data provides broader public context. The awareness results show that many respondents have heard at least something about AI. This matters because AI tools can only become part of mainstream help-seeking behavior if people are aware of them.

The attitude results show that public reactions are mixed and cautious rather than purely positive. This is important because increasing AI visibility does not automatically mean full trust or acceptance. People may search for or use AI tools while still having concerns about them.

---

## 11. Machine Learning Analysis

The machine learning part adds a predictive layer to the project. Instead of only describing search patterns, the models test whether AI-related and non-AI observations can be distinguished from the available data.

Two machine learning tasks were used:

| Task | Goal |
|---|---|
| Classification | Predict whether a Google Trends observation is AI-related or non-AI. |
| Regression | Predict the Google Trends search interest score. |

### 11.1 Classification Task

The classification task asks whether a model can identify AI-related observations from trend behavior. The project tests baseline classification, Logistic Regression, Decision Tree, and Random Forest models.

Two feature settings were used:

| Feature Set | Meaning |
|---|---|
| Pattern-only features | Uses trend score, time, and category, but not keyword names. |
| Full features | Includes keyword names, which makes the task easier but less meaningful for interpretation. |

The pattern-only feature set is more important because it tests whether AI-related behavior can be detected without directly giving the model the keyword name.

### 11.2 Classification Results

![Figure 7. Classification model comparison](../figures/09_classification_model_comparison.png)

The classification results show that the baseline model performs poorly for identifying AI-related observations, while the Random Forest pattern-only model performs strongly.

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Baseline | 0.6484 | 0.0000 | 0.0000 | 0.0000 | 0.5000 |
| Logistic Regression - pattern | 0.8402 | 1.0000 | 0.5455 | 0.7059 | 0.8436 |
| Decision Tree - pattern | 0.8858 | 0.8095 | 0.8831 | 0.8447 | 0.9552 |
| Random Forest - pattern | 0.9315 | 0.9189 | 0.8831 | 0.9007 | 0.9920 |

The best pattern-only model is Random Forest, with an F1-score of **0.9007** and ROC-AUC of **0.9920**. This suggests that trend behavior, timing, and category information contain useful signals for distinguishing AI-related and non-AI observations.

### 11.3 Confusion Matrix and Error Interpretation

![Figure 8. Confusion matrix for the best pattern-only classifier](../figures/10_confusion_matrix.png)

The best pattern-only classifier correctly classified **204 out of 219** test observations.

| Actual / Predicted | Predicted non-AI | Predicted AI |
|---|---:|---:|
| Actual non-AI | 136 | 6 |
| Actual AI | 9 | 68 |

Most errors occurred in contexts where AI-based study support and traditional study-support platforms may have overlapping search behavior. This is reasonable because students may search for AI-based and traditional study resources in similar time periods or under similar academic demand patterns.

### 11.4 Feature Importance

![Figure 9. Feature importance for the Random Forest pattern-only classifier](../figures/11_feature_importance.png)

Feature importance analysis shows that `trend_score` is the strongest signal in the Random Forest pattern-only model. Time-related variables such as `time_index` and `year` also contribute to classification.

This result is important because it suggests that the model is not only relying on category labels. Search interest level and time-related changes help distinguish AI-related observations from traditional platform observations. This directly addresses the ML feedback by explaining what the feature importances mean.

### 11.5 Model Validation

Cross-validation was used to check whether the classification performance was reliable:

| Metric | Mean Score | Standard Deviation |
|---|---:|---:|
| F1-score | 0.7851 | 0.2672 |
| Accuracy | 0.8642 | 0.1708 |

The model performs better than the baseline on average, but the standard deviation is relatively high. This means that performance changes depending on the split.

A time-based split was also tested:

| Model | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Random Forest - random split | 0.9315 | 0.9189 | 0.8831 | 0.9007 | 0.9920 |
| Random Forest - time-based split | 0.5845 | 0.3971 | 0.3506 | 0.3724 | 0.4153 |

The time-based split performs much worse than the random split. This shows that AI-related search behavior is dynamic: older patterns do not perfectly predict newer periods.

### 11.6 Regression Task

The regression task predicts the Google Trends search interest score. The best model is Random Forest Regression:

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Random Forest Regression | 2.6070 | 5.3726 | 0.9453 |

![Figure 10. Actual vs predicted trend scores](../figures/13_actual_vs_predicted_trend_scores.png)

The actual vs predicted plot shows that many predictions are close to the diagonal line, especially for low and medium search interest values. Some high spikes are harder to predict, which is expected because sudden Google Trends peaks can be irregular.

The regression results suggest that search interest is not random. It can be predicted from time, category, keyword, platform type, and AI/non-AI information.

---

## 12. Discussion

The results from different parts of the project tell a consistent but careful story. Google Trends shows that AI-related search behavior is becoming more visible in selected help-seeking contexts. Hypothesis tests show that AI-related and traditional search patterns differ statistically. Wilcoxon robustness checks support these findings even when the normality assumption is relaxed.

Platform traffic data adds another layer. Some AI platforms increased during the observed traffic window, while selected traditional study-support platforms decreased. However, the traffic results also show why scale matters: ChatGPT had a small negative percentage change in the short window but still had the largest traffic scale. This prevents an overly simple interpretation.

Survey evidence also supports the broader shift. Stack Overflow survey results show a strong increase in AI tool usage among respondents from 2023 to 2025. Pew data adds nuance by showing that AI awareness is high, but public attitudes remain mixed and cautious.

Machine learning adds a final layer of evidence. The classification model shows that AI-related and non-AI observations can often be separated using pattern-only features. Feature importance shows that `trend_score` and time-related variables are meaningful signals. The time-based split, however, shows that AI-related behavior changes over time and is not perfectly stable.

Taken together, the findings support the idea of a measurable shift in online attention toward AI-based help-seeking tools. The evidence is strongest for visibility, attention, and pattern differences. It is weaker for direct individual-level replacement, because none of the datasets track the same users over time.

---

## 13. Limitations

This project has several limitations.

First, Google Trends does not provide individual-level data. It shows aggregated search interest, so it cannot prove that the same people moved from traditional platforms to AI tools.

Second, the keyword operationalization is limited. The selected comparisons represent advice and interaction, general help-seeking, and study support, but they do not cover every possible form of online help-seeking.

Third, the traffic dataset covers only a short recent time window. It is useful as supporting context, but it cannot prove a long-term behavioral shift.

Fourth, the survey datasets represent specific respondent groups. Stack Overflow respondents are not the entire population, and Pew survey results describe broader awareness and attitudes rather than direct platform replacement.

Finally, the machine learning results show distinguishable patterns, but predictive performance does not imply causality. The models support the idea that AI-related and non-AI observations differ, but they do not explain all reasons behind the shift.

---

## 14. What This Project Does Not Claim

This project does **not** claim that traditional platforms have disappeared. Traditional platforms still remain visible in the data.

This project does **not** claim direct individual-level migration. Google Trends cannot show whether the same users switched from one platform to another.

This project does **not** claim causal proof. The analysis shows patterns, differences, associations, and predictive signals, but not direct causation.

The safest interpretation is that AI-related tools have become a measurable part of online help-seeking behavior and that search attention is shifting toward AI-based tools in selected contexts.

---

## 15. AI Assistance Disclosure

AI tools were used during this project for brainstorming, organizing the report and README structure, improving wording, debugging code errors, and making explanations clearer. AI assistance was also used to help design the project website and improve the presentation of results.

All datasets, code execution, analysis decisions, visualizations, results, and final interpretations were reviewed and completed by the student.

---

## 16. Conclusion

This project finds evidence that AI-based tools are becoming an important part of online help-seeking, advice-seeking, and study-support behavior. The strongest evidence comes from Google Trends, hypothesis testing, and robustness checks. Platform traffic data, Stack Overflow survey evidence, Pew survey context, and machine learning results strengthen the interpretation by adding external and predictive layers.

The project supports three main conclusions:

| Conclusion | Meaning |
|---|---|
| AI-related search behavior is visible | People are increasingly searching for AI-related help terms in selected contexts. |
| AI and traditional patterns differ | Their search trends are statistically and behaviorally different. |
| The shift is not complete replacement | Traditional platforms still remain, but AI tools are now part of the help-seeking environment. |

Overall, the findings suggest that the rise of AI tools is changing how people look for help online. The story is not complete replacement. It is a measurable reallocation of online attention toward AI-based help.

---

## Appendix: How to Reproduce the Analysis

Install the required packages:

```bash
pip install -r requirements.txt
```

Open and run the notebooks in order:

```text
01_data_preparation.ipynb
02_eda_and_hypothesis_tests.ipynb
03_machine_learning_analysis.ipynb
```

Raw source files are stored in `data/raw/`, while cleaned files used in analysis are stored in `data/processed/`. Figures used in the README, website, and report are stored in `figures/`.
