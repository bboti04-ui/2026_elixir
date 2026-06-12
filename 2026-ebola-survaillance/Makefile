# The URL to the annotation.
GFF_URL=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.gff.gz

# The URL to the genome FASTA file.
FASTA_URL=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.fna.gz

# The name of the genome.
GENOME_NAME=ebola-mayinga

# The path to the genome FASTA file.
GENOME_FASTA=refs/$(GENOME_NAME).fna

# The path to the genome GFF file.
GENOME_GFF=refs/$(GENOME_NAME).gff

# The SRR ID of the sample.
SRR=SRR1553425

# The name of the alignment BAM file.
BAM=alignments/$(SRR).bam

# The number of reads to use for the analysis.
LIMIT=1000

# The path to the read files.
R1_READS=reads/$(SRR)_1.fastq
R2_READS=reads/$(SRR)_2.fastq


# ---------------------- No CHANGES BELOW THIS LINE ----------------------
help:
	@echo "Use the source, Luke!"

# Make the directories that are needed then download and unzip the fasta and gff files and index the genome with bwa.
download:
	mkdir -p refs
	wget -O $(GENOME_FASTA).gz $(FASTA_URL)
	wget -O $(GENOME_GFF).gz $(GFF_URL)
	gunzip -f $(GENOME_FASTA).gz
	gunzip -f $(GENOME_GFF).gz
	bwa index $(GENOME_FASTA)

# Download the reads from SRA. Limit to LIMIT reads use the fastq-dump command.
fastq:
	mkdir -p reads
	fastq-dump -X $(LIMIT) --outdir reads --split-files $(SRR)

# Align the reads to the genome.
align: download fastq
	mkdir -p alignments
	bwa mem -t 4 $(GENOME_FASTA) $(R1_READS) $(R2_READS) | samtools view -bS - > $(BAM)
	samtools sort -o $(BAM).sorted.bam $(BAM)
	samtools index $(BAM).sorted.bam
	samtools flagstat $(BAM).sorted.bam

.PHONY: help download fastq align