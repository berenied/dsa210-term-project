# Phase 2 Report

## Project Topic

This project explores whether people may be shifting some forms of help-seeking, advice-seeking, and study support from traditional human-based platforms toward AI-based alternatives.

The main focus is not to prove that people completely stopped using platforms such as Quora, Chegg, Course Hero, Yahoo Answers, or Ask.fm. Instead, this phase examines whether search behavior and supporting datasets suggest that AI-based tools are becoming more important in these contexts.

## Data Sources

The main data source used in this phase is Google Trends. Three keyword comparison datasets were used to represent different types of help-seeking behavior:

- **Advice-Seeking Keyword Comparison**
- **General Help-Seeking Keyword Comparison**
- **Study Support Keyword Comparison**

In addition to Google Trends, this phase also uses supporting datasets:

- **Platform traffic context data**
- **Stack Overflow AI adoption survey data**
- **Pew AI survey data**

Google Trends is used as the main evidence because it directly shows search interest over time. The other datasets are used as external support and context.

## Keyword and Platform Context

The selected keywords represent different types of online help-seeking platforms and AI-related alternatives.

- **Yahoo Answers** and **Ask.fm** represent older question-and-answer or advice-seeking platforms where users asked questions to other people.
- **Quora** represents a human-based Q&A platform used for general questions and explanations.
- **Chegg** and **Course Hero** represent traditional online study-support platforms used by students for homework help, explanations, and course-related resources.
- **AI-related terms** such as `ai friend`, `chatgpt help`, and `chatgpt study` represent newer AI-based alternatives for interaction, help-seeking, and study support.

The platform traffic dataset also includes several additional platforms for recent context:

- **ChatGPT, Claude, and Character AI** represent AI-based platforms.
- **Quora** represents a forum/Q&A platform.
- **WikiHow** represents a general help platform.
- **Chegg, Course Hero, Khan Academy, and Quizlet** represent study-support platforms.

This grouping allows the project to compare traditional human-based platforms with AI-related search behavior and recent platform activity in similar categories.

## How the Data Was Prepared

The raw datasets were cleaned and processed in the first notebook, `01_data_preparation.ipynb`.

The Google Trends files were converted into a clean long-format dataset. Keyword names were cleaned, date columns were converted into datetime format, and trend scores were converted into numeric values. Values such as `<1` were treated as `0.5`.

The keywords were also classified by platform type:

- **AI platform**
- **Forum / Q&A platform**
- **Study support platform**

For the Stack Overflow survey, only AI-related columns were selected and then summarized by year. For the Pew survey, AI awareness and AI attitude variables were selected and summarized. The traffic dataset was also cleaned so that monthly visits could be compared across platforms.

## Exploratory Data Analysis

The EDA focused mainly on Google Trends data. The analysis included:

- line plots showing keyword trends over time
- descriptive statistics for each keyword
- comparison of AI-related terms with traditional platform terms
- difference calculations
- ratio calculations
- correlation analysis

The Google Trends data was also reshaped into separate category-level datasets:

- advice-seeking
- general help-seeking
- study support

This made it easier to compare AI-related terms directly with traditional platform terms in the same category.

## Initial Findings from Google Trends

The Google Trends results show that AI-related and traditional platform search terms do not follow the same pattern over time.

In the advice-seeking category, `ai friend` becomes more visible compared with older human-based platforms such as Yahoo Answers and Ask.fm.

In the general help-seeking category, `chatgpt help` follows a different pattern from Quora. Quora still has high search interest in many periods, but the AI-related search term shows a separate and growing pattern.

In the study-support category, `chatgpt study` gains importance compared with traditional study-support platforms such as Chegg and Course Hero. Traditional platforms still appear in the data, but AI-related study support becomes more visible over time.

These findings suggest that AI-related search behavior is becoming more important, especially in advice-seeking and study-support contexts.

## Difference and Ratio Analysis

To compare AI-related and traditional search interest more directly, two extra measures were calculated:

- **Difference:** AI-related search interest minus traditional platform average
- **Ratio:** AI-related search interest divided by traditional platform average

These measures help show whether AI-related search terms are becoming stronger or weaker compared with traditional platforms in the same time period.

