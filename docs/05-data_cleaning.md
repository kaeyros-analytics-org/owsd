

# Data cleaning

In the domain of data science, R reigns supreme as a tool for transforming raw data into actionable insights. 
Data cleaning, a core competency of R, empowers us to clean, filter, transform, and aggregate data, paving the way for meaningful analysis. This introductory paragraph delves into the world of data manipulation and data cleaning in R, highlighting its significance and exploring the key concepts involved.

There are several methods used for data cleansing, including:

## Renaming colums

During data cleansing, column renaming plays a crucial role in organizing and clarifying the dataset. This step involves assigning meaningful and consistent names to columns, which facilitates their interpretation and subsequent use in analysis.


```r
#load the package
library(dplyr)

tasba_data <- tasba_data %>%
  dplyr::rename(marital_status =`Are you married?`) %>%
  dplyr::rename(has_children =`Do you  have children?`) %>%
  dplyr::rename(nb_children =`How many children do you have?`) %>%
  dplyr::rename(religion =`What is your religion?`) %>%
  dplyr::rename(has_tasba_farm = `Do have a tasba farm?`) %>%
  dplyr::rename(size_farm = `What's the size of your farm?`) %>%
  dplyr::rename(years_growing_tasba = `How long have you been growing tasba?`) %>%
  dplyr::rename(direct_sowing = `Do you do direct sowing?`) %>%
  dplyr::rename(culture_type = `What type of culture do you do?`) %>%
  dplyr::rename(plants_grown_with_tasba = `If you do polyculture, with what plants do you grow Tasba with?`) %>%
  dplyr::rename(period_sowing_tasba = `When or what time of the year do you sow Tasba?`) %>%
  dplyr::rename(seeds_provider = `Where do you get your seeds?`) %>%
  dplyr::rename(varieties = `What varieties do you grow?`) %>%
  dplyr::rename(varieties_reproductive = `Are your varieties reproductive?`) %>%
  dplyr::rename(nb_varieties_same_field = `How many varieties do you grow on the same plot or in the same field?`) %>%
  dplyr::rename(campains_per_year = `How many campains do you per year?`) %>%
  dplyr::rename(tasba_growth_duration = `How long is the growth cycle in the field?`) %>%
  dplyr::rename(cost_bowl_tasba = `How much does a bowl of tasba cost (cost of buying or selling)`) %>%
  dplyr::rename(cost_kg_seed = `How much does 1kg of tasba seed cost?`) %>%
  dplyr::rename(store_seed = `How do you store your seed?`) %>%
  dplyr::rename(hybrid_varieties = `Do there exist hybride varities?`) %>%
  dplyr::rename(name_varieties = `How do you call these varieties you have?`) %>%
  dplyr::rename(production_kg = `What is the production in kg or ton/year?`) %>%
  dplyr::rename(cultural_system = `What is the cultural system that you use in the field?`) %>%
  dplyr::rename(off_season_cultivation = `Do you do off-season cultivation?`) %>%
  dplyr::rename(has_watering_system = `Do you have watering system?`) %>%
  dplyr::rename(symptoms_noticed = `what symptoms have you noticed?`) %>%
  dplyr::rename(insect_type = `What type of insect do you observe on plant during growth?`) %>%
  dplyr::rename(treatment = `How do you treat them?`) %>%
  dplyr::rename(phytosanitary_products_usage = `Do you use phytosanitary products? (Products used to fight against pests attacking plants)`) %>%
  dplyr::rename(phytosanitary_products_names = `Please give the name of the phytosanitary products you use`) %>%
  dplyr::rename(start_treatment = `To avoid diseases: at what age do you start treating plants?`) %>%
  dplyr::rename(fertilizer_type = `What type of fertilizer do you apply in the field?`) %>%
  dplyr::rename(effective_pest_treatment = `Have you found satisfactory treatment for the plant? ( Against pest action)`) %>%
  dplyr::rename(tasba_leaf_consumption = `How do you eat the leaves of tasba?`) %>%
  dplyr::rename(reason_consumption = `Why do you consume it?`) %>%
  dplyr::rename(tasba_tea_consumption = `If you use like a tea; how do you drink it?`) %>%
  dplyr::rename(treatment_human_disease = `Do you use the leaves of Tasba to treat human diseases?`) %>%
  dplyr::rename(tasba_treatment_type_diseases = `What type of disease can be treated by the leaves of tasba?`) %>%
  dplyr::rename(gic_work = `Do you work in GIC to grow Tasba?`)
```


## Handling Missing Data: 

Missing data, also known as missing values, is a common challenge encountered in data analysis. It refers to the absence of information for specific variables in certain observations within your dataset. To deal with missing data we have two options: impute data or remove data.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.1) Imputation

we can use imputation by mean, median or mode.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mean*:


```r
library(stringr)
#Create a new column of number of varieties
tasba_data$nb_varieties_same_field <- stringr::str_sub(tasba_data$nb_varieties_same_field, 1, 1)

#verify the type of the column
str(tasba_data$nb_varieties_same_field)
#>  chr [1:107] NA NA NA NA NA "1" "1" "1" NA NA "1" "1" ...

#transform the type into number
tasba_data$nb_varieties_same_field <- as.integer(tasba_data$nb_varieties_same_field)

#impute NA values by mean
tasba_data$nb_varieties_same_field[is.na(tasba_data$nb_varieties_same_field)]<-round(mean(tasba_data$nb_varieties_same_field, na.rm = TRUE))
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by median*:


