Stardew Valley: Farm Planning
================
Nick D. Ungson

**Last updated:** 2019-05-17 14:43:24

All data below from the [Stardew Valley
Wiki](https://stardewvalleywiki.com/Stardew_Valley_Wiki)

# prep

Load data:

``` r
require(tidyverse)
require(here)

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
         note1:note2) %>% 
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

    ##      gpd        name grow regrow          note1          note2
    ## 1  23.00      coffee   10      2 traveling cart spring, summer
    ## 2  11.67  strawberry    8      4   egg festival               
    ## 3   9.23     rhubarb   13      0          oasis               
    ## 4   7.92 cauliflower   12      0                              
    ## 5   7.20  green bean   10      3                              
    ## 6   6.67        kale    6      0                              
    ## 7   5.00      garlic    4      0                              
    ## 8   5.00      potato    6      0                              
    ## 9   3.75     parsnip    4      0                              
    ## 10  2.86   blue jazz    7      0                              
    ## 11  1.67       tulip    6      0

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

Most
    valuable?

``` r
GPD("summer")
```

    ##       gpd           name grow regrow          note1          note2
    ## 1   26.92      starfruit   13      0          oasis               
    ## 2   23.00         coffee   10      2 traveling cart spring, summer
    ## 3   20.80      blueberry   13      4                              
    ## 4   17.78    red cabbage    9      0                              
    ## 5   14.17          melon   12      0                              
    ## 6   13.52           hops   11      1                              
    ## 7   10.77     hot pepper    5      3                              
    ## 8    9.26         tomato   11      4                              
    ## 9    8.33         radish    6      0                              
    ## 10   7.41           corn   14      4   summer, fall               
    ## 11   5.71          poppy    7      0                              
    ## 12   5.00 summer spangle    8      0                              
    ## 13   3.75          wheat    4      0   summer, fall               
    ## 14 -15.00      sunflower    8      0   summer, fall

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

    ## [1] "On summer 1, you need $20630"