The results show that the relationship between AI and traditional platforms is not exactly the same in every category. In some areas, AI-related terms become much stronger. In others, traditional platforms still remain high, but AI terms show different trend behavior.

This suggests that the change is not a simple complete replacement. Instead, AI-related search behavior is becoming part of the broader help-seeking environment.

## Correlation Analysis

Correlation analysis was used to examine the relationship between AI-related and traditional search terms.

Several AI-related and traditional platform comparisons showed negative correlations. This means that in some cases, as AI-related search interest increased, traditional platform search interest moved in the opposite direction.

However, correlation does not prove causation. These results should be interpreted as evidence of different trend patterns, not as proof that one platform directly caused the decline of another.

## Hypothesis Testing

Paired t-tests were used to test whether the differences between AI-related and traditional platform search interest were statistically significant.

The tests compared:

- `ai friend` with the traditional advice-seeking average
- `chatgpt help` with `quora`
- `chatgpt study` with the traditional study-support average

The results showed statistically significant differences in all three comparisons. This means that the AI-related and traditional search terms differ in meaningful ways rather than only by random variation.

However, these tests do not prove that individual users directly replaced traditional platforms with AI tools. They only show that the search patterns are statistically different.

## Platform Traffic Context

Platform traffic data was used as supporting context. This dataset covers a six-month period, so it was not used as the main evidence or for hypothesis testing.

The traffic dataset includes AI platforms, Q&A platforms, general help platforms, and study-support platforms. This helped compare recent platform-level activity across different types of online help-seeking and support tools.

The traffic analysis compared:

- average monthly visits
- log-scale visit patterns
- relative traffic change
- percentage change from the first month to the last month

The results show that AI platforms have very large recent traffic volumes, especially because of ChatGPT. Claude and Character AI showed positive traffic change during the six-month period. Many traditional and study-support platforms, including Quora, WikiHow, Chegg, Course Hero, Quizlet, and Khan Academy, showed negative percentage change.

Because the traffic data covers only six months, it should be interpreted carefully. Still, it provides recent platform-level context that supports the broader pattern found in Google Trends.

## Stack Overflow Survey Validation

The Stack Overflow survey data was used as external validation for AI tool adoption.

The valid-response summary showed that the share of respondents using AI tools increased across survey years:

- 2023: 44.38%
- 2024: 61.84%
- 2025: 78.50%

The share of respondents who did not plan to use AI decreased over time. The “plans to use AI” group also decreased, but this is not necessarily negative. It may mean that many respondents who previously planned to use AI moved into the active “uses AI” group.

This dataset is not the main evidence because it represents Stack Overflow survey respondents rather than the whole population. However, it supports the idea that AI tools are becoming more common in online problem-solving and knowledge-seeking environments.

## Pew AI Survey Context

The Pew AI survey data was used to provide broader public context.

The AI awareness summary showed that many respondents had heard at least something about artificial intelligence. This supports the idea that AI has become a socially visible and widely recognized topic.

The AI attitude summary showed that public reactions are mixed and cautious. This is useful because it shows that AI visibility does not necessarily mean full trust or full acceptance.

For this project, Pew data is not used to prove a direct shift from traditional help-seeking platforms to AI platforms. Instead, it helps explain the broader social context around AI awareness and attitudes.

## Overall Findings

Overall, the findings suggest that AI-related search terms and traditional platform search terms are following different patterns.

The strongest evidence comes from Google Trends and hypothesis testing. Google Trends directly measures search behavior, and the hypothesis tests show that AI-related and traditional search interest differ statistically.

The traffic, Stack Overflow, and Pew datasets strengthen the analysis by adding context:

- traffic data shows recent platform-level changes
- Stack Overflow shows increasing AI tool adoption
- Pew shows high AI awareness and mixed public attitudes

Together, these findings support the idea that AI platforms are becoming increasingly important in help-seeking, advice-seeking, and study-support contexts.

## Conclusion

This phase provides evidence that AI-based tools are becoming more visible and important in online help-seeking and study-support behavior.

The results do not prove a complete replacement of traditional human-based platforms. However, they suggest a shift in attention and search behavior toward AI-based alternatives.

The next stage of the project can build on these findings by using the cleaned and analyzed datasets for further interpretation, final visualizations, and project conclusions.
