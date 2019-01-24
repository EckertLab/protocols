##List of initial and common steps to process ddRAD-seq data

Some degree of familiarity with navigating the grid engine environment and linux is assumed. 
Data is assumed to be obtained from the Illumina 4000 seqencing platform, although the approach has worked for older platforms too.
We also assume that anaconda and dDocent are installed and in the current path of the user.
Most steps can be submitted as a job by writing a bash script and requesting multiple cores. 

Some resources by VCU:

https://goo.gl/hYAqTL

https://wiki.vcu.edu/display/unix/
___
## Procuring sequence files and demultiplexing

Once your libraries are sequenced you will recieve a ftp link from the company. Use `wget` to download the large file, one library at a time or as a series of jobs.
wget --user=`userID`--password=`userPass` ftp://serverID/folderName/raw_data/*.gz

**_To demultiplex_** your *.gz file, navigate to the directory and utilize gbsx. 

[GBSX](https://github.com/GenomicsCoreLeuven/GBSX)
[Herten et al. 2015](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/s12859-015-0514-3)

_Basic command_ for Demultiplexing (modify the flags as seen fit for your data)

/location/of/jdk1.8.0_101/bin/java -jar /location/of/GBSX/GBSX_v1.2.jar --Demultiplexer -f1 /path/to/library/file/XYZ.fq -i /path/to/barcodes.txt -gzip false -rad true -mb 2 -me 1 -ea /path/to/ecori.txt

barcodes.txt is a simple tab seperated file (r*c), where the rows (r) are your individuals in a given library and columns (c=3) are name of the individual, barcode sequence and the last column has EcorI repeated r times.
In the barcode file the individuals are listed from well A1:A12, then B1:B12 and so on. 

e.g [barcode file](https://github.com/EckertLab/protocols/blob/master/barcodes.txt)

ecori.txt is a tab seperated file with the following on the first line:  *EcoRI   AATTC*

Once done, examine the *.stats file to determine how many reads were retained.

___
## Trimming 
NOTE: This step is not neccessary but in some cases has improved the performance of assemblers. We recommend to conduct assembly (implemented in dDocent) both ways for your data to determine which is best.
You can also look at the fastq output for your library to determine if end trimming implemented in this step will be required. 
      
[fastp](https://github.com/OpenGene/fastp)
[Chen et al. 2018](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6129281/)

We will be trimming off the ends of our reads to make them all equal length. You can also trim on quality at this stage (not implemented in this documentation).

fastp -i inFile -o trim_out -t 1 -b 80

*To double check this step*
Check the average length of the reads in the file. Repeat this check, comparing the original file and trimmed file to make sure the average length has decreased on several files. The length will be greater than the base pairs you specified, as fastp learns the adaptors at the beginning of the sequence and does not include that in the remaining tail that is trimmed to your specified length. Some files may have a larger average length, as the trimming command also removes the last round of sequencing that is usually short and low quality reads.

 awk '{if(NR%4==2) {count++; bases += length} } END{print bases/count}' filename.F.fq.gz

___
## Mapping and SNP calling (*_Assuming denovo assembly_*)

This step is conducted using dDocent. There are several other options that have been implemented by other folks in lab. 
Check out:

[Chris Friedline](https://github.com/cfriedline)
[Brandon Lind](https://github.com/brandonlind)

            
            
You can either create a seperate environment for dDocent or have all the dependencies and dDocent in your path.

Please go over the tutorial in detail before starting this step:
[dDocent web](http://ddocent.com/)


**_Things to keep in mind:_**

  - Create a directory and copy all the fastq files into it.
  
  - File naming scheme. Pop and Ind should be seperated by "_". 
  
  - Follow dDocent's naming scheme for fastq files (use `rename` command in bash to change file extensions)
  
  - We keep the gap penalty, match and mismatch value to default, but you can play around with the similarity threshold. 
  
  - Trimming can be turned on or off depending upon your settings in the previous step. If you only used fastp to trim on length you can alow dDocent to utilize trimmomatic at this stage.
  If you have already trimmed on quality in the previous step, turn off this setting. If turned off, make sure to rename your files to match the trim format in dDocent. Also create a symlink here to all the raw fastq files for dDocent to work properly.
  
- Both cutoffs in dDocent (Number of unique sequences with X coverage and Number of unique sequences in more than X individuals) can be picked near the asymptote.

- Once reference.fasta is assembled and SNPs are called, use the file before the final dDocent filtering to conduct all our custom post-filering steps. This file is called TotalRawSNPs.vcf.

**_More option outide dDocent_**

**IMPUTATION**

Conduct imputation in [BEAGLE](https://faculty.washington.edu/browning/beagle/beagle.html), if needed, and intersect the imputed and TotalRawSNPs.vcf file to get the final set of SNPs.

**Post mapping to reference genome**(under development)

If reference genome is available and you choose to conduct post assembly mapping to the reference genome you can do so with [BLAST](https://www.ncbi.nlm.nih.gov/books/NBK279690/). Either set BLAST in your source or specify path to the executable while running the steps below. Note that these steps can be conducted soon after dDocent is run or after all the post-filtering steps are completed.

  - Download the species.fasta file and convert it to a blastable database using `makeblastdb`. 

  - Use the reference.fasta file outputed from dDocent to blast (use `blastn`) against the searchable species.fasta file you generated above. There are several options to be set in `blastn` and they depend on the average length of the contigs in reference.fasta, the degree of divergence between your species and the reference species for which the genome is available. Ideal to use output option 6,7 or 8.
  - Filter your text file in R or python to retain only queries that pass the predetermined threshold.
  
  - Now subset your TotalRawSNPs.vcf file using the queries retained in the step. This can be done using vcftools. Alternatively, if you have converted your vcf into 012 format, this step can be implemented in R.
  
  - This will now be your final set of SNPs that have some similarity to a reference genome.



___
## Post filtering

After you obtain your final set of snps (TotalRawSNPs.vcf), you will use [vcftools](http://vcftools.sourceforge.net/man_latest.html) and R to process the output and filter based on several population genetics and techinal criteria specific to the study system, sequencing platform and study design.

*_NOTE: While using vcftools remember to use the recode flag_*

**_Below are the major filtering steps::_**

  - Remove indels, remove SNPs with more than 50% missing data. 
  
  - Keep only biallelic SNPs and SNPs with a min phred score of 20. *Phred score cutoff not implemented for imputed SNPs*
  
  - Get depth per SNP and choose either the 50th or 75th percentile as the cutoff. i.e remove any SNP that has a depth greater than the cutoff value. (This step can be done in R or in python too). This step is essential for conifer species due to the abundance of TE and paralogs. *This step not implemented for imputed SNPs*
  
  - Determine minor allele frequency cutoff (depends on sample size and number of individuals per site). In general it should be set low enough to retain variation that might be specific to a population. Remove all SNPs below the cutoff. *This step can be done in R manually (after converting to 012 file) or using vcftools.*
  
  - Recode to count of minor allele using the `recodeA` command in plink or a custom R script.
  
  - Estimate Wright's FIS and only retain SNPs that have a value between 0.5 and -0.5. This cutoff gets rid of repeats again and also removes SNPs that might be called heterozygotes due to null alleles or insufficient reads to call heterozygotes. 
      

 



