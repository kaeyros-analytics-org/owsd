# Basic of the R language 

## Variables
Variables are the identifier or the named space in the memory, which are stored and can be referenced and manipulated later in the program. 

### Rule variable in R {-}
It is recommended that you use nouns to name a variable. Use underscores (e.g. donnees_menages) rather than CamelCase (e.g. donneesMenages). If you prefer camelCase, use it systematically throughout the script to standardise the code.

Notes:

+ Do not use T or F to name variables (as these are abbreviations for the Booleans TRUE and FALSE);
+ Do not use names that are already basic R functions(mean for example). This doesn't always generate errors, but it does prevent errors that are difficult to detect!
+ The variable name must start with letter and can contain number,letter,underscore('_') and period('.').
+ Special characters such as '#', '&', etc., along with White space (tabs, space) are not allowed in a variable name.
+ Underscore('_') at the beginning of the variable name are not allowed

### Variable assignment {-}

Variables in R can be assigned in one of three ways.

- Assignment Operator: "=" used to assign the value.The following example contains 20 as value which is stored in the variable 'first.variable' Example: first.variable = 20

- '<-' Operator: The following example contains the New Program as the character which gets assigned to 'second_variable'.
Example: second_variable <- "New Program"

- '->' Operator: The following example contains 565 as the integer which gets assigned to 'third.variable'.
Example: 565 -> third.variable

## Types

## Operators

Cross-references make it easier for your readers to find and link to elements in your book.

## Chapters and sub-chapters

There are two steps to cross-reference any heading:

1. Label the heading: `# Hello world {#nice-label}`. 
    - Leave the label off if you like the automated heading generated based on your heading title: for example, `# Hello world` = `# Hello world {#hello-world}`.
    - To label an un-numbered heading, use: `# Hello world {-#nice-label}` or `{# Hello world .unnumbered}`.

1. Next, reference the labeled heading anywhere in the text using `\@ref(nice-label)`; for example, please see Chapter \@ref(cross). 
    - If you prefer text as the link instead of a numbered reference use: [any text you want can go here](#cross).

## Captioned figures and tables

Figures and tables *with captions* can also be cross-referenced from elsewhere in your book using `\@ref(fig:chunk-label)` and `\@ref(tab:chunk-label)`, respectively.

See Figure \@ref(fig:nice-fig).


```r
par(mar = c(4, 4, .1, .1))
plot(pressure, type = 'b', pch = 19)
```

<div class="figure" style="text-align: center">
<img src="02-cross-refs_files/figure-html/nice-fig-1.png" alt="Plot with connected points showing that vapor pressure of mercury increases exponentially as temperature increases." width="80%" />
<p class="caption">(\#fig:nice-fig)Here is a nice figure!</p>
</div>

Don't miss Table \@ref(tab:nice-tab).


```r
knitr::kable(
  head(pressure, 10), caption = 'Here is a nice table!',
  booktabs = TRUE
)
```



Table: (\#tab:nice-tab)Here is a nice table!

| temperature| pressure|
|-----------:|--------:|
|           0|   0.0002|
|          20|   0.0012|
|          40|   0.0060|
|          60|   0.0300|
|          80|   0.0900|
|         100|   0.2700|
|         120|   0.7500|
|         140|   1.8500|
|         160|   4.2000|
|         180|   8.8000|



Don't miss figure \@ref(fig:nice-fig).
