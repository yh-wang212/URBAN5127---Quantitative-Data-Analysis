> Source: [Chapter 8 Tutorial 7_ Model Building _ QDA Lab Workbook.html](../Tutorial/Tutorial_7/Chapter%208%20Tutorial%207_%20Model%20Building%20_%20QDA%20Lab%20Workbook.html) · [Original workbook page](https://qdaworkbook.netlify.app/tutorial-7-model-building)

<span id="tutorial-7-model-building"></span>

# 8 Tutorial 7: Model Building

We’re moving onto a new topic: Modelling. This will be the final set of Lab Tutorials: 7-10

Set up a new R Markdown document, read in the data and then recreate any prior changes from Tutorial 1-2.

<span id="introduction"></span>

## 8.1 **Introduction**

From Lab Tutorial 5, my research question is:

*“The price of an Airbnb listing can be predicted primarily by the type of room (room_type), even when controlling for other characteristics like number of rooms, review scores and even property type.”*

So I have a dependent variable (`price`), and a key independent variable that I’m primarily interested in (`room_type`) and control variables that will help isolate the unique effect of my variable of interest.

We see this approach in the lecture example: the unique effect of Gender on pay was isolated by adding in groups of control variables (Additional Demographics, Job characteristics, Firm characteristics etc.).

Let’s create a **model building strategy**. My first model is my Baseline **Model: My Research Question (DV-Key IV)** and so I will need my two variables `price` and `room_typ`e.

What are my *Rival or Alternative explanations*? OK, I’ll need to make this up for pedagogical purposes since I don’t know the literature or the area well. You will need to do this remember though.

OK, I’m thinking the following:

*Rival or Alternative explanation 1: Property characteristics.* I need to control not just for room type but for other characteristics of an Airbnb letting: not just whether it has a private room but whether it is a private room in an expensive hotel or in a boat or in a windmill. So I am wanting to control for all other property type characteristics. I only have one variable here to choose from: `property_type`. I haven’t chosen this dataset myself so I’ll just need to go with this. This will also explain `price` in addition to my Research Question (r`oom_type`)

*Rival or Alternative explanation 2: Hedonic influences.* I am vaguely aware of the literature on hedonic pricing so (and I am drastically simplifying!), another room is going to add value. Obviously, a room with *8 bedrooms* is going to be more expensive than a room with *only 1*: and that’s regardless of whether it is a hotel or windmill or whatever. So this is an additional factor which needs to be accounted for, as it surely explains price also, in addition to what my Research Question puts forward.

*Rival or Alternative explanation 3: Quality.* Now surely if a listing gets really good reviews, it’ll be more expensive? Higher quality (which reviews measure) will probably mean higher prices, right? OK, we’re going with this for now but we’ve already seen this assumption is problematic (when the correlation was negative not positive as we expected). Let’s pretend we don’t know this (never do this) and proceed. What do variables do we need to measure our *Quality* rival explanation: we have r`eview_scores_rating` so we’ll use that.

This is just a quick cobbling together for pedagogical purposes. Make sure you take time here however as this is very important. You need to demonstrate a well thought out modelling strategy if you are going to have a well thought out answer to your Research Questione: the two are not separate.

So putting this all together: we have our Baseline Model (Model 1: Our Research Question) and then we have 3 *Rival or Alternative explanations:*

1.  *Research Question:* My baseline bivariate model (`room_type`)

2.  *Property characteristics:* Add in the other Type variable (`property_type`)

3.  *Hedonic Influences:* Add in the Rooms variables (`bathrooms`, `bedrooms`, `accommodates`)

4.  *Quality:* Add in Reviews (`review_scores_rating`)

So I know how many models to build now: My Baseline and however many *Rival or Alternative explanations* I need to account for (here 3).

<span id="model-1-basic-bivariate-model"></span>

## 8.2 Model 1: Basic bivariate model

I will begin with my **baseline model** therefore, containing my dependent variable and independent variable of interest only: the simple bivariate model which represents the bivariate relationship of my Research Question (DV-Key IV). I can then subsequently control for the other important explanatory factors of price in subsequent models (Models 2-4), using a *Specific to General* approach to model building.

But let’s build model 1:

``` r
# Build model 1
m1 <- listings %>%
  lm(price ~ room_type, 
     data = .) 

# And pass to summary function to see regression output
m1 %>% summary()
```

``` text
## 
## Call:
## lm(formula = price ~ room_type, data = .)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -218.35  -57.58  -24.23    4.42  938.77 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            142.582      1.441  98.919  < 2e-16 ***
## room_typePrivate room  -81.348      2.399 -33.907  < 2e-16 ***
## room_typeShared room   100.766     16.228   6.209 5.47e-10 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 134.3 on 13644 degrees of freedom
## Multiple R-squared:  0.08172,    Adjusted R-squared:  0.08158 
## F-statistic: 607.1 on 2 and 13644 DF,  p-value: < 2.2e-16
```

We need to interpret our model now :

**Basic interpretation (Bivariate)**: For every one-unit increase in x, y changes by \[the coefficient\] on average.

This is straightforward for numeric variables but for factor variables, we need to realise that a one unit change is not along a continuous numeric scale. Instead it is a change in the *category* e.g. from 0 (reference category: Male) to 1 (Female). So what we are doing with factor variables is comparing each category (or factor level) *to a reference category*. This *reference category* will not appear as a coefficient: because it is the thing we are comparing *to*.

In our simple example above: we compared Female to the reference category (Male). We only get one coefficient, therefore (Female): which quantifies the difference to Males.

So the first thing we need to do to interpret a factor variable then is understand the reference category. Note that R will take the very first level (or category) of the factor variable and make *that* the reference category by default. Let’s look at the levels of the factor variable `room_type` to check what this will be:

``` r
levels(listings$room_type)
```

``` text
## [1] "Entire home/apt" "Private room"    "Shared room"
```

The very first level is `Entire home/apt` so this is our reference category.

We can now proceed to interpretation:

- A private room listing is going to be \$81.35 less (-81.348) on average than a listing which is an entire home or apartment (the reference category).

- A shared room listing is going to be \$100.76 more (100.766) on average than an entire home or apartment listing.

We need to use our common sense *and* specific knowledge (e.g. our research area of interest) when we look at regression coefficients. Here common sense tells us that a shared room is not going to be more expensive than having a whole apartment or home to yourself. So something is not right here and, from the tutorial, we saw that our prior work in previous tutorials told us that shared rooms only had 69 observations and was distributed quite differently to the other two levels of `room_type`.

In this instance, we can interpret the intercept. The intercept can be defined as where the regression line crosses the y axis. If you draw this out as a graph or plot, you will see that this is, at the same time, where x = 0.

Here x (or our independent variable ) = 0 is our *reference category*: `Entire home/apt` . So the coefficient here (142.582) means that, on average (i.e. not for *every* entire home or apartment in the dataset), an entire home or apartment listing will cost \$142.58.

Sometimes the intercept will not make any sense, however, especially with numeric variables (e.g. Age = 0).

<span id="model-1-baseline-is-our-inferential-test"></span>

### 8.2.1 Model 1: Baseline is our inferential test

Notice that the t-test is the same as our Baseline Model.

``` r
# 3. Is the difference in price statistically significant?
listings_subset <- filter(listings, room_type != "Shared room") 

t.test(price ~ room_type, data = listings_subset)
```

``` text
## 
##  Welch Two Sample t-test
## 
## data:  price by room_type
## t = 40.419, df = 13419, p-value < 2.2e-16
## alternative hypothesis: true difference in means between group Entire home/apt and group Private room is not equal to 0
## 95 percent confidence interval:
##  77.40350 85.29348
## sample estimates:
## mean in group Entire home/apt    mean in group Private room 
##                     142.58211                      61.23363
```

When we look at the output from the t-test:

- **the mean for Entire home/appt is 142.58211:** this is the same as the intercept in our baseline regression model.

- **the mean for Private Room is 61.23363:** our coefficient is -81.348, the difference between Entire home/appt and Private Room. So how much does a Private Room actually cost on average\> Let’s work it out:

  142.58211 (intercept = Entire home/appt) - 81.34848 (Private Room coefficient) = **61.23363**

It costs \$61.23. The same as the mean price for Private Room.

So the t-test gives us:

1.  the mean cost for Entire home/appt (\$142.58)

2.  and the mean cost for Private Room (\$61.23).

The regression model gives us

1.  the mean cost for Entire home/appt (*intercept*)

2.  and **the difference between Entire home/appt and Private Room** (*the coefficient*). That is, instead of the mean for Private Room the only difference is it gives us the *difference* between Entire home/appt and Private Room.

The only difference between the t-test and the baseline is **number two highlighted** above. The coefficient remember tells us the associated *change* in the price. In a factor variable this is the difference between the reference category (Entire home/appt) and the other category (or categories).

In other words, the t-test and the baseline model *are the same*: it is the same thing (t-test, baseline model) expressed in a slightly different way. This is *always* the case: your inferential test (t-test, ANOVA, correlation) *is* your Baseline Model. This was also what was meant (mainly) in the lecture: that a t-test or ANOVA is just a special case of linear regression.

<span id="model-2-add-property-type"></span>

## 8.3 Model 2: add property type

We then add the other **Type** variable (`property_type`) into our model to finish the independent variables of **Type**:

``` r
# Build model 2 and then pass to summary function
m2 <- listings %>%
  lm(price ~ room_type + property_type,
     data = .) 

m2 %>%  summary()
```

``` text
## 
## Call:
## lm(formula = price ~ room_type + property_type, data = .)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -425.00  -58.47  -20.39    9.36  949.36 
## 
## Coefficients:
##                                     Estimate Std. Error t value Pr(>|t|)    
## (Intercept)                          192.539     44.042   4.372 1.24e-05 ***
## room_typePrivate room                -89.650      2.458 -36.476  < 2e-16 ***
## room_typeShared room                 -54.221     20.462  -2.650  0.00806 ** 
## property_typeApartment               -52.251     44.024  -1.187  0.23530    
## property_typeBarn                    -67.539    103.156  -0.655  0.51266    
## property_typeBed and breakfast       -20.904     45.555  -0.459  0.64633    
## property_typeBoat                    382.461    103.156   3.708  0.00021 ***
## property_typeBoutique hotel          195.484     46.269   4.225 2.41e-05 ***
## property_typeBungalow                -47.329     45.955  -1.030  0.30307    
## property_typeCabin                   -82.989     87.962  -0.943  0.34546    
## property_typeCamper/RV              -106.820     53.432  -1.999  0.04561 *  
## property_typeCampsite               -106.539    139.078  -0.766  0.44367    
## property_typeCasa particular (Cuba)  -52.889    103.127  -0.513  0.60806    
## property_typeChalet                 -117.539    139.078  -0.845  0.39805    
## property_typeCondominium             -44.541     44.792  -0.994  0.32005    
## property_typeCottage                 -57.715     47.584  -1.213  0.22518    
## property_typeEarth house             -63.539    139.078  -0.457  0.64778    
## property_typeFarm stay              -122.539    139.078  -0.881  0.37829    
## property_typeGuest suite             -90.400     47.729  -1.894  0.05824 .  
## property_typeGuesthouse               -2.368     48.092  -0.049  0.96073    
## property_typeHostel                  202.445     48.743   4.153 3.30e-05 ***
## property_typeHotel                    -8.722     69.528  -0.125  0.90017    
## property_typeHouse                   -34.068     44.137  -0.772  0.44021    
## property_typeHut                     -72.889    139.056  -0.524  0.60017    
## property_typeLoft                    -62.685     49.346  -1.270  0.20400    
## property_typeOther                   -60.116     57.207  -1.051  0.29335    
## property_typeServiced apartment       11.971     45.580   0.263  0.79283    
## property_typeTent                    -45.279     73.596  -0.615  0.53841    
## property_typeTiny house              -80.989     87.962  -0.921  0.35721    
## property_typeTownhouse               -32.497     44.597  -0.729  0.46621    
## property_typeVilla                    -5.351     49.783  -0.107  0.91440    
## property_typeWindmill                -72.539    139.078  -0.522  0.60198    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 131.9 on 13615 degrees of freedom
## Multiple R-squared:  0.1154, Adjusted R-squared:  0.1134 
## F-statistic: 57.31 on 31 and 13615 DF,  p-value: < 2.2e-16
```

By adding in a second variable, the model moves from being a simple bivariate model to a *multiple linear regression model*. Which means we see the *unique effect* of our variable of interest `room_type`, because we are now controlling for `property_type`.

We can now add this element to our template for interpretation:

1.  **Basic interpretation (Bivariate)**: For every one-unit increase in x, y changes by \[the coefficient\] on average.

2.  **Controlling for (Multiple)**: Regardless of the other independent variable(s) (or controlling for them).

This means we can isolate the unique effect of our independent variable of interest.

**Interpretation:** Using the template above, we can then say that:

2.  **Controlling for (Multiple)**: *regardless of* whether the listing is a windmill or boutique hotel, a boat or an apartment (i.e. controlling for `property_type`)…

<!-- -->

1.  **Basic interpretation: …** a Private Room is going to cost \$89.65 less (-89.650) than an entire home or apartment (the reference category) on average (i.e. not for every single individual observation of Private Room in the dataset).

Having done so, we want to compare Model 1 and Model 2.

**Firstly,** we want to compare:

*Coefficients:*

- The statistical significance of the coefficients (p-values)

- The sign of the coefficients (negative or positive)

- The magnitude of the coefficients (the actual number)

- Are the coefficient values/signs reasonable?

*Explanatory Power:*

- The R2 and adjusted R2 value.

*Improved model fit (less error or improved predictive power):*

- The standard error (see Fogarty reading): is it going down?

*Dropped Observations:*

- Were any observations deleted due to missingness?

**And then secondly**, we want to understand what *this* model (compared to the previous) has added or accomplished i.e. what have we controlled for?

Specifically, we want to understand if our independent variable of interest has changed: have the coefficients gone up/down or changed sign? We said that a simple bivariate regression model will most likely have omitted variable bias: as we conceptually control for other likely factors (Types/Rooms/Reviews as here or Demographics/Jobs/Firms/Regions as in Assignment 2), then we increasingly isolate the unique effect of our variable of interest. In doing so, the coefficient is likely to change. What did we control *for* then and how is *that* related to change in the coefficient?

We want to do this here as well. The Airbnb dataset is a bit messy and we have not chosen our control variables ourselves (the variables have been chosen for us) so this is more difficult. I give an example from Assignment 2, therefore: after building **Model 3** and controlling for *Job Characteristics*, the Gender coefficient (the variable of interest) changes from -22% to -11% (it’s a percentage change because the dependent variable has been log transformed). Here is the explanation for the reduction:

*In Model 3 we introduce characteristics of the job. Part-time and non-permanent positions seem to have lower hourly wages. There is no statistically significant association with wages. As expected, more senior positions tend to have higher wages. We also note that in this model, the estimated wage gap is smaller. This is probably due to the fact that women are more likely to occupy part-time positions (which have lower wages) and they are less likely to occupy the most senior positions. (Assignment 2 example)*

You would want to take a similar approach. It would also be useful to interpret the individual control coefficients added (i.e. rather than just interpreting the whole chunk/group of variables that you added to the new model).

<span id="the-intercept"></span>

#### 8.3.0.1 The intercept

Note now, at this point, the intercept has changed meaning: x = 0 now means that it is the average price for *both* reference categories: for an `Entire home/apt` (`room_type` reference category) and an `Aparthotel` (`property_type` reference category). I’m not even sure that makes substantive sense. But, in other words, it represents x = 0 for every new independent variable we enter into our model.

By the time of our final model, we will have entered in six independent variables: `room_type`, `property_type`, `bathrooms`, `bedrooms`, `accommodates` and `review-scores_rating`. The intercept will represent where x = 0 for all of them i.e. or an `Entire home/apt` (`room_type` reference category) and an `Aparthotel` (`property_type` reference category) with zero bathrooms, zero bedrooms, zero accommodates and a zero review score. So again, you can see even more clearly that the intercept often does not make any substantive sense and is more of a mathematically necessary part of generating the linear model.

<span id="changing-property_type"></span>

#### 8.3.0.2 Changing `property_type`

“Aparthotel” doesn’t make intuitive sense to me so I will specify the reference category as “Apartment” so I can interpret the differences easier.

``` r
# refactor reference level: recode to 'Apartment' for ease of interpretation

listings$property_type <- relevel(listings$property_type, ref = "Apartment") 

# Build model 2 again and then pass to summary function
m2 <- listings %>%
  lm(price ~ room_type + property_type,
     data = .) 

m2 %>%  summary()
```

``` text
## 
## Call:
## lm(formula = price ~ room_type + property_type, data = .)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -425.00  -58.47  -20.39    9.36  949.36 
## 
## Coefficients:
##                                     Estimate Std. Error t value Pr(>|t|)    
## (Intercept)                         140.2882     1.4723  95.282  < 2e-16 ***
## room_typePrivate room               -89.6499     2.4578 -36.476  < 2e-16 ***
## room_typeShared room                -54.2214    20.4619  -2.650  0.00806 ** 
## property_typeAparthotel              52.2506    44.0239   1.187  0.23530    
## property_typeBarn                   -15.2882    93.2933  -0.164  0.86983    
## property_typeBed and breakfast       31.3466    12.0817   2.595  0.00948 ** 
## property_typeBoat                   434.7118    93.2933   4.660 3.20e-06 ***
## property_typeBoutique hotel         247.7349    14.5440  17.033  < 2e-16 ***
## property_typeBungalow                 4.9214    13.4165   0.367  0.71376    
## property_typeCabin                  -30.7382    76.1745  -0.404  0.68657    
## property_typeCamper/RV              -54.5698    30.2974  -1.801  0.07170 .  
## property_typeCampsite               -54.2882   131.9284  -0.411  0.68071    
## property_typeCasa particular (Cuba)  -0.6383    93.3055  -0.007  0.99454    
## property_typeChalet                 -65.2882   131.9284  -0.495  0.62070    
## property_typeCondominium              7.7092     8.4542   0.912  0.36185    
## property_typeCottage                 -5.4646    18.1654  -0.301  0.76355    
## property_typeEarth house            -11.2882   131.9284  -0.086  0.93182    
## property_typeFarm stay              -70.2882   131.9284  -0.533  0.59420    
## property_typeGuest suite            -38.1490    18.5155  -2.060  0.03938 *  
## property_typeGuesthouse              49.8824    19.5070   2.557  0.01056 *  
## property_typeHostel                 254.6956    21.0525  12.098  < 2e-16 ***
## property_typeHotel                   43.5284    53.8975   0.808  0.41933    
## property_typeHouse                   18.1827     3.9470   4.607 4.13e-06 ***
## property_typeHut                    -20.6383   131.9370  -0.156  0.87570    
## property_typeLoft                   -10.4339    22.3367  -0.467  0.64042    
## property_typeOther                   -7.8652    36.6270  -0.215  0.82998    
## property_typeServiced apartment      64.2218    11.8755   5.408 6.48e-08 ***
## property_typeTent                     6.9718    59.0103   0.118  0.90595    
## property_typeTiny house             -28.7382    76.1745  -0.377  0.70598    
## property_typeTownhouse               19.7540     7.5228   2.626  0.00865 ** 
## property_typeVilla                   46.8992    23.3670   2.007  0.04476 *  
## property_typeWindmill               -20.2882   131.9284  -0.154  0.87778    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 131.9 on 13615 degrees of freedom
## Multiple R-squared:  0.1154, Adjusted R-squared:  0.1134 
## F-statistic: 57.31 on 31 and 13615 DF,  p-value: < 2.2e-16
```

We’re now interpreting `property_type` in relation to “Apartment”.

Next, do we want to collapse factor levels for `property_type`? I’ll attempt to reduce them down and see if it’s any better:

``` r
listings <- listings %>% 
  mutate(property_type = fct_collapse(property_type,
                                      bespoke = c("Aparthotel", "Barn", "Boat", "Casa particular (Cuba)", "Earth house", "Hut", "Loft", "Tiny house", "Windmill", "Other" ),
                                      apartment = c("Apartment", "Bed and breakfast", "Guest suite", "Serviced apartment", "Chalet", "Condominium"),
                                      house = c("Bungalow", "Cottage", "Guesthouse", "House", "Townhouse", "Villa"),
                                      hotel = c("Boutique hotel", "Hotel"),
                                      rustic = c("Cabin", "Camper/RV", "Campsite", "Farm stay", "Hostel", "Tent")
                                       )
      )

# check
fct_count(listings$property_type)
```

``` text
## # A tibble: 5 × 2
##   f             n
##   <fct>     <int>
## 1 apartment 11554
## 2 bespoke      69
## 3 hotel        90
## 4 house      1840
## 5 rustic       94
```

It’s mainly apartments, which makes me feel better about the reference category. However, some of the observations in each category are still very low (\<100), which makes me uneasy. Perhaps I should just analyse apartments in my model? Or add houses and hotels together (House/Hotel) along with apartments and drop the rest? I’ll leave it for now…

We’ll now re-run the model:

``` r
m2 <- listings %>%
  lm(price ~ room_type + property_type,
     data = .) 

m2 %>%  summary()
```

``` text
## 
## Call:
## lm(formula = price ~ room_type + property_type, data = .)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -278.02  -58.72  -20.72    7.53  947.53 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)            140.719      1.455  96.720  < 2e-16 ***
## room_typePrivate room  -88.249      2.437 -36.206  < 2e-16 ***
## room_typeShared room    23.806     18.750   1.270    0.204    
## property_typebespoke     9.154     16.015   0.572    0.568    
## property_typehotel     232.305     14.129  16.442  < 2e-16 ***
## property_typehouse      16.868      3.404   4.956 7.29e-07 ***
## property_typerustic    127.488     16.066   7.935 2.26e-15 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 132.6 on 13640 degrees of freedom
## Multiple R-squared:  0.1044, Adjusted R-squared:  0.104 
## F-statistic:   265 on 6 and 13640 DF,  p-value: < 2.2e-16
```

We’re comparing the new categories in relation to the new reference, “apartment” (which includes Condominiums and other options I’ve grouped under this category).

They’re all significant except for the `bespoke` level, which is just a catch-all category for a wide variety of niche options. Obviously, a bit too wide and not really explaining much.

The coefficients still don’t make much sense: why would `rustic` (tents, campervans) be £127 (or dollars) more than an apartment (holding the other variables constant)? I’m still unsure of`'property_type` therefore, even having reduced it down.

We’ve now built our models covering TYPE; we can move on to the ROOMS set of variables now.

<span id="model-3-rooms"></span>

## 8.4 Model 3: Rooms

For Model 3, we entered in the *Rooms* variables

``` r
# model 3
m3 <- listings %>%
  lm(price ~ room_type + property_type + bathrooms + bedrooms + accommodates,
     data = .) 

m3 %>%
  summary()
```

``` text
## 
## Call:
## lm(formula = price ~ room_type + property_type + bathrooms + 
##     bedrooms + accommodates, data = .)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -328.59  -46.71  -17.41    5.63  976.63 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)             25.109      3.682   6.820 9.52e-12 ***
## room_typePrivate room  -39.955      2.819 -14.174  < 2e-16 ***
## room_typeShared room    67.276     18.028   3.732 0.000191 ***
## property_typebespoke    17.141     15.351   1.117 0.264180    
## property_typehotel     215.208     13.555  15.877  < 2e-16 ***
## property_typehouse      -1.125      3.315  -0.339 0.734421    
## property_typerustic    144.583     15.469   9.347  < 2e-16 ***
## bathrooms               30.036      2.628  11.427  < 2e-16 ***
## bedrooms                12.540      2.303   5.444 5.30e-08 ***
## accommodates            12.340      1.040  11.864  < 2e-16 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 127.1 on 13637 degrees of freedom
## Multiple R-squared:  0.1776, Adjusted R-squared:  0.1771 
## F-statistic: 327.2 on 9 and 13637 DF,  p-value: < 2.2e-16
```

And at this point, to see things more clearly, I will use the `texreg` package. Note this is the one also used in the assignment example.

You will need to install this in the console first. Do *not* install this in your RMarkdown document.

Please note the arguments in the curly brackets: especially, `results = "asis"`

``` r
library(texreg)

m3 <- listings  %>%  lm(price ~ room_type + property_type + bathrooms +
bedrooms, data = .)

htmlreg(list(m1, m2, m3))
```

*Statistical models*

|   | Model 1 | Model 2 | Model 3 |
|----|----|----|----|
| (Intercept) | 142.58<sup>\*\*\*</sup> | 140.72<sup>\*\*\*</sup> | 37.45<sup>\*\*\*</sup> |
|   | (1.44) | (1.45) | (3.55) |
| room_typePrivate room | -81.35<sup>\*\*\*</sup> | -88.25<sup>\*\*\*</sup> | -51.03<sup>\*\*\*</sup> |
|   | (2.40) | (2.44) | (2.67) |
| room_typeShared room | 100.77<sup>\*\*\*</sup> | 23.81 | 54.57<sup>\*\*</sup> |
|   | (16.23) | (18.75) | (18.09) |
| property_typebespoke |   | 9.15 | 17.66 |
|   |   | (16.01) | (15.43) |
| property_typehotel |   | 232.31<sup>\*\*\*</sup> | 221.19<sup>\*\*\*</sup> |
|   |   | (14.13) | (13.61) |
| property_typehouse |   | 16.87<sup>\*\*\*</sup> | -2.07 |
|   |   | (3.40) | (3.33) |
| property_typerustic |   | 127.49<sup>\*\*\*</sup> | 154.64<sup>\*\*\*</sup> |
|   |   | (16.07) | (15.52) |
| bathrooms |   |   | 33.49<sup>\*\*\*</sup> |
|   |   |   | (2.63) |
| bedrooms |   |   | 32.36<sup>\*\*\*</sup> |
|   |   |   | (1.59) |
| R<sup>2</sup> | 0.08 | 0.10 | 0.17 |
| Adj. R<sup>2</sup> | 0.08 | 0.10 | 0.17 |
| Num. obs. | 13647 | 13647 | 13647 |

\*\*\*p \< 0.001; \*\*p \< 0.01; \*p \< 0.05

I have used `echo=TRUE` to show *you* the code: you will not need this code in your report however. We just want to see the output (i.e. teh regression table) so you will need to switch this to: `echo=FALSE`

Now at this point I can implement our interpretation strategy (see Slides in Tutorial 8):

- **Step 1:** Interpret the Model (<u>within</u> the model) using the key questions from the lecture (i.e. coefficients, p-values, R squared etc.)

- **Step 2:** Interpret the Model in relation to the other Models (<u>*between*</u> *the Models*) i.e. in relation to the **Key DV-IV pair.**

So we can now see more clearly and track the changes in **Step 2.**

I had also said that we are still thinking about our data and variables in the model at this stage. Decisions:

1.  Is `Shared rooms` worth removing? Not because it’s not significant, but because it seems quite different: check our visualizations in Tutorial 3. It’s changed signs and coefficient values and appears very volatile.

2.  Is `property type` explaining much more than `room_type`? Is it adding any explanatory value? Perhaps. However, it still seems untrustworthy even after reducing down its levels: why are the coefficients for `House` and `Bespoke` not significant, for example?

So overall the TYPE set of independent factor variables seems more problematic than the ROOMS set (all numeric), which are far better behaved.

Finally, we’ll add the `review_scores_rating` to end with a full model.

Because we did prior exploratory data analysis (a scatterplot in Lab Tutorial 4), and did a correlation between price and `review_scores_rating` (in Lab Tutorial 6), we know this is likely to be counter-intuitive and likely to be a negative coefficient.

<span id="model-4-reviews"></span>

## 8.5 Model 4: Reviews

``` r
m4 <- listings %>% lm(price ~ room_type + property_type + bathrooms +
bedrooms + accommodates + review_scores_rating, data = .)

m4 %>% summary()
```

``` text
## 
## Call:
## lm(formula = price ~ room_type + property_type + bathrooms + 
##     bedrooms + accommodates + review_scores_rating, data = .)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -398.27  -41.83  -15.22    6.67  954.16 
## 
## Coefficients:
##                       Estimate Std. Error t value Pr(>|t|)    
## (Intercept)           109.8501    16.2158   6.774 1.31e-11 ***
## room_typePrivate room -35.9985     2.9242 -12.311  < 2e-16 ***
## room_typeShared room  138.5323    21.8592   6.337 2.43e-10 ***
## property_typebespoke   24.2471    14.8843   1.629 0.103333    
## property_typehotel    109.3190    34.0543   3.210 0.001330 ** 
## property_typehouse     -2.4539     3.4825  -0.705 0.481053    
## property_typerustic   144.4182    17.8032   8.112 5.51e-16 ***
## bathrooms              30.5470     2.7281  11.197  < 2e-16 ***
## bedrooms                8.2506     2.4039   3.432 0.000601 ***
## accommodates           12.9940     1.0748  12.090  < 2e-16 ***
## review_scores_rating   -0.9379     0.1651  -5.682 1.37e-08 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 117.7 on 11125 degrees of freedom
##   (2511 observations deleted due to missingness)
## Multiple R-squared:  0.182,  Adjusted R-squared:  0.1813 
## F-statistic: 247.5 on 10 and 11125 DF,  p-value: < 2.2e-16
```

Ending with our final model, `review_scores_rating` is indeed a negative coefficient: for every unit increase in `review_scores_rating` (i.e. for every additional point in the review from 1-100), `price` goes down by 0.9379 or nearly £1 (or dollar rather). Also, due to the missing values in this variable, our model has now dropped 2,511 observations. So we always need to keep an eye on this.

Again, we would go through the stages of interpretation as outlined above.

<span id="summary-of-our-models"></span>

## 8.6 Summary of our models

We created a **model building strategy** so we knew what we were were controlling for: that is, our *Rival our Alternative Explanations*. And therefore how many models to build:

1.  *Research Question:* My baseline bivariate model (`room_type`)

2.  *Property characteristics:* Add in the other Type variable (`property_type`)

3.  *Hedonic Influences:* Add in the Rooms variables (`bathrooms`, `bedrooms`, `accommodates`)

4.  *Quality:* Add in Reviews (`review_scores_rating`)

Each time, we were not adding in more control variables randomly, but achieving something conceptually and substantively by controlling for another concept (*Property characteristics*/*Hedonic Influences*/*Quality* or, as in the course example, *Demographics/Jobs/Industry/Regions*).

We then had an **interpretation strategy** which both helped us interpret our models but also how they *related to our Research Question*: since this is *the whole point* of building a model in the first place:

- **Step 1:** Interpret the Model (<u>within</u> the model) using the key questions from the lecture (i.e. coefficients, p-values, R squared etc.)

- **Step 2:** Interpret the Model in relation to the other Models (<u>*between*</u> *the Models*) i.e. in relation to the **Key DV-IV pair.**

I’ll use the `texreg` package again to summarise our four models:

``` r
htmlreg(list(m1, m2, m3, m4))
```

*Statistical models*

|   | Model 1 | Model 2 | Model 3 | Model 4 |
|----|----|----|----|----|
| (Intercept) | 142.58<sup>\*\*\*</sup> | 140.72<sup>\*\*\*</sup> | 37.45<sup>\*\*\*</sup> | 109.85<sup>\*\*\*</sup> |
|   | (1.44) | (1.45) | (3.55) | (16.22) |
| room_typePrivate room | -81.35<sup>\*\*\*</sup> | -88.25<sup>\*\*\*</sup> | -51.03<sup>\*\*\*</sup> | -36.00<sup>\*\*\*</sup> |
|   | (2.40) | (2.44) | (2.67) | (2.92) |
| room_typeShared room | 100.77<sup>\*\*\*</sup> | 23.81 | 54.57<sup>\*\*</sup> | 138.53<sup>\*\*\*</sup> |
|   | (16.23) | (18.75) | (18.09) | (21.86) |
| property_typebespoke |   | 9.15 | 17.66 | 24.25 |
|   |   | (16.01) | (15.43) | (14.88) |
| property_typehotel |   | 232.31<sup>\*\*\*</sup> | 221.19<sup>\*\*\*</sup> | 109.32<sup>\*\*</sup> |
|   |   | (14.13) | (13.61) | (34.05) |
| property_typehouse |   | 16.87<sup>\*\*\*</sup> | -2.07 | -2.45 |
|   |   | (3.40) | (3.33) | (3.48) |
| property_typerustic |   | 127.49<sup>\*\*\*</sup> | 154.64<sup>\*\*\*</sup> | 144.42<sup>\*\*\*</sup> |
|   |   | (16.07) | (15.52) | (17.80) |
| bathrooms |   |   | 33.49<sup>\*\*\*</sup> | 30.55<sup>\*\*\*</sup> |
|   |   |   | (2.63) | (2.73) |
| bedrooms |   |   | 32.36<sup>\*\*\*</sup> | 8.25<sup>\*\*\*</sup> |
|   |   |   | (1.59) | (2.40) |
| accommodates |   |   |   | 12.99<sup>\*\*\*</sup> |
|   |   |   |   | (1.07) |
| review_scores_rating |   |   |   | -0.94<sup>\*\*\*</sup> |
|   |   |   |   | (0.17) |
| R<sup>2</sup> | 0.08 | 0.10 | 0.17 | 0.18 |
| Adj. R<sup>2</sup> | 0.08 | 0.10 | 0.17 | 0.18 |
| Num. obs. | 13647 | 13647 | 13647 | 11136 |

\*\*\*p \< 0.001; \*\*p \< 0.01; \*p \< 0.05

And finally, I’ll tidy it up a little. You can look at the help in R or online to see more on the the additional arguments:

``` r
htmlreg(list(m1, m2, m3, m4),
          stars = 0.05,
          digits = 2, 
          caption = "Table 2: Regression results. Dependent variable: Price",
          caption.above = TRUE,
          groups = list("Room Type" = 2:3, "Property Type" = 4:7)
        )
```

*Table 2: Regression results. Dependent variable: Price*

|   | Model 1 | Model 2 | Model 3 | Model 4 |
|----|----|----|----|----|
| (Intercept) | 142.58<sup>\*</sup> | 140.72<sup>\*</sup> | 37.45<sup>\*</sup> | 109.85<sup>\*</sup> |
|   | (1.44) | (1.45) | (3.55) | (16.22) |
| Room Type |   |   |   |   |
|   |   |   |   |   |
|      room_typePrivate room | -81.35<sup>\*</sup> | -88.25<sup>\*</sup> | -51.03<sup>\*</sup> | -36.00<sup>\*</sup> |
|   | (2.40) | (2.44) | (2.67) | (2.92) |
|      room_typeShared room | 100.77<sup>\*</sup> | 23.81 | 54.57<sup>\*</sup> | 138.53<sup>\*</sup> |
|   | (16.23) | (18.75) | (18.09) | (21.86) |
| Property Type |   |   |   |   |
|   |   |   |   |   |
|      property_typebespoke |   | 9.15 | 17.66 | 24.25 |
|   |   | (16.01) | (15.43) | (14.88) |
|      property_typehotel |   | 232.31<sup>\*</sup> | 221.19<sup>\*</sup> | 109.32<sup>\*</sup> |
|   |   | (14.13) | (13.61) | (34.05) |
|      property_typehouse |   | 16.87<sup>\*</sup> | -2.07 | -2.45 |
|   |   | (3.40) | (3.33) | (3.48) |
|      property_typerustic |   | 127.49<sup>\*</sup> | 154.64<sup>\*</sup> | 144.42<sup>\*</sup> |
|   |   | (16.07) | (15.52) | (17.80) |
| bathrooms |   |   | 33.49<sup>\*</sup> | 30.55<sup>\*</sup> |
|   |   |   | (2.63) | (2.73) |
| bedrooms |   |   | 32.36<sup>\*</sup> | 8.25<sup>\*</sup> |
|   |   |   | (1.59) | (2.40) |
| accommodates |   |   |   | 12.99<sup>\*</sup> |
|   |   |   |   | (1.07) |
| review_scores_rating |   |   |   | -0.94<sup>\*</sup> |
|   |   |   |   | (0.17) |
| R<sup>2</sup> | 0.08 | 0.10 | 0.17 | 0.18 |
| Adj. R<sup>2</sup> | 0.08 | 0.10 | 0.17 | 0.18 |
| Num. obs. | 13647 | 13647 | 13647 | 11136 |

\*p \< 0.05

One thing I might want to do is clean up and tidy my variable names e.g. `property_typebespoke`, `review_scores_rating` etc. But I’ll leave that as an exercise.

We can now see all our models together. In Model 1 we started off with the simple bivariate model using `room_type`. We added the other type variable (`property_type`) in Model 2 and made some adjustments (to reference category and no. of levels in property_type). That concluded the TYPE variables and we saw they were somewhat problematic (e.g. `shared room`).

In Model 3, we added in the ROOM variables and saw that they were better behaved.

Finally in Model 4, we had the full model. We added in review_scores_rating. As discussed in the Tutorial, we might want to think more about whether this is measuring what we think it is (i.e. quality).

So before we proceed on to diagnostic testing, we already have a lot of information gained through (a) our prior exploratory data work in previous tutorials and (b) our process of model building. And at this point, there might be some decisions we could make (drop Shared Rooms?).

<span id="final-summary"></span>

## 8.7 Final Summary

Once we have our final model and *after we have tested it (Tutorials 9-10)*, we would return to our research question and use it to answer our question:

*“The price of an Airbnb listing can be predicted primarily by the type of room (room_type), even when controlling for other characteristics like number of rooms, review scores and even property type.”*

I would probably need to qualify this answer by saying that Room Type alone was a good predictor of price but not sufficient in itself: Rooms (bathrooms, bedrooms etc.) is also necessary. As discussed in the Tutorial, ideally this process would proceed with a substantive research question (and derived hypotheses) informed by prior literature. We’ve tried to simulate this process as best as we could, however.

**In doing so, the main elements you should take away are:**

1.  The difference between simple linear regression (bivariate) and multiple linear regression (multivariable). The value of multiple linear regression is statistically it ‘partials out’ the influence of other variables on our dependent variable. We can then isolate the unique effect of our variable of interest (our key independent variable)

2.  How our inferential test *is* our simple linear regression

3.  Why we need to proceed from our inferential test/simple linear regression onto multiple linear regression *by adding control variables*.

4.  *A model building strategy:* thinking through what conceptually we need to control for

5.  *An interpretation strategy:* interpreting each additional model in itself but also *in relation to our Research Question* - in other words, the **DV-IV pair** or inferential test/simple linear regression we started off with i.e. our baseline model. We can track the ‘story’ of this as it progresses through each subsequent model. By the time we reach our final model, we have a much fuller story with which to answer our Research Question.

[7 Tutorial 6: Inference - ANOVA and Correlation](https://qdaworkbook.netlify.app/tutorial-6-inference---anova-and-correlation) [9 Tutorial 8: Diagnostics I](https://qdaworkbook.netlify.app/tutorial-8-diagnostics-i)
