# Phase 1 Report

## Project Topic

This project explores whether people may be shifting some forms of interaction and support-seeking from human-based sources to AI-based alternatives. The broader focus includes asking questions, getting advice, emotional support, and interaction with AI.

## Data Sources

The main data source used in this phase is Google Trends. Three keyword comparison datasets were collected to represent different dimensions of human-based and AI-related search behavior.

The datasets used in this phase are:
- **Advice-Seeking Keyword Comparison**
- **General Help-Seeking Keyword Comparison**
- **Study Support Keyword Comparison**

In the later stages of the project, additional survey-based datasets may also be incorporated to strengthen the analysis. Based on the project proposal, these may include the **2025 Stack Overflow Developer Survey** and **Pew Research survey data**.  

## How the Data Was Collected

The datasets were collected from Google Trends by comparing selected keywords over time. The goal was to represent both traditional human-based platforms or behaviors and AI-related alternatives.

The datasets used in this phase include the following comparisons:

- **Advice / interaction:**  
  `Yahoo Answers` and `Ask.fm` were used as older human-based question-and-answer platforms, while `ai friend` was used as an AI-related interaction term.

- **General help-seeking:**  
  `quora` was used as a human-based question and answer platform, while `chatgpt help` was used as an AI-related help-seeking term.

- **Study support:**  
  `course hero` and `chegg` were used as traditional study-help platforms, while `chatgpt study` was used as an AI-related study-support term.

These data were downloaded as CSV files and then analyzed in Python.

## Data Cleaning and Preparation

The datasets were loaded into Python using pandas. Several preprocessing steps were applied:

- replacing `<1` values with `0.5`
- converting date columns into datetime format
- converting keyword columns into numeric format
- removing unnecessary formatting issues from Google Trends files when needed

For the advice and study comparisons, human-based terms were also combined into a **human average** variable in order to compare them more directly with the AI-related term.

## Exploratory Data Analysis

EDA was conducted using:
- line plots for keyword trends over time
- descriptive statistics
- correlation analysis
- difference calculations between AI-related and human-based terms
- ratio calculations to examine the relative strength of AI-related terms compared to human-based terms

## Initial Findings

The initial analysis suggests that AI-related and human-based search terms do not follow the same pattern over time.

In the advice / interaction comparison, older human-based platforms such as Yahoo Answers and Ask.fm show lower or declining relative strength, while the AI-related term `ai friend` becomes more prominent over time.

In the general help-seeking comparison, `quora` and `chatgpt help` show opposite trends over time, with one declining while the other rises. This suggests that AI-related help-seeking behavior does not follow the same path as the traditional human-based platform represented by `quora`.

In the study support comparison, `chatgpt study` gains relative strength compared to traditional study-help platforms such as Course Hero and Chegg.

Overall, the findings do not prove a complete shift from human-to-human interaction to human-to-AI interaction, but they do suggest that the relationship between these two forms of search behavior is changing over time.

## Hypothesis Testing

Paired t-tests were used to test whether the differences between AI-related and human-based terms are statistically significant.

The tests compared:
- `ai friend` and the human-based advice average
- `chatgpt help` and `quora`
- `chatgpt study` and the human-based study average

The results showed statistically significant differences in all three comparisons, indicating that the AI-related and human-based terms differ in meaningful ways rather than only by random variation.

## Planned Use of the Data

In the next phase of the project, these Google Trends datasets will continue to be used to analyze whether relative shifts can be observed between human-based and AI-based forms of interaction, help-seeking, and support.

In addition, two survey-based sources mentioned in the proposal may be incorporated in future stages:
- the **2025 Stack Overflow Developer Survey**, to examine how people use AI tools for learning and problem solving
- **Pew Research survey data**, to provide a broader perspective on emotional or personal uses of AI  [oai_citation:1‡DSA210 - Project Proposal.pdf](sediment://file_000000005b0872469d3d99c1b04853ee)

These additional datasets may help support the Google Trends findings with survey-based evidence and make the final analysis more comprehensive.
