---
layout: post
title: ʻOpihi Gene Expression Results
date: '2026-07-06'
tags: [ ʻopihi, RNAseq, DGE ]
---

reference: TrinityOut_trim3.Trinity.fasta

531270 transcripts

![CE t3 heatmap](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_t3_heatmap.png?raw=true)

![CE t3 heatmap w treatment](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_t3_heatmapWtreatment.png?raw=true)
control: blue
thermal: orange
desiccation: yellow

![CE t3 pca](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_t3_PCA.png?raw=true)

### Log2(FC) = log2(A/B) 
Where A is the average read counts for a given gene/transcript in treatment A
and B is the average read counts for a given gene/transcript in treatment B

A L2FC value < 0 indicates that gene is downregulated in treatment A
A L2FC value > 0 indicates that gene is upregulated in treatment B

Volcano plots help visualize L2FC with the negative natural log of the adjusted p-value on the y axis and L2FC on the x axis. This allows us to split the plot into 4 groups: 
The top 2 quadrants are significantly differentially expressed genes with those on the left (negative) being downregulated and those on the right (positive) upregulated.
The bottom two quadrants are not significantly differentially expressed genes.

![CE t3 thermal:control](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_t3_thermalVScontrol.png?raw=true)
L2FC = log2(thermal/control)

1312 significantly differentially expressed genes without p-value adjusted for multiple comparisons
169 significantly differentially expressed genes with BH adjusted p-value
146 significantly upregulated genes in thermal group ʻopihi (compared to control)
23 significantly downregulated genes in thermal group (compared to control)

![CE t3 desiccation:control](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_t3_desiccationVScontrol.png?raw=true)
L2FC = log2(desiccation/control)

602 significantly differentially expressed genes without adjustment for multiple comparisons
52 significantly differentially expressed genes with BH adjustment
35 significantly upregulated genes in desiccation group ʻopihi (compared to control)
17 significantly downregulated genes in desiccation group (compared to control)

![CE t3 desiccation:thermal](https://github.com/SophiSamus1/Samus_Lab_Notebook/blob/master/images/ThesisUpdate/CellanaExarata_t3_desiccationVSthermal.png?raw=true)
L2FC = log2(desiccation/thermal)

609 significantly differentially expressed genes without multiple comparisons adjustment
49 significantly differentially expressed genes with BH adjustment
19 significantly upregulated genes in desiccation group (compared to thermal)
30 significantly downregulated genes in desiccation group (compared to thermal)

## The biggest difference (most differentially expressed genes) is between control and thermal groups.
## The next steps are to run models to determine the effects of shell shape/size, thermal history (location in intertial), and environment on gene expression.