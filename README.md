# Microbial diversity of an Antarctic subglacial community and high-resolution replicate sampling inform hydrological connectivity in a polar desert 

R. Campen, J. Kowalski, W.B. Lyons, S. Tulaczyk, B. Dachwald, E.C. Pettit, K.A. Welch, J.A. Mikucki

---

### Abstract

Antarctic subglacial environments host microbial ecosystems and are proving to be geochemically and biologically diverse. The Taylor Glacier, Antarctica, periodically expels iron-rich brine through a conduit sourced from a deep subglacial aquifer, creating a dramatic red surface feature known as Blood Falls. We used Illumina MiSeq sequencing to describe the core microbiome of this subglacial brine, and identified previously undetected but abundant groups including the candidate bacterial phylum Atribacteria and archaeal phylum Pacearchaeota. Our work represents the first microbial characterization of samples collected from within a glacier using a melt probe and the only Antarctic subglacial aquatic environment that, to date, has been sampled twice. A comparative analysis showed the brine community to be stable at the operational taxonomic unit level of 99% identity over a decade. Higher-resolution sequencing enabled deconvolution of the microbiome of subglacial brines from mixtures of materials collected at the glacier surface. Diversity patterns between this brine and samples from the surrounding landscape provide insight into the hydrological connectivity of subglacial fluids to the surface polar desert environment. Understanding subice brines collected on the surfaces of thick ice covers has implications for analyses of expelled materials that may be sampled on icy extraterrestrial worlds.

---

### Requirements

It is recommended to use the [Anaconda Python3](https://www.anaconda.com/download/) environment to ensure the majority of dependencies for running the code in this repository are met. To install the remaining dependencies run `pip install mothur-py seq-experiment`.

You will also require [mothur](https://github.com/mothur/mothur) (See below for version compatibility issues), and the Silva reference alignment which can be downloaded using the script `0_download_silva.py`. Before doing so ensure you have read to, and agreed to the Silva [Terms of Use/License Agreement](https://www.arb-silva.de/silva-license-information).

You will also need to download the raw sequence files which the NCBI Short Read Archive (SRA) under accession number `<insert_accession_numbers>`, and place them in the `data/raw_seq/` folder.

---

### Repository layout

```
this_is_outflow
|- README.md   			# Top level readme file (this file)
|- .gitignore  				# configuration for git of which files to ignore
|
|- data/				# raw and intermediate processed files
| |- 515806.oligos 			# oligos file for running mothur's make.contigs command
| |- HMP_MOCK.v35.fasta 		# sequences assosiated with the Mock Community sample used for seq.error
| |- sample_metadata.csv 		# table of sample metadata
| |+ raw_seqs/				# folder containing raw sequence files
| |+ processed/				# folder containing intermediate processed files
| |+ silva/				# folder containing downloaded Silva reference files (if downloaded)
| |+ tmp/				# temporary files created during analysis that can be deleted safely
|
|+ results/				# final results tables output from analysis
|
|- code/				# folder contianing scripts for sequence processing and data analysis
| |- 0_download_silva.py  		# download Silva v128 reference files (SEE BELOW)
| |- 1_process_sequences.py 		# run mothur sequence processing pipeline (SEE BELOW)
| |- 2_correlate_geochemistry.py 	# correlate geochemical parameters
| |- 3_estimate_alpha_diversities.py 	# estimate alpha diversities and correlate with geochemistry
| |- 4_EMB_core_microbiome.py 		# determine the EMB core microbiome OTU composition
| |- 5_identify_biomarkers.py 		# identify biomarkers using LefSe and correlate with geochemistry
```

legend:
* `|-` denotes file
* `|- <directory_name>/` denotes directory whose contents are listed
* `|+ <directory_name>/` denotes directory whose contents are not listed
* `| |-` denotes file/directory is within another directory


**CAUTION:** Due to a bug in mothur v1.39.5 (and earlier) the outputs will vary slightly between each run of any mothur commands. This should be resolved in the next release version, or can be avoided by using a build of the `Threads_373` branch of mothur from commit [`1e8aa08`](https://github.com/mothur/mothur/commit/1e8aa085dc33d2d874b9819fc869d6b000eb2ab7) onwards where this bug was fixed. Re-running the files as denoted with `SEE BELOW` in the above file structure with a version of mothur with this bug will produce different final results tables/figures. It is therefore advised to not rerun these files unless absolutely necessary, or without a compatible version of mothur. The outputs of these files are already in the `data/processed/` directory if needed. All other files have fully reproducibly outputs and can be rerun as much as desired.
