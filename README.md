# outlier_detection_gene_expression_LOF
Outlier detection in gene expression for Cancer patients using LOF Algorithm.
# Outlier Detection in Gene Expression Values 

When a patient has cancer, multiple genetic changes occur, some of which cause the cancer to spread. Hence, gene expression measurements help us in monitoring these changes.

## Prerequisites

Dataset Used:[Gene Expression Cancer RNA-Seq Data Set ](https://archive.ics.uci.edu/ml/datasets/gene+expression+cancer+RNA-Seq) 
Source: UCI Repository Archive

This project was made using [Google Colab](https://colab.research.google.com/notebooks/intro.ipynb#recent=true)

## Problem Statement

### What is Gene Expression?

Genes are made up of DNA, and DNA encode proteins or other molecules needed by the body to carry out essential functions. This process by which a cell dictates the formation of requisite molecules of the body on the basis of the genetic code is called gene expression. Gene expression can be measured. 

(Note: The processes explained above are a very low-level description of the actual processes only to help readers who are not from a Life Sciences background to understand the dataset)

### Understaning the Dataset

The dataset contains the gene expression values of 2000+ genes of various cancer patients. There are 2 csv files - data.csv and labels.csv in the dataset.

data.csv  - It contains the gene expression values for a variety of patients suffering from different cancers.Each 'sample' refers to a patient. 


lables.csv - List of samples and the corresponding cancer which that patient is suffereing from like BRCA- Breast Cancer, LUAD-Lung Adenocarcinoma, and so on.



## Local Outlier Factor Algorithm         

It is a outlier detection technique which identifies local as well as global outliers.
For a given point A:                      
* K- distance or distk(A) is the distance between o and its k-nearest neighbor.
* K-distance neighborhood of A contains all objects of which the distance to is less than the distk(A). These points are labelled as o’ and the set of all these points forms the Nk(A).
* Reachability distance: For two objects, A and A’ the reachability distance from A′ to A is given by:
 reachdistk(A←A′) = max{distk(A), dist(A,A′)}
* Local Reachability distance of A: Inverse of the average reachability distance values of A.
lrdk(A)= ∥Nk(A)∥/ sum(reachdistk(A′←A)), for all A’ ∈ Nk
LOF score for A: 
       LOFk(A) =sum(lrdk(A’))/(lrd(A)*∥Nk (A)∥), for all A’ ∈ Nk
If the LOF score is beyond a certain threshold, the point is an outlier. The threshold is always set as a value more than 1.

{Source - Han, J., Kamber, M., & Pei, J. (2012). Data mining: Concepts and techniques, third edition (3rd ed.). Waltham, Mass.: Morgan Kaufmann Publishers.}

## Procedure

Algorithm used: Local Outlier Factor (LOF)
* Pre-process: Merge the two csv files to get a common dataframe;Extract only the BRCA samples and 2 genes only. This program is for BRCA patients only, this can be replicated for any other cancer too.
* Logic: Modularised code for calculating the Neighbours in k-neighbourhood, reachability distance, local reachabaility distance and local outlier factor score for every single sample in the data set.
The LOF algorithm finds a score for each sample based on which outliers are detected in the sample.
* Data Visualisation: Scatter Plot to see identification of Local Outliers

**Sci-kit libraries have only been used for Data Visualisation. No in-built libraries have been used for the implementation of DBSCAN Algorithm, the code is purely for understanding the algorithmic logic.**

## Inference
Outliers in such a dataset could mean an error in data collection or measurement which if not removed would cause major errors in further analysis. It could also mean a special case seen in Cancer Patients (and usually if you have more outlier tuples like this one, it is definitely investigated) – opens up research avenue. [Cancer Research is a huge field in itself, the amount we know about the disease is actually very little and a cure has not been found yet for many cancers.]


## Use Cases

## Points to be Noted

* Threshold for LOF Score has been assumed. It essentially needs domain expertise to be defined.

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
