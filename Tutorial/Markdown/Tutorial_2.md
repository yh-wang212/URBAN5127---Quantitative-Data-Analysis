> Source: [Chapter 3 Tutorial 2_ Descriptive Statistics _ QDA Lab Workbook.html](../Tutorial/Tutorial_2/Chapter%203%20Tutorial%202_%20Descriptive%20Statistics%20_%20QDA%20Lab%20Workbook.html) · [Original workbook page](https://qdaworkbook.netlify.app/tutorial-2-descriptive-statistics)

<span id="tutorial-2-descriptive-statistics"></span>

# 3 Tutorial 2: Descriptive Statistics

Let’s pick up where we left off. We will use the R Script you created last time (Lab Tutorial 1) for this Lab Tutorial. Here is a summary of what we did last time:

``` r
# Step 1: Load the tidyverse package(need to do this EACH time you open up R Studio)
library(tidyverse)

# Step 2: Read in our data: we've loaded the tidyverse, so we can use the read_csv function from the tidyverse now...
listings <- read_csv("listings_edinburgh.csv")

# Step 3: After inspeting our data, we had to coerce or change some of our variables using the mutate() function:
listings <- mutate(listings, room_type = factor(room_type))
listings <- mutate(listings, property_type = factor(property_type))
```

Then we had a quick check:

``` r
glimpse(listings)
```

``` text
## Rows: 14,014
## Columns: 10
## $ name                   <chr> "Georgian Boutique Apt City Centre", "Cool central Loft, sleeps 4…
## $ neighbourhood_cleansed <chr> "Old Town, Princes Street and Leith Street", "Meadows and Southsi…
## $ property_type          <fct> Apartment, Loft, Apartment, Condominium, Condominium, Apartment, …
## $ room_type              <fct> Entire home/apt, Entire home/apt, Entire home/apt, Private room, …
## $ accommodates           <dbl> 2, 4, 2, 2, 2, 3, 5, 5, 6, 10, 2, 4, 3, 2, 2, 4, 2, 4, 10, 5, 2, …
## $ bathrooms              <dbl> 1.0, 1.5, 1.0, 1.0, 1.0, 1.0, 1.0, 1.5, 1.0, 2.0, 1.0, 2.0, 1.0, …
## $ bedrooms               <dbl> 1, 2, 0, 1, 1, 1, 2, 3, 4, 4, 1, 1, 1, 1, 1, 2, 1, 1, 5, 1, 1, 1,…
## $ beds                   <dbl> 1, 2, 2, 1, 1, 2, 3, 2, 5, 7, 1, 1, 1, 1, 1, 2, 1, 1, 5, 2, 1, 1,…
## $ price                  <dbl> 80, 115, 46, 32, 100, 71, 175, 150, 139, 190, 85, 64, 79, 60, 55,…
## $ review_scores_rating   <dbl> 99, 92, 94, 93, 98, 97, 100, 92, 96, 99, 77, 98, 98, 96, 98, 89, …
```

It’s as it should be: `room_type` and `property_type` have been coerced to factor `<fct>` variables. Now we can move on to Tutorial 2.

<span id="exercises"></span>

## 3.1 Exercises

<span id="summary-statistics"></span>

### 3.1.1 Summary statistics

Let’s start off with using the [`summarise()`](https://dplyr.tidyverse.org/reference/summarise.html) function from the `tidyverse` package.

Type out and run the code below. Remember you can hit the `Run` button or use the keyboard shortcut: `Crtl + Enter`. Ask a Lab colleague or your Tutors if you are still unsure.

``` r
summarise(listings, min(price), max(price), mean(price), median(price))
```

``` text
## # A tibble: 1 × 4
##   `min(price)` `max(price)` `mean(price)` `median(price)`
##          <dbl>        <dbl>         <dbl>           <dbl>
## 1            0        12345          130.              75
```

The minimum value of price is zero: that means it’s free!? That’s doubtful. Let’s remember this but park it for now…

We can also write this another way: using the pipe operator %\>% from the tidyverse. The pipe operator just means “and then” and it is helps us make our code more readable: we can write out our code in simple steps (A *and then* B *and then* C etc). So we can understand more easily what we were doing last week (and so can others).

What is our first step: our dataset. We need to start with that *and then*… what’s next? We need to calculate various summary statistics of price:

``` r
# 1. Price 

listings %>%
  summarise(min(price), median(price), mean(price), max(price))
```

``` text
## # A tibble: 1 × 4
##   `min(price)` `median(price)` `mean(price)` `max(price)`
##          <dbl>           <dbl>         <dbl>        <dbl>
## 1            0              75          130.        12345
```

``` r
# 2. Bedrooms
listings %>%
  summarise(min(bedrooms), median(bedrooms), mean(bedrooms), max(bedrooms))
```

``` text
## # A tibble: 1 × 4
##   `min(bedrooms)` `median(bedrooms)` `mean(bedrooms)` `max(bedrooms)`
##             <dbl>              <dbl>            <dbl>           <dbl>
## 1              NA                 NA               NA              NA
```

``` r
# 3. Bathrooms
listings %>%
  summarise(min(bathrooms), median(bathrooms), mean(bathrooms), max(bathrooms))
```

``` text
## # A tibble: 1 × 4
##   `min(bathrooms)` `median(bathrooms)` `mean(bathrooms)` `max(bathrooms)`
##              <dbl>               <dbl>             <dbl>            <dbl>
## 1               NA                  NA                NA               NA
```

So we can also pipe this too: we’ll extract out our dataframe ‘listings’ (Step 1) and then pipe that to the [`summarise()`](https://dplyr.tidyverse.org/reference/summarise.html) function (Step 2). We call these pipelines. And whilst this is a simple example (only two steps), it can get more complicated and then the value becomes clear.

Note that we run the exact same command each time - we’re just changing the variable name (e.g. price, bedrooms, bathrooms).

Also, note there are some missing values in the following variables: `bedrooms, bathrooms`. Have a quick look through the dataset (you can use the [`View()`](https://rdrr.io/r/utils/View.html) function from last week) and you’ll see these for yourself.

If there is, however, *even just one* missing value, we get `NA` returned. So…

We’re going to pipe our **Airbnb** data to the function, [`drop_na()`](https://tidyr.tidyverse.org/reference/drop_na.html). That will remove those observations with missing values. Then we will pipe the result of *that* to our [`summarise()`](https://dplyr.tidyverse.org/reference/summarise.html) function: a pipeline of three steps now. And then re-run the code.

``` r
# Let's drop the missing values using drop_na()

# 1. Price 

listings %>% 
  drop_na(price) %>% 
  summarise(min(price), median(price), mean(price), max(price))
```

``` text
## # A tibble: 1 × 4
##   `min(price)` `median(price)` `mean(price)` `max(price)`
##          <dbl>           <dbl>         <dbl>        <dbl>
## 1            0              75          130.        12345
```

``` r
# 2. Bedrooms
listings %>%
  drop_na(bedrooms) %>% 
  summarise(min(bedrooms), median(bedrooms), mean(bedrooms), max(bedrooms))
```

``` text
## # A tibble: 1 × 4
##   `min(bedrooms)` `median(bedrooms)` `mean(bedrooms)` `max(bedrooms)`
##             <dbl>              <dbl>            <dbl>           <dbl>
## 1               0                  1             1.58              13
```

``` r
# 3. Bathrooms
listings %>%
  drop_na(bathrooms) %>% 
  summarise(min(bathrooms), median(bathrooms), mean(bathrooms), max(bathrooms))
```

``` text
## # A tibble: 1 × 4
##   `min(bathrooms)` `median(bathrooms)` `mean(bathrooms)` `max(bathrooms)`
##              <dbl>               <dbl>             <dbl>            <dbl>
## 1                0                   1              1.23                9
```

Finally, here is the Advanced version: this is just for reference.

``` r
listings %>%
  select(price,bedrooms,bathrooms) %>%
  drop_na() %>%
  pivot_longer(1:3, names_to = "variable") %>%
  group_by(variable) %>%
  summarise(min(value), median(value), mean(value), max(value))
```

``` text
## # A tibble: 3 × 5
##   variable  `min(value)` `median(value)` `mean(value)` `max(value)`
##   <chr>            <dbl>           <dbl>         <dbl>        <dbl>
## 1 bathrooms            0               1          1.23            9
## 2 bedrooms             0               1          1.58           13
## 3 price                0              75        130.          12345
```

Optional: See if you can work through the above example later on (or later on in the course) and see what’s going on. You might have to Google the [`pivot_longer()`](https://tidyr.tidyverse.org/reference/pivot_longer.html) function and do some reading.

<span id="filter-out-unreasonable-values"></span>

### 3.1.2 Filter out unreasonable values

We’re now going to sense check these values: do they look right? And if not, we’ll exclude them.

1.  First, let’s look at the ‘price’ variable: we’ll sort from highest to lowest - like sorting in Excel.

To do so we’ll use the Tidyverse function called [`arrange()`](https://dplyr.tidyverse.org/reference/arrange.html):

``` r
# lowest to highest
arrange(listings, price) 
```

``` text
## # A tibble: 14,014 × 10
##    name       neighbourhood_cleansed property_type room_type accommodates bathrooms bedrooms  beds
##    <chr>      <chr>                  <fct>         <fct>            <dbl>     <dbl>    <dbl> <dbl>
##  1 Large and… Slateford and Chesser  Apartment     Private …            2         1        1     1
##  2 Private r… South Leith            Apartment     Private …            1         1        1     1
##  3 Small cos… Gorgie West            Apartment     Private …            1         1        1     1
##  4 Attractiv… Murrayburn and Wester… Apartment     Private …            3         1        1     3
##  5 Modern Ci… Broughton South        Apartment     Entire h…            2         1        1     1
##  6 Bright to… Meadows and Southside  Apartment     Entire h…            6         1        3     4
##  7 Longer ro… Hillside and Calton H… Apartment     Shared r…            1         1        1     2
##  8 Edinburgh… Meadows and Southside  Hostel        Private …            1         1        1     1
##  9 Stunning … Meadows and Southside  Apartment     Private …            1         1        1     1
## 10 17 day le… Bruntsfield            Apartment     Private …            1         2        1     1
## # ℹ 14,004 more rows
## # ℹ 2 more variables: price <dbl>, review_scores_rating <dbl>
```

N.B: you can also do this in reverse order (highest to lowest): use [`desc()`](https://dplyr.tidyverse.org/reference/desc.html) for descending order.

``` r
# highest to lowest
arrange(listings, desc(price)) 
```

``` text
## # A tibble: 14,014 × 10
##    name       neighbourhood_cleansed property_type room_type accommodates bathrooms bedrooms  beds
##    <chr>      <chr>                  <fct>         <fct>            <dbl>     <dbl>    <dbl> <dbl>
##  1 Large Pen… Western Harbour and L… Apartment     Entire h…           15         4        4    15
##  2 CITY ONE … Tollcross              House         Entire h…            2         1        1     0
##  3 Double En… Leith (Albert Street)  Apartment     Private …            2         1        1     1
##  4 4 Bedroom… Leith (Albert Street)  Apartment     Entire h…            8         4        4     4
##  5 5 Bedroom… Leith (Albert Street)  Apartment     Entire h…           10         5        5     5
##  6 Studio Ap… Leith (Albert Street)  Apartment     Entire h…            2         1        0     1
##  7 Double En… Pilrig                 Apartment     Private …            2         1        1     1
##  8 5 Bedroom… Pilrig                 Apartment     Entire h…           10         5        5     5
##  9 Studio Ap… Pilrig                 Apartment     Entire h…            2         1        0     1
## 10 Double En… Old Town, Princes Str… Apartment     Private …            2         1        1     1
## # ℹ 14,004 more rows
## # ℹ 2 more variables: price <dbl>, review_scores_rating <dbl>
```

Now let’s sort (or arrange) low to high and just look at the first ten observations (or properties).

We’re going to use another function: [`head()`](https://rdrr.io/r/utils/head.html) which will give us just the first ten values of price rather than all 13,647 of them. Note head() takes an argument specifying how many of these observations (or properties) you want to see. We’ll request the first 10.

We can also use the opposite function: [`tail()`](https://rdrr.io/r/utils/head.html). Which gives us the *last* ten values of price. We do not need to stick with ten all the time. Let’s change this so we can see the last 20 values of price:

``` r
# these will be the cheapest
listings %>%
  arrange(price) %>%
  head(10)
```

``` text
## # A tibble: 10 × 10
##    name       neighbourhood_cleansed property_type room_type accommodates bathrooms bedrooms  beds
##    <chr>      <chr>                  <fct>         <fct>            <dbl>     <dbl>    <dbl> <dbl>
##  1 Large and… Slateford and Chesser  Apartment     Private …            2         1        1     1
##  2 Private r… South Leith            Apartment     Private …            1         1        1     1
##  3 Small cos… Gorgie West            Apartment     Private …            1         1        1     1
##  4 Attractiv… Murrayburn and Wester… Apartment     Private …            3         1        1     3
##  5 Modern Ci… Broughton South        Apartment     Entire h…            2         1        1     1
##  6 Bright to… Meadows and Southside  Apartment     Entire h…            6         1        3     4
##  7 Longer ro… Hillside and Calton H… Apartment     Shared r…            1         1        1     2
##  8 Edinburgh… Meadows and Southside  Hostel        Private …            1         1        1     1
##  9 Stunning … Meadows and Southside  Apartment     Private …            1         1        1     1
## 10 17 day le… Bruntsfield            Apartment     Private …            1         2        1     1
## # ℹ 2 more variables: price <dbl>, review_scores_rating <dbl>
```

``` r
# look at the last twenty properties
# these will be the most expensive
listings %>%
  arrange(price) %>%
  tail(20)
```

``` text
## # A tibble: 20 × 10
##    name       neighbourhood_cleansed property_type room_type accommodates bathrooms bedrooms  beds
##    <chr>      <chr>                  <fct>         <fct>            <dbl>     <dbl>    <dbl> <dbl>
##  1 The Canon… Canongate, Southside … Apartment     Entire h…            4         1        1     1
##  2 Sciennes … Marchmont East and Sc… Apartment     Entire h…            8         1        3     4
##  3 The Mille… Marchmont East and Sc… Apartment     Entire h…           10         2        5     5
##  4 Main Larg… Leith (Albert Street)  Apartment     Private …            3         1        1     5
##  5 CityLivei… Dalry and Fountainbri… Apartment     Entire h…           10         6        5     5
##  6 CityLivei… Dalry and Fountainbri… Apartment     Entire h…           12         7        6     6
##  7 Spacious … Bruntsfield            Apartment     Entire h…            4         1        2     3
##  8 Double En… Leith (Albert Street)  Apartment     Private …            2         1        1     1
##  9 4 Bedroom… Leith (Albert Street)  Apartment     Entire h…            8         4        4     4
## 10 5 Bedroom… Leith (Albert Street)  Apartment     Entire h…           10         5        5     5
## 11 Studio Ap… Leith (Albert Street)  Apartment     Entire h…            2         1        0     1
## 12 Double En… Pilrig                 Apartment     Private …            2         1        1     1
## 13 5 Bedroom… Pilrig                 Apartment     Entire h…           10         5        5     5
## 14 Studio Ap… Pilrig                 Apartment     Entire h…            2         1        0     1
## 15 Double En… Old Town, Princes Str… Apartment     Private …            2         1        1     1
## 16 4 Bedroom… Old Town, Princes Str… Apartment     Entire h…            8         4        4     4
## 17 Studio Ap… Old Town, Princes Str… Apartment     Entire h…            2         1        0     1
## 18 Penthouse… Old Town, Princes Str… Apartment     Entire h…            2         1        0     1
## 19 Large Pen… Western Harbour and L… Apartment     Entire h…           15         4        4    15
## 20 CITY ONE … Tollcross              House         Entire h…            2         1        1     0
## # ℹ 2 more variables: price <dbl>, review_scores_rating <dbl>
```

Some values look suspect: 9999 or -9999 is often used to designate missing values.

Also 12345 seems odd, especially appearing exactly like this twice.

So at this point, we might want to make a decision as to whether we exclude these. The documentation (and codebook) would be the first thing(s) we would check. We don’t have this however so we’ll need to use our own judgement.

2.  Let’s look at bedrooms

``` r
# We'll sort bathrooms from low to high again, and look at the first twenty observations:

listings %>% arrange(bathrooms) %>% 
  head(20)
```

``` text
## # A tibble: 20 × 10
##    name       neighbourhood_cleansed property_type room_type accommodates bathrooms bedrooms  beds
##    <chr>      <chr>                  <fct>         <fct>            <dbl>     <dbl>    <dbl> <dbl>
##  1 Nice Cent… Easter Road and Hawkh… Apartment     Private …            2         0        1     1
##  2 LUXURY  E… Deans Village          Apartment     Entire h…            4         0        2     3
##  3 LUXURY Ci… Deans Village          Apartment     Private …            3         0        1     2
##  4 Double ro… Marchmont West         Apartment     Private …            2         0        1     1
##  5 4 Person … Ratho, Ingliston and … Campsite      Entire h…            4         0        2     2
##  6 2 Person … Ratho, Ingliston and … Tent          Private …            2         0        1     2
##  7 1 Person … Ratho, Ingliston and … Tent          Private …            1         0        1     1
##  8 DOUBLE BI… The Calders            Apartment     Private …            1         0        1     1
##  9 Tidy and … Newington and Dalkeit… Apartment     Private …            1         0        1     1
## 10 Lovely ro… Cramond                House         Private …            1         0        1     1
## 11 A Cosy Be… Meadows and Southside  Apartment     Private …            2         0        1     1
## 12 Spacious … Pilrig                 Apartment     Private …            2         0        1     1
## 13 Twin bedd… Joppa                  Bed and brea… Private …            2         0        1     2
## 14 City Cent… Canongate, Southside … Apartment     Private …            2         0        1     1
## 15 Double be… Bruntsfield            Apartment     Private …            2         0        1     1
## 16 Art Resid… Easter Road and Hawkh… Apartment     Private …            1         0        0     1
## 17 Double be… Blackford, West Mains… Apartment     Private …            2         0        1     1
## 18 one singl… Blackford, West Mains… Apartment     Private …            1         0        1     1
## 19 Single ro… Corstorphine North     Apartment     Private …            1         0        1     1
## 20 LOVELY 3 … Canonmills and New To… Apartment     Private …            2         0        1     1
## # ℹ 2 more variables: price <dbl>, review_scores_rating <dbl>
```

Would we say that no bathrooms is realistic? Perhaps. Maybe it means no bathrooms in the actual room itself? So there is no bathroom in the room but maybe down the hall or in another part of the property? It’s hard to tell.

3.  Let’s move on to bathrooms:

``` r
# let's look at the higher end - those properties with the most bathrooms:

listings %>% arrange(bathrooms) %>% 
  tail(20)
```

``` text
## # A tibble: 20 × 10
##    name       neighbourhood_cleansed property_type room_type accommodates bathrooms bedrooms  beds
##    <chr>      <chr>                  <fct>         <fct>            <dbl>     <dbl>    <dbl> <dbl>
##  1 Bainfield… Dalry and Fountainbri… Apartment     Entire h…           14       7          7     7
##  2 Grade A L… Drylaw                 House         Entire h…           16       7.5        9    16
##  3 Bainfield… Dalry and Fountainbri… Apartment     Entire h…           16       8          8     8
##  4 Orwell Te… Dalry and Fountainbri… Apartment     Entire h…            8       8          8     8
##  5 Universit… Bruntsfield            Townhouse     Private …           16       9         13    17
##  6 Hen Party… Deans Village          Townhouse     Entire h…           16       9          7    22
##  7 Edinburgh… Bruntsfield            House         Private …           16       9         13    24
##  8 Orwell Te… Dalry and Fountainbri… Apartment     Entire h…            9       9          9     9
##  9 Bright Ce… Leith (Albert Street)  Apartment     Private …            2      NA          1     1
## 10 1 bedroom… Marchmont East and Sc… Apartment     Private …            2      NA          1     1
## 11 Huge doub… Broughton North and P… Apartment     Private …            2      NA          1     1
## 12 One of th… Easter Road and Hawkh… Apartment     Private …            2      NA          1     1
## 13 Tradition… Leith (Albert Street)  Apartment     Private …            2      NA          1     1
## 14 Elegant S… Deans Village          House         Entire h…           16      NA          5    16
## 15 Double be… The Shore and Constit… Apartment     Private …            1      NA          1     1
## 16 Lovely do… Portobello             Bed and brea… Private …            2      NA          1    NA
## 17 Attractiv… Meadows and Southside  Apartment     Private …            2      NA          1     1
## 18 quiet cit… Pilrig                 Apartment     Entire h…            6      NA          2    NA
## 19 Lovely Ro… Deans Village          House         Private …            2      NA          1     1
## 20 Modern co… Colinton and Kingskno… House         Private …            2      NA          1    NA
## # ℹ 2 more variables: price <dbl>, review_scores_rating <dbl>
```

There seems like an awful amount of bathrooms in some instances (up to 9 bathrooms) - again perhaps this means the total amount of bathrooms in the property as a whole (e.g. as in a hotel)?

4.  OK. We need to make a decision now. Let’s filter out the properties (or observations) where they don’t look right.

Let’s say:

1.  If price is below £25 and is above £1,000, we’re going to exclude them. Otherwise the huge outliers (e.g. 12,345) are going to distort our data.
2.  And let’s just say we’ll get rid of any properties where the number of bathrooms if five or over.

We’ll use the [`filter()`](https://dplyr.tidyverse.org/reference/filter.html) function from the Tidyverse. This will drop the observations (or properties) that do not meet our criteria.

``` r
# so let's keep (a) prices greater than or equal to £25 (b) prices £1,000 or under (c) five bathrooms or under 

listings <- filter(listings,
                   price >= 25, price <= 1000, bathrooms <= 5) %>%
  drop_na(price, bedrooms, bathrooms) # and drop any missing (na) values
```

<span id="make-a-frequency-table"></span>

### 3.1.3 Make a frequency table

Let’s make a frequency table showing the number *and* percentage of listings in each room type.

``` r
listings %>%
  count(room_type) %>%
  mutate(percent = (n / sum(n)*100) %>% round(2))
```

``` text
## # A tibble: 3 × 3
##   room_type           n percent
##   <fct>           <int>   <dbl>
## 1 Entire home/apt  8677   63.6 
## 2 Private room     4901   35.9 
## 3 Shared room        69    0.51
```

What did we do here?

1.  We piped the ‘listings’ dataset object to the [`count()`](https://dplyr.tidyverse.org/reference/count.html) function
2.  [`count()`](https://dplyr.tidyverse.org/reference/count.html) will count the number of room types and store it in a new column called ‘n’ which we can use in the next step…
3.  pass the result to the [`mutate()`](https://dplyr.tidyverse.org/reference/mutate.html) function, which performs a calculation on the new variable ‘n’ and stores the result in a new variable ‘percent’
4.  Then rounds the result to two decimal places and gives us the results in a table.

<span id="make-a-table-showing-the-summary-statistics"></span>

### 3.1.4 Make a table showing the summary statistics

Another useful function is [`group_by()`](https://dplyr.tidyverse.org/reference/group_by.html). For example, what if I wanted to see the average price (mean) by the property_type? That is, does the average Airbnb price vary if it is a hotel compared to a tent, say?

To explore this, we would group by `property_type`. Here is an example of the code we had earlier:

``` r
# simple summary of price (see Section 1 above)
listings %>%
  summarise(min(price), median(price), mean(price), max(price))
```

``` text
## # A tibble: 1 × 4
##   `min(price)` `median(price)` `mean(price)` `max(price)`
##          <dbl>           <dbl>         <dbl>        <dbl>
## 1           25              78          114.         1000
```

``` r
# We can now see if price varies by property type:

listings %>%
  group_by(property_type) %>%
  summarise(min(price), median(price), mean(price), max(price))
```

``` text
## # A tibble: 30 × 5
##    property_type     `min(price)` `median(price)` `mean(price)` `max(price)`
##    <fct>                    <dbl>           <dbl>         <dbl>        <dbl>
##  1 Aparthotel                  45           100           103.           200
##  2 Apartment                   25            79           112.          1000
##  3 Barn                       100           125           125            150
##  4 Bed and breakfast           25            70            82.6          636
##  5 Boat                       150           575           575           1000
##  6 Boutique hotel              45           144.          299.          1000
##  7 Bungalow                    30            54.5          83.9          913
##  8 Cabin                       30            60            79.7          149
##  9 Camper/RV                   35            75            81            160
## 10 Campsite                    86            86            86             86
## # ℹ 20 more rows
```

Let’s apply this example to the variable `room_type`:

``` r
#  Make a table showing the summary statistics for price broken down by room_type.

listings %>%
  group_by(room_type) %>%
  summarise(min(price), median(price), mean(price), max(price))
```

``` text
## # A tibble: 3 × 5
##   room_type       `min(price)` `median(price)` `mean(price)` `max(price)`
##   <fct>                  <dbl>           <dbl>         <dbl>        <dbl>
## 1 Entire home/apt           25              99         143.          1000
## 2 Private room              25              46          61.2         1000
## 3 Shared room               25              84         243.          1000
```

We can see the results of our filtering here: the minimum now being £25 per night and the maximum being £1,000 per night.

Also, compare the mean and median values: we can see that there is quite a difference between the median and mean of ‘Shared Room’, for example: the maximum value ‘pulling’ the mean away from the median.

Next time, we will start to plot and that will help us look at the distribution of price, for example. This will help us understand whether we might want to adjust our filter criteria i.e. maybe £1,000 is *still* too high and we want to lower this further. Creating a plot of the distribution of ‘price’ will help us decide.

<span id="the-functions-we-have-learned"></span>

## 3.2 The `functions()` we have learned

Tutorial 2 has learned us how to start exploring our data through some basic descriptive statistics and, based on their values, whether we might need to make any further changes to our data.

We learned how to use the pipe operator `%>%` and start to construct `pipelines`.

In addition, we have now learned some of the key Tidyverse functions for working with data:

1.  [`select()`](https://dplyr.tidyverse.org/reference/select.html) and [`mutate()`](https://dplyr.tidyverse.org/reference/mutate.html): or working with columns (or variables);
2.  [`filter()`](https://dplyr.tidyverse.org/reference/filter.html) and [`arrange()`](https://dplyr.tidyverse.org/reference/arrange.html): for working with rows (or observations);
3.  [`group_by()`](https://dplyr.tidyverse.org/reference/group_by.html) and [`summarise()`](https://dplyr.tidyverse.org/reference/summarise.html): for aggregating and summarising.

Moreover, we have learned a few other functions() along the way in both Tutorial 1 and Tutorial 2: `View(),` [`glimpse()`](https://pillar.r-lib.org/reference/glimpse.html), [`head()`](https://rdrr.io/r/utils/head.html), [`tail()`](https://rdrr.io/r/utils/head.html), `count(), drop_na()` as well as others like [`levels()`](https://rdrr.io/r/base/levels.html), [`factor()`](https://rdrr.io/r/base/factor.html) and [`library()`](https://rdrr.io/r/base/library.html).

Try to practice these functions. Play with the data and see what they do. See also the two optional recommendations from the Tutorial 2 slides:

1.  [Datacamp](https://www.datacamp.com/): Introduction to the Tidyverse
2.  [R for Data Science](https://r4ds.had.co.nz/): Introduction and Explore (sections 2-8)

[2 Tutorial 1: Reading in our data](https://qdaworkbook.netlify.app/tutorial-1-reading-in-our-data) [4 Tutorial 3: Data Visualisation - Numeric variables](https://qdaworkbook.netlify.app/tutorial-3-data-visualisation---numeric-variables)
