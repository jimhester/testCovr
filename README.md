
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
source_file <- tempfile()
test_file <- tempfile()

cat(file = source_file,
'
curry <- function(x)
{
  if(is.data.frame(x))
    return(1)
  else
    # test
    return(0)
}
')

cat(file = test_file,
'curry("a")')

cov <- file_coverage(source_file, test_file)
# report(cov)
as.data.frame(cov)
#>                                                                        filename
#> 1 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa612779a4c
#> 2 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa612779a4c
#> 3 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa612779a4c
#>   functions first_line first_byte last_line last_byte first_column
#> 1     curry          4          5         4        22            5
#> 2     curry          5          5         5        13            5
#> 3     curry          6          3         8        13            3
#>   last_column first_parsed last_parsed value
#> 1          22            4           4     1
#> 2          13            5           5     0
#> 3          13            6           8     1
file.remove(source_file, test_file)
#> [1] TRUE TRUE
```

![](https://www.dropbox.com/s/bnwp7tbv03fpc7a/Screenshot%202016-08-18%2018.14.02.png?raw=1)

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
# report(cov)
as.data.frame(cov)
#>                                                                        filename
#> 1 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa65d550e13
#> 2 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa65d550e13
#> 3 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa65d550e13
#> 4 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa65d550e13
#> 5 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa65d550e13
#> 6 /var/folders/dt/r5s12t392tb5sk181j3gs4zw0000gn/T//RtmpYonShG/file9fa65d550e13
#>   functions first_line first_byte last_line last_byte first_column
#> 1     curry          4          5         4        22            5
#> 2     curry          6          5         6        13            5
#> 3     curry          7          6        18         3            6
#> 4     curry          9          5         9        13            5
#> 5     curry         13          5        13        13            5
#> 6     curry         16          5        16        13            5
#>   last_column first_parsed last_parsed value
#> 1          22            4           4     1
#> 2          13            6           6     0
#> 3           3            7          18     1
#> 4          13            9           9     1
#> 5          13           13          13     0
#> 6          13           16          16     0
file.remove(source_file, test_file)
#> [1] TRUE TRUE
```

![](https://www.dropbox.com/s/cm97qorczh9zl48/Screenshot%202016-08-18%2018.14.13.png?raw=1)
