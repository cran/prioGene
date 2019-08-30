# prioGene

<!-- badges: start -->
<!-- badges: end -->

The goal of prioGene is to prioritize candidate genes for complex noncommunicable diseases.

## Installation

You can install the released version of prioGene from [CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("prioGene")
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(prioGene)
## basic example code
```
```{r setup}
library(prioGene)


#One-step interactions with known disease-causing genes are retained in networks
#'
#' net: a network
#' dise_gene: a matrix with one column of genes
#'
#' return: a matrix
net_disease <- deal_net(net,dise_gene)


#Get a one-to-many matrix of gene and GO term
#'
#'net_disease: a disease related network, matrix
#'GO_human: a matrix, gene and GO terms
#'
#' return: a matrix
genes_mat <- get_gene_mat(net_disease,GO_human)


#Get a one-to-many matrix of GO term and gene
#' net_disease: a disease related network, matrix
#' GO_human: a matrix, gene and GO terms
#'
#' return: a matrix
terms_mat <- get_term_mat(net_disease,GO_human)


#Get the GO term for each pair of nodes in the network
#' genes_mat: a one-to-many matrix of GO term and gene
#' net_disease: a disease related network, matrix
#'
#' return: a matrix
net_disease_term <- get_net_disease_term(genes_mat,net_disease)


#weighting gene
#' genes_mat: a one-to-many matrix of GO term and gene
#'
#' return: a matrix
node_weight <- get_node_weight(genes_mat)


#weighting edge
#' net_disease_term: GO terms for each pair of nodes in the network
#'
#' return: a matrix
edge_weight <- get_edge_weight(net_disease_term)


#Q is the disease risk transition probability matrix, 
#which is composed of transition probabilities from one gene to another
Q <- get_Q()


#R_0 is the vector of initial disease risk scores for all genes
R_0<- get_R_0(dise_gene,node_weight,f=1)


#get the result the output number is the number of iterations
#' Q:  the disease risk transition probability matrix
#' bet:  a parameter to measure the importance of genes and interactions
#' R_0: the vector of initial disease risk scores for all genes
#' node_weight: a matrix, genes and their weights
#' threshold: a threshold for terminating iterations
#'
#' return: a matrix
result <- get_R(Q,0.5,R_0,node_weight,10^(-9))
```
