


# Inferential statistics

Inferential statistics is a branch of statistics that aims to draw conclusions about a population from a sample of that population. Unlike descriptive statistics, which simply describes and summarizes the characteristics of a sample, inferential statistics uses statistical methods and models to make inferences or predictions about the wider population from which the sample is drawn.

The main techniques of inferential statistics include hypothesis testing, parameter estimation, analysis of variance (ANOVA), regression and forecasting methods. Here are some fundamental concepts associated with inferential statistics:

## Population and sample

In statistics, population is the entire set of items from which you draw data for a statistical study. It can be a group of individuals, a set of items, etc. It makes up the data pool for a study. Generally, population refers to the people who live in a particular area at a specific time. But in statistics, population refers to data on your study of interest. It can be a group of individuals, objects, events, organizations, etc. You use populations to draw conclusions.

A sample is defined as a smaller and more manageable representation of a larger group. A subset of a larger population that contains characteristics of that population. A sample is used in statistical testing when the population size is too large for all members or observations to be included in the test.\
The sample is an unbiased subset of the population that best represents the whole data.

The characteristics of samples and populations are described by numbers called statistics and parameters:

- A statistic is a measure that describes the sample (e.g., sample mean).
- A parameter is a measure that describes the whole population (e.g., population mean).

There are two important types of estimates you can make about the population: point estimates and interval estimates.

A point estimate is a single value estimate of a parameter. For instance, a sample mean is a point estimate of a population mean.
An interval estimate gives you a range of values where the parameter is expected to lie. A confidence interval is the most common type of interval estimate.

## Parameter estimations
Parameter estimation is the process of calculating the expected value of a population parameter based on samples taken from that population. 

## Confidence interval

A confidence interval uses the variability around a statistic to come up with an interval estimate for a parameter. Confidence intervals are useful for estimating parameters because they take sampling error into account.\
Each confidence interval is associated with a confidence level. A confidence level tells you the probability (in percentage) of the interval containing the parameter estimate if you repeat the study again.
A 95% confidence interval means that if you repeat your study with a new sample in exactly the same way 100 times, you can expect your estimate to lie within the specified range of values 95 times.

## Hypothesis

Hypothesis testing is a fundamental concept in inferential statistics that involves making decisions or drawing conclusions about populations based on sample data. In hypothesis testing, we start with two competing hypotheses: the null hypothesis (H0) and the alternative hypothesis (H1). These hypotheses are statements about the population parameter(s) of interest.

1. Null Hypothesis (H0):
    * The null hypothesis represents the status quo or the default assumption. It suggests that there is no significant difference or effect, or no relationship between variables in the population.
    * The null hypothesis typically states that the population parameter(s) equals a specific value or follows a specific distribution.
    * It is denoted by H0.

2. Alternative Hypothesis (H1):
    * The alternative hypothesis contradicts the null hypothesis and suggests that there is a significant difference, effect, or relationship in the population.
    * The alternative hypothesis can take different forms depending on the research question and the nature of the hypothesis being tested.
    * It is denoted by H1.
    
The process of hypothesis testing involves the following steps:

1) Formulate Hypotheses: Clearly state the null and alternative hypotheses based on the research; question or problem.
2) Select Significance Level: Choose a significance level (α), typically set at 0.05 or 0.01, which represents the probability of rejecting the null hypothesis when it is actually true.
3) Collect Data and Calculate Test Statistic:Collect sample data and compute a test statistic that measures the strength of evidence against the null hypothesis.
4) Determine Critical Region: Determine the critical region or rejection region, which consists of the values of the test statistic that lead to rejection of the null hypothesis.
5) Make Decision: Compare the calculated test statistic to the critical value(s) or use p-values to decide whether to reject the null hypothesis. If the test statistic falls in the critical region or if the p-value is less than the significance level, reject the null hypothesis in favor of the alternative hypothesis. Otherwise, fail to reject the null hypothesis.
6) Interpret Results: Interpret the results of the hypothesis test in the context of the research question. Draw conclusions about the population based on the sample data and the outcome of the hypothesis test.

## Statistical tests

There are various types of statistical tests, each designed to address different research questions and hypotheses. Some of the most commonly used statistical tests include:

1. T test or Student test

The Student's t-test is a statistical hypothesis test used to determine if there is a significant difference between the means of two groups. 

```r
corn_data <- read_excel("data/data_for_workshop2.xls", sheet = "corn_data")

# convert qualitative variables in factors
corn_data <- corn_data %>%
  mutate_if(is.character, as.factor)

# subset for the treatments "cont" and "rh"
cont_data <- subset(corn_data, Treatments == "Cont")
rh_data <- subset(corn_data, Treatments == "RH")

# Test de Student pour comparer les moyennes du nombre d'épis entre les traitements "Cont" et "RH"
t_test_result <- t_test_result <- t.test(cont_data$`Nb of ears`, rh_data$`Nb of ears`, alternative = "two.sided", mu = 0, conf.level = 0.95)

# Affichage des résultats du test de Student
print(t_test_result)
#> 
#> 	Welch Two Sample t-test
#> 
#> data:  cont_data$`Nb of ears` and rh_data$`Nb of ears`
#> t = -3.0566, df = 54.847, p-value = 0.003455
#> alternative hypothesis: true difference in means is not equal to 0
#> 95 percent confidence interval:
#>  -36.424992  -7.575008
#> sample estimates:
#> mean of x mean of y 
#>  14.73333  36.73333
```
The p-value is <0.05 so we accept the alternative hypothesis: there is a significant difference in the average number of ears between the cont treatment and rh treatment groups

2. ANOVA

ANOVA (Analysis of variance) is a statistical method used to analyze the differences between the means of two or more groups or treatments.

```r
#
data_anova <- subset(corn_data, (Condition=="rotation" | Condition=="non-rotation"))

anova_test <- aov(data_anova$`Nb of ears`~data_anova$Condition + data_anova$Treatments)
summary(anova_test)
#>                        Df Sum Sq Mean Sq F value   Pr(>F)
#> data_anova$Condition    1     14      14   0.030    0.863
#> data_anova$Treatments   3  12609    4203   8.719 2.93e-05
#> Residuals             115  55438     482                 
#>                          
#> data_anova$Condition     
#> data_anova$Treatments ***
#> Residuals                
#> ---
#> Signif. codes:  
#> 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

This strong evidence suggests that the "Treatments" factor has a statistically significant effect on "No. of ears". There is less than a 0.01% chance of observing this result by chance, which means that the differences observed in "No. of ears" are probably due to the different treatments applied.

3. Chi-Square test

The chi-square test is a statistical test used to determine if there is a significant association between two categorical variables.

```r
#load the data
heart_attack1 <- read.csv("data/heart_attack_prediction_dataset.csv")

#transform the variable into factors
heart_attack1$Heart.Attack.Risk <- factor(heart_attack1$Heart.Attack.Risk, 
                  levels = c(0, 1),
                  labels = c("No", "Yes"))

#construct the contingency table for the test between heart attack risk ans sex
chi_data = table(heart_attack1$Heart.Attack.Risk,heart_attack1$Sex) 
chi_data
#>      
#>       Female Male
#>   No    1708 3916
#>   Yes    944 2195
                 
#test of chi2
print(chisq.test(chi_data))
#> 
#> 	Pearson's Chi-squared test with Yates' continuity
#> 	correction
#> 
#> data:  chi_data
#> X-squared = 0.070494, df = 1, p-value = 0.7906
```
P-value >0.05 so we can conclude that the risk of heart attack is not statistically significant between men and women. 

