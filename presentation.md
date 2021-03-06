Intuitive big data manipulation with dplyr and tidyr
========================================================
author: Vlad Achimescu
date: 03/05/2019
autosize: false
css: presstyle.css

Download presentation and data here:
https://github.com/nomoteticus/R_data_manipulation

Summary
========================================================
<hr>
Data manipulation:
- import data into a tibble/data frame
- filter data -> select cases
- subset columns -> select variables
- add new variables to data frame
- aggregate variables
- reshape data
  - from columns to rows
  - from rows to columns
- merge data

The tidyverse
========================================================
<hr>
![tidy data](img/00_tidyverse.png)

***

<small>
www.tidyverse.com
</small>

- readr
- magrittr
- dplyr
- tidyr
- ggplot -> next tutorial

<small>

```r
install.packages( c("readr","magrittr",
    "dplyr","tidyr") )
```
</small>

Principles of tidy data
========================================================
<hr>
![tidy data](img/01_tidy_data.png)
<small><i>(Wickham & Grolemund 2017)</i></small>

Tidy datasets
========================================================

<small>
Untidy 
<table>
  <tr>
    <th><br>id</th>
    <th>var</th>
    <th>val_jan</th>
    <th>val_aug<br></th>
  </tr>
  <tr>
    <td>1</td>
    <td>City</td>
    <td>Mannheim</td>
    <td>Mannheim</td>
  </tr>
  <tr>
    <td>1</td>
    <td>temperature</td>
    <td>5C / 41F<br></td>
    <td>30C / 86F</td>
  </tr>
  <tr>
    <td>2</td>
    <td>City</td>
    <td>Hamburg</td>
    <td>Hamburg</td>
  </tr>
  <tr>
    <td>2</td>
    <td>temperature</td>
    <td>-5C / 23F</td>
    <td>25C / 77F</td>
  </tr>
</table>

- Same observation in diff. lines
- No unique measurement in cols
- Strings and numeric in same col
- 2 values in one cell

</table>
</small>

***

-


Tidy datasets
========================================================

<small>
Untidy 
<table>
  <tr>
    <th><br>id</th>
    <th>var</th>
    <th>val_jan</th>
    <th>val_aug<br></th>
  </tr>
  <tr>
    <td>1</td>
    <td>City</td>
    <td>Mannheim</td>
    <td>Mannheim</td>
  </tr>
  <tr>
    <td>1</td>
    <td>temperature</td>
    <td>5C / 41F<br></td>
    <td>30C / 86F</td>
  </tr>
  <tr>
    <td>2</td>
    <td>City</td>
    <td>Hamburg</td>
    <td>Hamburg</td>
  </tr>
  <tr>
    <td>2</td>
    <td>temperature</td>
    <td>-5C / 23F</td>
    <td>25C / 77F</td>
  </tr>
</table>

- Same observation in diff. lines
- No unique measurement in cols
- Strings and numeric in same col
- 2 values in one cell

***

Tidy
<table>
  <tr>
    <th><br>id</th>
    <th>City</th>
    <th>month</th>
    <th><br>temp_C</th>
    <th>temp_F</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Mannheim</td>
    <td>jan</td>
    <td>5</td>
    <td>41</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Mannheim</td>
    <td>aug</td>
    <td>25</td>
    <td>77</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Hamburg</td>
    <td>jan</td>
    <td>-5</td>
    <td>23</td>
  </tr>
  <tr>
    <td>4</td>
    <td>Hamburg</td>
    <td>aug</td>
    <td>25</td>
    <td>77</td>
  </tr>
</table>

- Every line is one case
- Every column is one variable
- Can summarise columns
- Cells are values
</small>



Load data 
========================================================
class: at75
<hr>

- <i>readr</i> reads file as tibbles
- tibbles = enhanced data frames
  - more classes for columns
  - look nicer when printed


```r
library(readr)
read_csv(filename)
read_tsv(filename)
read_delim(filename, 
           sep = "char")
```
---
https://github.com/nomoteticus/R_data_manipulation

Two datasets:
- https://ec.europa.eu/eurostat/data/database
- <b>EMP</b>: Employment rate of the age group 15-64 by NUTS 2 regions [tgs00007] <br> (% employed in each region) <br> <i>file: empl_rates_reg.tsv</i>
- <b>TRAIN</b>: Adult participation in learning by sex [sdg_04_60]<br> (% of population aged 25 to 64) <br> <i>file: traing_participation.csv</i>
- Which one is tidy?


Pipe operator
========================================================
<hr>
![magrittr](img/02_magrittr.png)
$$(f\circ g)(x) = f(g(x))$$

```r
### Without piping
f(g(arg_g), arg_f)
### With piping
arg_g %>% g %>% f(arg_f)
```

- similar to Python (. operator, e.g. ln(3).round(3))


SUBSETTING ROWS / FILTER
========================================================
<small>
<hr>
![tidy data](img/03_filter.png)

***
.
- select cases that satisfy certain conditions with <i>filter()</i>
- conditions can be separated by commas


```r
DF = DF %>% filter(condition1, condition2, condition3)
# all must be true to be kept in dataset
```
</small>

SUBSETTING COLUMNS / SELECT
========================================================
<hr>
<large>
![tidy data](img/04_select.png)
</large>

***

.
- select columns by names
- no need to quote variable names
- ranges can also be specified
- similar to Stata

ADDING NEW VARIABLES
========================================================
<hr>
![tidy data](img/05_mutate.png)
- can reference newly created variables
- comma separated
- <i>transmute()</i> keeps only new variables


***

![tidy data](img/05b_mutate.png)
</large>


AGGREGATING DATA
========================================================
<hr>
<hr>
![tidy data](img/06_groupby.png)

![tidy data](img/06b_groupby.png)


***
.
- similar to SQL
- <i>group_by(var1, var2)</i> to define grouping variables
- to aggregate by group, use <i>summarise()</i>
- to add group-level aggregates but keep current unit of analysis, use<br> <i>mutate()</i>
- in the end <i>ungroup()</i> to remove grouping



SUMMARY FUNCTIONS
========================================================
<hr>
<large>
![tidy data](img/07_summarise.png)
</large>


RESHAPING DATASETS
========================================================
<hr>
<large>
![tidy data](img/08_reshape.png)
</large>

- <b>gather()</b>: from wide to long data format
  - similar to <i>melt</i> from <i>reshape</i> package
- <b>spread()</b>: from long to wide data format
  - similar to <i>cast</i> from <i>reshape</i> package


MERGING DIFFERENT DATASETS
========================================================
class: at80
<hr>
<large>
![tidy data](img/09_merge.png)
</large>
- x1 is key value
- similar to <i>merge</i> from base R and SQL JOIN clauses


SOME RESOURCES
========================================================
<hr>
- Wickham, Hadley; Grolemund, Garrett (2017): <i>R for data science. Import, tidy, transform, visualize, and model data.</i>  Beijing: O'Reilly.
- www.tidyverse.com
- <a href = "https://cran.r-project.org/web/packages/dplyr/vignettes/dplyr.html"> Introduction to <i>dplyr</i> @ CRAN </a>
- <a href = "https://cran.r-project.org/web/packages/tidyr/vignettes/tidy-data.html"> Introduction to <i>tidyr</i> @ CRAN <a>
- <a href = "https://www.datacamp.com/courses?q=topic%3Adata_manipulation"> <i>datacamp</i> courses on data manipulation </a>
- <a href = "https://www.rstudio.com/wp-content/uploads/2015/02/data-wrangling-cheatsheet.pdf"> cheat sheet @ RStudio.com</a>
![tidy data](img/10_cheatsheet.png)
