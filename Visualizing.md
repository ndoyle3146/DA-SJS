Data Visualization Project
================
Nicole Doyle
9/9/2020

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------------------------ tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.1
    ## v tidyr   1.1.1     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts --------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readr)
netflix_titles <- read_csv("Data sets/netflix_titles Data Set/netflix_titles.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   show_id = col_double(),
    ##   type = col_character(),
    ##   title = col_character(),
    ##   director = col_character(),
    ##   cast = col_character(),
    ##   country = col_character(),
    ##   date_added = col_character(),
    ##   release_year = col_double(),
    ##   rating = col_character(),
    ##   duration = col_character(),
    ##   listed_in = col_character(),
    ##   description = col_character()
    ## )

``` r
View(netflix_titles)

library(readr)
StudentsPerformance <- read_csv("Data sets/StudentsPerformance Data Set/StudentsPerformance.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   gender = col_character(),
    ##   `race/ethnicity` = col_character(),
    ##   `parental level of education` = col_character(),
    ##   lunch = col_character(),
    ##   `test preparation course` = col_character(),
    ##   `math score` = col_double(),
    ##   `reading score` = col_double(),
    ##   `writing score` = col_double()
    ## )

``` r
View(StudentsPerformance)
```

``` r
netflix_titles
```

    ## # A tibble: 6,234 x 12
    ##    show_id type  title director cast  country date_added release_year rating
    ##      <dbl> <chr> <chr> <chr>    <chr> <chr>   <chr>             <dbl> <chr> 
    ##  1  8.11e7 Movie Norm~ Richard~ Alan~ United~ September~         2019 TV-PG 
    ##  2  8.01e7 Movie Jand~ <NA>     Jand~ United~ September~         2016 TV-MA 
    ##  3  7.02e7 TV S~ Tran~ <NA>     Pete~ United~ September~         2013 TV-Y7~
    ##  4  8.01e7 TV S~ Tran~ <NA>     Will~ United~ September~         2016 TV-Y7 
    ##  5  8.01e7 Movie #rea~ Fernand~ Nest~ United~ September~         2017 TV-14 
    ##  6  8.02e7 TV S~ Apac~ <NA>     Albe~ Spain   September~         2016 TV-MA 
    ##  7  7.03e7 Movie Auto~ Gabe Ib~ Anto~ Bulgar~ September~         2014 R     
    ##  8  8.02e7 Movie Fabr~ Rodrigo~ Fabr~ Chile   September~         2017 TV-MA 
    ##  9  8.01e7 TV S~ Fire~ <NA>     <NA>  United~ September~         2017 TV-MA 
    ## 10  7.03e7 Movie Good~ Henrik ~ Jame~ United~ September~         2014 R     
    ## # ... with 6,224 more rows, and 3 more variables: duration <chr>,
    ## #   listed_in <chr>, description <chr>

``` r
StudentsPerformance
```

    ## # A tibble: 1,000 x 8
    ##    gender `race/ethnicity` `parental level~ lunch `test preparati~ `math score`
    ##    <chr>  <chr>            <chr>            <chr> <chr>                   <dbl>
    ##  1 female group B          bachelor's degr~ stan~ none                       72
    ##  2 female group C          some college     stan~ completed                  69
    ##  3 female group B          master's degree  stan~ none                       90
    ##  4 male   group A          associate's deg~ free~ none                       47
    ##  5 male   group C          some college     stan~ none                       76
    ##  6 female group B          associate's deg~ stan~ none                       71
    ##  7 female group B          some college     stan~ completed                  88
    ##  8 male   group B          some college     free~ none                       40
    ##  9 male   group D          high school      free~ completed                  64
    ## 10 female group B          high school      free~ none                       38
    ## # ... with 990 more rows, and 2 more variables: `reading score` <dbl>, `writing
    ## #   score` <dbl>

``` r
StudentsPerformance <- rename(StudentsPerformance, reading.score = 'reading score', math.score = 'math score')

StudentsPerformance
```

    ## # A tibble: 1,000 x 8
    ##    gender `race/ethnicity` `parental level~ lunch `test preparati~ math.score
    ##    <chr>  <chr>            <chr>            <chr> <chr>                 <dbl>
    ##  1 female group B          bachelor's degr~ stan~ none                     72
    ##  2 female group C          some college     stan~ completed                69
    ##  3 female group B          master's degree  stan~ none                     90
    ##  4 male   group A          associate's deg~ free~ none                     47
    ##  5 male   group C          some college     stan~ none                     76
    ##  6 female group B          associate's deg~ stan~ none                     71
    ##  7 female group B          some college     stan~ completed                88
    ##  8 male   group B          some college     free~ none                     40
    ##  9 male   group D          high school      free~ completed                64
    ## 10 female group B          high school      free~ none                     38
    ## # ... with 990 more rows, and 2 more variables: reading.score <dbl>, `writing
    ## #   score` <dbl>

``` r
ggplot(data = StudentsPerformance) + geom_count (mapping = aes(x = reading.score, y = math.score, color = gender)) + labs(x = "Reading Score", y = "Math Score", title = "Math and Reading Scores of Students", subtitle = "Effects of Lunch on Student Performance: Trends by Sex", caption = "Source = Royce Simmions") + theme(axis.text.x = element_text(angle=90,hjust=1,vjust=0.5)) 
```

![](Visualizing_files/figure-gfm/unnamed-chunk-4-1.png)<!-- --> This
visualization compares the test scores between males and females in both
reading and writing. Using geom\_count counts the overlapping points at
certain places showing the densities of certain scores on the graph.
This plot shows that within these students females have lower math
stores as there is a higher density of larger points lower on the y-axis
than males. This plot also shows that the females generally have a
higher reading score as the density of female reading scores is more
right on the x-axis than male reading scores. The plot also shows that
both sexes tend to have correlating math and reading scores (75-75,
50,50), seen in the y = x trend the data seems to follow.

``` r
ggplot(data = netflix_titles, mapping = aes(x = type, fill  = rating)) + geom_bar(position = "dodge") + labs(x = "Media Type", y = "Count", title = "Ratings of Netflix Titles", subtitle = "Ratings of Movies and TV Shows", caption = "Source = Flixable") + theme(axis.text.x = element_text(angle=90,hjust=1,vjust=0.5))
```

![](Visualizing_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

This visualization shows the difference in ratings in Netflix movies and
TV shows. The bar graph is split by the categorical values of the type
of media, showing the different quantity of ratings in each. In both
movies and TV shows there is the most number of TV\_MA rating, followed
by TV-14 rating both of which could reflect their main target audience
of teens and young adults. They are also similar in that both have low
numbers of TV-G. Also, while there are more movies total on Netflix, the
TV show category has more TV-Y, TV-Y7, TV-Y7-FV, and UR titles than
movies of those same ratings.
