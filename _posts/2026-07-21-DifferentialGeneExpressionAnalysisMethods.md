---
layout: post
title: Differential Gene Expression Analysis - ʻopihi
date: '2026-07-06'
tags: [ ʻopihi, Gene Expression, R, DGE ]
---

Differential gene expression analysis requires the following R packages:    
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)

library(dplyr)
library(tidyr)
#install.packages("textshape")
library(textshape)

#setwd("~/Desktop/Thesis")

if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

#BiocManager::install("tximport")
#library(BiocManager)

#browseVignettes("tximport")
#library(tximport)

#if(!require("BiocManager", quietly = TRUE))
  #install.packages("BiocManager")
BiocManager::install("edgeR")
BiocManager::install("DESeq2")
library(DESeq2)
library(edgeR)

library(gplots)
library(factoextra)

```

The output of RSEM are genes.results files with transcript counts in TPM and FPKM. These are used to create a round count matrix.   

```{r import results files}

B026 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B026_t3.genes.results", header = T, sep = "\t")
#write.csv(B026, "CellanaExarataRNAseq/RSEM_trim3/B026_t3.genes.csv", row.names = F)

B030 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B030_t3.genes.results", header = T, sep = "\t")
#write.csv(B030, "CellanaExarataRNAseq/RSEM_trim3/B030_t3.genes.csv", row.names = F)

B033 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B033_t3.genes.results", header = T, sep = "\t")
#write.csv(B033, "CellanaExarataRNAseq/RSEM_trim3/B033_t3.genes.csv", row.names = F)

B034 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B034_t3.genes.results", header = T, sep = "\t")
#write.csv(B034, "CellanaExarataRNAseq/RSEM_trim3/B034_t3.genes.csv", row.names = F)

B037 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B037_t3.genes.results", header = T, sep = "\t")
#write.csv(B037, "CellanaExarataRNAseq/RSEM_trim3/B037_t3.genes.csv", row.names = F)

B038 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B038_t3.genes.results", header = T, sep = "\t")
#write.csv(B038, "CellanaExarataRNAseq/RSEM_trim3/B038_t3.genes.csv", row.names = F)

B039 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B039_t3.genes.results", header = T, sep = "\t")
#write.csv(B039, "CellanaExarataRNAseq/RSEM_trim3/B039_t3.genes.csv", row.names = F)

B040 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B040_t3.genes.results", header = T, sep = "\t")
#write.csv(B040, "CellanaExarataRNAseq/RSEM_trim3/B040_t3.genes.csv", row.names = F)

B042 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B042_t3.genes.results", header = T, sep = "\t")
#write.csv(B042, "CellanaExarataRNAseq/RSEM_trim3/B042_t3.genes.csv", row.names = F)

B043 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B043_t3.genes.results", header = T, sep = "\t")
#write.csv(B043, "CellanaExarataRNAseq/RSEM_trim3/B043_t3.genes.csv", row.names = F)

B044 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B044_t3.genes.results", header = T, sep = "\t")
#write.csv(B044, "CellanaExarataRNAseq/RSEM_trim3/B044_t3.genes.csv", row.names = F)

B045 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B045_t3.genes.results", header = T, sep = "\t")
#write.csv(B045, "CellanaExarataRNAseq/RSEM_trim3/B045_t3.genes.csv", row.names = F)

B046 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B046_t3.genes.results", header = T, sep = "\t")
#write.csv(B046, "CellanaExarataRNAseq/RSEM_trim3/B046_t3.genes.csv", row.names = F)

B047 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B047_t3.genes.results", header = T, sep = "\t")
#write.csv(B047, "CellanaExarataRNAseq/RSEM_trim3/B047_t3.genes.csv", row.names = F)

B048 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B048_t3.genes.results", header = T, sep = "\t")
#write.csv(B048, "CellanaExarataRNAseq/RSEM_trim3/B048_t3.genes.csv", row.names = F)

