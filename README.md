Meltos: Multi-Sample Tumor Phylogeny Reconstruction for Structural Variants
-----------------------

### About
Meltos is a novel approach to estimate the variant allele frequency of somatic SVs from whole genome sequencing (WGS) signals and using these VAFs to identify the phylogenetic relationship between SSVs in a multi-sample cell lineage tree using an SNV-only tree as a basis. Our probabilistic framework allows us to assess multiple types of signals taken from the data simultaneously and more accurately calculate the VAF of SV events. Following the maximum parsimony principle, Meltos uses a novel combinatorial algorithm to assign SV clusters on the branches of the given lineage tree, while modestly augmenting the tree topology if needed.

### Required Files

- SSNV Tree file produced by LICHEE (https://github.com/viq854/lichee)
- Tab delimited file of SSNVs used to build tree
- Configuration file produced by Meltos input preparation script

### Input
#Required:
- "-svFile \<filename\>": name of the file which contains your preprepared SV information.
- "-treeFile \<filename\>": name of the file which contains your premade SSNV lineage tree.
- "-ssnvFile \<filename\>": name of the file which contains your list of SSNVs that were used in your input lineage tree.
- "-numSamples \<integer\>": count of the number of spatially distinct samples in your sv and ssnv files.

#Optional:
  -outputFile <filename>: the prefix you want for your outputfiles. If not specified, defaults to the name of your sv file +".lapsi"
  NOTE: This will overwrite files with the same name. This prefix should include the directory in which you want the files to go.


### Output
Produces a series of files based on various combinations of parameters, and places them in the directory specified by output.
The file starts with parameter specifications used to create the file.
- Lineage Tree Node Assignments
After that comes VAF calculations and SV assignments for nodes in the lineage tree. Nodes from the original lineage tree will share the same index from the first file, and new nodes will be labeled sequentially after that.
The SV assignments will also share their indices with the indices of the SVs from their original input file. SSNVs are not shown in this output. Node 0 is the root node, and is not from the original lineage tree.
- SVs Assigned to Added New SV Nodes:
A repeat of information from the SV assignments, but only showing nodes that were generated by the algorithm, rather than nodes that originally came from the input tree.
- SVs Assigned to Inviable New SV Nodes:
A list of nodes that were created by the algorithm but were unable to be placed into the lineage tree, together with the indices of their SV assignments.

Finally, the tree's edges are displayed, with the index of the parent node on the left, and the index of the child node on the right.
