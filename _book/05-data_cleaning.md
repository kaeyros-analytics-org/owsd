
```r
knitr::knit_child("04-data_manipulation.Rmd")
#> 
#> 
#> processing file: ./04-data_manipulation.Rmd
#>   |                                       |                               |   0%  |                                       |.                              |   2% [unnamed-chunk-14]  |                                       |.                              |   4%                     |                                       |..                             |   6% [unnamed-chunk-15]  |                                       |...                            |   8%                     |                                       |...                            |  10% [unnamed-chunk-16]  |                                       |....                           |  12%                     |                                       |.....                          |  15% [unnamed-chunk-17]  |                                       |.....                          |  17%                     |                                       |......                         |  19% [unnamed-chunk-18]  |                                       |......                         |  21% [unnamed-chunk-19]  |                                       |.......                        |  23%                     |                                       |........                       |  25% [unnamed-chunk-20]  |                                       |........                       |  27%                     |                                       |.........                      |  29% [unnamed-chunk-21]  |                                       |..........                     |  31%                     |                                       |..........                     |  33% [unnamed-chunk-22]  |                                       |...........                    |  35%                     |                                       |............                   |  38% [unnamed-chunk-23]  |                                       |............                   |  40%                     |                                       |.............                  |  42% [unnamed-chunk-24]  |                                       |..............                 |  44%                     |                                       |..............                 |  46% [unnamed-chunk-25]  |                                       |...............                |  48%                     |                                       |................               |  50% [unnamed-chunk-26]  |                                       |................               |  52%                     |                                       |.................              |  54% [unnamed-chunk-27]  |                                       |.................              |  56%                     |                                       |..................             |  58% [unnamed-chunk-28]  |                                       |...................            |  60%                     |                                       |...................            |  62% [unnamed-chunk-29]  |                                       |....................           |  65%                     |                                       |.....................          |  67% [unnamed-chunk-30]  |                                       |.....................          |  69%                     |                                       |......................         |  71% [unnamed-chunk-31]  |                                       |.......................        |  73%                     |                                       |.......................        |  75% [unnamed-chunk-32]  |                                       |........................       |  77%                     |                                       |.........................      |  79% [unnamed-chunk-33]  |                                       |.........................      |  81%                     |                                       |..........................     |  83% [unnamed-chunk-34]  |                                       |..........................     |  85%                     |                                       |...........................    |  88% [unnamed-chunk-35]  |                                       |............................   |  90%                     |                                       |............................   |  92% [unnamed-chunk-36]  |                                       |.............................  |  94%                     |                                       |.............................. |  96% [unnamed-chunk-37]  |                                       |.............................. |  98%                     |                                       |...............................| 100% [unnamed-chunk-38]
```

