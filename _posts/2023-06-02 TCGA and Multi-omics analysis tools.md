---
title:  "TCGA와 multi-omics analysis tools"
date:   2023-06-02 
categories: [bioinformatics]
tags: [bioinformatics]
---

# TCGA

> This post is based on Das, Tonmoy et al. “Integration of Online Omics-Data Resources for Cancer Research.” *Frontiers in genetics* vol. 11 578345. 23 Oct. 2020
> 

## TCGA

The Cancer Genome Atlas (TCGA)는 

2005년 미국의 NCI와 NHGRI에서 미국 정부의 지원을 통해 시작된

암에 관한 유전변이 데이터를 high-throughput genome analysis technique들을 통해 축적한 프로젝트로,

33 종의 암에 대한 많은 환자들의 omics 데이터를 공개하고 있다. (June, 2023)

공개 중인 데이터들의 omics level은 다음과 같다. 

- Gene expression (mRNA count)
- Single Nucleotide Polymorphism (SNP)
- Copy Numver Variation (CNV)
- DNA methylation_epigenetic
- miRNA
- Exome Sequencing

또한 TCGA 샘플들의 Proteomics 데이터는 별도의 두 개의 프로젝트로 공개되었다. 

CPTCA은 Mass Spectrometry (MS) 방식으로

TCPA는 Reverse Phase Protein Array (RPPA) 방식으로  

 수집된 proteomics 데이터를 공개 중이다. 

두 가지 방식에 대해 비교한 링크를 첨부한다. 

