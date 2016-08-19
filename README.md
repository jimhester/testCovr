
<!-- README.md is generated from README.Rmd. Please edit that file -->
``` r
library(covr)
package_coverage()
#> test Coverage: 25.00%
#> R/addition.R: 0.00%
#> R/doublefun.R: 66.67%

file.rename("R/addition.R", "R/addition.R.bak")
#> [1] TRUE
package_coverage()
#> test Coverage: 66.67%
#> R/doublefun.R: 66.67%

file.rename("R/addition.R.bak", "R/addition.R")
#> [1] TRUE
```

``` r
library(knitr)
library(webshot)
source_file <- tempfile()
test_file <- tempfile()

cat(file = source_file,
'
curry2 <- function(x)
{
  if(is.data.frame(x))
    return(1)
  else
    # test
    return(0)
}
')

cat(file = test_file,
'curry2("a")')

cov <- file_coverage(source_file, test_file)
webshot(report(cov, browse = FALSE), selector = c("#files"), eval = "casper.then(function() { this.click('td a')});")
```

![](README-unnamed-chunk-3-1.png)

``` r
as.data.frame(cov)
#>                                                                        filename
#> 1 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c5ed3da27
#> 2 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c5ed3da27
#> 3 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c5ed3da27
#>   functions first_line first_byte last_line last_byte first_column
#> 1    curry2          4          6         4        21            6
#> 2    curry2          5          5         5        13            5
#> 3    curry2          8          5         8        13            5
#>   last_column first_parsed last_parsed value
#> 1          21            4           4     1
#> 2          13            5           5     0
#> 3          13            8           8     1
file.remove(source_file, test_file)
#> [1] TRUE TRUE
```

``` r
source_file <- tempfile()
test_file <- tempfile()

cat(file = source_file,
'
curry <- function(x)
{
  if(is.data.frame(x)){
    # test0
    return(1)
  }  else if (is.character(x)){
    # test
    return(0)

  } else if (is.numeric(x)){
    # test1
    return(2)

  } else{
    return(3)

  }
}
')

cat(file = test_file,
'curry("a")')

cov <- file_coverage(source_file, test_file)
webshot(report(cov, browse = FALSE), selector = c("#files"), eval = "casper.then(function() { this.click('td a')});")
```

![](README-unnamed-chunk-4-1.png)

``` r
as.data.frame(cov)
#>                                                                        filename
#> 1 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#> 2 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#> 3 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#> 4 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#> 5 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#> 6 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#> 7 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpyXdgHV/file899c72088620
#>   functions first_line first_byte last_line last_byte first_column
#> 1     curry          4          6         4        21            6
#> 2     curry          6          5         6        13            5
#> 3     curry          7         15         7        29           15
#> 4     curry          9          5         9        13            5
#> 5     curry         11         14        11        26           14
#> 6     curry         13          5        13        13            5
#> 7     curry         16          5        16        13            5
#>   last_column first_parsed last_parsed value
#> 1          21            4           4     1
#> 2          13            6           6     0
#> 3          29            7           7     1
#> 4          13            9           9     1
#> 5          26           11          11     0
#> 6          13           13          13     0
#> 7          13           16          16     0
file.remove(source_file, test_file)
#> [1] TRUE TRUE
```
