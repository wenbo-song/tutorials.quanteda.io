---
title: Correspondence analysis
weight: 40
draft: false
---

Correspondence analysis is a technique to scale documents on multiple dimensions. Correspondence analysis is similar to principal component analysis but works for categorical variables (contingency table).


```r
require(quanteda)
```

`textmodel_ca()` provides similar functionality to the **ca** package, but **quanteda**'s version is more efficient for textual data.

You can plot positions of documents on a one-dimensional scale using `textplot_scale1d()`.


```r
dfmat_irish <- dfm(data_corpus_irishbudget2010, 
          remove_punct = TRUE, 
          remove = stopwords('en'))

tmod_ca <- textmodel_ca(dfmat_irish)
textplot_scale1d(tmod_ca)
```

<img src="/machine-learning/ca.en_files/figure-html/unnamed-chunk-2-1.png" width="672" />

If you want to plot documents on multi-dimensional scale, you use `coef()` to obtain coordinates of lower dimensions.  


```r
dat_ca <- data.frame(dim1 = coef(tmod_ca, doc_dim = 1)$coef_document, 
                      dim2 = coef(tmod_ca, doc_dim = 2)$coef_document)
head(dat_ca)
```

```
##                            dim1        dim2
## Lenihan, Brian (FF)   1.3947058  0.07857887
## Bruton, Richard (FG) -0.7102673  0.75538166
## Burton, Joan (LAB)   -1.0420867  1.82837918
## Morgan, Arthur (SF)  -0.2428268 -0.09447121
## Cowen, Brian (FF)     1.4579375 -0.12655387
## Kenny, Enda (FG)     -0.9269172 -0.24479883
```

```r
plot(1, xlim = c(-2, 2), ylim = c(-2, 2), type = 'n', xlab = 'Dimension 1', ylab = 'Dimension 2')
grid()
text(dat_ca$dim1, dat_ca$dim2, labels = rownames(dat_ca), cex = 0.8, col = rgb(0, 0, 0, 0.7))
```

<img src="/machine-learning/ca.en_files/figure-html/unnamed-chunk-3-1.png" width="672" />

