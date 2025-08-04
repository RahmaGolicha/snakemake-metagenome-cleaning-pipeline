
This Snakemake workflow automates the preprocessing of raw metagenomic sequencing reads to generate high-quality cleaned reads ready for downstream analysis such as assembly.
Overview of Workflow Rules

	•	fastp: Performs quality control and trimming of raw paired-end reads. Removes low-quality bases, adapters, and filters out poor-quality reads to improve data quality.
	•	bowtie2: Aligns the cleaned reads to a reference genome (e.g., human genome) to identify and separate host contamination from microbial reads.
	•	samtools:sam_to_bam: Converts the alignment files from SAM format to BAM format, which is a compressed binary format suitable for efficient processing…
	•	samtools_retain_unmapped_reads: Extracts reads that did not map to the reference genome (unmapped reads), effectively enriching for microbial sequences by removing host contamination.
	•	samtools_sort_bam: Sorts the BAM files by genomic coordinates, which is required for many downstream tools and improves file indexing.
	•	samtools_cleanfastqc: Runs quality control checks (FastQC) on the cleaned and host-depleted reads to verify the quality and integrity of the processed data.
Purpose
By chaining these steps, the pipeline ensures that raw metagenomic data is cleaned, filtered to remove host contamination, properly formatted, and quality-checked — providing a robust foundation for accurate microbial community analysis and assembly.

Command: When running it on a cluster/farm:
snakemake --use-conda -k -j 100 --profile config/lfs --rerun-incomplete --latency-wait 120 --scheduler greedy -n
