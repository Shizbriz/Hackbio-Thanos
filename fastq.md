
# HOW TO RETRIEVE FASTQ FILES FROM ENA
Data can be retrieved from ENA using enaBrowserTools (https://github.com/enasequence/enaBrowserTools). enaBrowserTools is a set of scripts that interface with the ENA web services to download data from ENA easily, without any prior knowledge of scripting required. However, python and basic knowledge of how to use the command line are required. enaBrowserTools consists of two tools; enaDataGet and enaGroupGet.

**enaDataGet**
This tool downloads all data for a given sequence, assembly, WGS set, run, experiment or analysis accession. Printing help (**enaDataGet --help**) in the command line shows what arguments are available for enaDataGet and from there, you can choose the file format (submitted, fastq, sra) you want to download for each type of data record. For this guide, FASTQ format is used. Simply choose the desired file format, specify the accession and provide a destination directory and the raw read file will be downloaded. If a destination directory isn't provided, a new directory is created in the directory from which the command is run to hold all the files downloaded.

_Example_
To download the latest version of the _Mycobacterium bovis_, MB4, WGS project CDHE01000000 data:

> enaDataGet -f fastq -d <destination/directory> CDHE01
CDHE, CDHE01000000, and CDHE00000000 can also be used to download this set.

To also download the run metadata, the "-m" argument is used which downloads the ENA records in XML. This is only available for run and analysis records.

> enaDataGet -f fastq - d <destination/directory> -m CDHE01

__enaGroupGet__
This tool downloads all data of a particular group (sequence, WGS, assembly, analysis) for a given sample or study accession. It downloads all raw reads in a study or all analyses of a sample in bulk. Printing help (**enaGroupGet --help**) in the command line shows what arguments are available for enaDataGet and from there, you can choose the file format (submitted, fastq, sra) you want to download for each type of data record. FASTQ format would also be used here. If the data was submitted via an INSDC partner such as NCBI or DDBJ, the files will not be available. If a destination directory isn't provided, a new directory is created in the directory from which the command is run to hold all the files downloaded.

_Example_
To download the read data in FASTQ format for the local surveillance of infectious diseases and antimicrobial resistance from sewage project:

> enaGroupGet -g read -f fastq - d <destination/directory> PRJEB13832

To also download the run metadata, the "-m" argument is used which downloads the ENA records in XML. This is only available for run and analysis records.

> enaGroupGet -g read -f fastq - d <destination/directory> -m PRJEB13832



# HOW TO RETRIEVE FASTQ FILES FROM NCBI
Data can be retrieved from NCBI Sequence Read Archive (SRA) using tools such as Fastq-dump, SeqSphere+ and Kingfisher. SeqSphere+ can be used to also retrieve data from EMBL -EBI and DDBJ, while Kingfisher can also be used to retrieve files from ENA, AWS and GCP.

**Fastq-dump**
Fastq-dump is a direct NCBI tool used for retrieving data from the SRA. More information can be obtained on https://ncbi.github.io/sra-tools/fastq-dump.html. Fastq is used by;

> fastq-dump [options] <path/file> [<path/file> ...]
> fastq-dump [options] <accession>

-h | --help displays ALL options, general usage, and version information

*Example*
> fastq-dump -X 5 -Z SRR390728
Prints the first five spots (-X 5) to standard out (-Z). This is a useful starting point for verifying other formatting options before dumping a whole file.

> fastq-dump -I --split-files SRR390728
Produces two fastq files (--split-files) containing ".1" and ".2" read suffices (-I) for paired-end data.

> fastq-dump --split-files --fasta 60 SRR390728
Produces two (--split-files) fasta files (--fasta) with 60 bases per line ("60" included after -- fasta).

> fastq-dump --split-files --aligned -Q 64 SRR390728
Produces two fastq files (--split-files) that contain only aligned reads (--aligned; Note: only for files submitted as aligned data), with a quality offset of 64 (-Q 64) Please see the documentation on svdb-dump if you wish to produce fasta/qual data.

Fastq-dump tool has been replaced by fasterq-dump tool which runs faster and is better suited for large-scale conversion of SRA objects into FASTQ files that are common on sites with enough disk space for temporary files. However, fastq-dump is still supported as it handles more corner cases than fasterq-dump, but it is likely to be deprecated in the future. More information on fasterq-dump can be obtained on https://github.com/ncbi/sra-tools/wiki/HowTo:-fasterq-dump



**SeqSphere+**
SeqSphere+ can be used to download FASTQ files from NCBI Sequence Read Archive (SRA). To run SeqSphere+, invoke the function Tools | Download FASTQ from SRA to open a dialog window and enter or import the NCBI accessions that should be downloaded. The following types of accessions are supported (NCBI, EMBL-EBI, DDBJ):

SRA Run Accession (SRR.., ERR..., DRR...)
SRA Experiment Accession (SRX.., ERX..., DRX...)
SRA Sample Accession (SRS.., ERS..., DRS...)
SRA Study Accession (SRP.., ERP..., DRP...)
BioSample Accession (SAM...)
BioProject Accession (PRJ...)

More details about SeqSphere+ can be obtained on https://www.ridom.de/u/Download_FASTQ_from_SRA.html

