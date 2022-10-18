# RNAseq_illumina
RNA-seq analysis of Paired-end reads from honeybee mandibles using STAR 2.7.0 aligner, featureCounts, and DESeq2 for differential analysis.

##Run STAR aligner to map reads to genome. 
#Generate genome index

mkdir starAligned
STAR --runThreadN 4 --runMode genomeGenerate --genomeDir starAligned --genomeFastaFiles /path/to/FASTA-file --sjdbGTFfile /path/to/GTF_file

#Align reads in zipped FASTQ files to output a BAM file to be interpreted by featureCounts. There are two sets of paired end reads per sample. 

mkdir sampleName/sampleAlignment
STAR --runThreadN 4 readFilesIn /path/to/FASTQ1r1.gz,/path/to/FASTQ2r1.gz /path/to/FASTQ1r2.gz,/path/to/FASTQ2r2.gz --genomeDir starAligned --outFileNamePrefix sampleName --outSAMtype BAM --readFilesCommand gunzip -c 


##Generate counts from the BAM file generated in STAR, using the subread package featureCounts. All BAM files can be provided as input to be incorporated into a single output file.  

featureCounts -a /path/to/annotationFile -o sampleNameCounts.txt -g gene_id sampleName1Counts.BAM sampleName2Counts.BAM sampleName3Counts.BAM 

