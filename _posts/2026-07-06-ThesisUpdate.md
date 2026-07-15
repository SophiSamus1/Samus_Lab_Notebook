---
layout: post
title: Update on thesis project
date: '2026-07-06'
tags: [ ʻopihi, RNAseq, Thermal Performance ]
---

This post holds the results of my thesis project as of July 6, 2026. The project is split up into three sections: field surveys, gene expression analysis, and thermal performance which will be separated into their own notebook entries and linked below. As a reminder, the goal of my project is to determine the cellular mechanisms of ʻopihi in response to extreme thermal and desiccation stress through differential gene expression analysis, and to determine how or if shell morphology affects gene expression and thermal tolerance. To do so, I performed stress trials in situ with 24 ʻopihi split into three treatments: thermal, desiccation, and control (8 ʻopihi per treatment). Desiccation and thermal stress group ʻopihi were transplanted high in the intertidal, away from the splash zone. Thermal stress group ʻopihi were kept in direct sunlight and splashed once following transplantation while desiccation group ʻopihi were shaded and kept completely dry. To account for handling effects and to compare differential expression, control group ʻopihi were transplanted back to where they were found in the intertidal. 

![stress trial](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/stresstrial.png?raw=true)

See [here]() for results from the in situ stress trials.

See [here](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/_posts/2026-07-06-OpihiGeneExpressionResults.md) for differential gene expression analysis results.

See [here]() for results of thermal performance trials. 


Before creating Cellana exarata transcriptome, I performed a preliminary differential gene expression analysis using a Cellana radiata reference. These are the results.

38107 transcripts

![CR DGE heatmap](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaRadiata_DGEheatmap.png?raw=true)

![CR DGE heatmap w treatment](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaRadiata_DGEheatmapWtreatment.png?raw=true)
control: blue
thermal: orange
desiccation: yellow

![CR DGE PCA](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaRadiata_DGEpca.png?raw=true)


Explain L2FC, upregulation/downregulation, significance. Include number of transcripts in each quadrant

![CR DGE thermal:control](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaRadiata_DGEthermalVScontrol.png?raw=true)
results_clean <- results(deseq2_result,
                         contrast = c("treatment", "thermal", "control"))
# contrast: treatment is the factor in design formula, thermal is the numerator for fold change, control is the denominator

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 1390
sum(results_clean$padj < 0.05)
# 299

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 189
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 110

![CR DGE desiccation:thermal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaRadiata_DGEthermalVSdesiccation.png?raw=true)
results_clean <- results(deseq2_result,
                         contrast = c("treatment", "desiccation", "thermal"))
# contrast: treatment is the factor in design formula, desiccation is the numerator for fold change, thermal is the denominator

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 550
sum(results_clean$padj < 0.05)
# 44

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 5
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 39

![CR DGE desiccation:control](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaRadiata_DGEdesiccationVScontrol.png?raw=true)
results_clean <- results(deseq2_result,
                         contrast = c("treatment", "desiccation", "control"))
# contrast: treatment is the factor in design formula, desiccation is the numerator for fold change, control is the denominator

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 932
sum(results_clean$padj < 0.05)
# 29

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 22
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 7



These are the results with Cellana exarata transcriptome

190161 transcripts

![CE DGE heatmap](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_DGEheatmap.png?raw=true)

![CE DGE heatmap w treatment](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_DGEheatmapWtreatment.png?raw=true)
control: blue
thermal: orange
desiccation: yellow

![CE DGE PCA](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_DGEpca.png?raw=true)

![CE DGE desiccation:control](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_DGEdesiccationVScontrol.png?raw=true)

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 932 -> 645
sum(results_clean$padj < 0.05)
# 29 -> 109

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 22 -> 88
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 7 -> 21

![CE DGE desiccation:thermal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_DGEdesiccationVSthermal.png?raw=true)

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 550 -> 991
sum(results_clean$padj < 0.05)
# 44 -> 121

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 5 -> 25
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 39 -> 96

![CE DGE thermal:control](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_DGEthermalVScontrol.png?raw=true)

# count differentially expressed genes
sum(results_clean$pvalue < 0.05)
# 1390 -> 1760
sum(results_clean$padj < 0.05)
# 299 -> 404

sum(results_clean$padj < 0.05 & results_clean$log2FoldChange > 0) # upregulated = 189 -> 314
sum(results_clean$padj < 0.05 & results_clean$log2FoldChange < 0) # downregulated = 110 -> 90


### Biggest difference is between thermal and control





Cellana exarata transcriptome QC stats



# Thermal Performance
see [previous post](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/_posts/2025-09-13-OpihiThermalPerformance.md) for reference

![ABT Hi](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/ABTbyHi.png?raw=true)

![ABT tot](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/ABTbyTreatment.png?raw=true)

![ABT plus field](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/ABTbyTreatmentPLUSfield.png?raw=true)

![ABT desiccation](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/ABTdesiccationPLUSdistCrust.png?raw=true)

![ABT thermal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/ABTthermalPLUSdistCrust.png?raw=true)

Basically, no effect of height or dist crust




