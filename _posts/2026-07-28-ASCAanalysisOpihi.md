---
layout: post
title: ASCA Analysis for ʻopihi RNAseq dataset
date: '2026-07-28'
tags: [ ʻopihi, ASCA, RANseq, DGE ]
---

See [post](https://ahuffmyer.github.io/posts/2025-12-19-asca.html#overview) from Ariana Huffmyer for reference. 

ASCA (ANOVA Simultaneous Component Analysis) is a multivariate approach that combines ANOVA with Principal Component Analysis to identify patterns of variation in high dimensional datasets.   

[Bertinetto et al., 2020](https://doi.org/10.1016/j.acax.2020.100061) provides a tutorial review of ASCA analysis.     
*ASCA analyses are often used in chemistry and chemometirc studies. This paper provides an example of how to perform the anaylsis using a simulated chemical reaction and a second example from a real chemical ecology dataset*   
* Simple example: how do three temperatures, two catalysts affect the yield of the two final products
	* in my RNAseq experiment, the same would be: how do three treatments (control, thermal, desiccation) and shell morphology (could be split into discrete groups but can I use continuous variable for this analysis?) affect gene expression?
	* ASCA would answer the following questions:
		1. What is the effect of temperature (treatment) on yield (gene expression, read counts)?
		2. What is the effect of choosing a different catalyst (shel morphology)?
		3. Is the effect of temperature (treatment) different for each catalyst (morphology) - is there an interaction between the two?
* crossed nature: every level of one factor occurs at least once for every level of another factor
	* these realtionships can be established by combining ANOVA and multivariate analysis 
* ASCA principles
	* data are decomposed according to experimental design
		* single response ANOVA decomposition for all variables
	* PCA is applied to decomposed data
		* examine estimated effects for all variables simultaneously by applying PCA 
		* same construction of biplots applies as in normal PCA
		* bootstrapping confidence intervals for each loading coefficient can help interpret loadings of data with high number of variables and noisy measurements
		* Scaling can influence the result of ASCA and PCA:
			* effect matricies can be scaled with st devs of residual effect matrix to highlight variables with large between-group variance
			* reducing the dimensions of the data may highlight effects attributable to a factor or interaction and take into account within-group correlations
			* scaling with respect to reference group is possible
	* additional corrections for unbalanced data
		* if certain cells (transcripts ?) are over- or under-represented, resulting matrices are not orthogonal to eachother and PCs will not describe the variation solely due to the considered factor
		* sums of squares method as in ANOVA is applied to re-balance
* Statistical significance
	
	


