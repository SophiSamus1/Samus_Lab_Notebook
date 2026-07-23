---
layout: post
title: RSEM-Transcript Abundance Methods for ʻopihi
date: '2026-07-06'
tags: [ ʻopihi, Gene Expression, RSEM ]
---

[RSEM](https://deweylab.github.io/RSEM/) estimates gene and isoform expression levels from RNAseq data using an expectation-maximization (EM) algorithm. Output transcript-coordinate BAM files can be visualized using [IGV](http://software.broadinstitute.org/software/igv/).  

Prepare reference sequence
```

#!/bin/bash

#SBATCH -J RSEMprepare_CellanaExarata_t3
#SBATCH -o RSEMprepare_CellanaExarata_t3_%j.out                                    #output file
#SBATCH -e RSEMprepare_CellanaExarata_t3_%j.err                                    #error file
#SBATCH -N 1                                                                       #1 nodes
#SBATCH -n 12                                                                      #12 cores
#SBATCH -t 168:00:00                                                          	   #Time Limit
#SBATCH -p normal                                                                  #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3

rsem-prepare-reference --bowtie2 /work/birdlab/ssamus/TrinityOut_trim3.Trinity.fasta RSEM_trim3/CellanaExarata_t3

```

Calculate expression values
```

#!/bin/bash

#SBATCH -J RSEMcalculateB026_CellanaExarata_t3
#SBATCH -o RSEMcalculateB026_CellanaExarata_t3_%j.out                            #output file
#SBATCH -e RSEMcalculateB026_CellanaExarata_t3_%j.err                            #error file
#SBATCH -N 1                                                                 	 #1 nodes
#SBATCH -n 12                                                                    #12 cores
#SBATCH -t 168:00:00                                                             #Time Limit
#SBATCH -p normal                                                                #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3

rsem-calculate-expression --sort-bam-by-coordinate --time --bowtie2 --calc-ci --paired-end \
/work/birdlab/ssamus/TrimmedSeqs3/B0**_R2_trim3.paired.fastq \
/work/birdlab/ssamus/TrimmedSeqs3/B0**_R1_trim3.paired.fastq \
RSEM_trim3/CellanaExarata_t3 RSEM_trim3/B026_t3

```
This was run for each sample, replacing ** with sample number.   

In R Studio, genes.results files were used to generate a read count matrix with transcript abundance in FPKM or TPM (RSEM reports both) per transcript (row) for each sample (column). See [post]() on differential gene expression.
 
