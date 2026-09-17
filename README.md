# ProduceR

<!-- badges: start -->

<!-- badges: end -->

<img src="man/figures/logo.png" align="right" height="138.5"/>

ProduceR : Concise and Efficient Tools for Everyday Statistical Production

ProduceR proposes a set of concise and efficient tools for statistical production. Can also be used for data management.

In statistical production, you deal with complex data and need to control your process at each step of your work.

Concise functions are very helpful, because you do not hesitate to use them.

The five functions of ProduceR were developed by a statistician for his everyday's use.

The following functions are included in the package :

-   'dup()' checks duplicates.

-   'miss()' checks missing values.

-   'sums()' computes sums of all numeric columns.*
  
-   'tac()' computes contingency table of all columns.

-   'toc()' compares two tables, spotting significant deviations.

-   'chi2_find()' helps understanding problematic data (missing values, outliers, etc.) by suggesting correlations with the rest of the dataset.

# Details

The {ProduceR} package offers a set of 5 functions designed to meet the common needs of statistical production, a term that refers to the production of reliable and usable statistical data from raw information. These functions were developed based on the concrete work experience of their author, who has been working in statistical services for 20 years.

The underlying philosophy is as follows: statistical production generally involves handling complex data, particularly when raw information comes from administrative data (Lefebvre, Soulier, and Tortosa, 2024), but also when it comes from survey data. This information is almost systematically found in a set of tables, as the tabular representation is the canonical model for statistics (Dondon and Lamarche, 2023). Quality production requires understanding the structure of these tables and their content, as well as mastering the relationships between them. However, in everyday work, one hesitates to perform checks if they are time-consuming to program. Yet, it is desirable to control the data at different stages of production, for example, checking for duplicates or missing values following a join.

Thus, the five functions of {ProduceR} were developed to be concise and accessible, so that the producer does not hesitate to perform frequent checks. They are intended to address the main needs encountered in real life and are deliberately few in number.

# Examples

```{r example}
library(ProduceR)

# finding unique key
dup(ggplot2::txhousing, c("city", "year"))          # city and year do not define a unique key for txhousing
dup(ggplot2::txhousing, c("city", "year", "month")) # city, year and month do define a unique key for txhousing

# checking missing values
miss(ggplot2::txhousing) # many NA values on all columns except unique keys

# sum of all numeric columns
stat <- sums(ggplot2::txhousing)

# contengency tables
stat <- tac(ggplot2::txhousing)

# significant differences between 2005 and 2015
stat <- toc(ggplot2::txhousing %>% filter(year == 2015), ggplot2::txhousing %>% filter(year == 2005)) %>% filter(score != 0)

# finding why/where missing sales
stat <- chi2_find(ggplot2::txhousing, 'is.na(sales)')
```
