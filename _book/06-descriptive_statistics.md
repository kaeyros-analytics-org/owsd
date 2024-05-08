
```r
knitr::knit_child("05-data_cleaning.Rmd")
#> 
#> 
#> processing file: ./05-data_cleaning.Rmd
#>   |                                       |                               |   0%  |                                       |.                              |   4% [unnamed-chunk-13]  |                                       |..                             |   8%                     |                                       |....                           |  12% [unnamed-chunk-14]  |                                       |.....                          |  15%                     |                                       |......                         |  19% [unnamed-chunk-15]  |                                       |.......                        |  23%                     |                                       |........                       |  27% [unnamed-chunk-16]  |                                       |..........                     |  31%                     |                                       |...........                    |  35% [unnamed-chunk-17]  |                                       |............                   |  38%                     |                                       |.............                  |  42% [unnamed-chunk-18]  |                                       |..............                 |  46%                     |                                       |................               |  50% [unnamed-chunk-19]  |                                       |.................              |  54%                     |                                       |..................             |  58% [unnamed-chunk-20]  |                                       |...................            |  62%                     |                                       |....................           |  65% [unnamed-chunk-21]  |                                       |.....................          |  69%                     |                                       |.......................        |  73% [unnamed-chunk-22]  |                                       |........................       |  77%                     |                                       |.........................      |  81% [unnamed-chunk-23]  |                                       |..........................     |  85%                     |                                       |...........................    |  88% [unnamed-chunk-24]  |                                       |.............................  |  92%                     |                                       |.............................. |  96% [unnamed-chunk-25]  |                                       |...............................| 100%                   
```

