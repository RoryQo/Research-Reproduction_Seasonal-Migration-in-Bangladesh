# Research Reproduction: Underinvestment in a Profitable Technology: The Case of Seasonal Migration in Bangladesh

(In progress)

## Table of Contents
1. [Overview](#overview)
2. [Key Resources](#key-resources)
3. [Objective](#objective)
4. [Structure](#structure)
   1. [Data Loading and Exploration](#1-data-loading-and-exploration)
   2. [Data Cleaning](#2-data-cleaning)
   3. [Regression Analysis](#3-regression-analysis)
   4. [Replication of Key Results](#4-replication-of-key-results)
   5. [Instrumental Variables Analysis](#5-instrumental-variables-analysis)
   6. [Interpretation and Economic Meaning](#6-interpretation-and-economic-meaning)
5. [Conclusion](#conclusion)



## Overview

This repository focuses on the analysis of a **Randomized Control Trial (RCT)** from Bryan, G., Chowdhury, S., and Mobarak, A. M. (2014). The reproduction involves the analysis of the effects of **seasonal migration** on household consumption and expenditures in rural Bangladesh, as studied in their paper, *Underinvestment in a Profitable Technology: The Case of Seasonal Migration in Bangladesh*, published in *Econometrica*.

The primary objective of the assignment is to replicate key results from the paper and interpret the findings based on RCT methodology.

[![View Original Research Paper](https://img.shields.io/badge/View%20Original%20Research%20Paper-0056A0?style=flat&logo=external-link&logoColor=white&color=0056A0)](https://www.aeaweb.org/articles?id=10.1257/aer.98.1.311)



## Key Resources

1. **Dataset**: The data for this analysis comes from Bryan, G., Chowdhury, S., and Mobarak, A. M.'s (2014) paper. The datasets can be obtained from Mushfiq Mobarak's faculty page at Yale University and the Harvard Dataverse.
2. **Packages Required**:
   - `haven`: For reading Stata `.dta` files.
   - `dplyr`: For data manipulation.
   - `ggplot2`: For data visualization (optional).
   - `lfe`: For fixed effects regressions.
   - `stargazer`: For generating formatted regression tables.



## Objective

The repository involves the following tasks:

1. **Data Exploration**: Load and explore the provided datasets from Round 1 and Round 2. Determine the number of observations and the level of analysis (e.g., household, village).
   
2. **Data Cleaning**: Select specific variables for analysis from the Round 1 and Round 2 datasets. These include variables related to household expenditures, calorie consumption, savings, and migration.

3. **Regression Analysis**: Perform multiple regressions to study the effects of the `incentivized` treatment (cash or credit) on various household characteristics, including total household expenditures, calorie consumption, and savings.

4. **Replication of Results**: Replicate key results from the paper, particularly the effects of the treatment on migration behavior and household expenditures, including the use of instrumental variables (IV) where applicable.

5. **Interpretation**: Interpret the regression coefficients, particularly focusing on the economic meaning of the results and how they relate to the treatment effects observed in the study.



## Structure

### 1. Data Loading and Exploration

- **Task**: Load the datasets (`Round1_Controls_Table1.dta` and `Round2.dta`) and identify the number of observations and the level of analysis (e.g., household, village).
- **Outcome**: After loading the data, you will perform basic exploration to answer questions such as:
  - How many observations are in each dataset?
  - What is the unit of analysis (e.g., individual, household, village)?



### 2. Data Cleaning

- **Task**: Clean the data by selecting a subset of variables that will be used in the analysis. The relevant variables include:
  - **Round 1 Variables**: `incentivized`, `q9pdcalq9` (calories per person per day), `exp_total_pc_r1` (total monthly expenditures per capita), `hhmembers_r1` (household size), `tsaving_hh_r1` (total household savings).
  - **Round 2 Variables**: `incentivized`, `average_exp2` (total consumption per person), `upazila` (sub-district name), `village`, `migrant` (whether a household member migrates), `total_fish` (expenditure on fish).
- **Outcome**: Clean datasets ready for analysis.



### 3. Regression Analysis

- **Task**: Regress various household characteristics on the `incentivized` indicator. This will allow you to determine the effects of receiving the treatment (cash or credit) on key outcomes such as household expenditures, calorie consumption, and savings.
- **Outcome**: A series of regression results, including standard errors, regression coefficients, and significance levels. You will use fixed effects regressions to control for unobserved heterogeneity.



### 4. Replication of Key Results

- **Task**: Replicate specific tables and results presented in the original paper. For example:
  - Table 1: Regress baseline household characteristics on the `incentivized` treatment indicator and generate a table similar to the one in the paper.
  - Table 3: Replicate the results presented in the third row of the fourth column, adjusting for outliers and using the appropriate clustering of standard errors.
- **Outcome**: Reproduced tables and correct interpretation of the findings based on the paper's methodology.



### 5. Instrumental Variables Analysis

- **Task**: Use instrumental variables (IV) to address endogeneity concerns, specifically to estimate the **Local Average Treatment Effect (LATE)** of migration on household expenditures.
- **Outcome**: First-stage regression and IV estimation results, along with an interpretation of how the instrument is related to migration behavior.



### 6. Interpretation and Economic Meaning

- **Task**: Interpret the coefficients and standard errors from each regression. Discuss what the results mean in the context of the paper's findings and the broader implications for policy and theory.
- **Outcome**: Detailed analysis of the treatment effects, along with a discussion on policy relevance, especially regarding the cost-effectiveness of migration incentives.



## Conclusion




