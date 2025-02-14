# Visualization

This sections shows how to create and interpret simple graphs. In past exams, the SOA has provided code for any technical visualizations which are needed. 

## Create a plot object (ggplot)

Let's create a histogram of the claims.  The first step is to create a blank canvas that holds the columns that are needed.  The `aesthetic` argument, `aes`, means that the variable shown will the the claims.





```r
library(ExamPAData)
p <- insurance %>% ggplot(aes(claims))
```

If we look at `p`, we see that it is nothing but white space with axis for `count` and `income`.


```r
p
```

<img src="04-visualization_files/figure-html/unnamed-chunk-3-1.png" width="672" />

## Add a plot

We add a histogram


```r
p + geom_histogram()
```

<img src="04-visualization_files/figure-html/unnamed-chunk-4-1.png" width="672" />

Different plots are called "geoms" for "geometric objects".  Geometry = Geo (space) + metre (measure), and graphs measure data.  For instance, instead of creating a histogram, we can draw a gamma distribution with `stat_density`.


```r
p + stat_density()
```

<img src="04-visualization_files/figure-html/unnamed-chunk-5-1.png" width="672" />

Create an xy plot by adding and `x` and a `y` argument to `aesthetic`.


```r
insurance %>% 
  ggplot(aes(x = holders, y = claims)) + 
  geom_point()
```

<img src="04-visualization_files/figure-html/unnamed-chunk-6-1.png" width="672" />

## Data manipulation chaining

Pipes allow for data manipulations to be chained with visualizations.


```r
termlife %>% 
  filter(FACE > 0) %>% 
  mutate(INCOME_AGE_RATIO = INCOME/AGE) %>% 
  ggplot(aes(INCOME_AGE_RATIO, FACE)) + 
  geom_point() + 
  theme_bw()
```

<img src="04-visualization_files/figure-html/unnamed-chunk-7-1.png" width="672" />

