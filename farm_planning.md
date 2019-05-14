Stardew Valley: Farm Planning
================
Nick D. Ungson

**Last updated:** 2019-05-14 13:37:51

# Prep

``` r
require(tidyverse)
require(here)

crops <- read.csv(
  here("crops.csv"), 
  header = TRUE, 
  stringsAsFactors = TRUE)

print(colnames(crops))

crops %>% 
  filter(season == "spring") %>% 
  select(name:note2) %>% 
  print()
```

# Spring

What are the most profitable (by *gold per day*) spring crops?

``` r
crops %>%
  filter(season == "spring", 
         type == "fruit" | 
           type == "vegetable") %>% 
  select(name, 
         type, 
         buy, 
         gpd, 
         note1:note2) %>% 
  arrange(desc(gpd))
```

    ##          name      type buy   gpd        note1 note2
    ## 1  strawberry     fruit 100 11.67 egg festival    NA
    ## 2     rhubarb     fruit 100  9.23        oasis    NA
    ## 3 cauliflower vegetable  80  7.92                 NA
    ## 4  green bean vegetable  60  7.20                 NA
    ## 5        kale vegetable  70  6.67                 NA
    ## 6      garlic vegetable  40  5.00                 NA
    ## 7      potato vegetable  50  5.00                 NA
    ## 8     parsnip vegetable  20  3.75                 NA

**Planning:** Going to try and plant the following in 2nd Spring…

  - 32 cauliflower
  - 16 kale
  - 16 potato
  - 16 garlic
  - 16 parsnip
  - 32 green beans
  - 8 blue jazz
  - 8 tulip

**Cost Estimate**: How much money do I need on Spring 1 to buy all the
seeds I want?

First, I wrote a function that will multiply the amount of seeds by the
price of those seeds:

``` r
PriceSeeds <- function(crop, n){
  price <- crops[crops$name == crop, "buy"]
  
  return(price * n)
}
```

Then, I passed each crop and \# of seeds and summed them all:

``` r
spring_money <- PriceSeeds("cauliflower", 32) + 
  PriceSeeds("green bean", 32) + 
  PriceSeeds("kale", 16) + 
  PriceSeeds("potato", 16) + 
  PriceSeeds("garlic", 16) + 
  PriceSeeds("parsnip", 16) + 
  PriceSeeds("blue jazz", 8) + 
  PriceSeeds("tulip", 8)
```

``` r
print(paste("On Spring 1, you need $", spring_money, sep = ""))
```

    ## [1] "On Spring 1, you need $7760"
