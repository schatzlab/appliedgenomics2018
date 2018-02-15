## Assignment 2: Genome Assembly
Assignment Date: Thursday, Feb. 15, 2018 <br>
Due Date: Thursday, Feb. 22, 2018 @ 11:59pm <br>


### Question 1. de Bruijn Graph construction [10 pts]
- Q1a. Draw (by hand or by code) the de Bruijn graph for the following reads using k=3 (assume all reads are from the forward strand, no sequencing errors, complete coverage of the genome)

```
ATTC
ATTG
CATT
CTTA
GATT
TATT
TCAT
TCTT
TGAT
TTAT
TTCA
TTCT
TTGA
```

- Q1b. Assume that the maximum number of occurrences of any 3-mer in the actual genome is 3 using the k-mers from Q1a. Write one possible genome sequence


- Q1c. What is the longest repeat? 


### Question 2. Phylogenetics Analysis [10 pts]

Your colleague is developing an experimental and computational protocol to determine the species present in food samples based on DNA sequencing. (See [here](https://bmcgenomics.biomedcentral.com/articles/10.1186/1471-2164-15-639) for a technology working towards making this a reality!) She extracted DNA from a mixed-meat sausage and prepared a library for paired-end 100bp Illumina sequencing. When the data returns, she uses a short-read aligner such as Bowtie2 or BWA to align the sequencing reads. As the references, she chose several genomes of animals whose meat is commonly consumed, including chicken and pig and cow. Most of the reads align to these common genomes. Next, she extracts the unmapped reads and runs a short-read assembler such as Spades on those reads. She only gets a few contigs that are longer than a few hundred base pairs. 

**1. Suggest two reasons there are only a few, short contigs assembled from non-mapping reads. (2)**

She asks for your help in finding the origin of these "mystery meat" contigs. Fortunately you are familiar with genomic databases and offer to help her out. You use query the NCBI's database of reference genome assemblies with the longest contigs using the [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi) tool which finds local sequence alignments between your sequence and a database. One contig you examine has several high E-value alignments to scaffolds in the *Macropus eugenii* genome assembly. Two of the alignments are in annotated gene regions. However, the [wallaby genome assembly](https://www.ncbi.nlm.nih.gov/assembly/GCA_000004035.1/) seems pretty rough. 

**2. Based on the link above, give two indicators that this genome assembly is poor quality. (2)** 

Because the assembly is rough, you are suspicious that the contig has more than one alignment. It overlaps more than one annotated gene. Could there be a duplicated region or misassembly in the reference genome? Or does the tammar wallaby actually have genes that are similar enough for your contig to align to both?

*Homologous* genes are genes with a *shared evolutionary history*. Homologous genes in the same genome arise from a *gene duplication event* long ago in evolution. Homologous genes in the same genome are called *paralogs*
. Paralogs usually have detectable sequence similarity, so it is possible that ENSMEUG00000000695 and ENSMEUG00000000691 (the annotated genes within two of this contig's alignments) are paralogs. You decide to build a phylogenetic tree of these genes, as well as some sequences from other species to see whether these genes are paralogs.

Here are some protein sequences of some hits from a blastx search including the two sequences from *M. eugenii*. [multiplePROT.fa](multiplePROT.fa) Some proteins are annotated "hemoglobin epsilon" and others are annotated "hemoglobin beta" (B and E in the sequence names in the file). 

**3.** Use the web version of [MUSCLE](https://www.ebi.ac.uk/Tools/msa/muscle/) to create a multiple sequence alignment. The tool outputs a neighbor-joining, binary phylogenetic tree. Because MUSCLE's built in tree graphic is very poor, download the data in Newick format, and open the file in visualization software such as [FigTree](http://tree.bio.ed.ac.uk/software/figtree/) or a browser-based tool such as [Trex](http://www.trex.uqam.ca/index.php?action=newick). Include an image of the tree in your report. Feel free to explore a variety of visualization options, but just make sure the leaf labels are readable and the branches have proportional length.

**a. What do the leaves of the tree represent? Is the tree rooted or unrooted? (1)**

**b. Propose a location for the root of the tree, and justify your answer. (Mark it on the image of the tree) (1)**

**c. Do you think the "B" and "E" genes are paralogs? Justify your answer by referring to the tree. (2)**

Here is the output from MrBayes, a Bayesian MCMC tree algorithm, run on the same protein sequences.

![](assignment3.nex.txt.con.tre.png)
Large numbers = posterior probabilities  
Small numbers = branch lengths

**e. Does the output have an equivalent topology to your neighbor-joining tree from MUSCLE? (1)**

**f. What does the branch length in both trees indicate about *M.eugenii*, *M.giganteus*, and *M.rufus*? (1)**

It may not be reassuring that there is evidence of *M.eugenii* DNA in this sausage. Hopefully it's contamination, but the story of how the sample got contaminated would be interesting, to say the least! Now on to investigate the other contigs.

### Question 3. BWT Encoding [10 pts]

Linear time methods exist for computing the BWT, although for this assignment you can use the simple method based on standard sorting techniques. Your solution does *not* need to be an optimal algorithm and can use O(n^2) space and O(n^2 lg n) time. 

Here is the recommended pseudo code (make sure to submit your code as well as the encoded string):

```
computeBWT(string s)
  ## add the magic end-of-string character
  s = s + "$"
 
  ## build up the BWM from the cyclic permutations
  ## note the ith cyclic permutation is just "s[i..n] + s[0..i]"
  StringList rows = []
  for (i = 0; i < length(s); i++)
    rows.append(cyclic_permutation(s, i))

  ## just use the builtin sort command
  sort(rows)

  ## now extract the last column
  string bwt = ""
  for (i = 0; i < length(s); i++)
    bwt += substr(rows[i], length(s),1)
  return bwt
```

String to encode:
```
I_am_fully_convinced_that_species_are_not_immutable;_but_that_those_belonging_to_what_are_called_the_same_genera_are_lineal_descendants_of_some_other_and_generally_extinct_species,_in_the_same_manner_as_the_acknowledged_varieties_of_any_one_species_are_the_descendants_of_that_species._Furthermore,_I_am_convinced_that_natural_selection_has_been_the_most_important,_but_not_the_exclusive,_means_of_modification.
```


### Question 4. BWT Decoder [10 pts]

One of the essential properties of the BWT is that it can be decoded back into the source text without any other additional information. This is accomplished by iteratively applying the Last-First property starting with the first character of the BWT until reaching the end of string character `'$'`. The Last-First property states there is an equivalence between the ith occurrence of a character in the first column and the ith occurrence of that character in the last column. This equivalence can be evaluated by counting how many occurrences of a character are present in the BWT string (the last column of the BWM) or by counting characters in the first column (which you will have to determine from the BWT itself). Again, faster methods exist (the FM-index) to determine the rank of each character but you can just count it explicitly here

The pseudocode for decoding the string is as follows:

```
decodeBWT(String bwt) 
  String firstCol = makeFirstColumn(bwt)
  String text = ""
  
  ## By construction, '$' always starts the zeroth row
  row = 0;
  while (bwt.charAt(row) != '$')
      text.append(bwt.charAt(row));
      row = applyLF(firstCol, bwt.charAt(row), rank(bwt, row));
  
  return reverse(text)
```

String to decode:
```
ex.uspe_gr_______$!!,e.orrs,sdddeedkdsuoden-tf,tyewtktttt,sewteb_ce__ww__h_PPsm_u_naseueeennnrrlmwwhWcrskkmHwhttv_no_nnwttzKt_l_ocoo_be___aaaooaAakiiooett_oooi_sslllfyyD__uouueuceetenagan___rru_aasanIiatt__c__saacooor_ootjeae______ir__a
```

Hint: use your sourcecode from Q3 to debug Q4. Also start with simple strings like GATTACA or your own name.


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

