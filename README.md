# LRCAGE (long-read CAGE)
This repository contains custom scripts, inclusing calling peaks, retaining a list of confident transcripts, and building a proteome database for immunopeptidome analysis.

1. Installation
   * Run scripts using docker images
   1. Download scripts from github
   ```
   cd <your installation directory>
   git clone https://github.com/juheon/LRCAGE.git
   ```
   2. Download docker images from dockerhub
   ```
   docker pull jhmaeng/lrcage
   docker images ; See if you can find jhmaeng/lrcage
   ```
   3. Modify and run “run_with_docker.sh” script in ”your installation directory”
   
2. List of custom scripts
   1. callpeak: a script to call peaks from LRCAGE, LRhex, and nanoCAGE data
   ```
   usage: LRCAGE callpeak [-h] --inputlist INPUTLIST --peak PEAK
                          (--tpm TPM | --readcount READCOUNT) [--gcap GCAP]
                          [--gcap_mincount GCAP_MINCOUNT]
                          [--half_peak_width HALF_PEAK_WIDTH] [--thread THREAD]

   optional arguments:
     -h, --help            show this help message and exit
     --inputlist INPUTLIST
                           list of input bam files
     --peak PEAK           output peak file name
     --tpm TPM             minimum TPM per peak
     --readcount READCOUNT
                           minimum read count per peak
     --gcap GCAP           minimum G-cap ratio
     --gcap_mincount GCAP_MINCOUNT
                           minimum number of soft-clipped G reads
     --half_peak_width HALF_PEAK_WIDTH
                           half peak size
     --thread THREAD       number of threads
   ``` 
   2. filtertx: a script to retain a list of confident transcripts using transcripts identified from LRCAGE data and a list of peaks.
   ```
   usage: LRCAGE filtertx [-h] --gtf GTF --talon TALON [--libinfo LIBINFO]
                          [--mincount MINCOUNT] [--peak PEAK]
                          [--peakratio PEAKRATIO] --oprefix OPREFIX

   optional arguments:
     -h, --help            show this help message and exit
     --gtf GTF             input gtf file
     --talon TALON         input TALON.tsv file
     --libinfo LIBINFO     library size information
     --mincount MINCOUNT   minimum count to define confident transcripts
     --peak PEAK           peaks used to retain transcripts with complete 5' ends
     --peakratio PEAKRATIO
                           minimum fraction of reads for peak-transcript pair per
                           trancsript
     --oprefix OPREFIX     prefix for output files
   ```
   3. buildprot: a script to create a proteome database using newly characterized transcripts as input.
   ```
   usage: LRCAGE buildprot [-h] --gtf GTF --ref REF [--txinfo TXINFO]
                           [--thread THREAD] --oproteome OPROTEOME --refproteome
                           REFPROTEOME --refgtf REFGTF
   
   optional arguments:
     -h, --help            show this help message and exit
     --gtf GTF             input gtf file
     --ref REF             reference genome fasta
     --txinfo TXINFO       transcript information
     --thread THREAD       number of threads
     --oproteome OPROTEOME
                           output proteome
     --refproteome REFPROTEOME
                           reference proteome
     --refgtf REFGTF       reference gtf
   ```
3. WashU Epigenome Browser links
* [CTSS analysis - H1299 DMSO](https://epigenomegateway.wustl.edu/browser/?genome=hg38&sessionFile=https://wangftp.wustl.edu/~jmaeng/publication/H1299_LRCAGE_CTSS_DMSO.json)
* [Epigenetic treatment-induced transcripts - H1299 DACSB and DMSO](https://epigenomegateway.wustl.edu/browser/?genome=hg38&sessionFile=https://wangftp.wustl.edu/~jmaeng/publication/H1299_LRCAGE_transcripts_DACSB.json)