B049 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B049_t3.genes.results", header = T, sep = "\t")
#write.csv(B049, "CellanaExarataRNAseq/RSEM_trim3/B049_t3.genes.csv", row.names = F)

B050 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B050_t3.genes.results", header = T, sep = "\t")
#write.csv(B050, "CellanaExarataRNAseq/RSEM_trim3/B050_t3.genes.csv", row.names = F)

B063 <- read.table("CellanaExarataRNAseq/RSEM_trim3/B063_t3.genes.results", header = T, sep = "\t")
#write.csv(B063, "CellanaExarataRNAseq/RSEM_trim3/B063_t3.genes.csv", row.names = F)

```

combine all into one read matrix using FPKM   

```{r create read count matrix-FPKM}
B026counts <- B026[,c(2,7)]
B030counts <- B030[,c(2,7)]
B033counts <- B033[,c(2,7)]
B034counts <- B034[,c(2,7)]
B037counts <- B037[,c(2,7)]
B038counts <- B038[,c(2,7)]
B039counts <- B039[,c(2,7)]
B040counts <- B040[,c(2,7)]
B042counts <- B042[,c(2,7)]
B043counts <- B043[,c(2,7)]
B044counts <- B044[,c(2,7)]
B045counts <- B045[,c(2,7)]
B046counts <- B046[,c(2,7)]
B047counts <- B047[,c(2,7)]
B048counts <- B048[,c(2,7)]
B049counts <- B049[,c(2,7)]
B050counts <- B050[,c(2,7)]
B063counts <- B063[,c(2,7)]

B026counts <- column_to_rownames(B026counts, "transcript_id.s.")
colnames(B026counts) <- "B026"

B030counts <- column_to_rownames(B030counts, "transcript_id.s.")
colnames(B030counts) <- "B030"

B033counts <- column_to_rownames(B033counts, "transcript_id.s.")
colnames(B033counts) <- "B033"

B034counts <- column_to_rownames(B034counts, "transcript_id.s.")
colnames(B034counts) <- "B034"

B037counts <- column_to_rownames(B037counts, "transcript_id.s.")
colnames(B037counts) <- "B037"

B038counts <- column_to_rownames(B038counts, "transcript_id.s.")
colnames(B038counts) <- "B038"

B039counts <- column_to_rownames(B039counts, "transcript_id.s.")
colnames(B039counts) <- "B039"

B040counts <- column_to_rownames(B040counts, "transcript_id.s.")
colnames(B040counts) <- "B040"

B042counts <- column_to_rownames(B042counts, "transcript_id.s.")
colnames(B042counts) <- "B042"

B043counts <- column_to_rownames(B043counts, "transcript_id.s.")
colnames(B043counts) <- "B043"

B044counts <- column_to_rownames(B044counts, "transcript_id.s.")
colnames(B044counts) <- "B044"

B045counts <- column_to_rownames(B045counts, "transcript_id.s.")
colnames(B045counts) <- "B045"

B046counts <- column_to_rownames(B046counts, "transcript_id.s.")
colnames(B046counts) <- "B046"

B047counts <- column_to_rownames(B047counts, "transcript_id.s.")
colnames(B047counts) <- "B047"

B048counts <- column_to_rownames(B048counts, "transcript_id.s.")
colnames(B048counts) <- "B048"

B049counts <- column_to_rownames(B049counts, "transcript_id.s.")
colnames(B049counts) <- "B049"

B050counts <- column_to_rownames(B050counts, "transcript_id.s.")
colnames(B050counts) <- "B050"

B063counts <- column_to_rownames(B063counts, "transcript_id.s.")
colnames(B063counts) <- "B063"

readcountsFPKM <- cbind(B026counts, B030counts, B033counts, B034counts, B037counts, 
                    B038counts, B039counts, B040counts, B042counts, B043counts, 
                    B044counts, B045counts, B046counts, B047counts, B048counts, 
                    B049counts, B050counts, B063counts)

