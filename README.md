
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
