

# Data cleaning

In the domain of data science, R reigns supreme as a tool for transforming raw data into actionable insights. 
Data cleaning, a core competency of R, empowers us to clean, filter, transform, and aggregate data, paving the way for meaningful analysis. This introductory paragraph delves into the world of data manipulation and data cleaning in R, highlighting its significance and exploring the key concepts involved.

There are several methods used for data cleansing, including:

## Renaming colums

During data cleansing, column renaming plays a crucial role in organizing and clarifying the dataset. This step involves assigning meaningful and consistent names to columns, which facilitates their interpretation and subsequent use in analysis.


```r
#load the package
library(dplyr)

#rename the variable "Are you married?"
data_1 %>%
  dplyr::rename(marital_status=`Are you married?`)
```


## Handling Missing Data: 

Missing data, also known as missing values, is a common challenge encountered in data analysis. It refers to the absence of information for specific variables in certain observations within your dataset. To deal with missing data we have two options: impute data or remove data.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.1) Imputation

we can use imputation by mean, median or mode.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mean*:


```r
#Create a new column of number of varieties
data_1$number_variety <- str_sub(data_1$`How many varieties do you grow on the same plot or in the same field?`, 1, 1)

#verify the type of the column
str(data_1$number_variety)

#transform the type into number
data_1$number_variety <- as.integer(data_1$number_variety)

#impute NA values by mean
data_1$number_variety[is.na(data_1$number_variety)]<-round(mean(data_1$number_variety, na.rm = TRUE))
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by median*:


```r
library(stringr)
#function to extract the number of kg in the column
data_1$`What is the production in kg or ton/year?` <- sapply(data_1$`What is the production in kg or ton/year?`, function(x) {
    # Extract digits using regular expression and convert to numeric
    str_extract(x, "\\d+") %>% as.numeric()
})

#impute the column by median
data_1$`What is the production in kg or ton/year?`[is.na(data_1$`What is the production in kg or ton/year?`)]<-median(data_1$`What is the production in kg or ton/year?`, na.rm = TRUE)

```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mode*:


```r
data_1$`Where do you get your seeds?`[is.na(data_1$`Where do you get your seeds?`)] <- names(which.max(table(data_1$`Where do you get your seeds?`)))
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2) Removing data

There are 2 usuals methods for deleting data when dealing with missing data: listwise and dropping variables.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Listwise*:

In this method, all data for an observation that has one or more missing values are deleted. The analysis is run only on observations that have a complete set of data. 


```r
na.omit(data_1)
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Dropping variables*:

If data is missing for a large proportion of the observations, it may be best to discard the variable entirely if it is insignificant.


```r
subset( data_1, select = -c(`How do you call these varieties you have?`))
```

## Handling outliers

Data points far from the dataset’s other points are considered outliers. The presence of outliers can pose significant problems in statistical analysis and machine learning. They can bias model parameter estimates, lead to erroneous conclusions and affect algorithm performance.


```r
outlier_values <- boxplot.stats(data_1$`How many children do you have?`)$out  # outlier values.
boxplot(data_1$`How many children do you have?`, main="Number of children", boxwex=0.1)
mtext(paste("Outliers: ", paste(outlier_values, collapse=", ")), cex=0.6)
```

After identify outliers you can handle it by either impute those outliers by a value (mean, median, mode) or use the method of capping (For missing values that lie outside the **1.5 * IQR** limits, we could cap it by replacing those observations outside the lower limit with the value of 5th percentile and those that lie above the upper limit, with the value of 95th percentile)

## Removing duplicates: \
Removing duplicates ensures that each data point is represented only once, leading to more accurate and consistent data for analysis.


```r
data_1 <- data_1 %>% 
  dplyr::distinct()
```

## Checking data structure: 

Checking data types is a crucial step in data analysis because it ensures you're working with the data in the way it's intended in order to avoid errors later in the analysis.


```r
str(data_1)
```

You can change the type of your data across many functions like: as.numeric(), as.character(), as.factor() etc....if the data is not in the right type.

## Handling Inconsistent Categorical Data

Categorical variables may have inconsistent spellings or categories. The recode() function or manual recoding can help standardize categories.


```r
data_1 <- data_1 %>%
  dplyr::mutate(`How do you store your seed?` = dplyr::recode(`How do you store your seed?`, "In bags" = "in bags"))
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
data_1$`How much does 1kg of tasba seed cost?` <- gsub("FCFA", "", 
                        data_1$`How much does 1kg of tasba seed cost?`)
```



