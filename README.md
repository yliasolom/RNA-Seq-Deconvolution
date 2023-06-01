# **RNA-Seq-Deconvolution**
This GitHub repository provides an implementation of RNA-Seq deconvolution algorithms for estimating cell-type proportions from bulk RNA-Seq data. Deconvolution is a powerful computational technique that allows researchers to infer the cellular composition of heterogeneous samples based on gene expression profiles. 

### Data for analysis/training:
- `Expression_cells.tsv.gz` - expression of purified normal cell types
- `Annotation_cells.tsv.gz` - annotation
- `Expression_cell_lines.tsv.gz` - expression of malignant cell lines of different tumor types
- `Annotation_cell_lines.tsv.gz` - annotation

### Data for testing: - expression of 2 healthy patient blood samples in
- `Normal-blood-expr.tsv` - expression of 2 blood samples from healthy patients
- `LUAD-expr.tsv` - 6 adenocarcinoma samples
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# **Latent Dirichlet Allocation (LDA)**

Papers:
1. [Identifying gene expression programs of cell-type identity and cellular activity with single-cell RNA-Seq](https://elifesciences.org/articles/43803).

2. [Post-modified non-negative matrix factorization for deconvoluting the gene expression profiles of specific cell types from heterogeneous clinical samples based on RNA sequencing data](https://analyticalsciencejournals.onlinelibrary.wiley.com/doi/pdf/10.1002/cem.2929?casa_token=gf9lOZ_Fx2AAAAAA:mH44_dQVdxpM0PFdBtTonIo5geaSf6LAOe-2cxIG7iM2xEXDx0woQhnM2puhIZ_73W9nNGhw4Y5BYpY).

The **LDA** method is used to analyse the thematic structure of a collection of texts. In the context of cell data analysis, the authors applied a modified version of LDA to deconvolve and determine the proportions of different cell types from gene expression data. The method has been proposed for use in conditions where
expression of different cell types or signature genes is unknown.

The authors found that methods such as ICA (Independent Component Analysis), LDA and NMF (Non-Negative Matrix Factorization) but not PCA (Principal Component Analysis) can accurately detect both activity and gene expression identity (GEP). However, due to the stochastic nature of these algorithms, they can give different results when repeated many times, making them difficult to interpret.

This approach was first tested experimentally using synthetic mixtures of pure tissue types and simulated mixtures with well-designed proportions. The results showed that
deconvolved gene expression patterns were in good agreement with experimental patterns (r > 0.99). 

-----------------------------------
-----------------------------------
-----------------------------------
Thus, **LDA** is a generative probabilistic model, and it is assumed that each document (in this case, a `sample') can be viewed as a mixture of different `themes' (`types of cells') with certain proportions. Each theme represents a `probability distribution' on a set of genes. Similarly, each gene can be associated with different themes with certain probabilities. In our case, we can treat `each cell type as a topic' and the values of `expression of genes as input traits'.

Next - train LDA on the vectorized gene expression data -> the model will estimate the proportions of topics for each sample.




**LDA variables and parameters:**

$K$ - total number of topics (cell types)

$N$ - total number of genes

$M$ - total number of samples (documents)

$W$ - gene expression matrix of size $M \times N$, where each element $w_{ij}$ represents gene expression $j$ in sample $i$

$Z$ is a latent variable matrix of dimension $M \times K$, where each element $z_{ik}$ represents the proportion of topic $k$ in sample $i$

$\Theta$ is a matrix of topic distribution parameters in samples of dimension $M \times K$, where each element $\theta_{ik}$ represents the probability of topic $k$ in the sample. 

The final step is to extract cell type proportions: after training the LDA model, the cell type proportions for each sample can be extracted. These proportions represent the contribution of each cell type to the overall gene expression profile of the sample (i.e. simply an estimate of the cell type distribution probabilities in each sample and the gene distribution for each cell type. These distributions allow the proportions of cell types in each sample to be determined based on their gene expression profile).




---------------------------------------
---------------------------------------
---------------------------------------

In the context of cell type analysis, LDA can be used to detect the hidden structure of cell types in gene expression data. By representing cell types as topics and gene expression values as words, LDA can estimate the proportions of cell types for each sample based on observed gene expression patterns.

LDA assumes that each document (sample) is a mixture of themes (cell types) and the observed gene expression values are formed from these theme proportions. By training the LDA model on gene expression data, the proportions of latent cell types for each sample can be identified. These proportions provide a quantitative measure of the relative presence of different cell types in the samples.

The LDA process involves estimating the probabilities of the topic distribution for each cell and the gene distribution for each topic. These probabilities can be used to determine the proportions of cell types based on their gene expression. In this way, LDA can help identify hidden structure in the data and identify cell types based on their gene expression profile. That is, we model 'themes' and their distributions within each sample.
 
 
