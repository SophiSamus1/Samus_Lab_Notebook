---
layout: post
title: "Overview of RNA Extractions - ʻopihi RNAseq"
date: '2025-11-29'
tags: [ RNA, Extraction ]
---

| tube | sample | date extracted | 	treatment	 | starting material (mg) | concentration (ng/ul) | extracted twice? | 2nd extraction date | 2nd concentration (ng/ul) |
| ---- | ------ | -------------- | 	---------	 | ---------------------- | --------------------- | ---------------- | ------------------- | ------------------------- |
| 1    | B047   | 11/4/25        | control   	 | 17                     | 11.1                  | no               |					   |						   |
| 15   | B037	| 11/17/25 		 | control   	 | not measured           | 66.8                  | no               |					   |						   |
| 17   | B043	| 11/17/25 		 | control   	 | not measured           | 24.2                  | no               |					   |						   |
| 18   | B033	| 11/17/25 		 | control   	 | not measured           | too high              | no               |					   |						   |
| 21   | B039	| 11/17/25 		 | control   	 | not measured           | 29.2                  | no               |					   |						   |
| 4    | B025   | 11/4/25        | control   	 | 11                     | too low               | yes              | 11/25/25            | too low                   |
| 9    | B048	| 11/17/25 		 | control   	 | not measured           | 28                    | no               |					   |						   |
| 11   | B031	| 11/17/25 		 | control   	 | not measured           | 2.64                  | yes              | 11/25/25            | too low                   |
| 12   | B045	| 11/17/25 		 | thermal   	 | not measured           | 36.0                  | no               |					   |						   |
| 14   | B030	| 11/17/25 		 | thermal   	 | not measured           | 2.02                  | yes              | 11/25/25            | 3.68                      |
| 16   | B050	| 11/17/25 		 | thermal   	 | not measured           | 36.8                  | no               |					   |						   |
| 22   | B042	| 11/17/25 		 | thermal   	 | not measured           | 90.8                  | no               |					   |						   |
| 7    | B040   | 11/4/25        | thermal   	 | 9                      | 2.58                  | yes              | 11/25/25            | 13.5                      |
| 2    | B064   | 11/4/25        | thermal   	 | 13                     | 6.36                  | yes              | 11/25/25            | 1.42                      |
| 3    | B024   | 11/4/25        | thermal   	 | 15                     | 1.34                  | yes              | 11/25/25            | too low                   |
| 5    | B034   | 11/4/25        | thermal   	 | 9                      | too low               | yes              | 11/25/25            | 8.76                      |
| 23   | B063	| 11/17/25 		 |desiccation	 | not measured           | too high              | no               |					   |						   |
| 24   | B026	| 11/17/25 		 |desiccation	 | not measured           | 50.8                  | no               |					   |						   |
| 19   | B032	| 11/17/25 		 |desiccation	 | not measured           | 38.0                  | no               |					   |						   |
| 20   | B049	| 11/17/25 		 |desiccation	 | not measured           | 81.2                  | no               |					   |						   |
| 13   | B046	| 11/17/25 		 |desiccation	 | not measured           | 81.8                  | no               |					   |						   |
| 10   | B044	| 11/17/25 		 |desiccation	 | not measured           | 65.6                  | no               |					   |						   |
| 6    | B038   | 11/4/25        |desiccation	 | 15                     | 27.2                  | no               |					   |						   |
| 8    | B041   | 11/4/25        |desiccation	 | 8                      | 3.34                  | yes              | 11/25/25            | 2.46                      |


![concentration boxplot](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/concentration_final_boxplot.png?raw=true)

### Range, average and median concentrations per treatment

| treatment  | concentration range 		  | concentration mean | concentration median |
| ---------- | -------------------------- | ------------------ | -------------------- |
| control	 |0 (too low) - 100 (too high)| 32.74			   | 26.1 				  |
| thermal	 |1.34 - 90.8 				  | 24.66			   | 11.13 				  |
| desiccation|3.34 - 100 (too high)		  | 55.99			   | 58.2 				  |

### Average overall concentration is 37.8 ng/ul


![concentration hist](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/RNAconcentrationHist.png?raw=true)

## Control

