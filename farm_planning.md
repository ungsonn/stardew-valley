Stardew Valley: Farm Planning
================
Nick D. Ungson

**Last updated:** 2019-05-26 17:53:47

All data below from the [Stardew Valley
Wiki](https://stardewvalleywiki.com/Stardew_Valley_Wiki)

# prep

Load data:

``` r
require(tidyverse)
require(here)
require(DT)

crops <- read.csv(
  here("crops.csv"), 
  header = TRUE, 
  stringsAsFactors = TRUE)
```

Some functions: **What crops are available in a season?**

``` r
List <- function(season_name){
  crops %>% 
    filter(season == season_name) %>% 
    select(name, 
           type) %>% 
    arrange(desc(type)) %>% 
    return()
}
```

**What are the most profitable crops?** (measured in gold per day)

``` r
GPD <- function(season_name){
  crops %>%
  filter(season == season_name) %>% 
  select(gpd, 
         name, 
         grow:regrow, 
         max_harvest) %>% 
  arrange(desc(gpd))
}
```

**Cost Estimate**: How much do *n* seeds of a crop cost?

``` r
Price <- function(crop, n){
  price <- crops[crops$name == crop, "buy"]
  return(price * n)
}
```

# spring

What are all the crops available in
[spring](https://stardewvalleywiki.com/spring)?

``` r
List("spring")
```

    ##           name      type
    ## 1  cauliflower vegetable
    ## 2       garlic vegetable
    ## 3         kale vegetable
    ## 4      parsnip vegetable
    ## 5       potato vegetable
    ## 6   green bean vegetable
    ## 7      rhubarb     fruit
    ## 8   strawberry     fruit
    ## 9    blue jazz    flower
    ## 10       tulip    flower
    ## 11      coffee      crop

Most valuable?

``` r
GPD("spring")
```

    ##      gpd        name grow regrow max_harvest
    ## 1  23.00      coffee   10      2          NA
    ## 2  11.67  strawberry    8      4           2
    ## 3   9.23     rhubarb   13      0           2
    ## 4   7.92 cauliflower   12      0           2
    ## 5   7.20  green bean   10      3           6
    ## 6   6.67        kale    6      0           4
    ## 7   5.00      garlic    4      0           6
    ## 8   5.00      potato    6      0           4
    ## 9   3.75     parsnip    4      0           6
    ## 10  2.86   blue jazz    7      0           3
    ## 11  1.67       tulip    6      0           4

## planning

I want to plant the following in on the first day of spring…

  - 32 cauliflower
  - 16 kale
  - 16 potato
  - 16 garlic
  - 16 parsnip
  - 32 green beans
  - 8 blue jazz
  - 8 tulip

Then, I passed each crop and \# of seeds and summed them all:

``` r
spring_cost <- Price("cauliflower", 32) + 
  Price("green bean", 32) + 
  Price("kale", 16) + 
  Price("potato", 16) + 
  Price("garlic", 16) + 
  Price("parsnip", 16) + 
  Price("blue jazz", 8) + 
  Price("tulip", 8)
```

``` r
print(paste("On spring 1, you need $", spring_cost, sep = ""))
```

    ## [1] "On spring 1, you need $7760"

# summer

What are all the crops available in
[summer](https://stardewvalleywiki.com/summer)?

``` r
List("summer")
```

    ##              name      type
    ## 1          radish vegetable
    ## 2     red cabbage vegetable
    ## 3           wheat vegetable
    ## 4            corn vegetable
    ## 5            hops vegetable
    ## 6      hot pepper vegetable
    ## 7          tomato vegetable
    ## 8           melon     fruit
    ## 9       starfruit     fruit
    ## 10      blueberry     fruit
    ## 11          poppy    flower
    ## 12 summer spangle    flower
    ## 13      sunflower    flower
    ## 14         coffee      crop

Most valuable?

``` r
GPD("summer")
```

    ##       gpd           name grow regrow max_harvest
    ## 1   26.92      starfruit   13      0           2
    ## 2   23.00         coffee   10      2           9
    ## 3   20.80      blueberry   13      4           4
    ## 4   17.78    red cabbage    9      0           3
    ## 5   14.17          melon   12      0           2
    ## 6   13.52           hops   11      1          17
    ## 7   10.77     hot pepper    5      3           8
    ## 8    9.26         tomato   11      4           5
    ## 9    8.33         radish    6      0           4
    ## 10   7.41           corn   14      4           4
    ## 11   5.71          poppy    7      0           3
    ## 12   5.00 summer spangle    8      0           3
    ## 13   3.75          wheat    4      0           6
    ## 14 -15.00      sunflower    8      0           3

## planning

…

``` r
summer_cost <- 
  Price("blueberry", 16) + 
  Price("red cabbage", 64) + 
  Price("melon", 46) + 
  Price("hops", 32) + 
  Price("hot pepper", 24) + 
  Price("tomato", 7) + 
  Price("radish", 7) + 
  Price("sunflower", 16) + 
  Price("wheat", 16) + 
  Price("corn", 16)
```

``` r
print(paste("On summer 1, you need $", summer_cost, sep = ""))
```

    ## [1] "On summer 1, you need $20630" "On summer 1, you need $20630"

# fall

What are all the crops available in
[fall](https://stardewvalleywiki.com/fall)?

``` r
List("fall")
```

    ##          name      type
    ## 1     pumpkin vegetable
    ## 2   artichoke vegetable
    ## 3        beet vegetable
    ## 4    amaranth vegetable
    ## 5         yam vegetable
    ## 6    bok choy vegetable
    ## 7       wheat vegetable
    ## 8        corn vegetable
    ## 9    eggplant vegetable
    ## 10  cranberry     fruit
    ## 11      grape     fruit
    ## 12 fairy rose    flower
    ## 13  sunflower    flower

``` r
datatable(crops, rownames = FALSE, 
          filter = "top", 
          options = list(pageLength = 20, 
                         scrollX = TRUE))
```

Most valuable?

``` r
GPD("fall")
```

    ##       gpd       name grow regrow max_harvest
    ## 1   18.89  cranberry    7      5           5
    ## 2   16.92    pumpkin   13      0           2
    ## 3   16.80      grape   10      3           6
    ## 4   16.25  artichoke    8      0           3
    ## 5   13.33       beet    6      0           4
    ## 6   11.43   amaranth    7      0           3
    ## 7   11.20   eggplant    5      5           5
    ## 8   10.00        yam   10      0           2
    ## 9    7.50   bok choy    4      0           6
    ## 10   7.50 fairy rose   12      0           2
    ## 11   7.41       corn   14      4           4
    ## 12   3.75      wheat    4      0           6
    ## 13 -15.00  sunflower    8      0           3

## planning

…

``` r
fall_cost <- 
  Price("pumpkin", (32 * 3)) + 
  Price("artichoke", 64) + 
  Price("beet", 64) + 
  Price("cranberry", 64) + 
  Price("grape", 64) + 
  Price("amaranth", 16) + 
  Price("yam", 16) + 
  Price("eggplant", 16) + 
  Price("bok choy", 16)
```

``` r
print(paste("On fall 1, you need $", fall_cost, sep = ""))
```

    ## [1] "On fall 1, you need $35200"

``` r
fall_cost_all <- 
  Price("pumpkin", (32 * 3 * 2)) + 
  Price("artichoke", (64 * 3)) + 
  Price("beet", 64) + 
  Price("cranberry", 64) + 
  Price("grape", 64) + 
  Price("amaranth", (16 * 3)) + 
  Price("yam", (16 * 2)) + 
  Price("eggplant", 16) + 
  Price("bok choy", (16 * 6))

print(paste("On for entire fall, you need $", fall_cost_all, sep = ""))
```

    ## [1] "On for entire fall, you need $55840"
