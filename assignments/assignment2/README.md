## Assignment 2: Genome Assembly
Assignment Date: Thursday, Feb. 8, 2018 <br>
Due Date: Thursday, Feb. 15, 2018 @ 11:59pm <br>

### Assignment Overview

In this assignment, you are given a set of unassembled reads from a mysterious pathogen that contains a 
secret message encoded someplace in the genome. The secret message will be recognizable as a novel insertion 
of sequence not found in the reference. Your task is to assess the quality of the reads, assemble the genome, 
identify, and decode the secret message. If all goes well the secret message should decode into a recognizable 
english text, otherwise doublecheck your coordinates and try again. As a reminder, any questions about the assignment 
should be posted to [Piazza](https://piazza.com/jhu/spring2018/en601749/home)

Some of the tools you will need to use only run in a linux environment. Spades, for example, will *not* work under Mac, 
even though it will compile. If you do not have access to a linux machine, download and install a virtual 
machine following the directions here: https://github.com/schatzlab/appliedgenomics2018/blob/master/assignments/virtualbox.md

Alternatively, you might also want to try out this docker instance that has these tools preinstalled: 
https://github.com/srivathsapv/wga-essentials


#### Question 1. Coverage Analysis [10 pts]

Download the reads and reference genome from: https://github.com/schatzlab/appliedgenomics2018/raw/master/assignments/assignment2/asm.tgz

Note I have provided both paired-end and mate-pairs reads (see included README for details). 
Make sure to look at all of the reads for the coverage analysis and kmer analysis, as well as in the assembly.

- Question 1a. How long is the reference genome? [Hint: Try `samtools faidx`]
- Question 1b. How many reads are provided and how long are they? Make sure to measure each file separately [Hint: Try `FastQC`]
- Question 1c. How much coverage do you expect to have? [Hint: A little arthmetic]
- Question 1d. Plot the average quality value across the length of the reads [Hint: Screenshot from `FastQC`]

#### Question 2. Kmer Analysis [10 pts]

Use `Jellyfish` to count the 21-mers in the reads data. Make sure to use the "-C" flag to count cannonical kmers, 
otherwise your analysis will not correctly account for the fact that your reads come from either strand of DNA.

- Question 2a. How many kmers occur exactly 50 times? [Hint: try `jellyfish histo`]
- Question 2b. What are the top 10 most frequently occurring kmers [Hint: try `jellyfish dump` along with `sort` and `head`]
- Question 2c. What is the estimated genome size based on the kmer frequencies? [Hint: upload the jellyfish histogram to [GenomeScope](http://genomescope.org)]
- Question 2d. How well does the GenomeScope genome size estimate compare to the reference genome? [Hint: In a sentence or two]

#### Question 3. De novo assembly [10 pts]

Assemble the reads using `Spades`. Spades will *not* run on Mac or Windows, you must use a linux environment. 

- Question 3a. How many contigs were produced? [Hint: try `grep -c '>' contigs.fasta`]
- Question 3b. What is the total length of the contigs? [Hint: try `samtools faidx`, plus a short script/excel]
- Question 3c. What is the size of your large contig? [Hint: check `samtools faidx` plus `sort -n`]
- Question 3d. What is the contig N50 size? [Hint: Write a short script, or use excel]

#### Question 4. Whole Genome Alignment [10 pts]

- Question 4a. What is the average identify of your assembly compared to the reference? [Hint: try `dnadiff`]
- Question 4b. What is the length of the longest alignment [Hint: try `nucmer` and `show-coords`]
- Question 4c. How many insertions and deletions are in the assembly? [Hint: try `dnadiff`]

#### Question 5. Decoding the insertion [10 pts]
- Question 5a. What is the position of the insertion on the reference? [Hint: try `show-coords`]
- Question 5b. How long is the novel insertion? [Hint: try `show-coords`]
- Question 5c. What is the DNA sequence of the encoded message? [Hint: try `samtools faidx` to extract the insertion]
- Question 5d. What is the secret message? [Hint: run `dna-encode.pl -d` to decode the string from 5c]


### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and 
all relevant figures (as needed). Make sure to clearly label each of the subproblems and give the exact commands you used for 
solving the question. Submit your solutions by uploading the PDF to [Blackboard](https://blackboard.jhu.edu/). 

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 4 late days for the entire semester!



### Resources


#### [Bioconda](https://bioconda.github.io/) - Package manager for bioinformatics software

I *highly* recommend that you use bioconda to install the packages rather than installing from source. Once bioconda is configured,
all of the needed tools can be installed using:

```
$ conda install fastqc jellyfish spades mummer samtools
```

#### [FastQC](http://www.bioinformatics.babraham.ac.uk/projects/fastqc/) - Raw read quality assessment

```
$ fastqc /path/to/reads.fq
```

If you have problems, make sure java is installed (`sudo apt-get install default-jre`)


#### [Jellyfish](http://www.genome.umd.edu/jellyfish.html) - Fast Kmer Counting

Note Jellyfish requires a 64-bit operating system. Download the package and compile it like this:

```
$ jellyfish count -m 21 -C -s 1000000 /path/to/reads*.fq
$ jellyfish histo mer_counts.jf > reads.histo
```

#### [GenomeScope](http://www.genomescope.org/) - Analyze Kmer Profile to determine genome size and other properties

GenomeScope is a web-based tool so there is nothing to install. Hooray! Just make sure to use the `-C` when running jellyfish count so that the reads are correctly processed.

####  [Spades](http://cab.spbu.ru/software/spades/2) - Short Read Assembler. Note: Only works under linux

Normally spades would try several values of k and merge the results together, but here we will force it to just use k=31 to save time. The assembly
should take about 30 minutes to 1 hour.

```
$ spades.py --pe1-1 frag180.1.fq --pe1-2 frag180.2.fq --mp1-1 jump2k.1.fq --mp1-2 jump2k.2.fq -o asm -t 4 -k 31
```

#### [MUMmer](http://mummer.sourceforge.net/) - Whole Genome Alignment

```
$ dnadiff /path/to/ref.fa /path/to/qry.fa
$ nucmer /path/to/ref.fa /path/to/qry.fa
$ show-coords out.delta
```

#### [SAMTools](http://www.htslib.org/) - Extract part of a genome sequence using 'samtools faidx' (this will extract from contig_id bases 1234 through 5678)

```
$ ./samtools faidx /path/to/genome.fa contig_id:1234-5678
```
