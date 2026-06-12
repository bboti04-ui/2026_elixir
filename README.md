# 2026_elixir
Az órán bemutatott tananyag

# Használat és szükséges eszközök, környezet kialakítása
A workflow a Biostar Handbook alapján készült: https://www.biostarhandbook.com/

## Környezet kialakítása
Linuxos Windows-alrendszerre, Ubuntu-ra és pixi-re lesz szükség.
A Linuxos Windows-alrendszert powershell-ben vagy a parancssorban lehet letölteni:
```
wsl --install
```
Az Ubuntu a Microsoft Store-ban elérhető

A környezet kialakításához az alábbi sort kell futtatni:
```
curl -fsSL https://data.biostarhandbook.com/setup/biostar.setup.2026.sh | bash
```

A szükséges eszközöket pixi-vel lehet hozzáadni:
```
# Initialize the project environment. Will create the pixi.toml file.
pixi init

# Add the bioconda channel
pixi workspace channel add bioconda

# Add the samtools package to the environment.
pixi add samtools

# Add the bwa aligner to the environment.
pixi add bwa

# Adding common bioinformatics tools to the environment
pixi add make bwa samtools bcftools trimmomatic sra-tools \
         fastqc seqkit fastp parallel csvtk wget ncbi-datasets-cli \
         ucsc-bedgraphtobigwig bedtools \
         jq python==3.12 'biopython<1.86' bio
```
A környezetet egy szóval tudod aktiválni:
```
# Activate the bioinfo environment with just one word
bioinfo
```

## Eszközök használata/futtatása

Bármelyik eszköz futtatásához írd ezt:
```
pixi run bwa
```
Vagy a környezet aktiviálása után:
```
# The bwa command can be run directly.
bwa

# Run the samtools command
samtools
```