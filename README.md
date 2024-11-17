<h2 align="center"> Research Replication: Migration</h2>                            
    
     
<table align="center"> 
  <tr>    
    <td colspan="2" align="center"><strong>Table of Contents</strong></td>  
  </tr> 
  <tr>
    <td>1. <a href="#project-setup">Project Setup</a></td>   
    <td>5. <a href="#step-3-first-stage">Step 3: First Stage Effects</a></td> 
  </tr>
  <tr> 
    <td>2. <a href="#r-libraries">R Libraries</a></td>   
    <td>6. <a href="#step-4-reduced-form">Step 4: Reduced Form</a></td>
  </tr>
  <tr>
    <td>3. <a href="#loading-the-data">Loading the Data</a></td>   
    <td>7. <a href="#step-5-estimating-the-local-average-treatment-effect-late">Step 5: Estimating the Local Average Treatment Effect (LATE)</a></td>
  </tr>
  <tr>
    <td>4. <a href="#replication-steps">Replication Steps</a></td>   
    <td>8. <a href="#conclusion">Conclusion</a></td>
  </tr>
  <tr>
    <td colspan="2">9. <a href="#references">References</a></td>   
  </tr>
</table>





## Overview

This document provides a replication of the empirical analysis from Bryan, G., Chowdhury, S., and Mobarak, A. M. (2014), titled *"Underinvestment in a Profitable Technology: the Case of Seasonal Migration in Bangladesh,"* published in *Econometrica*. The study investigates how seasonal migration, subsidized by random treatment, impacts household consumption during the lean season in rural Bangladesh.

The purpose of this project is to replicate key analyses from the original paper using the provided dataset and R programming language. The focus is on estimating treatment effects, interpreting regression results, and understanding the causal relationship between migration and household welfare.

[![View Original Research Paper](https://img.shields.io/badge/View%20Original%20Research%20Paper-0056A0?style=flat&logo=external-link&logoColor=white&color=0056A0)](https://poverty-action.org/sites/default/files/publications/Under-investment%20in%20a%20Profitable%20Technology.pdf)

## Project Setup

### R Libraries

To replicate the analysis, the following R libraries are required:
- `haven`: for loading Stata `.dta` files.
- `dplyr`: for data manipulation.
- `ggplot2`: for data visualization (if needed).
- `lfe`: for fitting linear models with fixed effects.
- `stargazer`: for generating formatted regression tables.

### Loading the Data

The analysis uses two main rounds of data:
1. **Round 1 Data**: Contains baseline household characteristics.
2. **Round 2 Data**: Contains post-treatment data on migration and household expenditures.

The data is loaded into R, where each observation represents a household:
- `R1` contains data from Round 1 (baseline).
- `R2` contains data from Round 2 (post-treatment).

## Replication Steps

### Step 1: Merging Data

The first step is to merge the Round 1 and Round 2 datasets by household ID (`hhid`), village, and treatment indicator (`incentivized`). This combined dataset allows us to connect baseline characteristics with post-treatment data on migration and expenditures. This enables us to evaluate how treatment impacts migration and household consumption by linking pre- and post-treatment information.

### Step 2: Regression Analysis - Round 1

To replicate Table 1 (the difference column), we regress baseline household characteristics on the treatment indicator (`incentivized`), clustering standard errors by village. This regression estimates the intention-to-treat (ITT) effect on various baseline outcomes such as household savings, expenditures, and caloric intake.

<img src="https://github.com/RoryQo/Research-Reproduction_Seasonal-Migration-in-Bangladesh/blob/main/Table1.jpg?raw=true" alt="Table 1" width="550px"/>


#### Interpretation:
The ITT estimates measure the effect of being offered the migration incentive (i.e., receiving the treatment), regardless of whether the household actually migrates. For example, the ITT effect on total calories consumed, household expenditures, and savings will show how receiving the treatment (offered an incentive) impacts these variables on average, even for those who did not migrate. These estimates help us understand the broader impact of being in the treatment group, not just the direct effect of migration.

### Step 3: First Stage

Next, we estimate the effect of the treatment on migration using data from Round 2 (first-stage regression). Specifically, we regress whether a household member migrated (`migrant`) on the treatment indicator (`incentivized`). This regression allows us to estimate the likelihood that the treatment increases migration, clustering standard errors by village.

<img src="https://github.com/RoryQo/Research-Reproduction_Seasonal-Migration-in-Bangladesh/blob/main/Table_FirstStage.jpg?raw=true" alt="First Stage Table" width="400px"/>


#### Interpretation:
The migration effect captures the relationship between the treatment and the likelihood of seasonal migration. If the treatment (cash or credit) successfully incentivizes migration, the coefficient on `incentivized` should be positive, indicating that households in the treatment group are more likely to migrate. This regression is crucial for understanding the strength of the instrument.  

The instrument is strong because we can see the f stat (12.4) is greater than 10.

```
summary(model)$fstat[1]
```

### Step 4: Reduced Form

To replicate Table 3 (row 3, column 4), we regress total consumption per capita in Round 2 on the treatment indicator (`incentivized`), excluding outliers (e.g., extreme values of fish consumption). This regression estimates the effect of receiving the treatment on total household consumption in the post-treatment period.

<img src="https://github.com/RoryQo/Research-Reproduction_Seasonal-Migration-in-Bangladesh/blob/main/Table_ReducedForm.jpg?raw=true" alt="Reduced Form Table" width="450px"/>


#### Interpretation:
This analysis estimates the effect of the treatment on consumption outcomes (food and non-food). If the treatment increases household consumption, we would expect the coefficient on `incentivized` to be positive, showing an increase in total household consumption as a result of the treatment. Excluding outliers is important to ensure that the results are not unduly influenced by extreme data points, such as unusually high expenditures on fish.

### Step 5: Estimating the Local Average Treatment Effect (LATE)

To isolate the causal effect of migration on household consumption, we use an instrumental variable (IV) approach. Migration is treated as an endogenous variable, with the treatment indicator (`incentivized`) serving as the instrument. The instrumental variable approach allows us to estimate the Local Average Treatment Effect (LATE), which focuses on the effect of migration for those households who were induced to migrate by the treatment.

```
m1 <- felm(average_exp2 ~ 1 | upazila | (migrant ~ incentivized)|village, data = r2)
```

#### Interpretation:
The LATE estimates provide a more precise understanding of how migration affects household welfare for the subset of households who actually migrated as a result of the treatment. This method addresses the potential endogeneity of migration, as not all households who are incentivized to migrate will actually do so. By using the treatment as an instrument, we are able to isolate the causal effect of migration on household consumption, focusing on the "compliers" who migrate because of the treatment. The LATE is particularly useful for understanding the true effect of migration on consumption for those households who take up the treatment.

## Conclusion

This replication successfully reproduces key elements of the empirical analysis from Bryan et al. (2014) using R. By estimating treatment effects on migration and consumption, we gain insights into the impact of seasonal migration subsidies on household welfare.

The results contribute to understanding the causal relationship between migration and household welfare, providing important policy insights into how migration subsidies can improve household consumption. Through this process of replication, we not only validate the original findings but also enhance our understanding of the mechanisms through which seasonal migration can be leveraged as a tool for improving rural household welfare.


## References

Gharad, Bryan, et al. “Underinvestment in a Profitable Technology: The Case of Seasonal Migration in Bangladesh.” Econometrica, vol. 82, no. 5, 2014, pp. 1671–1748, https://doi.org/10.3982/ecta10489.
