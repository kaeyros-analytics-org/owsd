
```r
knitr::knit_child("05-data_cleaning.Rmd")
#> 
#> 
#> processing file: ./05-data_cleaning.Rmd
#>   |                                       |                               |   0%  |                                       |.                              |   4% [unnamed-chunk-13]  |                                       |..                             |   7%                     |                                       |...                            |  11% [unnamed-chunk-14]  |                                       |....                           |  14%                     |                                       |......                         |  18% [unnamed-chunk-15]  |                                       |.......                        |  21%                     |                                       |........                       |  25% [unnamed-chunk-16]  |                                       |.........                      |  29%                     |                                       |..........                     |  32% [unnamed-chunk-17]  |                                       |...........                    |  36%                     |                                       |............                   |  39% [unnamed-chunk-18]  |                                       |.............                  |  43%                     |                                       |..............                 |  46% [unnamed-chunk-19]  |                                       |................               |  50%                     |                                       |.................              |  54% [unnamed-chunk-20]  |                                       |..................             |  57%                     |                                       |...................            |  61% [unnamed-chunk-21]  |                                       |....................           |  64%                     |                                       |.....................          |  68% [unnamed-chunk-22]  |                                       |......................         |  71%                     |                                       |.......................        |  75% [unnamed-chunk-23]  |                                       |........................       |  79%                     |                                       |.........................      |  82% [unnamed-chunk-24]  |                                       |...........................    |  86%                     |                                       |............................   |  89% [unnamed-chunk-25]  |                                       |.............................  |  93%                     |                                       |.............................. |  96% [unnamed-chunk-26]  |                                       |...............................| 100%                   
```

