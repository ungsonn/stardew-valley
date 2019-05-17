Stardew Valley: Farm Planning
================
Nick D. Ungson

**Last updated:** 2019-05-17 14:20:32

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
List <- function(season){
  crops %>% 
    filter(season == paste(season)) %>% 
    select(name, 
           type) %>% 
    arrange(desc(type)) %>% 
    return()
}
```

**What are the most profitable crops?** (measured in gold per day)

``` r
GPD <- function(season){
  crops %>%
  filter(season == paste(season)) %>% 
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
List(spring)
```

    ##              name      type
    ## 1     cauliflower vegetable
    ## 2          garlic vegetable
    ## 3            kale vegetable
    ## 4         parsnip vegetable
    ## 5          potato vegetable
    ## 6      green bean vegetable
    ## 7          radish vegetable
    ## 8     red cabbage vegetable
    ## 9           wheat vegetable
    ## 10           corn vegetable
    ## 11           hops vegetable
    ## 12     hot pepper vegetable
    ## 13         tomato vegetable
    ## 14        rhubarb     fruit
    ## 15     strawberry     fruit
    ## 16          melon     fruit
    ## 17      starfruit     fruit
    ## 18      blueberry     fruit
    ## 19      blue jazz    flower
    ## 20          tulip    flower
    ## 21          poppy    flower
    ## 22 summer spangle    flower
    ## 23      sunflower    flower
    ## 24         coffee      crop
    ## 25         coffee      crop

Most
    valuable?

``` r
GPD(spring)
```

    ##       gpd           name grow regrow          note1          note2
    ## 1   26.92      starfruit   13      0          oasis               
    ## 2   23.00         coffee   10      2 traveling cart spring, summer
    ## 3   23.00         coffee   10      2 traveling cart spring, summer
    ## 4   20.80      blueberry   13      4                              
    ## 5   17.78    red cabbage    9      0                              
    ## 6   14.17          melon   12      0                              
    ## 7   13.52           hops   11      1                              
    ## 8   11.67     strawberry    8      4   egg festival               
    ## 9   10.77     hot pepper    5      3                              
    ## 10   9.26         tomato   11      4                              
    ## 11   9.23        rhubarb   13      0          oasis               
    ## 12   8.33         radish    6      0                              
    ## 13   7.92    cauliflower   12      0                              
    ## 14   7.41           corn   14      4 spring, summer               
    ## 15   7.20     green bean   10      3                              
    ## 16   6.67           kale    6      0                              
    ## 17   5.71          poppy    7      0                              
    ## 18   5.00         garlic    4      0                              
    ## 19   5.00         potato    6      0                              
    ## 20   5.00 summer spangle    8      0                              
    ## 21   3.75        parsnip    4      0                              
    ## 22   3.75          wheat    4      0   summer, fall               
    ## 23   2.86      blue jazz    7      0                              
    ## 24   1.67          tulip    6      0                              
    ## 25 -15.00      sunflower    8      0   summer, fall

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
List(summer)
```

    ##              name      type
    ## 1     cauliflower vegetable
    ## 2          garlic vegetable
    ## 3            kale vegetable
    ## 4         parsnip vegetable
    ## 5          potato vegetable
    ## 6      green bean vegetable
    ## 7          radish vegetable
    ## 8     red cabbage vegetable
    ## 9           wheat vegetable
    ## 10           corn vegetable
    ## 11           hops vegetable
    ## 12     hot pepper vegetable
    ## 13         tomato vegetable
    ## 14        rhubarb     fruit
    ## 15     strawberry     fruit
    ## 16          melon     fruit
    ## 17      starfruit     fruit
    ## 18      blueberry     fruit
    ## 19      blue jazz    flower
    ## 20          tulip    flower
    ## 21          poppy    flower
    ## 22 summer spangle    flower
    ## 23      sunflower    flower
    ## 24         coffee      crop
    ## 25         coffee      crop

Most
    valuable?

``` r
GPD(summer)
```

    ##       gpd           name grow regrow          note1          note2
    ## 1   26.92      starfruit   13      0          oasis               
    ## 2   23.00         coffee   10      2 traveling cart spring, summer
    ## 3   23.00         coffee   10      2 traveling cart spring, summer
    ## 4   20.80      blueberry   13      4                              
    ## 5   17.78    red cabbage    9      0                              
    ## 6   14.17          melon   12      0                              
    ## 7   13.52           hops   11      1                              
    ## 8   11.67     strawberry    8      4   egg festival               
    ## 9   10.77     hot pepper    5      3                              
    ## 10   9.26         tomato   11      4                              
    ## 11   9.23        rhubarb   13      0          oasis               
    ## 12   8.33         radish    6      0                              
    ## 13   7.92    cauliflower   12      0                              
    ## 14   7.41           corn   14      4 spring, summer               
    ## 15   7.20     green bean   10      3                              
    ## 16   6.67           kale    6      0                              
    ## 17   5.71          poppy    7      0                              
    ## 18   5.00         garlic    4      0                              
    ## 19   5.00         potato    6      0                              
    ## 20   5.00 summer spangle    8      0                              
    ## 21   3.75        parsnip    4      0                              
    ## 22   3.75          wheat    4      0   summer, fall               
    ## 23   2.86      blue jazz    7      0                              
    ## 24   1.67          tulip    6      0                              
    ## 25 -15.00      sunflower    8      0   summer, fall
