## Assignment 1: Chromosome Structures
Assignment Date: Thursday, Feb. 1, 2018 <br>
Due Date: Thursday, Feb. 8, 2017 @ 11:59pm <br>

### Assignment Overview

In this assignment you will profile the overall structure of the genomes of several important species and then study the yeast genome in more detail.
As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/jhu/spring2017/600649/home)

Some of the tools you will need to use this semester only run in a linux environment. If you do not have access to a linux machine, download and install a virtual machine following the directions here: https://github.com/schatzlab/appliedgenomics2018/blob/master/assignments/virtualbox.md


### Question 1: Chromosome structures

Download the chomosome size files for the following genomes (Note these have been preprocessed to only include main chromosomes):

1. [Arabidopsis thaliana (TAIR10)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/TAIR10.chrom.sizes) - An important plant model species [[info]](https://en.wikipedia.org/wiki/Arabidopsis_thaliana)
2. [Corn (Zea mays B73v4)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/zm4.chrom.sizes)) - The most widely grown crop in the world [[info]](https://en.wikipedia.org/wiki/Maize)
3. [E. coli (Escherichia coli K12)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/ecoli.chrom.sizes) - One of the most commonly studied bacteria [[info]](https://en.wikipedia.org/wiki/Escherichia_coli)
4. [Fruit Fly (Drosophila melanogaster, dm6)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/dm6.chrom.sizes) - One of the most important model species for genetics [[info]](https://en.wikipedia.org/wiki/Drosophila_melanogaster)
5. [Human (hg38)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/hg38.chrom.sizes) - us :) [[info]](https://en.wikipedia.org/wiki/Homo_sapiens)
6. [Rice (Oryza sativa, IRGSP-1.0)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/rice.chrom.sizes) - One of the most important crops in the world [[info]](https://en.wikipedia.org/wiki/Rice)
7. [Worm (Caenorhabditis elegans, ce10)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/ce10.chrom.sizes) - One of the most important animal model species [[info]](https://en.wikipedia.org/wiki/Caenorhabditis_elegans)
8. [Yeast (Saccharomyces cerevisiae, sacCer3)](http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/yeast.chrom.sizes) - an important eukaryotic model species, also good for bread and beer [[info]](https://en.wikipedia.org/wiki/Saccharomyces_cerevisiae)

Using these files, make a spreadsheet/table with the following information per species:

- Question 1.1. Total genome size
- Question 1.2. Number of chromosomes
- Question 1.3. Largest chromosome size and name
- Question 1.4. Smallest chromosome size and name
- Question 1.5. Mean chromosome length


### Question 2: Sequence content

Download the yeast genome from here: http://schatz-lab.org/appliedgenomics2018/assignments/assignment1/yeast.fa.gz

- Question 2.1. How many As, Cs, Gs, Ts are found in the entire genome
- Question 2.2. Make a scatterplot of the %GC of 1000bp windows across the genome: x-axis = genome location, y-axis = (#G + #C) / 1000. For this analysis the chromsomes can be concatenated together to form a long string of the chromosomes in numerical order: chr1, chr2, ... chrN. Make sure to draw a bar to indicate the ends of chromosomes



### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and 
all relevant figures (as needed). Make sure to clearly label each of the subproblems and give the exact commands you used for 
solving the question. Submit your solutions by uploading the PDF to Blackboard. 

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 4 late days for the entire semester!



