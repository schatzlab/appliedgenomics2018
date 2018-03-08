# Project Ideas

Here are a few selected projects organized by theme, although you are also free to present your own project ideas. A good project is one that (1) has a well defined goal; (2) has a well defined method proposed for solving it; and (3) has appropriate data and resources available. If any of these  are not available, your project will not be successful, especially in the limited time remaining for class. A successful model for the class project is to apply a technique developed in a different context to the biological problem of your choice. Another successful model is to identify an important paper of interest and then try to improve apon their method in some way (faster, less memory, more sensitive, more precise, novel species, etc).


## Basecalling and signal processing

1. Develop an improved base calling algorithm (potentially modification aware) for Oxford Nanopore or PacBio sequencing using recurrent neural networks or other ML approach:
[Nanocall](https://academic.oup.com/bioinformatics/article/33/1/49/2525680/Nanocall-an-open-source-basecaller-for-Oxford),
[Nanopolish for Methylation](http://www.nature.com/nmeth/journal/vaop/ncurrent/full/nmeth.4184.html?WT.feed_name=subjects_computational-biology-and-bioinformatics)

2. Align the raw signal from Oxford Nanopore or PacBio reads to a reference genome to improve variant detection, detect methlyation, and/or polishing:
[Nanopolish](http://www.nature.com/nmeth/journal/v12/n8/abs/nmeth.3444.html)


## Genome assembly and variant calling

1. Extend GenomeScope to infer the genome characteristics of genomes with long, error-prone reads:
[GenomeScope](http://biorxiv.org/content/early/2017/02/28/075978)

2. Benchmark and/or develop a de novo assembler for polyploid genomes. Note you *should* use existing tools for overlapping, and focus on unitting/scaffolding:
[FALCON](http://www.nature.com/nmeth/journal/v13/n12/full/nmeth.4035.html)

3. Benchmark and/or develop a scaffolder that can use long range information from 10X or HiC: 
[LACHESIS](http://www.nature.com/nbt/journal/v31/n12/full/nbt.2727.html), [fragScaff](http://genome.cshlp.org/content/24/12/2041), [ARCS](http://biorxiv.org/content/early/2017/01/17/100750)

4. Benchmark several SV callers, and create a classifier for identifying high confidence from low confidence SV calls:
[Parliament](http://bmcgenomics.biomedcentral.com/articles/10.1186/s12864-015-1479-3)

5. Develop an enhanced SV calling algorithm that leverages known SVs:
[1000 genomes SVs](http://www.nature.com/nature/journal/v526/n7571/full/nature15394.html)

6. Jointly analyze (de novo assemble or index the raw reads) the genomes of multiple varieties of rice (or other species) at once to identify sequences not present in the reference genome:
[PanRice](https://academic.oup.com/nar/article/45/2/597/2333876/RPAN-rice-pan-genome-browser-for-3000-rice-genomes); [Population BWT](http://genome.cshlp.org/content/27/2/300.abstract)

7. Studying the performance of using the MinHash algorithm to bin long reads for copy number analysis:
[Mash](http://biorxiv.org/content/early/2016/04/19/029827)

8. Adapt one or more learned data structures for genomics data:
[Learned Data Structures](https://arxiv.org/abs/1712.01208)

9. Evaluate whether predictions regarding new variant discovery made in 2009 were accurate using the latest consortium data and/or develop new predictions. [Estimating the number of unseen variants in the human genome](http://www.pnas.org/content/106/13/5008)

## Functional Genomics

1. Develop a EM based method for RNAseq analysis, and output the fractional assignments of reads to transcripts in the BAM file:
[Sailfish](http://www.nature.com/nbt/journal/v32/n5/full/nbt.2862.html)

2. Benchmark different RNA-seq aligners when using a phased diploid genome compared to a standard reference genome:
[Allele-Seq](http://msb.embopress.org/content/7/1/522.long)

3. Develop a RNA-seq aligner/pipeline that incorporates variants known from the population (graph genome):
[GraphGenomes](http://biorxiv.org/content/early/2017/01/18/101378)

4. Develop methods to identify genome variants from RNAseq data, apply to individuals with many tissues profiled to identify somatic mutations:
[SNPiR](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3791257/)

5. Run ChommHMM/Segway on a phased diploid genome (NA12878) and evaluate how that compares to annotating the reference genome:
[ChromHMM](http://www.nature.com/nmeth/journal/v9/n3/full/nmeth.1906.html)

6. Run ChromHMM/Segway on a non-human species such as rice or arabidopsis:
[ChromHMM](http://www.nature.com/nmeth/journal/v9/n3/full/nmeth.1906.html), [Segway Protocol](http://biorxiv.org/content/early/2016/10/17/080382)

7. Develop ChromHMM/Segway postprocessing algorithm to label the states with their biological functions:
[Segway Protocol](http://biorxiv.org/content/early/2016/10/17/080382)

8. Explore how single cell analysis works with minimal amounts of coverage. For example, reproduce the results from the Monocle paper, and experiment with how well it performs using lower amounts of coverage:
[Monocle](http://www.nature.com/nbt/journal/v32/n4/abs/nbt.2859.html)

9. Benchmark how different single cell pipelines work at recognizing different cell types:
[MetaNeighbor](https://www.nature.com/articles/s41467-018-03282-0)

## Evolution and Disease Genomics

1. Benchmark different non-coding mutation analysis schemes on a collection of diseased genomes (cancer, autism, etc): 
[CADD](http://www.nature.com/ng/journal/v46/n3/full/ng.2892.html), [funSeq2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0480-5), [fitCons](http://www.nature.com/ng/journal/v47/n3/full/ng.3196.html)

2. Develop methods for identifying somatic mutations using high error long reads (PacBio or Oxford Nanopore)
[Short read benchmarks](http://www.nature.com/articles/ncomms10001)

3. Metagenomics: Benchmark sailfish/salmon/kallisto approaches for inferring the abundance of different species present in a population
[Meta-kalisto](https://academic.oup.com/bioinformatics/article-abstract/doi/10.1093/bioinformatics/btx106/3038398/Pseudoalignment-for-metagenomic-read-assignment?redirectedFrom=fulltext)

4. Develop a new metagenomics classifier using deep learning or other advanced ML techniques.
[PhymmBL](http://www.nature.com/nmeth/journal/v6/n9/full/nmeth.1358.html)

5. Accelerate an important genomics pipeline using GPUs or cloud computing and use that to study a larger dataset
[Rail-RNA](https://academic.oup.com/bioinformatics/article-abstract/doi/10.1093/bioinformatics/btw575/2525684/Rail-RNA-Scalable-analysis-of-RNA-seq-splicing-and)

6. Benchmark and/or develop a method for inferring the ethnicity of an individual from their genotype:
[Genealogical DNA test](https://en.wikipedia.org/wiki/Genealogical_DNA_test)

7. Develop a novel visualization of genomics data (especially from 23-and-me reports):
[Circos](http://genome.cshlp.org/content/19/9/1639.full)

8. Apply metagenomics approaches to identifying species present in food samples. [AllFoodSeq](https://academic.oup.com/bioinformatics/article-lookup/doi/10.1093/bioinformatics/btw822) [Centrifuge](genome.cshlp.org/content/26/12/1721.full)

9. Investigate the rate of heterozygosity within and among human populations using consortium data. [Variation in Heterozygosity Predicts...](http://journals.plos.org/plosone/article/figure?id=10.1371/journal.pone.0063048.g001)

## Biologically inspired computing

1. Evaluate and/or improve the methods for storing binary data as DNA sequences: 
[DNA Fountain](http://science.sciencemag.org/content/355/6328/950)

2. Evaluate the amount of "junk data" in several widely used software packages:
[Regulatory control of software](http://www.pnas.org/content/107/20/9186.abstract), 
[Minimal Binary Executables](http://www.muppetlabs.com/~breadbox/software/tiny/teensy.html)


## Or your own idea! 

This should be more than you are already doing for your PhD work, but can be a novel twist to a dataset/idea you are already using. If you have a research idea but not the right data, let me know and I'll help you find some