| tube | sample | date extracted | 	treatment	 | concentration (ng/ul) | keep? |
| ---- | ------ | -------------- | 	---------	 | --------------------- | ----- |
| 1    | B047   | 11/4/25        | control   	 | 11.1                  | yes   |
| 15   | B037	| 11/17/25 		 | control   	 | 66.8                  | yes   |
| 17   | B043	| 11/17/25 		 | control   	 | 24.2                  | yes   |
| 18   | B033	| 11/17/25 		 | control   	 | too high              | yes   |
| 21   | B039	| 11/17/25 		 | control   	 | 29.2                  | yes   |
| 4    | B025   | 11/4/25        | control   	 | too low               |  no   |
| 9    | B048	| 11/17/25 		 | control   	 | 28                    | yes   |
| 11   | B031	| 11/17/25 		 | control   	 | 2.64                  | maybe |

### 6 yes, 1 no, 1 maybe

## Thermal

| tube | sample | date extracted | 	treatment	 | concentration (ng/ul) | keep? |
| ---- | ------ | -------------- | 	---------	 | --------------------- | ----- |
| 12   | B045	| 11/17/25 		 | thermal   	 | 36.0                  | yes   |
| 14   | B030	| 11/17/25 		 | thermal   	 | 3.68                  | maybe |
| 16   | B050	| 11/17/25 		 | thermal   	 | 36.8                  | yes   |
| 22   | B042	| 11/17/25 		 | thermal   	 | 90.8                  | yes   |
| 7    | B040   | 11/4/25        | thermal   	 | 13.5                  | yes   |
| 2    | B064   | 11/4/25        | thermal   	 | 6.36                  | yes   |
| 3    | B024   | 11/4/25        | thermal   	 | 1.34                  | maybe |
| 5    | B034   | 11/4/25        | thermal   	 | 8.76	                 | yes   |

### 6 yes, 2 maybe

## Desiccation

| tube | sample | date extracted | 	treatment	 | concentration (ng/ul) | keep? |
| ---- | ------ | -------------- | 	---------	 | --------------------- | ----- |
| 23   | B063	| 11/17/25 		 |desiccation	 | too high              | yes   |
| 24   | B026	| 11/17/25 		 |desiccation	 | 50.8                  | yes   |
| 19   | B032	| 11/17/25 		 |desiccation	 | 38.0                  | yes   |
| 20   | B049	| 11/17/25 		 |desiccation	 | 81.2                  | yes   |
| 13   | B046	| 11/17/25 		 |desiccation	 | 81.8                  | yes   |
| 10   | B044	| 11/17/25 		 |desiccation	 | 65.6                  | yes   |
| 6    | B038   | 11/4/25        |desiccation	 | 27.2                  | yes   |
| 8    | B041   | 11/4/25        |desiccation	 | 3.34                  |  no   |

### 7 yes, 1 no


If we use samples 1,2,5,6,7,9,10,12,13,15,16,17,18,20,21,22,23,24: 

![small hist](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/smallhist.png?raw=true)

![small boxplot](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/smallboxplot.png?raw=true)

Maybe do all libraries and QC then decide before seq?



# Notes on limpet genomes/transcriptomes

* *Patella caerula* genome > 700 Mp, ~24,000 protein coding genes
	* https://doi.org/10.1093/gbe/evae070
* *Cellana rota* RNAseq - 24 sampling points x 5 limpets = 120 samples
	* total of 311,558,569 raw equencing reads / 120 = 2,596,321.41 reads per sample
	* after trimming and QC = 108,167,257 paired-end high quality reads used for trinity assembly
Schnytzer, Y., Simon-Blecher, N., Li, J. et al. Tidal and diel orchestration of behaviour and gene expression in an intertidal mollusc. Sci Rep 8, 4917 (2018). https://doi.org/10.1038/s41598-018-23167-y
* deep sea limpet *Bathyacmaea lactea* 
	* 27,674 transcripts from 648,458,172 reads from 7 individuals = 92,636,881.7 reads per individual
	* https://www.cell.com/iscience/fulltext/S2589-0042(22)00362-5
* *Patella ulyssiponensis* 44.63 million total reads, 6.74 Gb (base count total)
	* mRNA libraries, concentration of 2.8 nM, diluted to 150 pM for loading. NovaSeq 6000  generated 150 bp PE reads
	* https://pmc.ncbi.nlm.nih.gov/articles/PMC12405849/#T1
* marine snail *Crepidula navicella* https://onlinelibrary.wiley.com/doi/abs/10.1002/jez.b.22674
	* three pooled samples each of embryos from four different adult females (6 total samples) on two lanes of Illumina HiSeq = 290,359,312 raw reads, 60,765,730 high quality reads for assembly
	* 290,359,312 / 6 = 48,393,218.7 reads per sample






