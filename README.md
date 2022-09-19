quanteda.dictionaries
================

> This is a fork of the original **quanteda.dictionaries** maintained by kbenoit.
> Please go to [https://github.com/kbenoit/quanteda.dictionaries](https://github.com/kbenoit/quanteda.dictionaries) 
> for the original package.

An R package consisting of dictionaries for text analysis and associated
utilities. Designed to be used with [**quanteda**](http://quanteda.io)
but can be used more generally with any text analytic package (e.g.
**tidytext**, **tm**, etc.).

## Experimental Regex support
This fork enables regular regex-based patterns in `liwcalike` by implementing
a complementary function, codenamed `liwcahead`, which allows the following
regex patterns to be used:
* `.`, e.g. `.ome` for {`some, home, ...`}
* `*`, e.g. `fil.*` for {`fil, file, filing, filet, ...`}
* `?`, e.g. `s.?lice` for {`splice, slice, ...`}

It accomplishes this by using the optional arg `regex` in `tokens_lookup`: 
``` r
tokens_lookup(toks, dictionary, valuetype="regex")
```

### DISCLAIMER
Note that the entire regex pattern set is not guaranteed to work.
For example, the brackets characters {`(`, `)`} are not functional, as
`liwcahead`'s dependencies remove the brackets.
 
## Installing

``` r
# the devtools package needs to be installed for this to work
devtools::install_github("lullabysinger/quanteda.dictionaries") 
```

## Usage
This is a drop-in replacement for the original `liwcalike` -- nothing has changed
for `liwcalike`, which forks the original code.

However, the `liwcahead` function is the regex-enabled version. Arguments
remain the same as the original kbenoit `liwcalike`, with one small difference.

If the LIWC-style dic file consists of wildcards, use the following:
``` r
output_lsd <- liwcahead(corpus, dictionary, regex = TRUE)
```

## Demonstration - as adapted from the original `kbenoit/quanteda.dictionaries`

With the `liwcalike()` function from the **quanteda.dictionaries**
package, you can easily analyze text corpora using exising or custom
dictionaries. Here we show how to apply the Lexicoder Sentiment
Dictionary (Young and Soroka 2012) to a corpus consting of 2000 movie
reviews (from the
[**quanteda.corpora**](https://github.com/quanteda/quanteda.corpora)
package).

``` r
library("quanteda.dictionaries")

output_lsd <- liwcalike(quanteda.corpora::data_corpus_movies, 
                        dictionary = data_dictionary_NRC)

head(output_lsd)
```

    ##           docname Segment  WC       WPS Sixltr   Dic anger anticipation
    ## 1 neg_cv000_29416       1 847  78.88889  13.11 19.36  0.71         2.95
    ## 2 neg_cv001_19502       2 278 240.00000  10.79 24.46  3.24         3.24
    ## 3 neg_cv002_17424       3 559 162.66667  16.46 21.29  1.07         2.86
    ## 4 neg_cv003_12683       4 594 239.50000  16.67 22.73  1.35         3.03
    ## 5 neg_cv004_12641       5 872 366.50000  19.04 19.38  1.26         1.49
    ## 6 neg_cv005_29357       6 753 671.00000  18.33 27.49  3.32         1.59
    ##   disgust fear  joy negative positive sadness surprise trust AllPunc
    ## 1    0.83 1.42 2.36     2.24     4.01    1.42     1.30  2.13   18.06
    ## 2    2.16 1.80 1.44     4.32     2.88    1.44     1.08  2.88   18.35
    ## 3    0.72 2.68 1.43     3.40     4.11    1.79     0.54  2.68   14.67
    ## 4    1.18 1.85 1.52     4.21     5.05    1.85     1.18  1.52   22.90
    ## 5    0.69 2.06 1.49     3.90     3.33    1.72     1.38  2.06   17.66
    ## 6    2.39 4.25 0.80     5.98     3.45    1.99     1.86  1.86   11.02
    ##   Period Comma Colon SemiC QMark Exclam Dash Quote Apostro Parenth OtherP
    ## 1   4.01  5.19  0.35  0.00  0.71   0.35 1.18  3.07    1.89       0  14.76
    ## 2   5.04  6.47  0.00  0.00  0.00   0.00 0.00  5.40    4.68       0  16.91
    ## 3   3.94  5.55  0.00  0.00  0.54   0.00 0.54  2.68    2.68       0  12.70
    ## 4   3.37  4.38  0.00  0.00  0.51   0.00 4.71  7.58    4.21       0  15.82
    ## 5   4.24  6.19  0.69  0.23  0.11   0.00 1.95  2.18    1.72       0  13.65
    ## 6   4.65  3.98  0.13  0.00  0.00   0.00 0.53  0.93    0.40       0   9.69


## Code of Conduct

Please note that this project is released with a [Contributor Code of
Conduct](CONDUCT.md), which we adhere to, based on the original 
from `kbenoit/quanteda.dictionaries`.

By participating in this project you agree to abide by its terms.
