# K-mer-based Understanding of Genomes and Transcriptomes (Part 1)

The objectives of Part 1 are to 1. plot k-mer distributions from WGS data to understand genome properties, and 2. perform k-mer-based filtering and normalization of RNA-Seq data in preparation for de novo transcriptome assembly.

The WGS data for this assigment are from 2 pipefish species. You’ll use just the forward reads from both data sets.

The transcriptome of interest is the male brood pouch transcriptome of the Gulf pipefish, Syngnathus scovelli. The RNA-seq data are paired-end, 100 nt reads sequenced from Illumina TruSeq libraries. We will k-mer filter and normalize this RNA-Seq data. This assignment is the first of two. In the next assignment (6) We will learn how to run Trinity (but not actually run it), and evaluate different Trinity assemblies based on read sets filtered and/or normalized differently. Each assignment is worth 75 points.

# k-mer spectra for WGS data

Copy or link these files to a working directory on Talapas:
```
/projects/bgmp/shared/Bi623/assign5/ssc_wgs.fastq
/projects/bgmp/shared/Bi623/assign5/cha_wgs.fastq
```
1.	Using jellyfish (a k-mer counting tool), enumerate k-mers in the two data sets and format them for k-mer spectrum plotting. Use the Jellyfish/1.1.11-foss-2016b module. Check out the jellyfish documentation, but you can run it like this:
```
jellyfish count -t 8 -C -m 19 -s 5G -o 19mer_out_ssc ssc_wgs.fastq
jellyfish histo -o 19mer_out_ssc.histo outfile_from_jfish_count
```
2.	Read your ssc and cha .histo files into R and make a line plot of the spectrum for the first 200 rows in each case.
3.	What can you infer about these two genomes based on the k-mer spectra?

# k-mer filtering and normalization

You will the process_shortreads program, which is part of the Stacks package, to k-mer filter and normalize paired-end RNA-Seq reads. Use the Stacks/1.46 module on Talapas. For details on flags and parameters, see:
http://catchenlab.life.illinois.edu/stacks/comp/process_shortreads.php Note that this set includes fewer than 60 million read pairs. This is adequate coverage for many transcriptome assembly projects, but the requirements will vary depending on the study objectives, organism, tissue, etc
4.	Copy or link these files to a working directory on Talapas:
```
/projects/bgmp/shared/Bi623/assign5/SscoPEclean_R1.fastq
/projects/bgmp/shared/Bi623/assign5/SscoPEclean_R2.fastq
```

Filter the data for rare k-mers using kmer_filter, also part of the Stacks package. Perform rare k-mer filtering ONLY, and rename the new files SscoPEcleanfil_R1.fastq and SscoPEcleanfil_R2.fastq.
-	Use the defaults for k-mer size and --min_lim. Explain in a sentence or two what this is doing to your data. Donʼt worry about carrying “orphaned” reads to the next step. Also, keep the output files uncompressed.
5.	Run kmer_filter again, this time to normalize the cleaned, filtered data to 2 different coverages. To save time, run these as two sbatchscripts in parallel.
	
- a.	Normalize to 40X k-mer coverage; compress the output files, and rename the new files SscoPEcleanfil40x_R1.fastq and SscoPEcleanfil40x_R2.fastq.

- b.	Similarly, normalize the cleaned, filtered data to 20X k-mer coverage, compress the output files, and rename the new files SscoPEcleanfil20x_R1.fastq and SscoPEcleanfil20x_R2.fastq.

- c.	Use the default k-mer size of 15. Again, donʼt worry about carrying “orphaned” reads to the next step.

- d.	Briefly explain in a sentence or two what this is doing to your data.
5.	At this point you should have 4 sets of processed paired-end reads:
-	a set that has been cleaned
-	a set that has be cleaned and k-mer filtered
-	a set that has been cleaned, k-mer filtered, and normalized to 40X
-	a set that has been cleaned, k-mer filtered, and normalized to 20X
Count and report the number of total read pairs for each set.
6.	Now generate k-mer counts and histogram files using jellyfish (as above) 3 times - 1. on SscoPEclean_R1.fastq, 2. on SscoPEcleanfil_R1.fastq, and 3. on SscoPEcleanfil20x_R1.fastq Plot the spectra in R and include the figures with the rest of the assignment. How do the 3 RNA-Seq data spectra differ? How are they different from the WGS data spectra?

