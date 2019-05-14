Stardew Valley: Farm Planning
================
Nick D. Ungson

**Last updated:** 2019-05-14 13:40:32

# Prep

Load data:

``` r
require(tidyverse)
require(here)

crops <- read.csv(
  here("crops.csv"), 
  header = TRUE, 
  stringsAsFactors = TRUE)
```

# Spring

What are all the crops available in spring:

``` r
crops %>% 
  filter(season == "spring") %>% 
  select(name:note2) %>% 
  print()
```

    ##           name      type  buy grow regrow max_harvest   gpd          note1
    ## 1    blue jazz    flower   30    7      0           3  2.86               
    ## 2  cauliflower vegetable   80   12      0           2  7.92               
    ## 3       garlic vegetable   40    4      0           6  5.00               
    ## 4         kale vegetable   70    6      0           4  6.67               
    ## 5      parsnip vegetable   20    4      0           6  3.75               
    ## 6       potato vegetable   50    6      0           4  5.00               
    ## 7      rhubarb     fruit  100   13      0           2  9.23          oasis
    ## 8        tulip    flower   20    6      0           4  1.67               
    ## 9       coffee      crop 2500   10      2          NA 23.00 traveling cart
    ## 10  green bean vegetable   60   10      3           6  7.20               
    ## 11  strawberry     fruit  100    8      4           2 11.67   egg festival
    ##    note2
    ## 1     NA
    ## 2     NA
    ## 3     NA
    ## 4     NA
    ## 5     NA
    ## 6     NA
    ## 7     NA
    ## 8     NA
    ## 9     NA
    ## 10    NA
    ## 11    NA

What are the most *profitable* (by gold per day) spring crops?

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
