# Phylogenomics Analysis 1

Question -> Do we want infer the mtDNA tree? 

## Inferring the maximum likelihood phylogeny using the nuclear genome
We will infer a maximum likelihood phylogenetic tree of the nuclear genomic data using 17 different species of birds within the family Gruidae. This will allow us to assess the evolutionary relationship of the Guam Rail to other closely related Rail species. 

These include: 

```
Common moorhen - Gallinula chloropus	
South Island takahe - Porphyrio hochstetteri 	
Virginia rail - Rallus limicola 	
Eurasian coot - Fulica atra	
California black rail - Laterallus jamaicensis coturniculus 	
Clapper rail - Rallus crepitans	
Henderson crake - Zapornia atra	
Okinawa rail - Hypotaenidia okinawae	
Buff-banded rail - Hypotaenidia philippensis
Weka - Gallirallus australis
Inaccessible Island rail - Atlantisia rogersi 
Australian swamphen - Porphyrio melanotus	
```
With five outgroups: Sungrebe (Heliornis fulica), Whooping crane (Grus americana), Eurasian crane (Grus grus), Limpkin (Aramus guarauna), Common trumpeter (Psophia crepitans). 

## Preparing the dataset 
** Question for Klaus and Taylor --  where to start with this? VCF stage or BWA alignments). 

### Pre-filtering to keep high quality SNPs
We can use a VCF where each species genome is aligned and completed variant calling to the Guam Rail. First we will filter the VCF to obtain only high quality SNPs.

Let's change directory to our xxxx folder and copy the variant calling file (vcf) to this folder. The file is located here: 'pool/genomics/ariasc/SMSC_2023/mapping/xxx/xxx.vcf'

Next, we will run vcftools to filter our dataset
```
vcftools --vcf rails.vcf --keep ${SAMPLES} \ #keep only samples we want to include in the phylogenetic tree
--minDP xx \ #minimum depth filter #keep sites that have a depth at least xxx
--minQ xxx \ #keep sites that have a minimum quality of 30
--remove-indels \ #remove indels
--min-alleles 2 \ # keeping biallelic snps
--max-alleles 2 \ # keeping biallelic snps
--non-ref-ac-any 1 \ # remove non-invariant sites in the VCF
--max-missing xxx \ #keep only sites that have a certain percentage of individuals present - such if 0.9, this means to keep sites that have at least 90% of individuals have data
--recode \
--recode-INFO-all \
--out rails_filtered
```

### Convert VCF to a Multiple Species Alignment
Next, we will convert our VCF to the multiple species alignment (MSA) format PHYLIP. The MSA is the sequence alignment between species in regions of the genome where we can observe sequence differences between species (can add a better definition later). 

The PHYLIP format is commonly used to contain multiple species alignments for phylogenetic analyses. The PHYLIP format is a text file that contains two columns: one column on the sample names, and a second column showing the sequence alignment. The sequenecs are written as IUPAC nucleotide codes.

Here, we will need to choose an outgroup species to root the tree. (more information on what an outgroup is and why its needed). We will use the vcf2phylip.py script to convert our VCF to PHYLIP
```
python /projects/mjolnir1/people/crq857/Geneflow_Dogs/bin/vcf2phylip/vcf2phylip.py -i ${DIR}/autosomes.vcf --output-folder ${OUTDIR} --output-prefix autosomes_phy -o xxxx
```
We can look at the phylip file with ```less``` to see the alignments. 

## Infer a maximum likelihood phylogenetic tree 

We will use the program IQ-Tree to infer a maximum likelihood tree from our dataset. IQ-tree is a useful phylogenetics inference tool that performs model selection via ModelFinder (Kalyaanamoorthy et al. 2017) and bootstrapping. ModelFinder computes the log-likelihoods of an intial parsimony tree for various models and the Bayesian information criterion (BIC). ModelFinder chooses the model that minimizes the BIC score. 

First we will infer what substutition model fits our data the best 

```
iqtree -s example.phy -m MFP #MFP means ModelFinder Plus which will perform model selection
```
Now we can take a look at the output using ```less``` xxxxx.xx.

We can see all the different models that ModelFinder tested with our datasets. At the bottom, we can find the substutition model that best fits our data, having the lowest BIC score. 

Next, we will run the phylogenetic inference using our selected model 

```/home/crq857/bin/iqtree-1.6.12-Linux/bin/iqtree -s autosomes_filtered.phy -bb 1000 -nt AUTO -m bestmodel ```
The -bb flag tells IQ-tree to run 1000 ultrafast bootstrap replicates. IQ-tree will produce various files related to the analysis. 

We can take a look at the output after its finished running ```less.iqtree``` to see the log-likelihood of the tree. At the bottom, we can see the topology and the drawn out phylogenetic tree from our dataset. 

## Visualizing phylogenetic trees 

Now that we have finished the phylgoenetic inference, we can visualize the phylogenetic tree using a couple different programs. 

First, we can use R to plot the tree and the bootstrap, node support etc. 

** Talk about what the findings and bootsupport values mean. 

** question for Klaus and Taylor: we can visualize the tree with Figtree GIU (everyone will need to download it). Or with R **

** with R, I can add some scripts to combine some geographic or heterozygosity estimates on the tips. For example, having the phylogeny and map to see  whether the rails are on islands vs. mainland are closely related to eachother. For example: http://blog.phytools.org/2019/03/projecting-phylogenetic-tree-onto-map.html






Nuclear inference
mtDNA inference 

