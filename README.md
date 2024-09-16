# Phylogenomics_workshop

## Ideas for lecture to cover 
- Why is phylogenomics important for conservation? How does it have implications for management?
    - Defining taxonomic and management units
    - Assess role of gene flow in evolutionary history (hybrid speciation or recent gene flow) -> implications on management and protection (ESA)
    - Examples of where phylogenomics matters for conservation
          - Red wolf, other examples? 
- Types of phylogenomic data: UCEs, mitochondria, Y chromosome, reduced representation, whole genome. 
  - What questions and what challenges/limitations each data source presents for phylogenomic inference
- Gene trees vs. species trees
  - phylogenetic discordance - what is it? why is it important to keep in mind? how does it arise?
- Types of ways to infer phylogenies
   - maximum likelihood (ML), bayesian methods, using gene trees (quartet scores in ASTRAL)
- More detail into the methods
   - Multispecies Alignment -> this document has nice visuals: https://training.galaxyproject.org/training-material/topics/evolution/tutorials/abc_intro_phylo-msa/slides-plain.html
 
- Show an example phylogeny with nodes, bootstrap values
   - Go through exactly what the branch lengths mean, node support means, how node support is inferred, confidence in phylogeny 


# Phylogenomic Analysis 1
- inferring a maximum likelihood phylogeny using nuclear data
    - Preparing the dataset - VCF filtering
    - VCF to the Multiple Species Alignment (PHYLIP)
    - Model selection with ModelFinder within IQtree
    - Run the phylogenetic analysis with IQ-tree
    - Visualize the phylogenetic tree
         - Using R to plot the phylogeny and bootstrap support values/branch length values
         - Using R to plot the phylogenetic tree against a map of rail locations -> how does evolutionary relationships correspond to geography? 


