# this is the read count matrix using FPKM values!!
```

combine all into one read matrix using TPM   

```{r create read count matrix-TPM}
B026counts <- B026[,c(2,6)]
B030counts <- B030[,c(2,6)]
B033counts <- B033[,c(2,6)]
B034counts <- B034[,c(2,6)]
B037counts <- B037[,c(2,6)]
B038counts <- B038[,c(2,6)]
B039counts <- B039[,c(2,6)]
B040counts <- B040[,c(2,6)]
B042counts <- B042[,c(2,6)]
B043counts <- B043[,c(2,6)]
B044counts <- B044[,c(2,6)]
B045counts <- B045[,c(2,6)]
B046counts <- B046[,c(2,6)]
B047counts <- B047[,c(2,6)]
B048counts <- B048[,c(2,6)]
B049counts <- B049[,c(2,6)]
B050counts <- B050[,c(2,6)]
B063counts <- B063[,c(2,6)]

B026counts <- column_to_rownames(B026counts, "transcript_id.s.")
colnames(B026counts) <- "B026"

B030counts <- column_to_rownames(B030counts, "transcript_id.s.")
colnames(B030counts) <- "B030"

B033counts <- column_to_rownames(B033counts, "transcript_id.s.")
colnames(B033counts) <- "B033"

B034counts <- column_to_rownames(B034counts, "transcript_id.s.")
colnames(B034counts) <- "B034"

B037counts <- column_to_rownames(B037counts, "transcript_id.s.")
colnames(B037counts) <- "B037"

B038counts <- column_to_rownames(B038counts, "transcript_id.s.")
colnames(B038counts) <- "B038"

B039counts <- column_to_rownames(B039counts, "transcript_id.s.")
colnames(B039counts) <- "B039"

B040counts <- column_to_rownames(B040counts, "transcript_id.s.")
colnames(B040counts) <- "B040"

B042counts <- column_to_rownames(B042counts, "transcript_id.s.")
colnames(B042counts) <- "B042"

B043counts <- column_to_rownames(B043counts, "transcript_id.s.")
colnames(B043counts) <- "B043"

B044counts <- column_to_rownames(B044counts, "transcript_id.s.")
colnames(B044counts) <- "B044"

B045counts <- column_to_rownames(B045counts, "transcript_id.s.")
colnames(B045counts) <- "B045"

B046counts <- column_to_rownames(B046counts, "transcript_id.s.")
colnames(B046counts) <- "B046"

B047counts <- column_to_rownames(B047counts, "transcript_id.s.")
colnames(B047counts) <- "B047"

B048counts <- column_to_rownames(B048counts, "transcript_id.s.")
colnames(B048counts) <- "B048"

B049counts <- column_to_rownames(B049counts, "transcript_id.s.")
colnames(B049counts) <- "B049"

B050counts <- column_to_rownames(B050counts, "transcript_id.s.")
colnames(B050counts) <- "B050"

B063counts <- column_to_rownames(B063counts, "transcript_id.s.")
colnames(B063counts) <- "B063"

readcountsTPM <- cbind(B026counts, B030counts, B033counts, B034counts, B037counts, 
                    B038counts, B039counts, B040counts, B042counts, B043counts, 
                    B044counts, B045counts, B046counts, B047counts, B048counts, 
                    B049counts, B050counts, B063counts)

# this is the read count matrix using TPM values!!
```

import file with associated metadata (treatment, temperature, etc. See [here](https://sophisamus1.github.io/Samus_Lab_Notebook/CellanaExarataStressTrials/))   

```{r metadata}

CEmetadata <- read.csv("DGE/CEmetadata.csv")
View(CEmetadata)

CEmetadata <- column_to_rownames(CEmetadata, loc = "sample")

```

DDS Variance stabilizing transformation   

```{r dds and VST}

dds <- DESeqDataSetFromMatrix(countData = round(readcountsFPKM),
                              colData = CEmetadata,
                              design = ~treatment)

# vst transformed matrix

