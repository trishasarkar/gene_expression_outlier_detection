# Outlier Detection in Gene Expression Values 

Cancer research has seen many developments, but we still do not know enough about the disease. When a patient has cancer, multiple genetic changes occur, some of which cause the cancer to spread. Even anomalies in data can sometimes be the starting point of some vital research. Monitoring gene expression measurements is one such way of  keeping track of genetic changes in Cancer Patients. This code identifies outliers in gene expression data of Breast Cancer Patients.

## Prerequisites

Dataset Used: [Gene Expression Cancer RNA-Seq Data Set ](https://archive.ics.uci.edu/ml/datasets/gene+expression+cancer+RNA-Seq) 

Source: UCI Repository Archive

This project was made using [Google Colab](https://colab.research.google.com/notebooks/intro.ipynb#recent=true).

## Problem Statement

### What is Gene Expression?

Genes are made up of DNA, and DNA encode proteins or other molecules needed by the body to carry out essential functions. This process by which a cell dictates the formation of requisite molecules of the body on the basis of the genetic code is called gene expression. Gene expression can be measured. 

(Note: The processes explained above are a very low-level description of the actual processes only to help readers who are not from a Life Sciences background to understand the dataset)

### Understanding the Dataset

The dataset contains the gene expression values of 2000+ genes of various cancer patients. There are 2 csv files - data.csv and labels.csv in the dataset.

data.csv  - It contains the gene expression values for a variety of patients suffering from different cancers.Each 'sample' refers to a patient. 


lables.csv - List of samples and the corresponding cancer which that patient is suffering from like BRCA- Breast Cancer, LUAD-Lung Adenocarcinoma, and so on.



## Local Outlier Factor Algorithm         

It is an outlier detection technique which identifies local as well as global outliers.
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
* Logic: Modularised code for calculating the Neighbours in k-neighbourhood, reachability distance, local reachability distance and local outlier factor score for every single sample in the data set.
The LOF algorithm finds a score for each sample based on which outliers are detected in the sample.
* Data Visualisation: Scatter Plot to see identification of Local Outliers

**Inbuilt libraries have only been used for Data Visualisation and Dataframes. No in-built libraries have been used for the implementation of DBSCAN Algorithm, the code is purely for understanding the algorithmic logic.**

## Inference & Use Cases

Outliers in gene expression values could have multiple interpretations, especially in case of cancer. Some interpretations are- 
* Outliers in such a dataset could mean an error in data collection or measurement which if not removed would cause major errors in further analysis. 
* They could also mean a special case seen in Cancer Patients (and usually if you have more outlier tuples like this one, it is definitely investigated) – opens up research avenue.Such information is of vital importance.

[Reference](https://www.longdom.org/open-access/robust-detection-of-outlier-samples-and-genes-in-expression-datasets-jpb-1000387.pdf)

## Contributors

* [Trisha Sarkar](https://github.com/trishasarkar)

## Points to be Noted

* Manhattan distance has been used as the distance metric. I have approached the problem from an algorithmic standpoint, in order to fit any exact use case, domain experts need to carry out the feature selection, choose an appropriate distance metric or even algorithm based on what kind of an output is desired.
* Estimation of Hyper parameters:
1. Estimating k value: A plot of Error rate vs K should be plotted (elbow curve) and the point at the elbow like protrusion of the resulting curve gives us an optimal K value.
But in this case,the gene sequencing dataset does not have any labels and the LOF algorithm also isn't supervised or doesn't involve prediction of classes to which tuples belong. Hence, it wasn't possible to plot it for the given dataset and check.However, using the elbow method, it has been estimated that optimal K value is approximately sqrt(n) where n is the number of tuples in the dataset.[Resource](https://towardsdatascience.com/how-to-find-the-optimal-value-of-k-in-knn-35d936e554eb).So for eg: when df is considered only for BRCA, n=300; therefore K is taken as sqrt(300) which is approximately 17.
2. Estimating a threshold for LOF score: 
This is domain or application specific and needs a domain expert to specify this value. Any other approach couldn't be found at present hence, it has been randomly chosen at 1.5.
