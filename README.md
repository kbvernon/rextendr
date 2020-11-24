
<!-- README.md is generated from README.Rmd. Please edit that file -->

Call Rust code from R using the ‘extendr’ crate
===============================================

<!-- badges: start -->

[![R build
status](https://github.com/clauswilke/rextendr/workflows/R-CMD-check/badge.svg)](https://github.com/clauswilke/rextendr/actions)
[![CRAN
status](https://www.r-pkg.org/badges/version/rextendr)](https://CRAN.R-project.org/package=rextendr)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
<!-- badges: end -->

Installation
------------

To install the package, run:

    remotes::install_github("clauswilke/rextendr")

Note that this will install the package but does not guarantee that the
package can do anything useful. You will also need to set up a working
Rust toolchain, including libclan/llvm-config support to run
[bindgen](https://rust-lang.github.io/rust-bindgen/). See the
[installation instructions for
libR-sys](https://github.com/extendr/libR-sys) for help. If you can
successfully build libR-sys you’re good.

Usage
-----

Basic use example:

    library(rextendr)

    # some simple Rust code with two functions
    rust_src <- "use extendr_api::*;

    #[extendr]
    fn hello() -> &'static str {
        \"Hello, this string was created by Rust.\"
    }

    #[extendr]
    fn add(a: i64, b: i64) -> i64 {
        a + b
    }
    "

    rust_source(code = rust_src, quiet = TRUE)

    # call `hello()` function from R
    hello()
    #> [1] "Hello, this string was created by Rust."

    # call `add()` function from R
    add(14, 23)
    #> [1] 37