````
#> [1] "\n\n```r\nsource(\"./dependencies.R\")\n#> \n#> Attachement du package : 'dplyr'\n#> Les objets suivants sont masqués depuis 'package:stats':\n#> \n#>     filter, lag\n#> Les objets suivants sont masqués depuis 'package:base':\n#> \n#>     intersect, setdiff, setequal, union\n#> Warning: le package 'plotly' a été compilé avec la version\n#> R 4.3.3\n#> Le chargement a nécessité le package : ggplot2\n#> \n#> Attachement du package : 'plotly'\n#> L'objet suivant est masqué depuis 'package:ggplot2':\n#> \n#>     last_plot\n#> L'objet suivant est masqué depuis 'package:stats':\n#> \n#>     filter\n#> L'objet suivant est masqué depuis 'package:graphics':\n#> \n#>     layout\n```\n\n# Data manipulation\n\nData manipulation involves modifying data to make it easier to read and to be more organized. We manipulate data for analysis and visualization. At times, the data collection process done by machines involves a lot of errors and inaccuracies in reading. Data manipulation is also used to remove these inaccuracies and make data more accurate and precise.\n\n## Importation of data\nData import is an essential step in the data analysis process. It involves retrieving data from various sources, such as local files, databases, APIs or real-time feeds. This step acquires the data needed for analysis and decision-making, and is often the starting point for analytical work.\n\nIn this part, we will learn to load commonly used **CSV**, **Excel**, **JSON**, **Database**, and **XML/HTML** data files in R. Moreover, we will also look at less commonly used file formats such as **SPSS** and **Stata**. \n\nImporting data from csv to R:\n\n```r\n#load data\nchildren_anemia <- read.csv(\"./data/children_anemia.csv\")\n```\n\nImporting data from excel to R:\n\n```r\n#load package\nlibrary(readxl)\n\n#load data\ndata_1 <- readxl::read_excel(\"./data/data_for_workshop1.xls\")\n```\n\n\nImporting data from json to R:\n\n```r\n#load package\nlibrary(jsonlite)\n\n#load data\ndata_json <- jsonlite::fromJSON(\"./data/sample4.json\")\n\n#transform data into dataframe\nas.data.frame(data_json)\n```\n\n\nImporting data from database to R:\n\n```r\n#load package\nlibrary(RSQLite)\n\n#establish the connection to the database\nconn <- dbConnect(RSQLite::SQLite(), \"./data/mental_health.sqlite\")\n\n#list names of all the tables in the database\ndbListTables(conn)\n#> [1] \"Answer\"   \"Question\" \"Survey\"\n```\n\n```r\n#retrieve data from table Question\ndata_sqlite <- dbGetQuery(conn, \"SELECT * FROM Question\")\nhead(data_sqlite)\n```\n\n\nImporting data from spss to R:\n\n```r\n#load package\nlibrary(haven)\n\n#load data\ndata_spss <- haven::read_sav(\"./data/mental_health.sav\")\n```\n\nImporting data from stata to R:\n\n```r\n#load data\ndata_stata <- haven::read_dta(\"./data/SMOKE.DTA\")\n```\n\n\n\n## Basic exploration of data\n\nData exploration helps you explore and think about the data you're working. The goal with data exploration is to understand,  and visualize data so that you can discover insights, relationships, patterns, and anomalies.\nTo explore data in R we have many functions to achieve that.\n\n+ Function head(): is used to view the first few rows of your dataset.\n\n```r\nhead(data_1)\n```\n\n\n+ Function tail(): is used to view the last few rows of your dataset.\n\n```r\ntail(data_1)\n```\n\n\n+ Function str(): is used to provide the structure of your data frame, showing you the data types.\n\n```r\nstr(data_1)\n```\n\n\n+ Function dim(): is used to know about the number of rows and columns.\n\n```r\ndim(data_1)\n```\n\n\n+ Function summary(): it gives you an overview of your data, including minimum and maximum values, quartiles, and more.\n\n```r\nsummary(data_1)\n```\n\n\n+ Function table(): used to build a contingency table of the counts at each combination of factor levels.\n\n```r\ntable(data_1$Sex)\n#> \n#> Female   Male \n#>     58     49\n```\n\n\n+ Function unique(): The unique() function in R is used to eliminate or delete the duplicate values or the rows present in the vector, data frame, or matrix as well.\n\n```r\nunique(data_1$`Do you  have children?`)\n#> [1] \"NO\"  \"YES\"\n```\n\n+ Function hist(): function to plot a basic histogram to view distribution of a variable.\n\n```r\nhist(data_1$`How many children do you have?`)\n```\n\n\n<img src=\"05-data_cleaning_files/figure-html/unnamed-chunk-29-1.png\" width=\"672\" />\n\n\n+ Function boxplot(): function to plot a boxplot, it provides a compact summary of the data's central tendency, spread, and potential outliers.\n\n```r\nboxplot(data_1$`How many children do you have?`)\n```\n\n\n<img src=\"05-data_cleaning_files/figure-html/unnamed-chunk-30-1.png\" width=\"672\" />\n\n\n## Data manipulation with dplyr\n\n**IMPORTANT POINT:**\nOne of the more useful ways to use dplyr is with the pipe operator. The pipe operator looks like this: %>% ,and it is common practice to use the pipe operator to “pipe” dplyr commands together. It is a way to chain multiple operations together in a concise and precise way. The %>% operator takes the output of the expression on its left and passes it as the first argument to the function on its right.\n\nIn order to manipulate and clean the data, R provides a library called dplyr which consists of many built-in methods to manipulate the data. So to use the data manipulation function, first need to import the dplyr package using library(dplyr) line of code. Below is the list of fundamental data manipulation verbs that you will use to do most of your data manipulations.\n\n+ filter(): \n\n  The filter() function is used to produce the subset of the data that satisfies the condition specified in the filter() method. In the condition, we can use conditional operators, logical operators, NA values, range operators etc. to filter out data. Syntax of filter() function is given below:\n\n        filter(dataframeName,condition)\n        \nExample:\n\n```r\ndplyr::filter(data_1, Sex==\"Female\")\n```\n\n+ distinct(): \n\n  The distinct() method removes duplicate rows from data frame or based on the specified columns. The syntax of distinct() method is given below:\n  \n        distinct(dataframeName, col1, col2,.., .keep_all=TRUE)\n        \nExample:\n\n```r\ndata_1 %>% \n  dplyr::distinct()\n```\n\n\n+ arrange():\n\n  In R, the arrange() method is used to order the rows based on a specified column. The syntax of arrange() method is specified below:\n  \n        arrange(dataframeName, columnName)\n        \nExample:\n\n```r\ndata_1 %>% \n  dplyr::arrange(Sex)\n```\n\n\n+ select():\n\n  The select() method is used to extract the required columns as a table by specifying the required column names in select() method. The syntax of select() method is mentioned below:\n        \n        select(dataframeName, col1,col2,…)\n        \nExample:\n\n```r\ndata_1 %>% \n  dplyr::select(Sex,`Do you  have children?`)\n```\n\n\n+ rename():\n\n  The rename() function is used to change the column names. This can be done by the below syntax:\n  \n        rename(dataframeName, newName=oldName)\n        \nExample:\n\n```r\ndata_1 %>%\n  dplyr::rename(Status= `Are you married?`)\n```\n\n\n+ mutate():\n\n  The mutate() function creates new variables without dropping the old ones. The syntax of mutate() is specified below:\n  \n        mutate(dataframeName, newVariable=formula)\n        \nExample:\n\n```r\ndata_1 %>%\n  dplyr::mutate(sex=ifelse(Sex==\"Female\", \"F\", \"M\"))\n```\n\n\n+ transmute():\n\n  The transmute() function drops the old variables and creates new variables. Here is the syntax:\n  \n        transmute(dataframeName, newVariable=formula)\n        \nExample:\n\n```r\ndata_1 %>%\n  dplyr::transmute(sex=ifelse(Sex==\"Female\", \"F\", \"M\"))\n```\n\n\n+ summarize():\n\n  Using the summarize method we can summarize the data in the data frame by using aggregate functions like sum(), mean(), etc. Usually this function is used with the `group_by()` function. The syntax of summarize() method is specified below:\n  \n        summarize(dataframeName, aggregate_function(columnName))\n        \nExample:\n\n```r\ndata_1 %>%\n  group_by(Sex) %>%\n  summarize(mean=mean(`How many children do you have?`), count=n())\n#> # A tibble: 2 × 3\n#>   Sex     mean count\n#>   <chr>  <dbl> <int>\n#> 1 Female  2.88    58\n#> 2 Male    1.76    49\n```"
````