`````
#> [1] "\n\n```r\nknitr::knit_child(\"04-data_manipulation.Rmd\")\n#> \n#> \n#> processing file: ./04-data_manipulation.Rmd\n#> \r  |                                     \r  |                               |   0%\r  |                                     \r  |.                              |   2% [unnamed-chunk-26]\r  |                                     \r  |.                              |   4%                   \r  |                                     \r  |..                             |   6% [unnamed-chunk-27]\r  |                                     \r  |...                            |   8%                   \r  |                                     \r  |...                            |  10% [unnamed-chunk-28]\r  |                                     \r  |....                           |  12%                   \r  |                                     \r  |.....                          |  15% [unnamed-chunk-29]\r  |                                     \r  |.....                          |  17%                   \r  |                                     \r  |......                         |  19% [unnamed-chunk-30]\r  |                                     \r  |......                         |  21% [unnamed-chunk-31]\r  |                                     \r  |.......                        |  23%                   \r  |                                     \r  |........                       |  25% [unnamed-chunk-32]\r  |                                     \r  |........                       |  27%                   \r  |                                     \r  |.........                      |  29% [unnamed-chunk-33]\r  |                                     \r  |..........                     |  31%                   \r  |                                     \r  |..........                     |  33% [unnamed-chunk-34]\r  |                                     \r  |...........                    |  35%                   \r  |                                     \r  |............                   |  38% [unnamed-chunk-35]\r  |                                     \r  |............                   |  40%                   \r  |                                     \r  |.............                  |  42% [unnamed-chunk-36]\r  |                                     \r  |..............                 |  44%                   \r  |                                     \r  |..............                 |  46% [unnamed-chunk-37]\r  |                                     \r  |...............                |  48%                   \r  |                                     \r  |................               |  50% [unnamed-chunk-38]\r  |                                     \r  |................               |  52%                   \r  |                                     \r  |.................              |  54% [unnamed-chunk-39]\r  |                                     \r  |.................              |  56%                   \r  |                                     \r  |..................             |  58% [unnamed-chunk-40]\r  |                                     \r  |...................            |  60%                   \r  |                                     \r  |...................            |  62% [unnamed-chunk-41]\r  |                                     \r  |....................           |  65%                   \r  |                                     \r  |.....................          |  67% [unnamed-chunk-42]\r  |                                     \r  |.....................          |  69%                   \r  |                                     \r  |......................         |  71% [unnamed-chunk-43]\r  |                                     \r  |.......................        |  73%                   \r  |                                     \r  |.......................        |  75% [unnamed-chunk-44]\r  |                                     \r  |........................       |  77%                   \r  |                                     \r  |.........................      |  79% [unnamed-chunk-45]\r  |                                     \r  |.........................      |  81%                   \r  |                                     \r  |..........................     |  83% [unnamed-chunk-46]\r  |                                     \r  |..........................     |  85%                   \r  |                                     \r  |...........................    |  88% [unnamed-chunk-47]\r  |                                     \r  |............................   |  90%                   \r  |                                     \r  |............................   |  92% [unnamed-chunk-48]\r  |                                     \r  |.............................  |  94%                   \r  |                                     \r  |.............................. |  96% [unnamed-chunk-49]\r  |                                     \r  |.............................. |  98%                   \r  |                                     \r  |...............................| 100% [unnamed-chunk-50]\r\n```\n\n````\n#> [1] \"\\n\\n```r\\nsource(\\\"./dependencies.R\\\")\\n#> \\n#> Attachement du package : 'dplyr'\\n#> Les objets suivants sont masqués depuis 'package:stats':\\n#> \\n#>     filter, lag\\n#> Les objets suivants sont masqués depuis 'package:base':\\n#> \\n#>     intersect, setdiff, setequal, union\\n#> Warning: le package 'plotly' a été compilé avec la version\\n#> R 4.3.3\\n#> Le chargement a nécessité le package : ggplot2\\n#> \\n#> Attachement du package : 'plotly'\\n#> L'objet suivant est masqué depuis 'package:ggplot2':\\n#> \\n#>     last_plot\\n#> L'objet suivant est masqué depuis 'package:stats':\\n#> \\n#>     filter\\n#> L'objet suivant est masqué depuis 'package:graphics':\\n#> \\n#>     layout\\n```\\n\\n# Data manipulation\\n\\nData manipulation involves modifying data to make it easier to read and to be more organized. We manipulate data for analysis and visualization. At times, the data collection process done by machines involves a lot of errors and inaccuracies in reading. Data manipulation is also used to remove these inaccuracies and make data more accurate and precise.\\n\\n## Importation of data\\nData import is an essential step in the data analysis process. It involves retrieving data from various sources, such as local files, databases, APIs or real-time feeds. This step acquires the data needed for analysis and decision-making, and is often the starting point for analytical work.\\n\\nIn this part, we will learn to load commonly used **CSV**, **Excel**, **JSON**, **Database**, and **XML/HTML** data files in R. Moreover, we will also look at less commonly used file formats such as **SPSS** and **Stata**. \\n\\nImporting data from csv to R:\\n\\n```r\\n#load data\\nchildren_anemia <- read.csv(\\\"./data/children_anemia.csv\\\")\\n```\\n\\nImporting data from excel to R:\\n\\n```r\\n#load package\\nlibrary(readxl)\\n\\n#load data\\ndata_1 <- readxl::read_excel(\\\"./data/data_for_workshop1.xls\\\")\\n```\\n\\n\\nImporting data from json to R:\\n\\n```r\\n#load package\\nlibrary(jsonlite)\\n\\n#load data\\ndata_json <- jsonlite::fromJSON(\\\"./data/sample4.json\\\")\\n\\n#transform data into dataframe\\nas.data.frame(data_json)\\n```\\n\\n\\nImporting data from database to R:\\n\\n```r\\n#load package\\nlibrary(RSQLite)\\n\\n#establish the connection to the database\\nconn <- dbConnect(RSQLite::SQLite(), \\\"./data/mental_health.sqlite\\\")\\n\\n#list names of all the tables in the database\\ndbListTables(conn)\\n#> [1] \\\"Answer\\\"   \\\"Question\\\" \\\"Survey\\\"\\n```\\n\\n```r\\n#retrieve data from table Question\\ndata_sqlite <- dbGetQuery(conn, \\\"SELECT * FROM Question\\\")\\nhead(data_sqlite)\\n```\\n\\n\\nImporting data from spss to R:\\n\\n```r\\n#load package\\nlibrary(haven)\\n\\n#load data\\ndata_spss <- haven::read_sav(\\\"./data/mental_health.sav\\\")\\n```\\n\\nImporting data from stata to R:\\n\\n```r\\n#load data\\ndata_stata <- haven::read_dta(\\\"./data/SMOKE.DTA\\\")\\n```\\n\\n\\n\\n## Basic exploration of data\\n\\nData exploration helps you explore and think about the data you're working. The goal with data exploration is to understand,  and visualize data so that you can discover insights, relationships, patterns, and anomalies.\\nTo explore data in R we have many functions to achieve that.\\n\\n+ Function head(): is used to view the first few rows of your dataset.\\n\\n```r\\nhead(data_1)\\n```\\n\\n\\n+ Function tail(): is used to view the last few rows of your dataset.\\n\\n```r\\ntail(data_1)\\n```\\n\\n\\n+ Function str(): is used to provide the structure of your data frame, showing you the data types.\\n\\n```r\\nstr(data_1)\\n```\\n\\n\\n+ Function dim(): is used to know about the number of rows and columns.\\n\\n```r\\ndim(data_1)\\n```\\n\\n\\n+ Function summary(): it gives you an overview of your data, including minimum and maximum values, quartiles, and more.\\n\\n```r\\nsummary(data_1)\\n```\\n\\n\\n+ Function table(): used to build a contingency table of the counts at each combination of factor levels.\\n\\n```r\\ntable(data_1$Sex)\\n#> \\n#> Female   Male \\n#>     58     49\\n```\\n\\n\\n+ Function unique(): The unique() function in R is used to eliminate or delete the duplicate values or the rows present in the vector, data frame, or matrix as well.\\n\\n```r\\nunique(data_1$`Do you  have children?`)\\n#> [1] \\\"NO\\\"  \\\"YES\\\"\\n```\\n\\n+ Function hist(): function to plot a basic histogram to view distribution of a variable.\\n\\n```r\\nhist(data_1$`How many children do you have?`)\\n```\\n\\n\\n\\n<img src=\\\"06-descriptive_statistics_files/figure-html/unnamed-chunk-41-1.png\\\" width=\\\"672\\\" />\\n\\n\\n+ Function boxplot(): function to plot a boxplot, it provides a compact summary of the data's central tendency, spread, and potential outliers.\\n\\n```r\\nboxplot(data_1$`How many children do you have?`)\\n```\\n\\n\\n\\n<img src=\\\"06-descriptive_statistics_files/figure-html/unnamed-chunk-42-1.png\\\" width=\\\"672\\\" />\\n\\n\\n## Data manipulation with dplyr\\n\\n**IMPORTANT POINT:**\\nOne of the more useful ways to use dplyr is with the pipe operator. The pipe operator looks like this: %>% ,and it is common practice to use the pipe operator to “pipe” dplyr commands together. It is a way to chain multiple operations together in a concise and precise way. The %>% operator takes the output of the expression on its left and passes it as the first argument to the function on its right.\\n\\nIn order to manipulate and clean the data, R provides a library called dplyr which consists of many built-in methods to manipulate the data. So to use the data manipulation function, first need to import the dplyr package using library(dplyr) line of code. Below is the list of fundamental data manipulation verbs that you will use to do most of your data manipulations.\\n\\n+ filter(): \\n\\n  The filter() function is used to produce the subset of the data that satisfies the condition specified in the filter() method. In the condition, we can use conditional operators, logical operators, NA values, range operators etc. to filter out data. Syntax of filter() function is given below:\\n\\n        filter(dataframeName,condition)\\n        \\nExample:\\n\\n```r\\ndplyr::filter(data_1, Sex==\\\"Female\\\")\\n```\\n\\n+ distinct(): \\n\\n  The distinct() method removes duplicate rows from data frame or based on the specified columns. The syntax of distinct() method is given below:\\n  \\n        distinct(dataframeName, col1, col2,.., .keep_all=TRUE)\\n        \\nExample:\\n\\n```r\\ndata_1 %>% \\n  dplyr::distinct()\\n```\\n\\n\\n+ arrange():\\n\\n  In R, the arrange() method is used to order the rows based on a specified column. The syntax of arrange() method is specified below:\\n  \\n        arrange(dataframeName, columnName)\\n        \\nExample:\\n\\n```r\\ndata_1 %>% \\n  dplyr::arrange(Sex)\\n```\\n\\n\\n+ select():\\n\\n  The select() method is used to extract the required columns as a table by specifying the required column names in select() method. The syntax of select() method is mentioned below:\\n        \\n        select(dataframeName, col1,col2,…)\\n        \\nExample:\\n\\n```r\\ndata_1 %>% \\n  dplyr::select(Sex,`Do you  have children?`)\\n```\\n\\n\\n+ rename():\\n\\n  The rename() function is used to change the column names. This can be done by the below syntax:\\n  \\n        rename(dataframeName, newName=oldName)\\n        \\nExample:\\n\\n```r\\ndata_1 %>%\\n  dplyr::rename(Status= `Are you married?`)\\n```\\n\\n\\n+ mutate():\\n\\n  The mutate() function creates new variables without dropping the old ones. The syntax of mutate() is specified below:\\n  \\n        mutate(dataframeName, newVariable=formula)\\n        \\nExample:\\n\\n```r\\ndata_1 %>%\\n  dplyr::mutate(sex=ifelse(Sex==\\\"Female\\\", \\\"F\\\", \\\"M\\\"))\\n```\\n\\n\\n+ transmute():\\n\\n  The transmute() function drops the old variables and creates new variables. Here is the syntax:\\n  \\n        transmute(dataframeName, newVariable=formula)\\n        \\nExample:\\n\\n```r\\ndata_1 %>%\\n  dplyr::transmute(sex=ifelse(Sex==\\\"Female\\\", \\\"F\\\", \\\"M\\\"))\\n```\\n\\n\\n+ summarize():\\n\\n  Using the summarize method we can summarize the data in the data frame by using aggregate functions like sum(), mean(), etc. Usually this function is used with the `group_by()` function. The syntax of summarize() method is specified below:\\n  \\n        summarize(dataframeName, aggregate_function(columnName))\\n        \\nExample:\\n\\n```r\\ndata_1 %>%\\n  group_by(Sex) %>%\\n  summarize(mean=mean(`How many children do you have?`), count=n())\\n#> # A tibble: 2 × 3\\n#>   Sex     mean count\\n#>   <chr>  <dbl> <int>\\n#> 1 Female  2.88    58\\n#> 2 Male    1.76    49\\n```\"\n````\n\n```r\nsource(\"./dependencies.R\")\n```\n\n# Data cleaning\n\nIn the domain of data science, R reigns supreme as a tool for transforming raw data into actionable insights. \nData cleaning, a core competency of R, empowers us to clean, filter, transform, and aggregate data, paving the way for meaningful analysis. This introductory paragraph delves into the world of data manipulation and data cleaning in R, highlighting its significance and exploring the key concepts involved.\n\nThere are several methods used for data cleansing, including:\n\n1) Renaming colums\n\nDuring data cleansing, column renaming plays a crucial role in organizing and clarifying the dataset. This step involves assigning meaningful and consistent names to columns, which facilitates their interpretation and subsequent use in analysis.\n\n```r\ndata_1 %>%\n  rename(marital_status=`Are you married?`)\n```\n\n\n2) Handling Missing Data: \n\nMissing data, also known as missing values, is a common challenge encountered in data analysis. It refers to the absence of information for specific variables in certain observations within your dataset. To deal with missing data we have two options: impute data or remove data.\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.1) Imputation\n\nwe can use imputation by mean, median or mode.\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mean*:\n\n```r\n#Create a new column of number of varieties\ndata_1$number_variety <- str_sub(data_1$`How many varieties do you grow on the same plot or in the same field?`, 1, 1)\n\n#verify the type of the column\nstr(data_1$number_variety)\n\n#transform the type into number\ndata_1$number_variety <- as.integer(data_1$number_variety)\n\n#impute NA values by mean\ndata_1$number_variety[is.na(data_1$number_variety)]<-round(mean(data_1$number_variety, na.rm = TRUE))\n```\n\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by median*:\n\n```r\n#function to extract the number of kg in the column\ndata_1$`What is the production in kg or ton/year?` <- sapply(data_1$`What is the production in kg or ton/year?`, function(x) {\n    # Extract digits using regular expression and convert to numeric\n    str_extract(x, \"\\\\d+\") %>% as.numeric()\n})\n\n#impute the column by median\ndata_1$`What is the production in kg or ton/year?`[is.na(data_1$`What is the production in kg or ton/year?`)]<-median(data_1$`What is the production in kg or ton/year?`, na.rm = TRUE)\n\n```\n\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Imputation by mode*:\n\n```r\ndata_1$`Where do you get your seeds?`[is.na(data_1$`Where do you get your seeds?`)] <- names(which.max(table(data_1$`Where do you get your seeds?`)))\n```\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;2.2) Removing data\n\nThere are 2 usuals methods for deleting data when dealing with missing data: listwise and dropping variables.\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Listwise*:\n\nIn this method, all data for an observation that has one or more missing values are deleted. The analysis is run only on observations that have a complete set of data. \n\n```r\n#remove all rows who does'nt have a tasba farm\ndata_listwise <- data_1\nna.omit(data_listwise)\n```\n\n\n&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Dropping variables*:\n\nIf data is missing for a large proportion of the observations, it may be best to discard the variable entirely if it is insignificant.\n\n```r\nsubset( data_1, select = -c(`How do you call these varieties you have?`))\n```\n\n3) Handling outliers\nData points far from the dataset’s other points are considered outliers. The presence of outliers can pose significant problems in statistical analysis and machine learning. They can bias model parameter estimates, lead to erroneous conclusions and affect algorithm performance.\n\n\n```r\n# data_1 <- data_1$`How many children do you have?`[!data_1$`How many children do you have?` %in% boxplot.stats(data_1$`How many children do you have?`)$out]\n```\n\n\n4) Removing duplicates: \nRemoving duplicates ensures that each data point is represented only once, leading to more accurate and consistent data for analysis.\n\n```r\ndata_1 <- data_1 %>% \n  distinct()\n```\n\n5) Checking data structure: \n\nChecking data types is a crucial step in data analysis because it ensures you're working with the data in the way it's intended in order to avoid errors later in the analysis.\n\n```r\nstr(data_1)\n```\nYou can change the type of your data across many functions like: as.numeric(), as.character(), as.factor() etc....if the data is not in the right type.\n\n6) Combine dataframes\n\nSuppose the dataset combines data from different sources, we can combine differents datasets into one. When combining data from multiple sources, ensure that all data fields align correctly.\n&nbsp;&nbsp;&nbsp;&nbsp;- Combine by column\n00\n\n```r\nculture1 <- data.frame(\n  Culture = c(\"wheat\", \"maize\", \"rice\"),\n  Area = c(100, 150, 120)\n)\n\nculture2 <- data.frame(\n  Culture = c(\"wheat\", \"maize\", \"rice\"),\n  Return = c(50, 60, 45)\n)\n\nculture_final1 <- cbind(culture1, culture2)\n```\n\n&nbsp;&nbsp;&nbsp;&nbsp;- combine by row\n\n```r\nculture3 <- data.frame(\n  Culture = c(\"wheat\", \"maize\", \"rice\"),\n  Area = c(100, 150, 120)\n)\n\nculture4 <- data.frame(\n  Culture = c(\"potato\", \"cassava\"),\n  Area = c(250, 400)\n)\n\nculture_final2 <- rbind(culture3, culture4)\n```\n\n\n\n```r\n\n# 7) Data inconsistencies:\n# \n# When faced with a data set, we are often confronted with data inconsistencies. This can take the form of spelling errors, language heterogeneity in the dataset, etc.\n# \n# &nbsp;&nbsp;&nbsp;&nbsp;Handling spelling errors\n\n#&nbsp;&nbsp;&nbsp;&nbsp; Handling language heterogeneity\n\n```\n\n\n\n\n\n"
`````

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


