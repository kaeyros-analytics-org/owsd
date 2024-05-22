


# Descriptive statistics

## Central Tendency Indicators

Central tendency indicators, also known as measures of central tendency, are statistical measures used to summarize a set of data by finding a single value that represents the middle or center of that data. They basically give you an idea of where most of the data points tend to cluster around.

There are three main types of central tendency indicators:

1. Mean\
This is the most common one, also called the average. It's calculated by adding up all the values in your data set and then dividing by the number of values.\

```r
mean(tasba_data$production_kg)
#> [1] 138.3084
```


2. Median\
This is the middle number when you arrange your data set in order, from least to greatest. If you have an even number of data points, the median is the average of the two middle numbers.\

```r
median(tasba_data$production_kg)
#> [1] 8
```


3. Mode\
This is the most frequent value in your data set. You can have multiple modes, by the way, if there are a couple of values that tie for the most frequent.

```r
names(which.max(table(tasba_data$marital_status)))
#> [1] "YES"
```


## Variability indicators

Variability indicators, in contrast to central tendency, tell you how spread out your data is. They describe how much the data points differ from each other and from the central value (mean, median, or mode).  There are a few common ways to measure variability:

1. Variance\
This is the average of the squared deviations of each data point from the mean. It tells you how much your data varies on average, but since it uses squared values, it can be sensitive to extreme values.

```r
var(tasba_data$production_kg)
#> [1] 296798.9
```


2. Standard deviation\
This is the square root of the variance. Standard deviation is expressed in the same units as your original data (e.g., meters, dollars), which can be easier to interpret than variance. It also reflects how much your data deviates from the mean on average.

```r
#1st approch using the native function
sd(tasba_data$production_kg)
#> [1] 544.7925

#2nd approch
sqrt(var(tasba_data$production_kg))
#> [1] 544.7925
```


3. Range\
This is the simplest method. It's just the difference between the highest and lowest values in your data set. While easy to calculate, the range can be misleading if your data has outliers.

```r
max(tasba_data$nb_children) - min(tasba_data$nb_children)
#> [1] 12
```

4. Interquartile range (IQR)\
This focuses on the middle half of your data. It represents the range between the first quartile (Q1) and the third quartile (Q3). Half your data falls within this IQR, giving a better idea of how spread out the bulk of the data is.

```r
IQR(tasba_data$nb_children)
#> [1] 4
```
## Quantiles

Quantiles are values that split sorted data or a probability distribution into equal parts. In general terms, a q-quantile divides sorted data into q parts. The most commonly used quantiles have special names:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Quartiles:

```r
quantile(tasba_data$nb_children)
#>   0%  25%  50%  75% 100% 
#>    0    0    2    4   12
```


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Deciles:

```r
quantile(tasba_data$nb_children,probs = seq(0, 1, by = 0.1))
#>   0%  10%  20%  30%  40%  50%  60%  70%  80%  90% 100% 
#>    0    0    0    0    0    2    2    3    5    6   12
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Percentiles:

```r
quantile(tasba_data$nb_children,probs = seq(0, 1, by = 0.01))
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
#contingency table with counts 
table(tasba_data$Sex, tasba_data$marital_status)
#>         
#>          NO YES
#>   Female 19  39
#>   Male   28  21

#contingency table with percentages
round(prop.table(table(tasba_data$Sex, tasba_data$marital_status))*100,2) 
#>         
#>             NO   YES
#>   Female 17.76 36.45
#>   Male   26.17 19.63
```