```r
#function to extract the number of kg in the column
tasba_data$production_kg <- sapply(tasba_data$production_kg, function(x) {
    # Extract digits using regular expression and convert to numeric
    str_extract(x, "\\d+") %>% as.numeric()
})

#impute the column by median
tasba_data$production_kg[is.na(tasba_data$production_kg)] <- median(tasba_data$production_kg, na.rm = TRUE)
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mode*:


```r
tasba_data$seeds_provider[is.na(tasba_data$seeds_provider)] <- names(which.max(table(tasba_data$seeds_provider)))
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2) Removing data

There are 2 usuals methods for deleting data when dealing with missing data: listwise and dropping variables.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Listwise*:

In this method, all data for an observation that has one or more missing values are deleted. The analysis is run only on observations that have a complete set of data. 


```r
na.omit(tasba_data)
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Dropping variables*:

If data is missing for a large proportion of the observations, it may be best to discard the variable entirely if it is insignificant.


```r
subset( tasba_data, select = -c(name_varieties))
```

## Handling outliers

Data points far from the dataset’s other points are considered outliers. The presence of outliers can pose significant problems in statistical analysis and machine learning. They can bias model parameter estimates, lead to erroneous conclusions and affect algorithm performance.


```r
outlier_values <- boxplot.stats(tasba_data$nb_children)$out
boxplot(tasba_data$nb_children, main="Number of children", boxwex=0.1)
mtext(paste("Outliers: ", paste(outlier_values, collapse=", ")), cex=0.6)
```

<img src="05-data_cleaning_files/figure-html/unnamed-chunk-8-1.png" width="672" />

After identify outliers you can handle it by either impute those outliers by a value (mean, median, mode) or use the method of capping (For missing values that lie outside the **1.5 * IQR** limits, we could cap it by replacing those observations outside the lower limit with the value of 5th percentile and those that lie above the upper limit, with the value of 95th percentile)

## Removing duplicates: \
Removing duplicates ensures that each data point is represented only once, leading to more accurate and consistent data for analysis.

&nbsp;&nbsp;&nbsp;&nbsp;Remove duplicates consider all rows:

```r
tasba_data <- tasba_data %>% 
  dplyr::distinct()
```

&nbsp;&nbsp;&nbsp;&nbsp; Remove duplicates on selected columns: 

```r
tasba_data %>% distinct(Sex, Age, .keep_all = TRUE)
#> # A tibble: 9 × 42
#>   Sex    Age         marital_status has_children nb_children
#>   <chr>  <chr>       <chr>          <chr>              <dbl>
#> 1 Male   25_40 years NO             NO                     0
#> 2 Male   15_25 years NO             NO                     0
#> 3 Female 15_25 years NO             NO                     0
#> 4 Female 40_50 years YES            YES                    3
#> 5 Male   40_50 years YES            YES                    5
#> 6 Female 25_40 years YES            YES                    5
#> 7 Female 50 years a… YES            YES                   10
#> 8 Male   50 years a… YES            YES                   12
#> 9 Male   25_40 FCFA  YES            YES                    1
#> # ℹ 37 more variables: religion <chr>,
#> #   has_tasba_farm <chr>, size_farm <chr>,
#> #   years_growing_tasba <chr>, direct_sowing <chr>,
#> #   culture_type <chr>, plants_grown_with_tasba <chr>,
#> #   period_sowing_tasba <chr>, seeds_provider <chr>,
#> #   varieties <chr>, varieties_reproductive <chr>,
#> #   nb_varieties_same_field <dbl>, …
```


## Checking data structure: 

Checking data types is a crucial step in data analysis because it ensures you're working with the data in the way it's intended in order to avoid errors later in the analysis.


```r
str(tasba_data)
```

You can change the type of your data across many functions like: as.numeric(), as.character(), as.factor() etc....if the data is not in the right type.
Example:

```r
tasba_data$Sex <- as.factor(tasba_data$Sex)
```


## Handling Inconsistent Categorical Data

Categorical variables may have inconsistent spellings or categories. The recode() function or manual recoding can help standardize categories.


```r
tasba_data <- tasba_data %>%
  dplyr::mutate(store_seed = dplyr::recode(store_seed, "In bags" = "in bags"))
```


## Combine dataframes

Suppose the dataset combines data from different sources, we can combine differents datasets into one. When combining data from multiple sources, ensure that all data fields align correctly.
&nbsp;&nbsp;&nbsp;&nbsp;- Combine by column


```r
culture1 <- data.frame(
  Culture = c("wheat", "maize", "rice"),
  Area = c(100, 150, 120)
)

culture2 <- data.frame(
  Culture = c("wheat", "maize", "rice"),
  Return = c(50, 60, 45)
)

culture_final1 <- cbind(culture1, culture2)
```

&nbsp;&nbsp;&nbsp;&nbsp;- combine by row


```r
culture3 <- data.frame(
  Culture = c("wheat", "maize", "rice"),
  Area = c(100, 150, 120)
)

culture4 <- data.frame(
  Culture = c("potato", "cassava"),
  Area = c(250, 400)
)

culture_final2 <- rbind(culture3, culture4)
```

## Data Validation

Data validation involves checking data against predefined rules or criteria. It ensures that data adheres to specific requirements or constraints.

Validation checks can prevent incorrect or inconsistent data from entering your analysis.

## Regular expressions

Regular expressions (regex) are powerful tools for pattern matching and replacement in text data. The gsub() function is commonly used for global pattern substitution.


```r
tasba_data$cost_kg_seed <- gsub("FCFA", "",
                        tasba_data$cost_kg_seed)
```



