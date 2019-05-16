# Comp_Genomics_Scipts
A repository for scripts associated with the Tsetse fly comparative genomics analysis project.

These PERL scripts were utilized to generate gene count data from a raw Ensemble Orthology dataset (which can be found as Additional File 3.tsv).

Ensemble_Orthology_Data_Parser_PERL_Script.pl - parses orthology group data and generates a tab delimited file providing the count of genes from each species within an orthology group as well as a list of the gene identifiers from each species for each group. The script should be called with the filename of the file containing the orthology group data as the sole arguement.

Orthology_group_sequence_and_ID_extractor_PERL_Script.pl - this script will extract FASTA sequences from a list orthology groups from a multiFASTA file and generate individual multifasta files containing the associated sequences for each orthology group. The script requires three arguments.
  Argument 1 - text file listing orthology group of interest in a text file.
  Argument 2 - a tab delimited file with a line for each gene from all species of interest containing: Orthology_group_ID<tab>gene id<tab>species
  (Example - Group_1<tab>GAUT000001<tab>Glossina austeni)
  Argument 3 - a FASTA file containing all sequences of interest.
  
  
