# Cardiac cis-regulatory elements predictor
## Description
A pipeline for predicting cis-regulatory elements (CREs) in heart development and diseases

Code for the manuscript: Louis Dang, Harshini Thiyagarajah, Hieu T. Nim, Tennille Sibbritt, Nicolas Fossat, Richard Burke, Patrick P. L. Tam, Coral G. Warr*, Travis K. Johnson*, Mirana Ramialison*. "Predicting  genes essential for heart development irrespective of their spatial expression pattern".

Languages: Bash, Perl, Python.
Operating systems: Windows, Linux, Mac OSX. 
Fully tested on Linux Ubuntu 20.04. 

## Getting the Source Code

To get the source code, please click the "fork" button in the upper-right and then add this repo as an upstream source:

````
$ git clone <your_fork_of_the_repo> ppds
$ cd ppds
$ REPO=https://github.com/nimt0001/CardiacRegulatoryElementsPredictor.git
$ git remote add upstream $REPO
````

To get new content, use 
````
$ git pull upstream master 
````

Usage:

```text
1. Calculating histone marks subsets between different ChIP-Seq files. 
Usage: python3 LD_getSubsets.py [INPUT_FILES] [OPTIONS]... >> [OUTPUT_DIR}

Input filess:
  BED file format, each separated by a space
  
Options:
  --help                  Show this message and exit.

Output directory:
  A directory path where the output BED files are deposited

2. Screening GREAT output file for cardiac-specific gene candidates. 
Usage: perl compare_GREAT_genes.pl [INPUT_FILE] [OPTIONS]... >> [OUTPUT_FILE]

Input file:
  TXT (tab-separated) file format, the output files from GREAT database
  
Options:
  --help                  Show this message and exit.

Output file:
  TXT (tab-separated) file format, containing the predicted cardiac-specific genes
  
```


## An example execution of the pipeline

### Step 1 (Python) - Calculating all the CREs between the organs and their overlaps

````
$ cd data/h3k4me1
$ python3 ../../scripts/LD_getSubsets.py H3K4me1Heartmm9E14halfEncodeLicr.bed H3K4me1Limbmm9E14halfEncodeLicr.bed H3K4me1Livermm9E14halfEncodeLicr.bed H3K4me1Wbrainmm9E14halfEncodeLicr.bed ../../out/
$ cd ../h3k4me3
$ python3 ../../scripts/LD_getSubsets.py H3K4me3Heartmm9UE14halfEncodeLicr.bed H3K4me3Limbmm9UE14halfEncodeLicr.bed H3K4me3Livermm9UE14halfEncodeLicr.bed H3K4me3Wbrainmm9UE14halfEncodeLicr.bed ../../out/
$ cd ../h3k27ac
$ python3 ../../scripts/LD_getSubsets.py H3K27acHeartmm9UE14halfEncodeLicr.bed H3K27acLimbmm9UE14halfEncodeLicr.bed H3K27acLivermm9UE14halfEncodeLicr.bed H3K27acWbrainmm9UE14halfEncodeLicr.bed ../../out/

````

### Step 2: Use GREAT database to map the CREs to the associated genes
The steps for associating CREs to genes using GREAT database (http://great.stanford.edu/great/public-3.0.0/html/) are as below.
#### GREAT - Screenshot 1 
![GREAT-Screenshot1](https://raw.githubusercontent.com/nimt0001/CardiacRegulatoryElementsPredictor/main/images/GREAT-screenshot1.png)

#### GREAT - Screenshot 2
![GREAT-Screenshot2](https://raw.githubusercontent.com/nimt0001/CardiacRegulatoryElementsPredictor/main/images/GREAT-screenshot2.png)

#### GREAT - Screenshot 3
![GREAT-Screenshot3](https://raw.githubusercontent.com/nimt0001/CardiacRegulatoryElementsPredictor/main/images/GREAT-screenshot3.png)


### Step 3 (Perl): Process GREAT output files to produce heart-specific gene candidates
````
$ perl scripts/compare_GREAT_genes.pl data/great_output/enhancer_promoters_heart_only.txt >> out/enhancer_promoters_heart_only_expressed.txt
$ perl scripts/compare_GREAT_genes.pl data/great_output/enhancers_heart_only.txt >> out/enhancers_heart_only_expressed.txt
$ perl scripts/compare_GREAT_genes.pl data/great_output/promoters_heart_only.txt >> out/promoters_heart_only_expressed.txt
$ perl scripts/compare_GREAT_genes.pl data/great_output/enhancer_promoters_ubiquitous.txt >> out/enhancer_promoters_ubiquitous_expressed.txt

````

## Additional analyses: network analyses with STRING-db and Cytoscape 
### STRING-db (https://string-db.org)
Input: network_analysis/163_heart_enhancer_promoter_genes.txt 

Output: network_analysis/string_interactions.tsv

#### STRING-db - Screenshot 1 
![STRING-db-Screenshot1](https://github.com/nimt0001/CardiacRegulatoryElementsPredictor/raw/main/images/STRING-DB-Screenshot1.png)
#### STRING-db - Screenshot 2
![STRING-db-Screenshot2](https://github.com/nimt0001/CardiacRegulatoryElementsPredictor/raw/main/images/STRING-DB-Screenshot2.png)
#### STRING-db - Screenshot 3
![STRING-db-Screenshot3](https://github.com/nimt0001/CardiacRegulatoryElementsPredictor/raw/main/images/STRING-DB-Screenshot3.png)
### Cytoscape (https://cytoscape.org) 

Input: network_analysis/string_interactions.tsv (File -> Import -> Network from file)

#### Cytoscape - Screenshot 1 
![Cytoscape-Screenshot1](https://github.com/nimt0001/CardiacRegulatoryElementsPredictor/raw/main/images/Cytoscape-Screenshot1.png)
#### Cytoscape - Screenshot 2 
![Cytoscape-Screenshot2](https://github.com/nimt0001/CardiacRegulatoryElementsPredictor/raw/main/images/Cytoscape-Screenshot2.png)
#### Cytoscape - Screenshot 3 
![Cytoscape-Screenshot3](https://github.com/nimt0001/CardiacRegulatoryElementsPredictor/raw/main/images/Cytoscape-Screenshot3.png)