dds_vst <- vst(dds)
dds_vst_counts <- assay(dds_vst)
dds_vst_counts

# get top 500 most variable genes to use for clustering

top500 <- apply(dds_vst_counts, 1, FUN = var)
top500 <- sort(top500, decreasing = T)
top500 <- top500[1:500]
top500names <- names(top500)

dds_vst_counts <- as.data.frame(dds_vst_counts)
top500.VST <- dds_vst_counts[top500names,]
top500.VST <- as.matrix(top500.VST) # has to be matrix for heatmap.2

```

create heatmaps to visualize clustering (see [here](https://sophisamus1.github.io/Samus_Lab_Notebook/OpihiGeneExpressionResults/) for results)   

```{r heatmaps}

palette.g <- hcl.colors(100, palette = "RdBu")

# this will cluster based on average expression
heatmap.2(top500.VST, trace = "none",
          col = palette.g, scale = "none")

# to color based on treatment - blue is control, coral is thermal, yellow is desiccation
treatment_colors <- rep("steelblue", 18)
treatment_colors[CEmetadata$treatment == "thermal"] <- "coral1"
treatment_colors[CEmetadata$treatment == "desiccation"] <- "yellow"

heatmap.2(top500.VST, trace = "none",
          col = palette.g, scale = "row",
          ColSideColors = treatment_colors,
          cexRow = 0.5, cexCol = 0.65)

```

PCA (see results [here](https://sophisamus1.github.io/Samus_Lab_Notebook/OpihiGeneExpressionResults/))   

```{r PCA}

pca <- prcomp(t(top500.VST))
scores <- pca$x
dim(scores)
head(scores)

scores[,1]
CEmetadata$treatment

#library(ggfortify)
#autoplot(pca, data = CEmetadata, colour = "treatment")

# does PC1 correlate with treatment?
plot(scores[,1] ~factor(CEmetadata$treatment),
     col = "purple", pch =20,
     xlab = "Treatment", ylab = "PC1 scores")

# clustering based on treatment?
fviz_pca_ind(pca, axes = c(1,2),
             col.ind = CEmetadata$treatment,
             label = "none")

# look at eigen vectors

fviz_eig(pca) # scree plot

#loadings <- pca$rotation
#dim(loadings)
#head(loadings)

```

### Differential Gene Expression Analysis   

There are three treatments: thermal, desiccation, and control. I can only compare two at a time.   

Here is how I compared gene expression between thermal and control groups:   
```{r DGE analysis - thermal:control}

#reminder, dds <- DESeqDataSetFromMatrix(countData = round(readcounts), colData = CEmetadata, design = ~treatment)

deseq2_result <- DESeq(dds)

results_clean <- results(deseq2_result,
                         contrast = c("treatment", "thermal", "control"))
# contrast: treatment is the factor in design formula, thermal is the numerator for fold change, control is the denominator
head(results_clean)
# cols are: mean read count corrected for library size, log2FC (thermal-control), SE, stat (not important), raw p-value for Wald test, p-adjusted with BH

# p-adj with NA are genes that have low expression, remove them like this:
results_clean <- results_clean[complete.cases(results_clean),]
head(results_clean)

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 1312
sum(results_clean$padj < 0.05)
# 169

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 146
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 23


# volcano plots
colours <- rep("steelblue", dim(results_clean)[1])
colours[results_clean$padj < 0.05] <- "salmon"

plot(-log(padj) ~ log2FoldChange, data = results_clean,
     pch = 20, col = colours,
     ylab = "-ln of adjusted p", xlab = "L2FC",
     xlim = c(-15,15), ylim = c(0,20))
abline(h = -log(0.05), col = "black", lwd = 2, lty = 2)
abline(v = 0, col = "black", lwd = 2, lty = 2)
# use the negative log in plot to see smaller p-values (more significant)

# top right quadrant = significantly upregulated genes
# bottom left = downregulated, not significant
# top left = significant downregulation
# bottom right = upregulated, not significant

