
# Getting started checklist

In order to best profit from the workshop please follow the instruction below. **R** is a programming language that is especially powerful for data exploration, visualization, and statistical analysis. To interact with **R**, we recommend to use RStudio.

1. Install [R](https://www.r-project.org/)
2. Install [RStudio](https://www.rstudio.com/) (not mandatory but strongly recommended)
3. Install [abn](https://cran.r-project.org/package=abn) from **CRAN** and all dependencies
```r
install.packages("abn")
```
3.1 *Optionally*, install latest version not yet on CRAN:  
```r
install.packages("abn")
```
4. Install [INLA](http://www.r-inla.org/)
```r
install.packages("INLA", repos=c(getOption("repos"), INLA="https://inla.r-inla-download.org/R/stable"), dep=TRUE)
```
4.1 Alternatively, you can download it and install from a local repository
```r
download.file("https://inla.r-inla-download.org/R/stable", path_to_file)
install.packages(path_to_file, repos = NULL, type="source")
```
5. Install [Rgraphviz](http://www.bioconductor.org/packages/release/bioc/html/Rgraphviz.html)
```r
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
BiocManager::install("Rgraphviz")
```
6. Install [JAGS](http://mcmc-jags.sourceforge.net/). Operating System dependant
