---
layout: post
title: ASCA Analysis for ʻopihi RNAseq dataset
date: '2026-07-28'
tags: [ ʻopihi, ASCA, RANseq, DGE ]
---

See [post](https://ahuffmyer.github.io/posts/2025-12-19-asca.html#overview) from Ariana Huffmyer for reference. 

ASCA (ANOVA Simultaneous Component Analysis) is a multivariate approach that combines ANOVA with Principal Component Analysis to identify patterns of variation in high dimensional datasets.   

[Bertinetto et al., 2020](https://doi.org/10.1016/j.acax.2020.100061) provides a tutorial review of ASCA analysis.     
*ASCA analyses are often used in chemistry and chemometric studies. This paper provides an example of how to perform the anaylsis using a simulated chemical reaction and a second example from a real chemical ecology dataset*   

<details>
<summary>Notes</summary>
	
* test        
	
- Simple example: how do three temperatures, two catalysts affect the yield of the two final products      
	- in my RNAseq experiment, the same would be: how do three treatments (control, thermal, desiccation) and shell morphology (could be split into discrete groups but can I use continuous variable for this analysis?) affect gene expression?       
	- ASCA would answer the following questions:     
		1. What is the effect of temperature (treatment) on yield (gene expression, read counts)?      
		2. What is the effect of choosing a different catalyst (shel morphology)?       
		3. Is the effect of temperature (treatment) different for each catalyst (morphology) - is there an interaction between the two?       
- crossed nature: every level of one factor occurs at least once for every level of another factor       
	- these realtionships can be established by combining ANOVA and multivariate analysis        
- ASCA principles        
	- data are decomposed according to experimental design       
		- single response ANOVA decomposition for all variables      
	- PCA is applied to decomposed data     
		- examine estimated effects for all variables simultaneously by applying PCA     
		- same construction of biplots applies as in normal PCA    
		- bootstrapping confidence intervals for each loading coefficient can help interpret loadings of data with high number of variables and noisy measurements      
		- Scaling can influence the result of ASCA and PCA:     
			- effect matrices can be scaled with st devs of residual effect matrix to highlight variables with large between-group variance     
			- reducing the dimensions of the data may highlight effects attributable to a factor or interaction and take into account within-group correlations     
			- scaling with respect to reference group is possible     
	- additional corrections for unbalanced data    
		- if certain cells (transcripts ?) are over- or under-represented, resulting matrices are not orthogonal to eachother and PCs will not describe the variation solely due to the considered factor      
		- sums of squares method as in ANOVA is applied to re-balance      
- Statistical significance     
	- significant effects are defined as those for which a clear difference is observed in at least one of the levels     
	- common significance testing involves resampling methods like bootstrap and permutation     
		- bootstrapping substitutes samples with repetitions of others in the same dataset and allows you to determine the significance of the whole model and confidence intervals for scores and loading parameters which help determine with response variables are significant     
		- permutation tests randomly permute the factor levels and recalculate the level-mean differences every time. This creates a null distribution to compare to the real model     
		

</details>



<details>
<summary>How do I dropdown?</summary>
<br>
This is how you dropdown.   

*Does this work
</details>


<details>

<summary>Tips for collapsed sections</summary>

### You can add a header

You can add text within a collapsed section.

You can add an image or a code block, too.

```ruby
   puts "Hello World"
```

* but why cant I add bullet points

</details>


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
			* effect matrices can be scaled with st devs of residual effect matrix to highlight variables with large between-group variance
			* reducing the dimensions of the data may highlight effects attributable to a factor or interaction and take into account within-group correlations
			* scaling with respect to reference group is possible
	* additional corrections for unbalanced data
		* if certain cells (transcripts ?) are over- or under-represented, resulting matrices are not orthogonal to eachother and PCs will not describe the variation solely due to the considered factor
		* sums of squares method as in ANOVA is applied to re-balance
* Statistical significance
	* significant effects are defined as those for which a clear difference is observed in at least one of the levels
	* common significance testing involves resampling methods like bootstrap and permutation
		* bootstrapping substitutes samples with repetitions of others in the same dataset and allows you to determine the significance of the whole model and confidence intervals for scores and loading parameters which help determine with response variables are significant
		* permutation tests randomly permute the factor levels and recalculate the level-mean differences every time. This creates a null distribution to compare to the real model

	
	
[Nueda et al., 2007](https://doi.org/10.1093/bioinformatics/btm251) uses ASCA for microarray experiments.   



