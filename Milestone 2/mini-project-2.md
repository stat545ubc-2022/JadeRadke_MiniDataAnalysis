Mini Data Analysis Milestone 2
================

*To complete this milestone, you can edit [this `.rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are commented out with
`<!--- start your work here--->`. When you are done, make sure to knit
to an `.md` file by changing the output in the YAML header to
`github_document`, before submitting a tagged release on canvas.*

# Welcome to your second (and last) milestone in your mini data analysis project!

In Milestone 1, you explored your data, came up with research questions,
and obtained some results by making summary tables and graphs. This
time, we will first explore more in depth the concept of *tidy data.*
Then, you’ll be sharpening some of the results you obtained from your
previous milestone by:

- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

# Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-2.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 55 points (compared to the 45 points
of the Milestone 1): 45 for your analysis, and 10 for your entire
mini-analysis GitHub repository. Details follow.

**Research Questions**: In Milestone 1, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Learning Objectives

By the end of this milestone, you should:

- Understand what *tidy* data is, and how to create it using `tidyr`.
- Generate a reproducible and clear report using R Markdown.
- Manipulating special data types in R: factors and/or dates and times.
- Fitting a model object to your data, and extract a result.
- Reading and writing data as separate files.

# Setup

Begin by loading your data and the tidyverse package below:

``` r
library(datateachr) # <- might contain the data you picked!
library(tidyverse)
```

# Task 1: Tidy your data (15 points)

In this task, we will do several exercises to reshape our data. The goal
here is to understand how to do this reshaping with the `tidyr` package.

A reminder of the definition of *tidy* data:

- Each row is an **observation**
- Each column is a **variable**
- Each cell is a **value**

*Tidy’ing* data is sometimes necessary because it can simplify
computation. Other times it can be nice to organize data so that it can
be easier to understand when read manually.

### 2.1 (2.5 points)

Based on the definition above, can you identify if your data is tidy or
untidy? Go through all your columns, or if you have \>8 variables, just
pick 8, and explain whether the data is untidy or tidy.

<!--------------------------- Start your work below --------------------------->

``` r
steam_games
```

    ## # A tibble: 40,833 × 21
    ##       id url         types name  desc_…¹ recen…² all_r…³ relea…⁴ devel…⁵ publi…⁶
    ##    <dbl> <chr>       <chr> <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://st… app   DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ##  2     2 https://st… app   PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ##  3     3 https://st… app   BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado…
    ##  4     4 https://st… app   DayZ  The po… Mixed,… Mixed,… Dec 13… Bohemi… Bohemi…
    ##  5     5 https://st… app   EVE … EVE On… Mixed,… Mostly… May 6,… CCP     CCP,CCP
    ##  6     6 https://st… bund… Gran… Grand … NaN     NaN     NaN     Rockst… Rockst…
    ##  7     7 https://st… app   Devi… The ul… Very P… Very P… Mar 7,… CAPCOM… CAPCOM…
    ##  8     8 https://st… app   Huma… Human:… Very P… Very P… Jul 22… No Bra… Curve …
    ##  9     9 https://st… app   They… They A… Very P… Very P… Dec 12… Numant… Numant…
    ## 10    10 https://st… app   Warh… In a w… <NA>    Mixed,… May 31… Eko So… Bigben…
    ## # … with 40,823 more rows, 11 more variables: popular_tags <chr>,
    ## #   game_details <chr>, languages <chr>, achievements <dbl>, genre <chr>,
    ## #   game_description <chr>, mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, discount_price <dbl>,
    ## #   and abbreviated variable names ¹​desc_snippet, ²​recent_reviews,
    ## #   ³​all_reviews, ⁴​release_date, ⁵​developer, ⁶​publisher

``` r
#The data appears to be tidy according to the definition provided above. Each row is an observation, each column is a variable, and each cell is a value. For example, the variables that are listed in the columns include id, types, name, recent_reviews, all_reviews, publisher, languages, achievements, genre, and more similar variables. The rows contain observations for each variable, and each cell is a value. 
```

<!----------------------------------------------------------------------------->

### 2.2 (5 points)

Now, if your data is tidy, untidy it! Then, tidy it back to it’s
original state.

If your data is untidy, then tidy it! Then, untidy it back to it’s
original state.

Be sure to explain your reasoning for this task. Show us the “before”
and “after”.

<!--------------------------- Start your work below --------------------------->

``` r
#Before 
steam_games
```

    ## # A tibble: 40,833 × 21
    ##       id url         types name  desc_…¹ recen…² all_r…³ relea…⁴ devel…⁵ publi…⁶
    ##    <dbl> <chr>       <chr> <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://st… app   DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ##  2     2 https://st… app   PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ##  3     3 https://st… app   BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado…
    ##  4     4 https://st… app   DayZ  The po… Mixed,… Mixed,… Dec 13… Bohemi… Bohemi…
    ##  5     5 https://st… app   EVE … EVE On… Mixed,… Mostly… May 6,… CCP     CCP,CCP
    ##  6     6 https://st… bund… Gran… Grand … NaN     NaN     NaN     Rockst… Rockst…
    ##  7     7 https://st… app   Devi… The ul… Very P… Very P… Mar 7,… CAPCOM… CAPCOM…
    ##  8     8 https://st… app   Huma… Human:… Very P… Very P… Jul 22… No Bra… Curve …
    ##  9     9 https://st… app   They… They A… Very P… Very P… Dec 12… Numant… Numant…
    ## 10    10 https://st… app   Warh… In a w… <NA>    Mixed,… May 31… Eko So… Bigben…
    ## # … with 40,823 more rows, 11 more variables: popular_tags <chr>,
    ## #   game_details <chr>, languages <chr>, achievements <dbl>, genre <chr>,
    ## #   game_description <chr>, mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, discount_price <dbl>,
    ## #   and abbreviated variable names ¹​desc_snippet, ²​recent_reviews,
    ## #   ³​all_reviews, ⁴​release_date, ⁵​developer, ⁶​publisher

``` r
#Untidying process
pivot_wider(steam_games, names_from = types, values_from = original_price)
```

    ## # A tibble: 40,833 × 23
    ##       id url       name  desc_…¹ recen…² all_r…³ relea…⁴ devel…⁵ publi…⁶ popul…⁷
    ##    <dbl> <chr>     <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://… DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes… FPS,Go…
    ##  2     2 https://… PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C… Surviv…
    ##  3     3 https://… BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado… Mechs,…
    ##  4     4 https://… DayZ  The po… Mixed,… Mixed,… Dec 13… Bohemi… Bohemi… Surviv…
    ##  5     5 https://… EVE … EVE On… Mixed,… Mostly… May 6,… CCP     CCP,CCP Space,…
    ##  6     6 https://… Gran… Grand … NaN     NaN     NaN     Rockst… Rockst… NaN    
    ##  7     7 https://… Devi… The ul… Very P… Very P… Mar 7,… CAPCOM… CAPCOM… Action…
    ##  8     8 https://… Huma… Human:… Very P… Very P… Jul 22… No Bra… Curve … Funny,…
    ##  9     9 https://… They… They A… Very P… Very P… Dec 12… Numant… Numant… Early …
    ## 10    10 https://… Warh… In a w… <NA>    Mixed,… May 31… Eko So… Bigben… RPG,Ad…
    ## # … with 40,823 more rows, 13 more variables: game_details <chr>,
    ## #   languages <chr>, achievements <dbl>, genre <chr>, game_description <chr>,
    ## #   mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, discount_price <dbl>, app <dbl>,
    ## #   bundle <dbl>, sub <dbl>, `NA` <dbl>, and abbreviated variable names
    ## #   ¹​desc_snippet, ²​recent_reviews, ³​all_reviews, ⁴​release_date, ⁵​developer,
    ## #   ⁶​publisher, ⁷​popular_tags

``` r
pivot_wider(steam_games, names_from = types, values_from = discount_price)
```

    ## # A tibble: 40,833 × 23
    ##       id url       name  desc_…¹ recen…² all_r…³ relea…⁴ devel…⁵ publi…⁶ popul…⁷
    ##    <dbl> <chr>     <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://… DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes… FPS,Go…
    ##  2     2 https://… PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C… Surviv…
    ##  3     3 https://… BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado… Mechs,…
    ##  4     4 https://… DayZ  The po… Mixed,… Mixed,… Dec 13… Bohemi… Bohemi… Surviv…
    ##  5     5 https://… EVE … EVE On… Mixed,… Mostly… May 6,… CCP     CCP,CCP Space,…
    ##  6     6 https://… Gran… Grand … NaN     NaN     NaN     Rockst… Rockst… NaN    
    ##  7     7 https://… Devi… The ul… Very P… Very P… Mar 7,… CAPCOM… CAPCOM… Action…
    ##  8     8 https://… Huma… Human:… Very P… Very P… Jul 22… No Bra… Curve … Funny,…
    ##  9     9 https://… They… They A… Very P… Very P… Dec 12… Numant… Numant… Early …
    ## 10    10 https://… Warh… In a w… <NA>    Mixed,… May 31… Eko So… Bigben… RPG,Ad…
    ## # … with 40,823 more rows, 13 more variables: game_details <chr>,
    ## #   languages <chr>, achievements <dbl>, genre <chr>, game_description <chr>,
    ## #   mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, app <dbl>,
    ## #   bundle <dbl>, sub <dbl>, `NA` <dbl>, and abbreviated variable names
    ## #   ¹​desc_snippet, ²​recent_reviews, ³​all_reviews, ⁴​release_date, ⁵​developer,
    ## #   ⁶​publisher, ⁷​popular_tags

``` r
pivot_longer(steam_games, cols=c(recent_reviews, all_reviews),
             names_to = "review_time",
             values_to = "review")
```

    ## # A tibble: 81,666 × 21
    ##       id url         types name  desc_…¹ relea…² devel…³ publi…⁴ popul…⁵ game_…⁶
    ##    <dbl> <chr>       <chr> <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://st… app   DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single…
    ##  2     1 https://st… app   DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single…
    ##  3     2 https://st… app   PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-…
    ##  4     2 https://st… app   PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-…
    ##  5     3 https://st… app   BATT… Take c… Apr 24… Harebr… Parado… Mechs,… Single…
    ##  6     3 https://st… app   BATT… Take c… Apr 24… Harebr… Parado… Mechs,… Single…
    ##  7     4 https://st… app   DayZ  The po… Dec 13… Bohemi… Bohemi… Surviv… Multi-…
    ##  8     4 https://st… app   DayZ  The po… Dec 13… Bohemi… Bohemi… Surviv… Multi-…
    ##  9     5 https://st… app   EVE … EVE On… May 6,… CCP     CCP,CCP Space,… Multi-…
    ## 10     5 https://st… app   EVE … EVE On… May 6,… CCP     CCP,CCP Space,… Multi-…
    ## # … with 81,656 more rows, 11 more variables: languages <chr>,
    ## #   achievements <dbl>, genre <chr>, game_description <chr>,
    ## #   mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, discount_price <dbl>,
    ## #   review_time <chr>, review <chr>, and abbreviated variable names
    ## #   ¹​desc_snippet, ²​release_date, ³​developer, ⁴​publisher, ⁵​popular_tags,
    ## #   ⁶​game_details

``` r
steam_games_untidy <- all_of(steam_games) %>%
    pivot_longer(cols=c(recent_reviews, all_reviews),
             names_to = "review_time",
             values_to = "review")

sg_untidy <- steam_games_untidy %>%
    pivot_wider(names_from = types, values_from = original_price)

#After (untidy)
sg_untidy
```

    ## # A tibble: 81,666 × 23
    ##       id url       name  desc_…¹ relea…² devel…³ publi…⁴ popul…⁵ game_…⁶ langu…⁷
    ##    <dbl> <chr>     <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  2     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  3     2 https://… PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-… Englis…
    ##  4     2 https://… PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-… Englis…
    ##  5     3 https://… BATT… Take c… Apr 24… Harebr… Parado… Mechs,… Single… Englis…
    ##  6     3 https://… BATT… Take c… Apr 24… Harebr… Parado… Mechs,… Single… Englis…
    ##  7     4 https://… DayZ  The po… Dec 13… Bohemi… Bohemi… Surviv… Multi-… Englis…
    ##  8     4 https://… DayZ  The po… Dec 13… Bohemi… Bohemi… Surviv… Multi-… Englis…
    ##  9     5 https://… EVE … EVE On… May 6,… CCP     CCP,CCP Space,… Multi-… Englis…
    ## 10     5 https://… EVE … EVE On… May 6,… CCP     CCP,CCP Space,… Multi-… Englis…
    ## # … with 81,656 more rows, 13 more variables: achievements <dbl>, genre <chr>,
    ## #   game_description <chr>, mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, discount_price <dbl>, review_time <chr>,
    ## #   review <chr>, app <dbl>, bundle <dbl>, sub <dbl>, `NA` <dbl>, and
    ## #   abbreviated variable names ¹​desc_snippet, ²​release_date, ³​developer,
    ## #   ⁴​publisher, ⁵​popular_tags, ⁶​game_details, ⁷​languages

``` r
#Re-tidying process
pivot_wider(sg_untidy, names_from = review_time, values_from = review)
```

    ## # A tibble: 40,833 × 23
    ##       id url       name  desc_…¹ relea…² devel…³ publi…⁴ popul…⁵ game_…⁶ langu…⁷
    ##    <dbl> <chr>     <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  2     2 https://… PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-… Englis…
    ##  3     3 https://… BATT… Take c… Apr 24… Harebr… Parado… Mechs,… Single… Englis…
    ##  4     4 https://… DayZ  The po… Dec 13… Bohemi… Bohemi… Surviv… Multi-… Englis…
    ##  5     5 https://… EVE … EVE On… May 6,… CCP     CCP,CCP Space,… Multi-… Englis…
    ##  6     6 https://… Gran… Grand … NaN     Rockst… Rockst… NaN     Single… Englis…
    ##  7     7 https://… Devi… The ul… Mar 7,… CAPCOM… CAPCOM… Action… Single… Englis…
    ##  8     8 https://… Huma… Human:… Jul 22… No Bra… Curve … Funny,… Single… Englis…
    ##  9     9 https://… They… They A… Dec 12… Numant… Numant… Early … Single… Englis…
    ## 10    10 https://… Warh… In a w… May 31… Eko So… Bigben… RPG,Ad… Single… Englis…
    ## # … with 40,823 more rows, 13 more variables: achievements <dbl>, genre <chr>,
    ## #   game_description <chr>, mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, discount_price <dbl>, app <dbl>,
    ## #   bundle <dbl>, sub <dbl>, `NA` <dbl>, recent_reviews <chr>,
    ## #   all_reviews <chr>, and abbreviated variable names ¹​desc_snippet,
    ## #   ²​release_date, ³​developer, ⁴​publisher, ⁵​popular_tags, ⁶​game_details,
    ## #   ⁷​languages

``` r
pivot_longer(sg_untidy, cols=c(app, bundle, sub, "NA"),
             names_to = "types",
             values_to = "original_price")
```

    ## # A tibble: 326,664 × 21
    ##       id url       name  desc_…¹ relea…² devel…³ publi…⁴ popul…⁵ game_…⁶ langu…⁷
    ##    <dbl> <chr>     <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  2     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  3     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  4     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  5     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  6     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  7     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  8     1 https://… DOOM  Now in… May 12… id Sof… Bethes… FPS,Go… Single… Englis…
    ##  9     2 https://… PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-… Englis…
    ## 10     2 https://… PLAY… PLAYER… Dec 21… PUBG C… PUBG C… Surviv… Multi-… Englis…
    ## # … with 326,654 more rows, 11 more variables: achievements <dbl>, genre <chr>,
    ## #   game_description <chr>, mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, discount_price <dbl>, review_time <chr>,
    ## #   review <chr>, types <chr>, original_price <dbl>, and abbreviated variable
    ## #   names ¹​desc_snippet, ²​release_date, ³​developer, ⁴​publisher, ⁵​popular_tags,
    ## #   ⁶​game_details, ⁷​languages

``` r
steam_games_tidy <- all_of(sg_untidy) %>%
  pivot_longer(cols=c(app, bundle, sub, "NA"),
             names_to = "types",
             values_to = "original_price")

sg_tidy <- all_of(steam_games_tidy) %>%
  pivot_wider(names_from = review_time, values_from = review)

sg_tidy_order <- select(sg_tidy, id, url, types, name, desc_snippet, recent_reviews, all_reviews, everything(), original_price) %>%
  relocate(discount_price, .after = last_col())

#Tidy version same as original
sg_tidy_order
```

    ## # A tibble: 163,332 × 21
    ##       id url         types name  desc_…¹ recen…² all_r…³ relea…⁴ devel…⁵ publi…⁶
    ##    <dbl> <chr>       <chr> <chr> <chr>   <chr>   <chr>   <chr>   <chr>   <chr>  
    ##  1     1 https://st… app   DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ##  2     1 https://st… bund… DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ##  3     1 https://st… sub   DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ##  4     1 https://st… NA    DOOM  Now in… Very P… Very P… May 12… id Sof… Bethes…
    ##  5     2 https://st… app   PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ##  6     2 https://st… bund… PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ##  7     2 https://st… sub   PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ##  8     2 https://st… NA    PLAY… PLAYER… Mixed,… Mixed,… Dec 21… PUBG C… PUBG C…
    ##  9     3 https://st… app   BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado…
    ## 10     3 https://st… bund… BATT… Take c… Mixed,… Mostly… Apr 24… Harebr… Parado…
    ## # … with 163,322 more rows, 11 more variables: popular_tags <chr>,
    ## #   game_details <chr>, languages <chr>, achievements <dbl>, genre <chr>,
    ## #   game_description <chr>, mature_content <chr>, minimum_requirements <chr>,
    ## #   recommended_requirements <chr>, original_price <dbl>, discount_price <dbl>,
    ## #   and abbreviated variable names ¹​desc_snippet, ²​recent_reviews,
    ## #   ³​all_reviews, ⁴​release_date, ⁵​developer, ⁶​publisher

``` r
#I decided to use pivot_wider and pivot_longer to untidy my data as it was already considered tidy. I used pivot_wider to move the values of types of games into columns as variables and use the original_price values as their values (which is very untidy). I also used the pivot_longer function to combine the variables of recent_reviews and all_reviews to become values under "review_time" and moved their values into a new column titled review. To re-tidy the data I used the same functions to undo all the untidying I previously did, but then the order of the columns was different from the original. So, I decided to use the select and relocate functions to reorder the columns so that they were in the same order as the original data set. 
```

<!----------------------------------------------------------------------------->

### 2.3 (7.5 points)

Now, you should be more familiar with your data, and also have made
progress in answering your research questions. Based on your interest,
and your analyses, pick 2 of the 4 research questions to continue your
analysis in the next four tasks:

<!-------------------------- Start your work below ---------------------------->

1.  Are action games more expensive than racing games?
2.  Is the language of the game related to it’s original price?

<!----------------------------------------------------------------------------->

Explain your decision for choosing the above two research questions.

<!--------------------------- Start your work below --------------------------->

I chose “are action games more expensive than racing games?” because I
am very interested in looking at the prices of games compared to their
genres. Perhaps I can expand this question further to include more
genres going forward.

I chose “is the language of the game related to it’s original price?”
because there is much more exploring that I can do with the data to
answer this question. Now that I have learned that I can separate my
data and create a “primary language” variable and a “secondary language”
variable, I can examine the difference in prices between languages more
accurately.

<!----------------------------------------------------------------------------->

Now, try to choose a version of your data that you think will be
appropriate to answer these 2 questions. Use between 4 and 8 functions
that we’ve covered so far (i.e. by filtering, cleaning, tidy’ing,
dropping irrelevant columns, etc.).

<!--------------------------- Start your work below --------------------------->

``` r
sg_tidy_genre <- steam_games %>%
  separate(genre, into = c("primary_genre", "secondary_genre"), sep = ",")
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 19801 rows [2, 3, 4,
    ## 5, 10, 11, 13, 15, 17, 31, 32, 34, 35, 37, 42, 45, 46, 50, 51, 55, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 8221 rows [1, 7,
    ## 12, 14, 18, 20, 21, 22, 23, 27, 29, 33, 36, 38, 40, 41, 43, 44, 47, 48, ...].

``` r
sg_tidy_languages <- steam_games %>%
  separate(languages, into = c("primary_language", "secondary_language"), sep = ",")
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 16534 rows [1, 2, 3,
    ## 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 16, 18, 19, 20, 21, 23, 24, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 19098 rows [13,
    ## 15, 17, 28, 36, 37, 40, 45, 50, 89, 97, 98, 100, 112, 121, 137, 139, 140, 144,
    ## 156, ...].

``` r
sg_tidy_publisher <- steam_games %>%
  separate(publisher, into = c("publisher"), sep = ",")
```

    ## Warning: Expected 1 pieces. Additional pieces discarded in 33165 rows [1, 2, 3,
    ## 4, 5, 7, 8, 9, 10, 11, 12, 13, 14, 15, 17, 18, 19, 20, 21, 22, ...].

``` r
sg_tidy_allreviews <- steam_games %>%
  separate(all_reviews, into = c("all_reviews"), sep = ",")
```

    ## Warning: Expected 1 pieces. Additional pieces discarded in 28470 rows [1, 2, 3,
    ## 4, 5, 7, 8, 9, 10, 11, 12, 13, 14, 15, 17, 18, 19, 20, 21, 22, ...].

``` r
sg_tidy_recentreviews <- steam_games %>%
  separate(recent_reviews, into = c("recent_reviews"), sep = ",")
```

    ## Warning: Expected 1 pieces. Additional pieces discarded in 2706 rows [1, 2, 3,
    ## 4, 5, 7, 8, 9, 11, 12, 13, 14, 15, 17, 18, 19, 20, 21, 22, 24, ...].

``` r
sg_tidy <- steam_games %>%
  separate(languages, into = c("primary_language", "secondary_language"), sep = ",") %>%
  separate(genre, into = c("primary_genre", "secondary_genre"), sep = ",") %>%
  filter(!is.na(secondary_language)) %>%
  filter(!is.na(original_price)) %>%
  filter(!is.na(primary_genre))
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 16534 rows [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 16, 18, 19, 20, 21, 23, 24, ...].
    ## Expected 2 pieces. Missing pieces filled with `NA` in 19098 rows [13, 15, 17, 28, 36, 37, 40, 45, 50, 89, 97, 98, 100, 112, 121, 137, 139, 140, 144, 156, ...].

    ## Warning: Expected 2 pieces. Additional pieces discarded in 19801 rows [2, 3, 4,
    ## 5, 10, 11, 13, 15, 17, 31, 32, 34, 35, 37, 42, 45, 46, 50, 51, 55, ...].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 8221 rows [1, 7,
    ## 12, 14, 18, 20, 21, 22, 23, 27, 29, 33, 36, 38, 40, 41, 43, 44, 47, 48, ...].

``` r
sg_tidiest = subset(sg_tidy, select = c(primary_language, secondary_language, original_price, discount_price, primary_genre))
```

<!----------------------------------------------------------------------------->

# Task 2: Special Data Types (10)

For this exercise, you’ll be choosing two of the three tasks below –
both tasks that you choose are worth 5 points each.

But first, tasks 1 and 2 below ask you to modify a plot you made in a
previous milestone. The plot you choose should involve plotting across
at least three groups (whether by facetting, or using an aesthetic like
colour). Place this plot below (you’re allowed to modify the plot if
you’d like). If you don’t have such a plot, you’ll need to make one.
Place the code for your plot below.

<!-------------------------- Start your work below ---------------------------->

``` r
sg_tidiest %>%
  filter(primary_genre %in% c("Action", "Racing", "RPG", "Strategy", "Adventure", "Indie", "Free to Play", "Casual")) %>%
  group_by(primary_genre, primary_language) %>%
  summarise(mean = mean(original_price)) %>%
  ggplot() +
  geom_bar(aes(x = primary_genre, y = mean, fill = primary_language),
           stat = "identity") +
          ylab("Average Price ($)") +
          xlab("Genre")
```

    ## `summarise()` has grouped output by 'primary_genre'. You can override using the
    ## `.groups` argument.

![](mini-project-2_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

<!----------------------------------------------------------------------------->

Now, choose two of the following tasks.

1.  Produce a new plot that reorders a factor in your original plot,
    using the `forcats` package (3 points). Then, in a sentence or two,
    briefly explain why you chose this ordering (1 point here for
    demonstrating understanding of the reordering, and 1 point for
    demonstrating some justification for the reordering, which could be
    subtle or speculative.)

2.  Produce a new plot that groups some factor levels together into an
    “other” category (or something similar), using the `forcats` package
    (3 points). Then, in a sentence or two, briefly explain why you
    chose this grouping (1 point here for demonstrating understanding of
    the grouping, and 1 point for demonstrating some justification for
    the grouping, which could be subtle or speculative.)

3.  If your data has some sort of time-based column like a date (but
    something more granular than just a year):

    1.  Make a new column that uses a function from the `lubridate` or
        `tsibble` package to modify your original time-based column. (3
        points)

        - Note that you might first have to *make* a time-based column
          using a function like `ymd()`, but this doesn’t count.
        - Examples of something you might do here: extract the day of
          the year from a date, or extract the weekday, or let 24 hours
          elapse on your dates.

    2.  Then, in a sentence or two, explain how your new column might be
        useful in exploring a research question. (1 point for
        demonstrating understanding of the function you used, and 1
        point for your justification, which could be subtle or
        speculative).

        - For example, you could say something like “Investigating the
          day of the week might be insightful because penguins don’t
          work on weekends, and so may respond differently”.

<!-------------------------- Start your work below ---------------------------->

**Task Number**: 1

``` r
sg_tidiest %>%
  filter(primary_genre %in% c("Action", "Racing", "RPG", "Strategy", "Adventure", "Indie", "Free to Play", "Casual")) %>%
  mutate(primary_genre = fct_relevel(primary_genre, "Casual", "Racing", "Free to Play", "Indie", "Strategy", "RPG", "Action", "Adventure")) %>%
  group_by(primary_genre, primary_language) %>%
  summarise(mean = mean(original_price)) %>%
  ggplot() +
  geom_bar(aes(x = primary_genre, y = mean, fill = primary_language), stat = "identity") +
  ylab("Average Price ($)") +
  xlab("Genre")
```

    ## `summarise()` has grouped output by 'primary_genre'. You can override using the
    ## `.groups` argument.

![](mini-project-2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
#I decided to reorder the genre by the level of the bar so that the cheapest genre of game is at the beginning and the price continues to rise with each genre until the most expensive genre is at the end. This allows us to quickly look at the graph and see that Casual games are the cheapest on average while Adventure games are the most expensive on average. 
```

<!----------------------------------------------------------------------------->
<!-------------------------- Start your work below ---------------------------->

**Task Number**: 2

``` r
sg_tidiest %>%
  group_by(primary_genre, primary_language) %>%
  summarise(mean = mean(original_price)) %>%
  ggplot() +
  geom_bar(aes(x = fct_other(primary_genre, keep = c("Action", "Racing", "RPG", "Strategy", "Adventure", "Indie", "Free to Play", "Casual", "Simulation"), other_level = "Other"), y = mean, fill = primary_language),
           stat = "identity") +
          ylab("Average Price ($)") +
          xlab("Genre")
```

    ## `summarise()` has grouped output by 'primary_genre'. You can override using the
    ## `.groups` argument.

![](mini-project-2_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
#I chose this grouping because I wanted to compare the prices of the more popular/well-known genres of games, and then group the rest of the genres together in an "other" category. There are too many different genres to look at all of the prices individually in a graph. Apparently, some of the more obscure/less frequent genres of games are very expensive! It's also interesting to see that none of the more popular genres are made in Russian, but Russian is included in the Other category. 
```

<!----------------------------------------------------------------------------->

# Task 3: Modelling

## 2.0 (no points)

Pick a research question, and pick a variable of interest (we’ll call it
“Y”) that’s relevant to the research question. Indicate these.

<!-------------------------- Start your work below ---------------------------->

**Research Question**: Are action games more expensive than casual
games?

**Variable of interest**: original_price

<!----------------------------------------------------------------------------->

## 2.1 (5 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

- **Note**: It’s OK if you don’t know how these models/tests work. Here
  are some examples of things you can do here, but the sky’s the limit.

  - You could fit a model that makes predictions on Y using another
    variable, by using the `lm()` function.
  - You could test whether the mean of Y equals 0 using `t.test()`, or
    maybe the mean across two groups are different using `t.test()`, or
    maybe the mean across multiple groups are different using `anova()`
    (you may have to pivot your data for the latter two).
  - You could use `lm()` to test for significance of regression.

<!-------------------------- Start your work below ---------------------------->

``` r
lm_df <- sg_tidiest %>% 
  mutate(genre_dummy = case_when(primary_genre == "Action" ~ 1,
                                 primary_genre == "Casual" ~ 0)) %>% 
  filter(!is.na(genre_dummy))

model <- lm(original_price ~ genre_dummy, data = lm_df)
summary(model)
```

    ## 
    ## Call:
    ## lm(formula = original_price ~ genre_dummy, data = lm_df)
    ## 
    ## Residuals:
    ##    Min     1Q Median     3Q    Max 
    ## -11.48  -8.49  -6.49   0.23 613.26 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)   9.7581     0.4395  22.203  < 2e-16 ***
    ## genre_dummy   1.7195     0.5233   3.286  0.00102 ** 
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 24.67 on 10689 degrees of freedom
    ## Multiple R-squared:  0.001009,   Adjusted R-squared:  0.0009157 
    ## F-statistic:  10.8 on 1 and 10689 DF,  p-value: 0.00102

<!----------------------------------------------------------------------------->

## 2.2 (5 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

- Be sure to indicate in writing what you chose to produce.
- Your code should either output a tibble (in which case you should
  indicate the column that contains the thing you’re looking for), or
  the thing you’re looking for itself.
- Obtain your results using the `broom` package if possible. If your
  model is not compatible with the broom function you’re needing, then
  you can obtain your results by some other means, but first indicate
  which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

``` r
#I am choosing to produce a p-value. 

library(broom)
tidy(model)
```

    ## # A tibble: 2 × 5
    ##   term        estimate std.error statistic   p.value
    ##   <chr>          <dbl>     <dbl>     <dbl>     <dbl>
    ## 1 (Intercept)     9.76     0.439     22.2  8.09e-107
    ## 2 genre_dummy     1.72     0.523      3.29 1.02e-  3

``` r
#Within this tibble the p.value column contains the p values. This column is telling me whether the estimates from the regression model are statistically significant. 
```

<!----------------------------------------------------------------------------->

# Task 4: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 3.1 (5 points)

Take a summary table that you made from Milestone 1 (Task 4.2), and
write it as a csv file in your `output` folder. Use the `here::here()`
function.

- **Robustness criteria**: You should be able to move your Mini Project
  repository / project folder to some other location on your computer,
  or move this very Rmd file to another location within your project
  repository / folder, and your code should still work.
- **Reproducibility criteria**: You should be able to delete the csv
  file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

``` r
here::here()
```

    ## [1] "/Users/jader/Desktop/Test/MiniDataAnalysis_Jade_Radke"

``` r
genre_achievements_csv <- steam_games %>%
  group_by(genre) %>%
  summarise(genre_achievements_mean = mean(achievements, na.rm = TRUE))

write_csv(genre_achievements_csv, here::here("output", "genre_achievements.csv"))
```

<!----------------------------------------------------------------------------->

## 3.2 (5 points)

Write your model object from Task 3 to an R binary file (an RDS), and
load it again. Be sure to save the binary file in your `output` folder.
Use the functions `saveRDS()` and `readRDS()`.

- The same robustness and reproducibility criteria as in 3.1 apply here.

<!-------------------------- Start your work below ---------------------------->

``` r
saveRDS(model, here::here("output", "model.rds"))

rdsmodel <- readRDS(here::here("output", "model.rds"))
rdsmodel
```

    ## 
    ## Call:
    ## lm(formula = original_price ~ genre_dummy, data = lm_df)
    ## 
    ## Coefficients:
    ## (Intercept)  genre_dummy  
    ##       9.758        1.720

<!----------------------------------------------------------------------------->

# Tidy Repository

Now that this is your last milestone, your entire project repository
should be organized. Here are the criteria we’re looking for.

## Main README (3 points)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

- In a sentence or two, explains what this repository is, so that
  future-you or someone else stumbling on your repository can be
  oriented to the repository.
- In a sentence or two (or more??), briefly explains how to engage with
  the repository. You can assume the person reading knows the material
  from STAT 545A. Basically, if a visitor to your repository wants to
  explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## File and Folder structure (3 points)

You should have at least four folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (2 points)

All output is recent and relevant:

- All Rmd files have been `knit`ted to their output, and all data files
  saved from Task 4 above appear in the `output` folder.
- All of these output files are up-to-date – that is, they haven’t
  fallen behind after the source (Rmd) files have been updated.
- There should be no relic output files. For example, if you were
  knitting an Rmd to html, but then changed the output to be only a
  markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

PS: there’s a way where you can run all project code using a single
command, instead of clicking “knit” three times. More on this in STAT
545B!

## Error-free code (1 point)

This Milestone 1 document knits error-free, and the Milestone 2 document
knits error-free.

## Tagged release (1 point)

You’ve tagged a release for Milestone 1, and you’ve tagged a release for
Milestone 2.

### Attribution

Thanks to Victor Yuan for mostly putting this together.