```r
source("./dependencies.R")
```

# Data cleaning

In the domain of data science, R reigns supreme as a tool for transforming raw data into actionable insights. 
Data cleaning, a core competency of R, empowers us to clean, filter, transform, and aggregate data, paving the way for meaningful analysis. This introductory paragraph delves into the world of data manipulation and data cleaning in R, highlighting its significance and exploring the key concepts involved.

There are several methods used for data cleansing, including:

1) Renaming colums

During data cleansing, column renaming plays a crucial role in organizing and clarifying the dataset. This step involves assigning meaningful and consistent names to columns, which facilitates their interpretation and subsequent use in analysis.

```r
data_1 %>%
  rename(marital_status=`Are you married?`)
```


2) Handling Missing Data: 

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
#remove all rows who does'nt have a tasba farm
data_listwise <- data_1
na.omit(data_listwise)
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- *Dropping variables*:

If data is missing for a large proportion of the observations, it may be best to discard the variable entirely if it is insignificant.

```r
subset( data_1, select = -c(`How do you call these varieties you have?`))
```

3) Handling outliers
Data points far from the dataset’s other points are considered outliers. The presence of outliers can pose significant problems in statistical analysis and machine learning. They can bias model parameter estimates, lead to erroneous conclusions and affect algorithm performance.


```r
# data_1 <- data_1$`How many children do you have?`[!data_1$`How many children do you have?` %in% boxplot.stats(data_1$`How many children do you have?`)$out]
```


4) Removing duplicates: 
Removing duplicates ensures that each data point is represented only once, leading to more accurate and consistent data for analysis.

```r
data_1 <- data_1 %>% 
  distinct()
```

5) Checking data structure: 

Checking data types is a crucial step in data analysis because it ensures you're working with the data in the way it's intended in order to avoid errors later in the analysis.

```r
str(data_1)
```
You can change the type of your data across many functions like: as.numeric(), as.character(), as.factor() etc....if the data is not in the right type.

6) Combine dataframes

Suppose the dataset combines data from different sources, we can combine differents datasets into one. When combining data from multiple sources, ensure that all data fields align correctly.
&nbsp;&nbsp;&nbsp;&nbsp;- Combine by column
00

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



```r

# 7) Data inconsistencies:
# 
# When faced with a data set, we are often confronted with data inconsistencies. This can take the form of spelling errors, language heterogeneity in the dataset, etc.
# 
# &nbsp;&nbsp;&nbsp;&nbsp;Handling spelling errors

#&nbsp;&nbsp;&nbsp;&nbsp; Handling language heterogeneity

```






