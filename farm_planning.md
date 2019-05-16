Stardew Valley: Farm Planning
================
Nick D. Ungson

**Last updated:** 2019-05-16 19:28:16

All data below from the [Stardew Valley
Wiki](https://stardewvalleywiki.com/Stardew_Valley_Wiki)

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

What are all the crops available in
[Spring](https://stardewvalleywiki.com/Spring)?

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
    ##             note2
    ## 1                
    ## 2                
    ## 3                
    ## 4                
    ## 5                
    ## 6                
    ## 7                
    ## 8                
    ## 9  spring, summer
    ## 10               
    ## 11

What are the most *profitable* (by gold per day) Spring crops?

``` r
crops %>%
  filter(season == "spring") %>% 
  select(name, 
         gpd,
         buy, 
         type, 
         note1:note2) %>% 
  arrange(desc(gpd))
```

    ##           name   gpd  buy      type          note1          note2
    ## 1       coffee 23.00 2500      crop traveling cart spring, summer
    ## 2   strawberry 11.67  100     fruit   egg festival               
    ## 3      rhubarb  9.23  100     fruit          oasis               
    ## 4  cauliflower  7.92   80 vegetable                              
    ## 5   green bean  7.20   60 vegetable                              
    ## 6         kale  6.67   70 vegetable                              
    ## 7       garlic  5.00   40 vegetable                              
    ## 8       potato  5.00   50 vegetable                              
    ## 9      parsnip  3.75   20 vegetable                              
    ## 10   blue jazz  2.86   30    flower                              
    ## 11       tulip  1.67   20    flower

**Planning:** I want to plant the following in on the first day of
Spring…

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

# Summer

What are all the crops available in
[Summer](https://stardewvalleywiki.com/Summer)?

``` r
crops %>% 
  filter(season == "summer") %>% 
  select(name:note2) %>% 
  arrange(desc(type)) %>% 
  print()
```

    ##              name      type  buy grow regrow max_harvest    gpd
    ## 1          radish vegetable   40    6      0           4   8.33
    ## 2     red cabbage vegetable  100    9      0           3  17.78
    ## 3           wheat vegetable   10    4      0           6   3.75
    ## 4            corn vegetable  150   14      4           4   7.41
    ## 5            hops vegetable   60   11      1          17  13.52
    ## 6      hot pepper vegetable   40    5      3           8  10.77
    ## 7          tomato vegetable   50   11      4           5   9.26
    ## 8           melon     fruit   80   12      0           2  14.17
    ## 9       starfruit     fruit  400   13      0           2  26.92
    ## 10      blueberry     fruit   80   13      4           4  20.80
    ## 11          poppy    flower  100    7      0           3   5.71
    ## 12 summer spangle    flower   50    8      0           3   5.00
    ## 13      sunflower    flower  200    8      0           3 -15.00
    ## 14         coffee      crop 2500   10      2           9  23.00
    ##             note1          note2
    ## 1                               
    ## 2                               
    ## 3    summer, fall               
    ## 4  spring, summer               
    ## 5                               
    ## 6                               
    ## 7                               
    ## 8                               
    ## 9           oasis               
    ## 10                              
    ## 11                              
    ## 12                              
    ## 13   summer, fall               
    ## 14 traveling cart spring, summer

What are the most *profitable* (by gold per day) summer crops?

``` r
crops %>%
  filter(season == "summer") %>% 
  select(name, 
         gpd,
         buy, 
         type, 
         note1:note2) %>% 
  arrange(desc(gpd))
```

    ##              name    gpd  buy      type          note1          note2
    ## 1       starfruit  26.92  400     fruit          oasis               
    ## 2          coffee  23.00 2500      crop traveling cart spring, summer
    ## 3       blueberry  20.80   80     fruit                              
    ## 4     red cabbage  17.78  100 vegetable                              
    ## 5           melon  14.17   80     fruit                              
    ## 6            hops  13.52   60 vegetable                              
    ## 7      hot pepper  10.77   40 vegetable                              
    ## 8          tomato   9.26   50 vegetable                              
    ## 9          radish   8.33   40 vegetable                              
    ## 10           corn   7.41  150 vegetable spring, summer               
    ## 11          poppy   5.71  100    flower                              
    ## 12 summer spangle   5.00   50    flower                              
    ## 13          wheat   3.75   10 vegetable   summer, fall               
    ## 14      sunflower -15.00  200    flower   summer, fall
