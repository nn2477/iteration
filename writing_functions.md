writing_functions
================
Nhu Nguyen
2023-11-01

set seed for reproducibility

``` r
set.seed(12345) 
```

### lists

``` r
vec_numeric = 1:4
vec_char = c("my", "name", "is", "jeff")

tibble(
  num = vec_numeric,
  char = vec_char
)
```

    ## # A tibble: 4 × 2
    ##     num char 
    ##   <int> <chr>
    ## 1     1 my   
    ## 2     2 name 
    ## 3     3 is   
    ## 4     4 jeff

different stuff with different lengths

``` r
vec_numeric = 1:5
vec_char = LETTERS
```

but if we do it as a list

``` r
l = 
  list(
    vec_numeric = 1:5,
    vec_char = LETTERS,
    matrix = matrix(1:10, nrow = 5, ncol = 2),
    summary = summary(rnorm(100))
  )
```

accessing lists

``` r
l$vec_char
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[[2]]
```

    ##  [1] "A" "B" "C" "D" "E" "F" "G" "H" "I" "J" "K" "L" "M" "N" "O" "P" "Q" "R" "S"
    ## [20] "T" "U" "V" "W" "X" "Y" "Z"

``` r
l[["summary"]]
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -2.3804 -0.5901  0.4837  0.2452  0.9004  2.4771

### loops

``` r
list_norm_samples = 
  list(
    a = rnorm(10, 1, 5),
    b = rnorm(20, 0, 7),
    c = rnorm(20, 20, 1),
    d = rnorm(20, -45, 13)
  )
```

mean and sd function

``` r
mean_and_sd = function(x) { 
  
  if (!is.numeric(x)) {
    stop("argument should be numbers")
  } else if (length(x) < 2) {
    stop("you need at least 2 numbers to get z scores")
  }
  
  mean_x = mean(x) 
  sd_x = sd(x)
  
  tibble(
    mean = mean_x,
    sd = sd_x
  )
    }
```

``` r
mean_and_sd(list_norm_samples$a)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.444  4.19

``` r
mean_and_sd(list_norm_samples$b)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.441  8.90

``` r
mean_and_sd(list_norm_samples$c)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  20.0  1.14

``` r
mean_and_sd(list_norm_samples$d)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -46.5  11.0

trying to write it as a for loop instead

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  
  output[[i]] = mean_and_sd(list_norm_samples[[i]])
  
}
```

### use `map`

``` r
output = map(list_norm_samples, mean_and_sd)

##can use different variables too 

output = map(list_norm_samples, summary)
```
