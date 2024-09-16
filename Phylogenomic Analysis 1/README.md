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
Next, we will convert our VCF to the multiple species alignment (MSA). The MSA is the sequence alignment between species in regions of the genome where 

The PHYLIP format is commonly used to contain multiple species alignments for phylogenetic analyses. The PHYLIP format is a text file that contains two columns: one column on the sample names, and a second column showing the sequence alignment. 







Nuclear inference
mtDNA inference 

