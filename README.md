
<!-- README.md is generated from README.Rmd. Please edit that file -->

# ragg

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/thomasp85/ragg.svg?branch=master)](https://travis-ci.org/thomasp85/ragg)
[![AppVeyor build
status](https://ci.appveyor.com/api/projects/status/github/thomasp85/ragg?branch=master&svg=true)](https://ci.appveyor.com/project/thomasp85/ragg)
[![CRAN
status](https://www.r-pkg.org/badges/version/ragg)](https://cran.r-project.org/package=ragg)
<!-- badges: end -->

This package provides graphic devices for R based on the AGG library
developed by the late Maxim Shemanarev. AGG provides both higher
performance and higher quality than the standard cairo based drivers
provided by grDevices, and is further system agnostic so that output
should be identical across operating systems.

## Installation

The package is currently under development and has only been configured
for Mac and Linux. You’ll need to have pkg-config, freetype, fontconfig,
libpng, and libtiff available on your system to compile the package. If
you have these libraries available you should be able to install the
package using devtools:

``` r
# install.packages('devtools')
devtools::install_github('thomasp85/ragg')
```

## Use

ragg provides *almost* drop-in replacements for the png and tiff graphic
devices provided by default from the grDevices packages and can both
produce png and tiff files. Notable features, that sets itself apart
from the build-in devices, includes:

  - Faster (up to 40% faster than anti-aliased cairo device)
  - Direct access to all system fonts
  - High quality anti-aliasing
  - High quality rotated text
  - Support 16-bit output
  - System independent rendering (output from Mac, Windows, and Linux
    should be identical)

You can use it like any other device. The main functions are `agg_png()`
and `agg_tiff()`, both have arguments that closely match that of the
`png()` and `tiff()` functions, so switching over should be easy.

``` r
library(ragg)
library(ggplot2)

file <- knitr::fig_path('.png')

agg_png(file, width = 1000, height = 500, res = 144)
ggplot(mtcars) + 
  geom_point(aes(mpg, disp, colour = hp)) + 
  labs(title = 'System fonts — Oh My!') + 
  theme(text = element_text(family = 'Papyrus'))
invisible(dev.off())

knitr::include_graphics(file)
```

<img src="man/figures/README-unnamed-chunk-3-1.png" width="100%" />
