# Plotting functions for CNV data

## Installation

Install from github:
```{R}
library(devtools)
install_github("nriddiford/cnvPlotteR")
```

## Input

* Designed to read output from [CNV-Seq](http://tiger.dbs.nus.edu.sg/cnv-seq/doc/manual.pdf), although should work for any coverage data with cols:

"chromosome"  
"start" - 1-based window start  
"end" - 1-based window end  
"test" - reads mapped in window in tumour sample  
"ref" - reads mapped in window in normal sample  
"position" - (end - start) +1  
"log2" - log2 FC for tumour/normal reads per window  

Example output from CNV-Seq:

```
"chromosome"    "start" "end"   "test"  "ref"   "position"      "log2"  "p.value"       "cnv"   "cnv.size"      "cnv.log2"      "cnv.p.value"
"X"     1       10000   50      74      5000    -0.292601981038923      2.85779196291872e-06    0       NA      NA      NA
"X"     5001    15000   50      72      10000   -0.253073616852285      4.12598434147092e-05    0       NA      NA      NA
"X"     10001   20000   2       2       15000   0.272995194815302       7.96882592007325e-06    0       NA      NA      NA
"X"     15001   25000   0       0       20000   NA      NA      0       NA      NA      NA
"X"     20001   30000   0       0       25000   NA      NA      0       NA      NA      NA
"X"     25001   35000   0       0       30000   NA      NA      0       NA      NA      NA
"X"     30001   40000   0       0       35000   NA      NA      0       NA      NA      NA
```

### Plot all cnvs in specified directory for all chromosomes

* Currently assumes *Drosophila* genome, and excludes chroms 4 and Y for grid plot

```
plot.all.grid <- function(path = NA)
````

### Plot single chromosome

* Will default to plotting X chrom if not chrom specified

```
plot.chrom(cnv_file = "data/HUM-7.tagged.SC.hits.filt-vs-HUM-9.tagged.SC.hits.filt.window-10000.minw-4.cnv")
```

### Plot region for specified chromosome

* Will by defualt plot region around N on X if no to or from specified

```
plot.region(cnv_file="data/w_500/HUM-7.tagged.SC.hits.filt-vs-HUM-9.tagged.SC.hits.filt.window-500.minw-4.cnv", from=3029368, to=3452041, bp1=3129368,bp2=3352041,chrom="X", tick=100000, title="222Kb DEL on X")
```


# To do
- [x] Allow user to control Y axis limits (for subtle CN changes)
- [ ] Build in depth plots
- [ ] Fix the ticks in Notch plots (show every 10kb?, start at round number)
- [ ] Clean up the function calls (i.e. chrom=NA -> chrom=X to set as default)