```
*see volcano plot results [here](https://sophisamus1.github.io/Samus_Lab_Notebook/OpihiGeneExpressionResults/)*    

Here is how I compared gene expression between desiccation and control groups:   
```{r DGE analysis - desiccation:control}

#reminder, dds <- DESeqDataSetFromMatrix(countData = round(readcounts), colData = CEmetadata, design = ~treatment)

#deseq2_result <- DESeq(dds)

results_clean <- results(deseq2_result,
                         contrast = c("treatment", "desiccation", "control"))
# contrast: treatment is the factor in design formula, thermal is the numerator for fold change, control is the denominator
head(results_clean)
# cols are: mean read count corrected for library size, log2FC (thermal-control), SE, stat (not important), raw p-value for Wald test, p-adjusted with BH

# p-adj with NA are genes that have low expression, remove them like this:
results_clean <- results_clean[complete.cases(results_clean),]
head(results_clean)

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 932 -> 645 -> 952 -> 602
sum(results_clean$padj < 0.05)
# 29 -> 109 -> 132 -> 52

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 22 -> 88 -> 106 -> 35
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 7 -> 21 -> 26 -> 17


# volcano plots
colours <- rep("steelblue", dim(results_clean)[1])
colours[results_clean$padj < 0.05] <- "salmon"

plot(-log(padj) ~ log2FoldChange, data = results_clean,
     pch = 20, col = colours,
     ylab = "-ln of adjusted p", xlab = "L2FC",
     xlim = c(-15,15), ylim = c(0,20))
abline(h = -log(0.05), col = "black", lwd = 2, lty = 2)
abline(v = 0, col = "black", lwd = 2, lty = 2)
# use the negative log in plot to see smaller p-values (more significant)

# top right quadrant = significantly upregulated genes
# bottom left = downregulated, not significant
# top left = significant downregulation
# bottom right = upregulated, not significant

```
*see volcano plot results [here](https://sophisamus1.github.io/Samus_Lab_Notebook/OpihiGeneExpressionResults/)*   

Here is how I compared gene expression between desiccation and thermal groups:    
```{r DGE analysis - desiccation:thermal}

#reminder, dds <- DESeqDataSetFromMatrix(countData = round(readcounts), colData = CEmetadata, design = ~treatment)

#deseq2_result <- DESeq(dds)

results_clean <- results(deseq2_result,
                         contrast = c("treatment", "desiccation", "thermal"))
# contrast: treatment is the factor in design formula, thermal is the numerator for fold change, control is the denominator
head(results_clean)
# cols are: mean read count corrected for library size, log2FC (thermal-control), SE, stat (not important), raw p-value for Wald test, p-adjusted with BH

# p-adj with NA are genes that have low expression, remove them like this:
results_clean <- results_clean[complete.cases(results_clean),]
head(results_clean)

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 550 -> 991 -> 945 -> 609
sum(results_clean$padj < 0.05)
# 44 -> 121 -> 188 -> 49

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 5 -> 25 -> 32 -> 19
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 39 -> 96 -> 156 -> 30


# volcano plots
colours <- rep("steelblue", dim(results_clean)[1])
colours[results_clean$padj < 0.05] <- "salmon"

plot(-log(padj) ~ log2FoldChange, data = results_clean,
     pch = 20, col = colours,
     ylab = "-ln of adjusted p", xlab = "L2FC",
     xlim = c(-15,15), ylim = c(0,20))
abline(h = -log(0.05), col = "black", lwd = 2, lty = 2)
abline(v = 0, col = "black", lwd = 2, lty = 2)
# use the negative log in plot to see smaller p-values (more significant)

# top right quadrant = significantly upregulated genes
# bottom left = downregulated, not significant
# top left = significant downregulation
# bottom right = upregulated, not significant

```
*see volcano plot results [here](https://sophisamus1.github.io/Samus_Lab_Notebook/OpihiGeneExpressionResults/)*    

