````
#> [1] "\n\n\n# Data cleaning\n\nIn the domain of data science, R reigns supreme as a tool for transforming raw data into actionable insights. \nData cleaning, a core competency of R, empowers us to clean, filter, transform, and aggregate data, paving the way for meaningful analysis. This introductory paragraph delves into the world of data manipulation and data cleaning in R, highlighting its significance and exploring the key concepts involved.\n\nThere are several methods used for data cleansing, including:\n\n## Renaming colums\n\nDuring data cleansing, column renaming plays a crucial role in organizing and clarifying the dataset. This step involves assigning meaningful and consistent names to columns, which facilitates their interpretation and subsequent use in analysis.\n\n\n```r\n#load the package\nlibrary(dplyr)\n\n#rename the variable \"Are you married?\"\ndata_1 %>%\n  dplyr::rename(marital_status=`Are you married?`)\n```\n\n\n## Handling Missing Data: \n\nMissing data, also known as missing values, is a common challenge encountered in data analysis. It refers to the absence of information for specific variables in certain observations within your dataset. To deal with missing data we have two options: impute data or remove data.\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.1) Imputation\n\nwe can use imputation by mean, median or mode.\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mean*:\n\n\n```r\n#Create a new column of number of varieties\ndata_1$number_variety <- str_sub(data_1$`How many varieties do you grow on the same plot or in the same field?`, 1, 1)\n\n#verify the type of the column\nstr(data_1$number_variety)\n\n#transform the type into number\ndata_1$number_variety <- as.integer(data_1$number_variety)\n\n#impute NA values by mean\ndata_1$number_variety[is.na(data_1$number_variety)]<-round(mean(data_1$number_variety, na.rm = TRUE))\n```\n\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by median*:\n\n\n```r\nlibrary(stringr)\n#function to extract the number of kg in the column\ndata_1$`What is the production in kg or ton/year?` <- sapply(data_1$`What is the production in kg or ton/year?`, function(x) {\n    # Extract digits using regular expression and convert to numeric\n    str_extract(x, \"\\\\d+\") %>% as.numeric()\n})\n\n#impute the column by median\ndata_1$`What is the production in kg or ton/year?`[is.na(data_1$`What is the production in kg or ton/year?`)]<-median(data_1$`What is the production in kg or ton/year?`, na.rm = TRUE)\n\n```\n\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mode*:\n\n\n```r\ndata_1$`Where do you get your seeds?`[is.na(data_1$`Where do you get your seeds?`)] <- names(which.max(table(data_1$`Where do you get your seeds?`)))\n```\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2) Removing data\n\nThere are 2 usuals methods for deleting data when dealing with missing data: listwise and dropping variables.\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Listwise*:\n\nIn this method, all data for an observation that has one or more missing values are deleted. The analysis is run only on observations that have a complete set of data. \n\n\n```r\nna.omit(data_1)\n```\n\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Dropping variables*:\n\nIf data is missing for a large proportion of the observations, it may be best to discard the variable entirely if it is insignificant.\n\n\n```r\nsubset( data_1, select = -c(`How do you call these varieties you have?`))\n```\n\n## Handling outliers\n\nData points far from the dataset’s other points are considered outliers. The presence of outliers can pose significant problems in statistical analysis and machine learning. They can bias model parameter estimates, lead to erroneous conclusions and affect algorithm performance.\n\n\n```r\noutlier_values <- boxplot.stats(data_1$`How many children do you have?`)$out  # outlier values.\nboxplot(data_1$`How many children do you have?`, main=\"Number of children\", boxwex=0.1)\nmtext(paste(\"Outliers: \", paste(outlier_values, collapse=\", \")), cex=0.6)\n```\n\nAfter identify outliers you can handle it by either impute those outliers by a value (mean, median, mode) or use the method of capping (For missing values that lie outside the **1.5 * IQR** limits, we could cap it by replacing those observations outside the lower limit with the value of 5th percentile and those that lie above the upper limit, with the value of 95th percentile)\n\n## Removing duplicates: \\\nRemoving duplicates ensures that each data point is represented only once, leading to more accurate and consistent data for analysis.\n\n\n```r\ndata_1 <- data_1 %>% \n  dplyr::distinct()\n```\n\n## Checking data structure: \n\nChecking data types is a crucial step in data analysis because it ensures you're working with the data in the way it's intended in order to avoid errors later in the analysis.\n\n\n```r\nstr(data_1)\n```\n\nYou can change the type of your data across many functions like: as.numeric(), as.character(), as.factor() etc....if the data is not in the right type.\n\n## Handling Inconsistent Categorical Data\n\nCategorical variables may have inconsistent spellings or categories. The recode() function or manual recoding can help standardize categories.\n\n\n```r\ndata_1 <- data_1 %>%\n  dplyr::mutate(`How do you store your seed?` = dplyr::recode(`How do you store your seed?`, \"In bags\" = \"in bags\"))\n```\n\n\n## Combine dataframes\n\nSuppose the dataset combines data from different sources, we can combine differents datasets into one. When combining data from multiple sources, ensure that all data fields align correctly.\n&nbsp;&nbsp;&nbsp;&nbsp;- Combine by column\n\n\n```r\nculture1 <- data.frame(\n  Culture = c(\"wheat\", \"maize\", \"rice\"),\n  Area = c(100, 150, 120)\n)\n\nculture2 <- data.frame(\n  Culture = c(\"wheat\", \"maize\", \"rice\"),\n  Return = c(50, 60, 45)\n)\n\nculture_final1 <- cbind(culture1, culture2)\n```\n\n&nbsp;&nbsp;&nbsp;&nbsp;- combine by row\n\n\n```r\nculture3 <- data.frame(\n  Culture = c(\"wheat\", \"maize\", \"rice\"),\n  Area = c(100, 150, 120)\n)\n\nculture4 <- data.frame(\n  Culture = c(\"potato\", \"cassava\"),\n  Area = c(250, 400)\n)\n\nculture_final2 <- rbind(culture3, culture4)\n```\n\n## Data Validation\n\nData validation involves checking data against predefined rules or criteria. It ensures that data adheres to specific requirements or constraints.\n\nValidation checks can prevent incorrect or inconsistent data from entering your analysis.\n\n## Regular expressions\n\nRegular expressions (regex) are powerful tools for pattern matching and replacement in text data. The gsub() function is commonly used for global pattern substitution.\n\n\n```r\ndata_1$`How much does 1kg of tasba seed cost?` <- gsub(\"FCFA\", \"\", \n                        data_1$`How much does 1kg of tasba seed cost?`)\n```\n\n\n"
````

```r
source("./dependencies.R")
```


# Descriptive statistics

## Central Tendency Indicators

Central tendency indicators, also known as measures of central tendency, are statistical measures used to summarize a set of data by finding a single value that represents the middle or center of that data. They basically give you an idea of where most of the data points tend to cluster around.

There are three main types of central tendency indicators:

1. Mean\
This is the most common one, also called the average. It's calculated by adding up all the values in your data set and then dividing by the number of values.\

```r
mean(data_1$`What is the production in kg or ton/year?`)
#> [1] 138.3084
```