[This or That: RPPA vs Mass Spectrometry vs ELISA](https://theralink.com/blog/rppa-vs-mass-spectrometry-vs-elisa/)

---

## TCGA associative tools

TCGA의 많고 다양한 종류의 데이터를 분석하기 위해 개발된 

공개 프로그램, 데이터베이스 등의 툴들을 소개한다.

GDC 

- data repository of TCGA, TARGET(****Therapeutically Applicable Research to Generate Effective Treatments****), GENIE(genomics evidence neoplasia information exchange)
- Data visualization options
- analysis platform
- survival analysis (Kaplan-Meier survival plot)
- limitation: pan-cancer omics comparison is not possible

Firebrowse

- Download archive file
- Offers various analysis and visualization
- a list of genes that are associated with various status of patient
- correlation between different omic level

cBioPortal

- analysis of multiple data set
- correlation, expression, methylation, co-expression, network analysis
- MutationMapper: 3D protein structure database
- OncoPrinter: intuitive diagrams of genomic alteration
- limitation: lack of omics datasets from tumor adjacent non-tumor(NT)

Driverdb3

- Utilization of published algorithm for driver gene and mutation
- GO, pathway, protein/genetic interaction analysis
    - utilize KEGG, Reactome, PID, Biocarta, MsigDB, miRTar, miRWalk
- limitation: donot offer features to integrate molecular-clinical feature(stage, location)

TCPA

- RPPA data repository
    - can download in firebrowse too
- analysis and visualization related with RPPA data
- protein-drug analysis
- network-visualization module

Regulome Explorer

- interration between clinical and molecular features of TCGA samples
- correlation analysis of genes according to various data/states

GEPIA

- the comparison of expression profile of a gene of normal tissue(GTEx) to corresponding TCGA
- dot polot, body map
- DEG analysis on chromosomal distribution
- correlation, survial analysis, co-expression
- dimensionality reduction (PCA)
- limitation: cannot get processed and normalized omics data of TCGA

UCSC Xena

- exploring TCGA, GDC, ICGC, GTEx, TARGETand PARADIGM pathway inference along with individual study involving multi-omics data
- survival
- tumor vs normal
- relationship among genomic and clinical
- mainly many plots

Wanderer

- interactive viewer to DNA meythylation in TCGA data
- methylation comparison betwenn normal and tumor in a TCGA project

ICGC

- comprehensive repository for cancer-specific multi-omics datasets
- more various countries, races than originial TCGA
- limitation: not all omics data types are available for different population(projects)

## Cancer specific single omics resources

TCGA 이외 암에 대한 single omics level의 데이터를 얻을 수 있는 소스들을 정리한다. 

COSMIC

- the largest source of manually curated catalogs of somatic mutation
- Gene or protein overview (cancer census, hallmark)
- durg resistance
- tissue distribution
- genome browser
- mutation distribution summary
- Variant
- graphical representation of the mutational frequence (COSMIC 3D)
- limitation: cannot integrate mutational dataset to other data type (ex mRNA exp)

Pathology Atlas (Human Protein Atlas)

- in HPA
    - tissue
    - brain
    - single cell
    - tissue cell
    - pathology
    - disease
    - immune cell
    - blood protein
    - subcellular
    - cell line
    - structure
    - metabolic

- Pathology Atlas: analyzing the althered mRNA and protein level in canc er states

## Multi-omics data integration

multi-omics 데이터를 통합 하는 두 가지 방식, horizontal & vertical data integration에 대해 요약하고

개발된 알고리즘, 패키지의 예시들을 소개한다. 

![integration summary](/images/post-images/integration.png)

Horizontal data integration

- integration of single level omics data across different studies
- ex: uncovering diver mutations among different types of tumors
- to investigate the origins of cancerous transformation and the evolution of tumors in terms of clonal and subclonal genomic alteration.
- limitation: cannot explore the effect of genomic aberration events on other omics levels and not  be a suitable to stratifying (階層化）patients and discovering biomarkers

Vertical data integration

- intergration of different types of omics data for the same type of sample
- ex: proteogenomics analysis
- exploration of the multidimensionality of tumor cells in terms of molecular association of multi-omics levels
- possible to identify new molecular features, genotype to phenotype correlation, patient-stratificaiton, and biomarker discovery
1. post-analysis data integration
- analyze  single omics data individually and integrate by focusing on key **overlapping** features
- limitation: hard to the latent multi-modal molecular signatures across different omics level.
1. integrated data analysis
- using specialized algorithms and tools to combine pre-analyzed data sets across different omics platforms
- exploratory tools to generate a new hypothesis or to provide some mechanistic explanation of cancer phenotype.

## Data integration algorithms

1. Network-based
2. Bayesian
3. Fusion-based
4. Similarity-based
5. Correlation-based
6. Multivariate analysis 

Similarity Network Fusion 2014

- network-based
- construction of individual network of patient sample fron each single omics and fusion of the individual networks into single network representing all omics data
- suitable for distinguishing different subtypes of a particular cancer type
- limitation: not be applicapable to identify biomarkers or provide mechanistic insight to cancer phenotype.

[](https://www.nature.com/articles/nmeth.2810)

iOmicsPASS 2019

- network-based
- supervised analysis of quantitative multi-omics data by computing biological interaction scores for the user given network
- identifying the distinct molecular signature and protein markers

[iOmicsPASS: network-based integration of multiomics data for predictive subnetwork discovery](https://www.nature.com/articles/s41540-019-0099-y)

iClusterPlus 2013

- Bayesian information criterion based model selection (clustering)
- Bioconductor

[NCBI - WWW Error Blocked Diagnostic](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3600490/)

Pattern Fusion Anlysis (PFA) 2017

- fusion local sample-patterns originating from each dataset into a global sample-pattern corresponding to phenotypes in an automated manner
- clustering patterns that were similar to SNF and iCluster but with higher clinical prognosis efficiency
- matlab

[Pattern fusion analysis by adaptive alignment of multiple heterogeneous omics data](https://academic.oup.com/bioinformatics/article/33/17/2706/3100314)

NEighborhood Based Multi-Omics Clustering (NEMO) 2019

- Due to their partial nature, the three omics datasets cannot be directly clustered using conventional algorithms rather the clustering must be restricted to a sub-cohort
- NEMO appears to perform clustering analysis that is highly correlated with prognosis using partial multi-omics datasets without imputation or reducing sample numbers

[NCBI - WWW Error Blocked Diagnostic](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6748715/)

Canonical Correlation Analysis (CCA) 2013

- typically used to explore the extent of correlation across copy number, methylation, and gene-expression
- limitaiton: low applicability in distinguishing disease-subtypes and identifying biomarkers.

moCluster  2016

- multivariate analysis based
- identify the latent patterns across DNA methylation, gene expression, and protein expression data
- effective in identifying the latent molecular subtypes