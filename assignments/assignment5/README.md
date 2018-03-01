## Assignment 5: Genome Arithmetic
Assignment Date: Thursday, March 1, 2018  
Due Date: Thursday, March 8, 2018 @ 11:59pm  

### Assignment Overview

In this assignment, you will call structural variants and analyze the properties of variants in the human genome. **Make sure to show your work in your writeup!** As before, any questions about the assignment should be posted to [Piazza](https://piazza.com/class/jcumooljtd46p7).


#### Question 1. Gene Annotation Preliminaries [10 pts]

Download the annotation of build 38 of the human genome from here:  
[ftp://ftp.ensembl.org/pub/release-87/gtf/homo_sapiens/Homo_sapiens.GRCh38.87.gtf.gz](ftp://ftp.ensembl.org/pub/release-87/gtf/homo_sapiens/Homo_sapiens.GRCh38.87.gtf.gz)

- Question 1a. How many many GTF data lines are in this file? [Hint: The first few lines in the file beginning with "#" are so-called "header" lines describing thing like the creation date, the genome version (more on that later in the course), etc. Header lines should not be counted as data lines.]

- Question 1b. How many annotated protein coding genes are on each autosome of the human genome? [Hint: Protein coding genes will have "gene" in the 3rd column, and contain the following text: gene\_biotype "protein\_coding"]

- Question 1c. What is the maximum, minimum, mean, and standard deviation of the span of protein coding genes? [Hint: use the genes identified in 1b]

- Question 1d. What is the maximum, minimum, mean, and standard deviation in the number of exons for protein coding genes? [Hint: you should separately consider each isoform for each protein coding gene]

#### Question 2. Small Variant Analysis [6 pts]

In homework 4, you aligned a set of reads to **chromosome 22** and used freebayes to call small variants. If you don't have it, the filtered VCF file output from question 1c is [here](freebayes_filtered.vcf).

- Question 2a. How many of the variants fall into genes? How many fall into exons? [Hint: `bedtools`]

- Question 2b. What is the [transition/transversion ratio](https://www.mun.ca/biology/scarr/Transitions_vs_Transversions.html) of the variants in protein coding genes? What is the ratio of variants in the exons? [Hint: try `bedtools` and then `bcftools stats` like in homework 4, 1c.]

#### Question 3. Structural Variation Analysis [10 pts]

Run the structural variant caller [lumpy-sv](https://github.com/arq5x/lumpy-sv) for the reads you were analyzing in homework 4 [here](lumpy.vcf). `lumpy-sv` uses split-read alignments and discordant alignments to find breakpoints. See the **Resources** section for more detailed instructions.

- Question 3a. How many structural variations are in the sample were found by `lumpy-sv`? How many of these are duplications, inversions, insertions, and deletions, respectively? 

- Question 3b. Create a BED file with the SV breakpoints based on the information in the lumpy.vcf file. Which genes have structural variation breakpoints in them? [Hint: `bedtools`]

#### Question 4. Copy Number Analysis [10 pts]

Run the copy number variant caller [cnvkit](http://cnvkit.readthedocs.io/en/stable/) using the bwa-mem alignments from question 3. See the **Resources** section for more detailed instructions.

- Question 4a. Run `cnvkit` and create a scatterplot for the region chr22:20000000-30000000. Include the figure in your report.

- Question 4b. Based on the y-axis of the plot and/or the information in the .cns file, estimate the copy number of the region(s) within chr22:20000000-30000000 with significant deviations from baseline.

- Question 4c. Using the data in the .cns file, create a BED file of the regions with CNV. [Hint: If a region does not have a clear-cut copy number profile, simplify your BED file to contain a single interval including all the deviations from baseline.] Copy the text of the BED file into your report. How many genes have at least 1 base pair in a region of copy number variation? [Hint: you guessed it, `bedtools`]

#### Question 5. De novo mutation analysis [10 pts]

For this question, we will be focusing on the de novo variants identified in this paper:<br>
[http://www.nature.com/articles/npjgenmed201627](http://www.nature.com/articles/npjgenmed201627)

Download the de novo variant positions from here (Supplementary Table S4):<br>
[http://www.nature.com/article-assets/npg/npjgenmed/2016/npjgenmed201627/extref/npjgenmed201627-s3.xlsx](http://www.nature.com/article-assets/npg/npjgenmed/2016/npjgenmed201627/extref/npjgenmed201627-s3.xlsx)

Download the annotation of regulatory variants from here:<br>
[ftp://ftp.ensembl.org/pub/release-87/regulation/homo_sapiens/homo_sapiens.GRCh38.Regulatory_Build.regulatory_features.20161111.gff.gz](ftp://ftp.ensembl.org/pub/release-87/regulation/homo_sapiens/homo_sapiens.GRCh38.Regulatory_Build.regulatory_features.20161111.gff.gz)

- Question 5a. How many variants are in protein coding genes? [Hint: convert xlsx to BED, then `bedtools`]

- Question 5b. How many variants are in *any* annotated regulatory regions? [Hint: `bedtools`]

- Question 5c. What type of annotated regulatory region has the most variants? [Hint: `bedtools`]

- Question 5d. Is this a statistically significant number of variants (P-value < 0.05)? [Hint: If you don't want to calculate this analytically, you can do an experiment. Try simulating the same number of variants as the original file 100 times, and see how many fall into this regulatory type. If at least this many variants fall into this feature type more than 5% of the trials, this is not statistically significant]

### Packaging

Upload a single PDF document to Blackboard.

### Resources


#### [BEDTools](http://bedtools.readthedocs.io/en/latest/) - Genome Arithmetic

Get bedtools from conda, if you haven't already.

```
conda install bedtools
```

#### [lumpy-sv](https://github.com/arq5x/lumpy-sv) - Structural Variation Detection

Through conda, lumpy-sv requires python 2.7. On your virtual machine, you may have to `conda install python=2.7`
and allow other packages to be updated to compatible versions. 

```
conda install lumpy-sv bwa
wget https://raw.githubusercontent.com/arq5x/lumpy-sv/master/scripts/extractSplitReads_BwaMem
chmod +x extractSplitReads_BwaMem
```

```
# Realign the reads with bwa mem
$ bwa mem -R "@RG\tID:id\tSM:sample\tLB:lib" chr22.fa sample/pair.1.fq sample/pair.2.fq > bwa.sam
# Extract the discordant paired-end alignments.
$ samtools view -b -F 1294 bwa.sam > sample.discordants.unsorted.bam

# Extract the split-read alignments
$ samtools view -h bwa.sam \
    | ./extractSplitReads_BwaMem -i stdin \
    | samtools view -Sb - \
    > sample.splitters.unsorted.bam

# Sort both alignments
$ samtools sort sample.discordants.unsorted.bam > sample.discordants.bam
$ samtools sort sample.splitters.unsorted.bam > sample.splitters.bam

# Now run lumpy

$ lumpyexpress \
    -B bwa.bam \
    -S sample.splitters.bam \
    -D sample.discordants.bam \
    -o lumpy.vcf
```

#### [cnvkit](http://cnvkit.readthedocs.io/en/stable/) - Copy Number Variation Detection

Use conda to install cnvkit.

```
conda install cnvkit
```


```
samtools sort bwa.sam | samtools view -b > bwa.bam
cnvkit.py batch -m wgs -f chr22.fa --output-reference chr22.cnn -n bwa.bam
cnvkit.py scatter -s bwa.cn{s,r} -c chr22:20000000-30000000 -o scatterchr22.pdf
```