2. Median\
This is the middle number when you arrange your data set in order, from least to greatest. If you have an even number of data points, the median is the average of the two middle numbers.\

```r
median(data_1$`What is the production in kg or ton/year?`)
#> [1] 8
```


3. Mode\
This is the most frequent value in your data set. You can have multiple modes, by the way, if there are a couple of values that tie for the most frequent.

```r
names(which.max(table(data_1$`Are you married?`)))
#> [1] "YES"
```


## Variability indicators

Variability indicators, in contrast to central tendency, tell you how spread out your data is. They describe how much the data points differ from each other and from the central value (mean, median, or mode).  There are a few common ways to measure variability:

1. Variance\
This is the average of the squared deviations of each data point from the mean. It tells you how much your data varies on average, but since it uses squared values, it can be sensitive to extreme values.

```r
var(data_1$`What is the production in kg or ton/year?`)
#> [1] 296798.9
```


2. Standard deviation\
This is the square root of the variance. Standard deviation is expressed in the same units as your original data (e.g., meters, dollars), which can be easier to interpret than variance. It also reflects how much your data deviates from the mean on average.

```r
#1st approch using the native function
sd(data_1$`What is the production in kg or ton/year?`)
#> [1] 544.7925

#2nd approch
sqrt(var(data_1$`What is the production in kg or ton/year?`))
#> [1] 544.7925
```


3. Range\
This is the simplest method. It's just the difference between the highest and lowest values in your data set. While easy to calculate, the range can be misleading if your data has outliers.

```r
max(data_1$`How many children do you have?`) - min(data_1$`How many children do you have?`)
#> [1] 12
```

4. Interquartile range (IQR)\
This focuses on the middle half of your data. It represents the range between the first quartile (Q1) and the third quartile (Q3). Half your data falls within this IQR, giving a better idea of how spread out the bulk of the data is.

```r
IQR(data_1$`How many children do you have?`)
#> [1] 4
```
## Quantiles

Quantiles are values that split sorted data or a probability distribution into equal parts. In general terms, a q-quantile divides sorted data into q parts. The most commonly used quantiles have special names:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Quartiles:

```r
quantile(data_1$`How many children do you have?`)
#>   0%  25%  50%  75% 100% 
#>    0    0    2    4   12
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Deciles:

```r
quantile(data_1$`How many children do you have?`,probs = seq(0, 1, by = 0.1))
#>   0%  10%  20%  30%  40%  50%  60%  70%  80%  90% 100% 
#>    0    0    0    0    0    2    2    3    5    6   12
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentiles:

```r
quantile(data_1$`How many children do you have?`,probs = seq(0, 1, by = 0.01))
#>    0%    1%    2%    3%    4%    5%    6%    7%    8%    9% 
#>  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00 
#>   10%   11%   12%   13%   14%   15%   16%   17%   18%   19% 
#>  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00 
#>   20%   21%   22%   23%   24%   25%   26%   27%   28%   29% 
#>  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00 
#>   30%   31%   32%   33%   34%   35%   36%   37%   38%   39% 
#>  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00  0.00 
#>   40%   41%   42%   43%   44%   45%   46%   47%   48%   49% 
#>  0.00  0.46  1.00  1.00  1.00  1.00  1.00  1.00  1.88  2.00 
#>   50%   51%   52%   53%   54%   55%   56%   57%   58%   59% 
#>  2.00  2.00  2.00  2.00  2.00  2.00  2.00  2.00  2.00  2.00 
#>   60%   61%   62%   63%   64%   65%   66%   67%   68%   69% 
#>  2.00  2.00  2.00  2.00  2.00  2.90  3.00  3.00  3.00  3.00 
#>   70%   71%   72%   73%   74%   75%   76%   77%   78%   79% 
#>  3.00  3.00  3.00  3.38  4.00  4.00  4.00  4.00  4.68  5.00 
#>   80%   81%   82%   83%   84%   85%   86%   87%   88%   89% 
#>  5.00  5.00  5.00  5.00  5.00  5.00  5.00  5.00  5.28  6.00 
#>   90%   91%   92%   93%   94%   95%   96%   97%   98%   99% 
#>  6.00  6.00  6.00  6.58  7.64  8.70  9.76 10.00 10.00 11.88 
#>  100% 
#> 12.00
```
## Contingency table 

A contingency table displays frequencies for combinations of two categorical variables. 

```r
table(data_1$Sex, data_1$`Are you married?`)
#>         
#>          NO YES
#>   Female 19  39
#>   Male   28  21
```

