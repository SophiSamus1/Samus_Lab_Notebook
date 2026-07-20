---
layout: post
title: Trinity Assembly Methods for ʻopihi
date: '2026-07-06'
tags: [ ʻopihi, Gene Expression, Trinity ]
---

[Trinity](https://github.com/trinityrnaseq/trinityrnaseq/wiki) is a program designed for de novo construction of transcriptomes from RNAseq data. 
The assembly is split into three steps: 
1. **Inchowrm** assembles RNAseq reads into unique transcripts
2. **Chrysalis** clusters contigs made by Inchworm and constructs de Bruijn graphs for each cluster, representing sets of genes that share sequences. Chrysalis partitions the full read set among these disjoint graphs.
3. **Butterfly** processes each individual de Bruijn graph in parallel and reports the full length transcript.



```

#!/bin/bash

#SBATCH -J Trinity_trim3
#SBATCH -o Trinity_trim3_%j.out                         #output file
#SBATCH -e Trinity_trim3_%j.err               		  	#error file
#SBATCH -N 1                                            #1 nodes
#SBATCH -n 12                                           #12 cores
#SBATCH -t 168:00:00                                    #Time Limit
#SBATCH -p normal                                       #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END
#SBATCH --mem 200000

module load rsem/1.3.3

$TRINITY_HOME/Trinity --seqType fq --max_memory 200G \
					  --left /work/birdlab/ssamus/seqsLeft_trim3.fastq \
					  --right /work/birdlab/ssamus/seqsRight_trim3.fastq \
					  --SS_lib_type RF --CPU 12 --output /work/birdlab/ssamus/TrinityOut_trim3

```
Trinity_trim3 job ran for 1-02:40:30

# Assembly Quality Assessment

### Assessing Read Content

Build bowtie2 index for the transcriptome:
```

#!/bin/bash

#SBATCH -J TrinityQC_trim3_bowtiebuild
#SBATCH -o TrinityQC_trim3_bowtiebuild_%j.out                                   #output file
#SBATCH -e TrinityQC_trim3_bowtiebuild_%j.err                                   #error file
#SBATCH -N 1                                                                    #1 nodes
#SBATCH -n 12                                                                   #12 cores
#SBATCH -t 168:00:00                                                            #Time Limit
#SBATCH -p normal                                                               #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3

bowtie2-build /work/birdlab/ssamus/TrinityOut_trim3.Trinity.fasta TrinityQC_t3/CellanaExarata_t3

```

Perform alignment (for PE reads) to capture read alignment stats:
```

#!/bin/bash

#SBATCH -J TrinityQC_trim3_bowtiealign
#SBATCH -o TrinityQC_trim3_bowtiealign_%j.out                                   #output file
#SBATCH -e TrinityQC_trim3_bowtiealign_%j.err                                   #error file
#SBATCH -N 1                                                                    #1 nodes
#SBATCH -n 12                                                                   #12 cores
#SBATCH -t 168:00:00                                                            #Time Limit
#SBATCH -p normal                                                               #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3

bowtie2 -p 10 -q --no-unal -k 20 -x TrinityQC_t3/CellanaExarata_t3 \
		-1 /work/birdlab/ssamus/seqsLeft_trim3.fastq -2 /work/birdlab/ssamus/seqsRight_trim3.fastq \
		2>align_stats_t3.txt| samtools view -@10 -Sb -o bowtie2_t3.bam

```

Visualize statistics:
```

cat 2>&1 align_stats_t3.txt

```

Output:
```

439529004 reads; of these:
  439529004 (100.00%) were paired; of these:
    59540720 (13.55%) aligned concordantly 0 times
    27875845 (6.34%) aligned concordantly exactly 1 time
    352112439 (80.11%) aligned concordantly >1 times
    ----
    59540720 pairs aligned concordantly 0 times; of these:
      3807564 (6.39%) aligned discordantly 1 time
    ----
    55733156 pairs aligned 0 times concordantly or discordantly; of these:
      111466312 mates make up the pairs; of these:
        26175702 (23.48%) aligned 0 times
        4749730 (4.26%) aligned exactly 1 time
        80540880 (72.26%) aligned >1 times
97.02% overall alignment rate

```

From [Trinity](https://github.com/trinityrnaseq/trinityrnaseq/wiki/RNA-Seq-Read-Representation-by-Trinity-Assembly): A typical Trinity transcriptome assembly will have the vast majority of all reads mapping back to the assembly, and ~70-80% of the mapped fragments found mapped as proper pairs (yielding concordant alignments 1 or more times to the reconstructed transcriptome). Note, if you see high rates of duplication, usually this is not a cause for concern. Highly expressed transcripts with alternatively spliced isoforms will account for multiple read mappings. Later, abundance estimation (transcript expression quantification) takes these multiple mappings into account.


### Visualize read support using [IGV](http://software.broadinstitute.org/software/igv/):


Sort alignments by coordinate:
```

#!/bin/bash

#SBATCH -J TrinityQC_trim3_samsort
#SBATCH -o TrinityQC_trim3_samsort_%j.out                                       #output file
#SBATCH -e TrinityQC_trim3_samsort_%j.err                                       #error file
#SBATCH -N 1                                                                    #1 nodes
#SBATCH -n 12                                                                   #12 cores
#SBATCH -t 168:00:00                                                            #Time Limit
#SBATCH -p normal                                                               #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3

samtools sort bowtie2_t3.bam -o bowtie2_t3.coordSorted.bam

```

Index coordinate-sorted bam file:
```

#!/bin/bash

#SBATCH -J TrinityQC_trim3_samindex
#SBATCH -o TrinityQC_trim3_samindex_%j.out                                      #output file
#SBATCH -e TrinityQC_trim3_samindex_%j.err                                      #error file
#SBATCH -N 1                                                                    #1 nodes
#SBATCH -n 12                                                                   #12 cores
#SBATCH -t 168:00:00                                                            #Time Limit
#SBATCH -p normal                                                               #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3



samtools index /work/birdlab/ssamus/bowtie2_t3.coordSorted.bam

```

Index Trinity.fasta file
```

#!/bin/bash

#SBATCH -J TrinityQC_trim3_samtrindex
#SBATCH -o TrinityQC_trim3_samtrindex_%j.out                                  #output file
#SBATCH -e TrinityQC_trim3_samtrindex_%j.err                                  #error file
#SBATCH -N 1                                                                  #1 nodes
#SBATCH -n 12                                                                 #12 cores
#SBATCH -t 168:00:00                                                          #Time Limit
#SBATCH -p normal                                                             #normal partition
#SBATCH --mail-user=ssamus1@my.hpu.edu
#SBATCH --mail-type=BEGIN,END   
#SBATCH --mem 200000

module load rsem/1.3.3

samtools faidx /work/birdlab/ssamus/TrinityOut_trim3.Trinity.fasta

```
Resultant bowtie2_t3.coordSorted.bam files can be loaded in IGV and viewed.

To identify protein coding regions within transcripts, use [TransDecoder](https://github.com/TransDecoder/TransDecoder/wiki). See [here]() for my code.   
To estimate transcript abundance, use [RSEM](https://deweylab.github.io/RSEM/). See [here]() for my code.


























