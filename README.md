# Seasonal influenza surveillance pipeline for JHSPH

This repository includes scripts to determine the influenza type (i.e., A, B, C) and segment (i.e., 1, 2, ...8) for raw .fasta files generated as part of our surveillance pipeline.

This workflow is based off of the software provided by [NCBI BLAST+](https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html) and functions similarly to the [Influenza Virus Sequence Annotation Tool](https://www.ncbi.nlm.nih.gov/genomes/FLU/annotation/). 

# Overview

1. Installation of the NCBI BLAST+ software (from: [NCBI BLAST+](https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html), see [index of BLAST executables](https://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) and select format compatible with your operating system) and appropriate _dependencies_
   
   	BLAST+ software will automatically be installed into /Users/<your_name_here>, but may be moved into a specified directory based on preference
   
2. Installation of and/or creation of database for subsequent searches. The databse in this repository should be used for assigning segment (i.e., 1 - 8) and type (i.e., flu A or B) to a .fasta file that encodes DNA, _not protein!_

		# clone database into your local environment
		git clone https://github.com/anniewerner/JHU_seasonal_flu_surveillance/flu_db
		mkdir -p /complete_path_to <blast_directory>/blastdb
		mv /current_path_to <flu_db> /complete_path_to <blast_directory>/blastdb
  
4. change directory to where you have downloaded the NCBI BLAST+ files, make an input and output directory with your sequence files.

		# changing working directory & configuring input and output directories
   		cd /complete_path_to <blast_directory>
   		mkdir /complete_path_to <blast_directory>/<input_data>
   		mkdir /complete_path_to <blast_directory>/<output_data>
   
5. run blastn command to obtain results for your sequences of unspecified type and segment

  		# run BLAST to determine virus type & genome segment
   		blastn -task blastn \
   			-query $HOME/complete_path_to <blast_directory>/<input_data>/<your_sequences>.fasta \
   			-db $HOME/complete_path_to <blast_directory>/blastdb/influenza_annotation_blastdb.fasta \
   			-outfmt 10 \
   			-out <YYYYMMDD_name_of_output_file>.csv
   	
   	
