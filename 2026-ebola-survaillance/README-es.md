A Makefile az NCBI datasets-ről szerzett URL-okkal dolgozik

https://www.ncbi.nlm.nih.gov/datasets/

# The URL to the annotation.
GFF_URL=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.gff.gz

# The URL to the genome FASTA file.
FASTA_URL=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.fna.gz

Az első lépés, hogy letöltsd a genomot (automatikusan indexel is)
///
make download
///

Második lépés, hogy letöltsd a read-eket az SRA-ból. Limitáld a LIMIT-hez a read-eket, használd a fastq-dump parancsot.
///
make fastq
///

Harmadik lépés, hogy illeszd a read-eket a genomhoz.
///
make align
///
