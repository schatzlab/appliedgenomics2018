## Assignment 4: Read mapping and variant calling
Assignment Date: Thursday, Feb. 22, 2018  
Due Date: Thursday, Mar. 1, 2018 @ 11:59pm  

### Assignment Overview

In this assignment, you will align reads to a reference genome to call SNPs and short indels. Then, you will perform an experiment to empirically determine the "mappability" of a genomic region. Finally, you will investigate some empirical behavior of the binomial test for heterozygous variant calling.  
As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/class/jcumooljtd46p7). Don't forget to read the **Resources** section at the bottom of the page!

### Question 1. Small Variant Analysis [XX pts]

Download chromosome 22 from build 38 of the human genome from here:  
[http://hgdownload.cse.ucsc.edu/goldenPath/hg38/chromosomes/chr22.fa.gz](http://hgdownload.cse.ucsc.edu/goldenPath/hg38/chromosomes/chr22.fa.gz)

Download the read set from here:  
[http://schatzlab.cshl.edu/data/teaching/sample.tgz](http://schatzlab.cshl.edu/data/teaching/sample.tgz)

For this question, you may find this tutorial helpful:  
[http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html](http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html)

- 1a. How many reads align to the reference? How many reads did not align? How many aligned reads had a mate that did not align (AKA singletons)? Count each read in a pair separately.  
[Hint: Build the index using `bowtie2-build`, align reads using `bowtie2`, analyze with `samtools flagstat`.]

- 1b. How many reads are mapped to the reverse strand? Count each read in a pair separately.   
[Hint: Find out what SAM flags mean [here](https://broadinstitute.github.io/picard/explain-flags.html) and use samtools view.]

- 1c. How many high-quality (QUAL > 20) single nucleotide and indel variants does the sample have? Of the high-quality SNPs, what is the transition / transversion ratio? Of the indels, how many are insertions and how many are deletions?  
[Hint:  Identify variants using `freebayes` - sort the SAM file first. Filter using `bcftools filter`, and summarize using `bcftools stats`.]

- 1d. Does the sample have any nonsense or missense mutations?  
[Hint: try the [Variant Effect Predictor](http://useast.ensembl.org/Tools/VEP) using the `Gencode basic transcripts`]

### Question 2. Read Mapping Uncertainty [XX pts]

For the region chr22:21000000-22000000 of the reference sequence for chromosome 22, extract every substring of length 35. Format the substrings as a FASTA file and use read names that indicate the origin. (No need to construct quality values or read pairs: use bowtie2 with `-f` and `-U` respectively). Make a new index and align these "reads" to chr22:21000000-22000000.  
[Hint: On the command line or in a script, load the sequence once and extract substrings in a loop.]

- 2a. How many reads align more than one time to the reference? How many reads did not align?

- 2b. How many reads align correctly? Consider a read aligned correctly if the left end of the alignment is within 5bp of the true location.  
[Hint: Investigate the [SAM file format specification](https://samtools.github.io/hts-specs/SAMv1.pdf).]

- 2c. For 1000bp nonoverlapping windows, plot the average mapping quality of the reads that mapped to this location, regardless of correctness. On the plot, the x-axis is starting coordinate of the bin and y-axis is the value.

- 2d. For 1000bp nonoverlapping windows, plot the fraction of reads that *belonged* there that were *correct*. On the plot, the x-axis is starting coordinate of the bin and y-axis is the valuez

- 2e. What do you observe about how well reads map within this region of chromosome 22? Look at the UCSC Genome Browser [umap24Quantitative](https://genome.ucsc.edu/cgi-bin/hgTrackUi?g=umap) "mappability" track in this region, and qualitatively compare the results from your plot to the track.  

### Question 3. Binomial Distribution [XX pts]

- 3a. For coverage n = 10 to 200, calculate the maximum number of minor allele reads (round down) that would make your one-sided binomial test reject the null hypothesis p=0.5 at 0.05 significance. Plot coverage on the x-axis and (number of reads)/(depth) on the y-axis.

- 3b. What asymptote does the plot seem to approach? Why is this?

### Resources

#### [FreeBayes](https://github.com/ekg/freebayes) - Small Variant Identification

```
conda install freebayes
freebayes -f chr22.fa sample.bam > sample.vcf
```

#### [bcftools](https://samtools.github.io/bcftools/bcftools.html) - VCF Summarry

```
conda install bcftools
bcftools filter -e "QUAL<20" sample.vcf > filtered.vcf
bcftools stats filtered.vcf > stats.txt
```

#### [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml) - Short read aligner

```
conda install bowtie2
bowtie2-build chr22.fa chr22
bowtie2 -x chr22 -1 sample/pair.1.fq -2 sample/pair.2.fq > sample.sam
```

While running alignments, if you get an error `Warning: Exhausted best-first chunk memory for read XXXX; skipping read` increase the command-line parameter `--chunkmbs`.

#### [Variant Effect Predictor](http://useast.ensembl.org/Tools/VEP) - Variant Interpretation

Nothing to install, just upload the VCF

