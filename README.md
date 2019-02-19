# scds

**s**ingle **c**ell **d**oublet **s**coring: In-silico doublet annotation for single cell RNA sequencing data

```scds``` is an ```R``` package for computational doublet annotation of single cell RNA sequencing data. It interfaces with the S4 ```SingleCellExperiment``` class [(see here)](https://bioconductor.org/packages/release/bioc/html/SingleCellExperiment.html), so it should easily integrate into many ```R```/Bioconductor scRNA-seq analysis workflows. 

#### Installation

```
devtools::install_github('kostkalab/scds')
```

#### Quick Start

In the following ```sce``` is a ```SingleCellExperiment``` holding at least raw counts in an assay called ```counts```.

```
#- Annotate doublet using co-expression based doublet scoring:
sce = cxds(sce)

#- Annotate doublet using binary classification based doublet scoring:
sce = bcds(sce)

#- Combine both annotations into a hybrid annotation
sce = cxds_bcds_hybrid(sce)

#- Doublet scores are now available via colData:
CD  = colData(sce)
head(cbind(CD$cxds_score,CD$bcds_score, CD$hybrid_score))
rm(CD)

#- Visualize the top 5% annotated doublets
plotDbl(sce, score="cxds_score",   frac=0.05)
plotDbl(sce, score="bcds_score",   frac=0.05)
plotDbl(sce, score="hybrid_score", frac=0.05)
#- Or:
library(scater)
scater::plotTSNE(sce,col="hybrid_score")

#- Visualize gene pairs contributing to doublet annotation:
plotCxdsPairs(sce,n=5)

```


