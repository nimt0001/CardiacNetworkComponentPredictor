# Cardiac cis-regulatory elements predictor
## Description
A pipeline for predicting cis-regulatory elements (CREs) in heart development and diseases

Code for the manuscript: Louis Dang, Harshini Thiyagarajah, Hieu T. Nim, Tennille Sibbritt, Nicolas Fossat, Richard Burke, Patrick P. L. Tam, Coral G. Warr*, Travis K. Johnson*, Mirana Ramialison*. "Predicting  genes essential for heart development irrespective of their spatial expression pattern".

Languages: Bash, Perl, Python
Operating systems: Windows, Linux, Mac OSX. Fully tested on Linux Ubuntu 20.04. 

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

To execute the code 
````
$ git pull upstream master 
````

## An example script to run the pipeline

Calculating all the CREs between the organs and their overlaps

````
$ #!/bin/bash
$ cd ../001_raw_histone_data/h3k4me1
$ python3 ../../000_scripts/HN_LD_getSubsets.py H3K4me1Heartmm9E14halfEncodeLicr.bed H3K4me1Limbmm9E14halfEncodeLicr.bed H3K4me1Livermm9E14halfEncodeLicr.bed H3K4me1Wbrainmm9E14halfEncodeLicr.bed ../../000_scripts/out/
$ cd ../h3k4me3
$ python3 ../../000_scripts/HN_LD_getSubsets.py H3K4me3Heartmm9UE14halfEncodeLicr.bed H3K4me3Limbmm9UE14halfEncodeLicr.bed H3K4me3Livermm9UE14halfEncodeLicr.bed H3K4me3Wbrainmm9UE14halfEncodeLicr.bed ../../000_scripts/out/
$ cd ../h3k27ac
$ python3 ../../000_scripts/HN_LD_getSubsets.py H3K27acHeartmm9UE14halfEncodeLicr.bed H3K27acLimbmm9UE14halfEncodeLicr.bed H3K27acLivermm9UE14halfEncodeLicr.bed H3K27acWbrainmm9UE14halfEncodeLicr.bed ../../000_scripts/out/

````

Use GREAT database to map the CREs to the associated genes
````
$ #TODO: SOCKET CONNECTION TO GREAT etc. 
````

Use GREAT database to map the CREs to the associated genes
````
$ cd ../../000_scripts
$ perl compare_GREAT_genes.pl ../003_GREAT_data/001_output/001_heart_enhancer_genes.txt >> out/001_heart_enhancer_genes.txt
$ perl compare_GREAT_genes.pl ../003_GREAT_data/001_output/001_heart_promoter_genes.txt >> out/001_heart_promoter_genes.txt
$ perl compare_GREAT_genes.pl ../003_GREAT_data/001_output/001_ubiquitous_enhancer_genes.txt >> out/001_ubiquitous_enhancer_genes.txt
$ perl compare_GREAT_genes.pl ../003_GREAT_data/001_output/001_ubiquitous_promoter_genes.txt >> out/001_ubiquitous_promoter_genes.txt

````
