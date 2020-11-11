exploring
================
Nicole Doyle
10/30/20

Load the necessary libraries

``` r
library(tidyverse)
```

    ## -- Attaching packages ------------------------------------- tidyverse 1.3.0 --

    ## v ggplot2 3.3.2     v purrr   0.3.4
    ## v tibble  3.0.3     v dplyr   1.0.1
    ## v tidyr   1.1.1     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts ---------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(readr)
listings <- read_csv("C:/Users/ndai7/Desktop/Git Directories/exploring-ndoyle3146/listings.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   id = col_double(),
    ##   name = col_character(),
    ##   host_id = col_double(),
    ##   host_name = col_character(),
    ##   neighbourhood_group = col_logical(),
    ##   neighbourhood = col_character(),
    ##   latitude = col_double(),
    ##   longitude = col_double(),
    ##   room_type = col_character(),
    ##   price = col_double(),
    ##   minimum_nights = col_double(),
    ##   number_of_reviews = col_double(),
    ##   last_review = col_date(format = ""),
    ##   reviews_per_month = col_double(),
    ##   calculated_host_listings_count = col_double(),
    ##   availability_365 = col_double()
    ## )

``` r
View(listings)
```

Take a look inside your dataset

``` r
listings
```

    ## # A tibble: 67,565 x 16
    ##       id name  host_id host_name neighbourhood_g~ neighbourhood latitude
    ##    <dbl> <chr>   <dbl> <chr>     <lgl>            <chr>            <dbl>
    ##  1  2577 Loft~    2827 Karine    NA               Entrepôt          48.9
    ##  2  3109 zen ~    3631 Anne      NA               Observatoire      48.8
    ##  3  4886 Coun~    6792 Jennifer~ NA               Popincourt        48.9
    ##  4  4890 Quie~    6792 Jennifer~ NA               Temple            48.9
    ##  5  5396 Expl~    7903 Borzou    NA               Hôtel-de-Vil~     48.9
    ##  6  7397 MARA~    2626 Franck    NA               Hôtel-de-Vil~     48.9
    ##  7  7964 Larg~   22155 Anaïs     NA               Opéra             48.9
    ##  8  9359 Cozy~   28422 Bernadet~ NA               Louvre            48.9
    ##  9  9952 Pari~   33534 Elisabeth NA               Popincourt        48.9
    ## 10 10586 Mont~   37107 Michael   NA               Buttes-Montm~     48.9
    ## # ... with 67,555 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

### Variation

Perform an analysis of the variation in the “neighbourhood” column.

``` r
ggplot(data = listings) + 
  geom_bar(mapping = aes(x = neighbourhood)) + 
  theme(axis.text.x = element_text(angle = 90))
```

![](Exploring_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

  - Which values are the most common? Why?

The Buttes-Montmartre is the most common neighborhood. This neighborhood
could be the most common because it contains tourist locations like the
Basilica of the Sacré-Cœur and is also the nightclub district. This
could make it more popular for air bnbs.

  - Which values are rare? Why? Does that match your expectations?

The Louvre neighborhood is the least common neighborhood, this did not
match my expectations because I thought the location would be good for
visiting the Louvre, but this could also be a reason why there is less
airbnbs there, because of the high numbers of tourists.

  - Can you see any unusual patterns? What might explain them?

I don’t really ses any unusual patterns.

Perform an analysis of the variation in the “room\_type” column.

``` r
ggplot(data = listings) + 
  geom_bar(mapping = aes(x = room_type))
```

![](Exploring_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

  - Which values are the most common? Why?

Most commonly the airbnb has the entire home/apt available. This makes
sense because people would prefer to have the house to themselves rather
than shared or just one room.

  - Which values are rare? Why? Does that match your expectations?

The shared room airbnbs are the least common. This makes sense because
toursits or people who come into the city would most likely not want to
share a room with another person.

  - Can you see any unusual patterns? What might explain them?

I don’t see any unusual patterns.

Perform an analysis of the variation in the “price” column. Make sure to
explore different “binwidth” values in your analysis.

``` r
ggplot(data = listings) + 
  geom_histogram(mapping = aes(x = price))
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Exploring_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ggplot(data = listings) +
  geom_histogram(mapping = aes(x = price), binwidth = 100) +
   coord_cartesian(xlim = c(0, 1750))
```

![](Exploring_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

``` r
ggplot(data = listings) +
  geom_histogram(mapping = aes(x = price), binwidth = 30) +
  coord_cartesian(xlim = c(0, 1750))
```

![](Exploring_files/figure-gfm/unnamed-chunk-5-3.png)<!-- -->

  - Which values are the most common? Why?

There is a spike in values that are cheaper, but there is lower amounts
of value closest to 0. This could be because the cheapest airbnbs could
be the ones that less people want because of lower quality, but then
people also want the cheapest good quality airbnbs.

  - Which values are rare? Why? Does that match your expectations?

As the prices get over about 300 there is not many airbnbs. This makes
sense because these would be either very nice places, which is more
rare, or just very expensive, which less people would want.

  - Can you see any unusual patterns? What might explain them?

I don’t see any unusual patterns.

Perform an analysis of the variation in the “minimum\_nights” column.
Make sure to explore different “binwidth” values in your analysis.

``` r
ggplot(data = listings) +
  geom_histogram(mapping = aes(x = minimum_nights), binwidth = 20) +
   coord_cartesian(xlim = c(0, 200))
```

![](Exploring_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggplot(data = listings) +
  geom_histogram(mapping = aes(x = minimum_nights), binwidth = 10) + 
  coord_cartesian(xlim = c (0, 200))
```

![](Exploring_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

  - Which values are the most common? Why?

The lowest values are the most common because people who are visiting
for a short time would like the airbnbs where the minimum nights is very
low

  - Which values are rare? Why? Does that match your expectations?

As the minimum\_nights gets higher there are less airbnbs. This makes
sense because customers are more likely to only want to rent for a few
nights so that would be the most common type of airbnb.

  - Can you see any unusual patterns? What might explain them?

There is a slight increase around the 100 day minimum nights. This might
be because if customers are renting the airbnb for a entire summer.

Perform an analysis of the variation in the “number\_of\_reviews”
column. Make sure to explore different “binwidth” values in your
analysis.

``` r
ggplot(data = listings) + 
  geom_histogram(mapping = aes(x = number_of_reviews), binwidth = 20) + 
  coord_cartesian(xlim = c(0, 400))
```

![](Exploring_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
ggplot(data = listings) +
  geom_histogram(mapping = aes(x = number_of_reviews), bindwidth = 50) + 
  coord_cartesian(xlim = c(0, 400))
```

    ## Warning: Ignoring unknown parameters: bindwidth

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](Exploring_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

  - Which values are the most common? Why?

There are many airbnbs that do not have any reviews. This could because
there are so many airbnbs that theres is likely to be many where people
don’t leave reviews.

  - Which values are rare? Why? Does that match your expectations?

Airbnbs with over 100 reviews are very rare. The count of airbnbs gets
more rare as the number of reviews increases.

  - Can you see any unusual patterns? What might explain them? There are
    not any unusual patterns.

Perform an analysis of the variation in the “availability\_365” column.
Make sure to explore different “binwidth” values in your analysis.

``` r
ggplot(data = listings) +
  geom_histogram(mapping = aes(x = availability_365), binwidth = 20)
```

![](Exploring_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
ggplot(data = listings) + 
  geom_histogram(mapping = aes(x = availability_365), binwidth = 30)
```

![](Exploring_files/figure-gfm/unnamed-chunk-8-2.png)<!-- -->

  - Which values are the most common? Why? The most airbnbs have very
    low availability. This could because many airbnbs only rent out for
    a few days a year.

  - Which values are rare? Why? Does that match your expectations? The
    values are rare around 50, 150, 250 days. This could be because the
    number of days doesn’t match the number of days in a multiples of
    months.

  - Can you see any unusual patterns? What might explain them?

There is an unusal pattern because the number of airbnbs increasing at
75, 175, 275, and 365. This could again be because this amount of time
could be more normal for people renting.

``` r
listings
```

    ## # A tibble: 67,565 x 16
    ##       id name  host_id host_name neighbourhood_g~ neighbourhood latitude
    ##    <dbl> <chr>   <dbl> <chr>     <lgl>            <chr>            <dbl>
    ##  1  2577 Loft~    2827 Karine    NA               Entrepôt          48.9
    ##  2  3109 zen ~    3631 Anne      NA               Observatoire      48.8
    ##  3  4886 Coun~    6792 Jennifer~ NA               Popincourt        48.9
    ##  4  4890 Quie~    6792 Jennifer~ NA               Temple            48.9
    ##  5  5396 Expl~    7903 Borzou    NA               Hôtel-de-Vil~     48.9
    ##  6  7397 MARA~    2626 Franck    NA               Hôtel-de-Vil~     48.9
    ##  7  7964 Larg~   22155 Anaïs     NA               Opéra             48.9
    ##  8  9359 Cozy~   28422 Bernadet~ NA               Louvre            48.9
    ##  9  9952 Pari~   33534 Elisabeth NA               Popincourt        48.9
    ## 10 10586 Mont~   37107 Michael   NA               Buttes-Montm~     48.9
    ## # ... with 67,555 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

What seems to be the most common name (of a person) in the city you
selected?

Marie

``` r
listings %>%
  count(host_name) %>%
  arrange(desc(n)) 
```

    ## # A tibble: 10,674 x 2
    ##    host_name     n
    ##    <chr>     <int>
    ##  1 Marie       692
    ##  2 Pierre      585
    ##  3 Nicolas     533
    ##  4 Guillaume   471
    ##  5 Sophie      459
    ##  6 Camille     454
    ##  7 Thomas      444
    ##  8 Julien      434
    ##  9 Sandra      416
    ## 10 Antoine     411
    ## # ... with 10,664 more rows

Do the number of review affect the price off the Airbnb? How? Why do you
think this happens?

As the number of review increases the price increases up to 100 reviews,
but then decreases as reviews increases past 100. This could be because
slightly lower numbers of reviews could be positive and helpful for
people trying to get feedback. The decrease in price after 200 reviews
could be because there are more negative reviews or that it is so
congested with reviews that it is not helpful.

``` r
smaller_price <- filter(listings, price < 500)
ggplot(data = smaller_price) + 
  geom_point(mapping = aes(x = number_of_reviews, y = price)) +
  geom_smooth(mapping = aes(x = number_of_reviews, y = price), se = FALSE)
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

![](Exploring_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

What type of room tends to have the highest Airbnb price?

The hotel room airbnbs have the highest Airbnb price.

``` r
ggplot(data = smaller_price) +
  geom_boxplot(mapping = aes(x = reorder(room_type,price,FUN=median), y = price))
```

![](Exploring_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

Suppose you could purchase a property in the city you selected, and that
you could rent it to others as an Airbnb. In what neighborhood would you
want to purchase your property? Why?

I would choose Elysée because it has the higheset average price out of
all the neighborhoods, but also doesn’t have m any Airbnbs in that area
so there would be less competition. Also Marie does not have many
properties there.

``` r
ggplot(data = smaller_price) +
  geom_boxplot(mapping = aes(x = reorder(neighbourhood,price,FUN=median), y = price))
```

![](Exploring_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
Marie <- listings %>%
  filter(host_name == 'Marie')

Marie %>%
  count(neighbourhood) %>%
  arrange(desc(n))
```

    ## # A tibble: 20 x 2
    ##    neighbourhood           n
    ##    <chr>               <int>
    ##  1 Buttes-Montmartre      85
    ##  2 Popincourt             62
    ##  3 Batignolles-Monceau    61
    ##  4 Entrepôt               56
    ##  5 Ménilmontant           48
    ##  6 Buttes-Chaumont        46
    ##  7 Opéra                  41
    ##  8 Panthéon               37
    ##  9 Reuilly                37
    ## 10 Passy                  35
    ## 11 Vaugirard              35
    ## 12 Temple                 25
    ## 13 Gobelins               22
    ## 14 Luxembourg             20
    ## 15 Observatoire           20
    ## 16 Palais-Bourbon         17
    ## 17 Hôtel-de-Ville         16
    ## 18 Bourse                 13
    ## 19 Élysée                 12
    ## 20 Louvre                  4

Visit a real estate website and find a property that is for sale in the
neighborhood you selected. Take notes of the price and address of the
property.

Use your dataset to find what the average Airbnb price/night is in the
neighborhood you selected.

Use your dataset to find what the average number of available nights per
year is for an Airbnb in the neighborhood you selected.

Suppose you bought the property you selected above. If you were to rent
it as an Airbnba t the average neighborhood price, for the average
number of days, how long will it take you to break even?

``` r
listings
```

    ## # A tibble: 67,565 x 16
    ##       id name  host_id host_name neighbourhood_g~ neighbourhood latitude
    ##    <dbl> <chr>   <dbl> <chr>     <lgl>            <chr>            <dbl>
    ##  1  2577 Loft~    2827 Karine    NA               Entrepôt          48.9
    ##  2  3109 zen ~    3631 Anne      NA               Observatoire      48.8
    ##  3  4886 Coun~    6792 Jennifer~ NA               Popincourt        48.9
    ##  4  4890 Quie~    6792 Jennifer~ NA               Temple            48.9
    ##  5  5396 Expl~    7903 Borzou    NA               Hôtel-de-Vil~     48.9
    ##  6  7397 MARA~    2626 Franck    NA               Hôtel-de-Vil~     48.9
    ##  7  7964 Larg~   22155 Anaïs     NA               Opéra             48.9
    ##  8  9359 Cozy~   28422 Bernadet~ NA               Louvre            48.9
    ##  9  9952 Pari~   33534 Elisabeth NA               Popincourt        48.9
    ## 10 10586 Mont~   37107 Michael   NA               Buttes-Montm~     48.9
    ## # ... with 67,555 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

``` r
Elysee <- filter(listings, neighbourhood == "Élysée")

summarize(Elysee, avg_price = mean(price, na.rm = TRUE), avg_nights = mean(availability_365, na.rm = TRUE))
```

    ## # A tibble: 1 x 2
    ##   avg_price avg_nights
    ##       <dbl>      <dbl>
    ## 1      231.       161.

``` r
Elysee
```

    ## # A tibble: 1,848 x 16
    ##        id name  host_id host_name neighbourhood_g~ neighbourhood latitude
    ##     <dbl> <chr>   <dbl> <chr>     <lgl>            <chr>            <dbl>
    ##  1  10710 "Cal~   38170 Josiane   NA               Élysée            48.9
    ##  2  22158 "Art~   84874 Fabienne  NA               Élysée            48.9
    ##  3  24260 "Lov~   98012 Emmanuel  NA               Élysée            48.9
    ##  4  48592 "Cha~  152242 Delphine  NA               Élysée            48.9
    ##  5  55239 "Lux~  260696 Joseph    NA               Élysée            48.9
    ##  6 108591 "Lux~  561870 Madame D  NA               Élysée            48.9
    ##  7 162163 "Bra~  775000 Justin &~ NA               Élysée            48.9
    ##  8 171159 "Lov~  193142 Carole    NA               Élysée            48.9
    ##  9 183599 "Cha~  876138 Dina      NA               Élysée            48.9
    ## 10 219564 "LOF~  189040 Morgane   NA               Élysée            48.9
    ## # ... with 1,838 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

<https://www.residences-immobilier.com/en/75/annonce-vente-appartement-paris-8eme-2173583.html>

231$ a night, 161 nights a year

400,000 euros = 474,452$

231\*161 = 37,191

474,452$/37,191 = 12.75

It would take about 13 years to pay remake the price of the apartment.
