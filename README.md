# metagenomics-lib

This file will be updated. The repository contains materials and literature on different topics related to unix, bioinformatics, metagenomics.

Далее следует список программ для функциональной аннотации геномов и метагеномов.
The following is the list of software dedicated to functional profiling of genomes and metagenomes.

1. FeGenie: Программа для поиска генов цикла железа:

  FeGenie: HMM-based identification and categorization of iron genes and iron gene operons in genomes and metagenomes.
  
  https://github.com/Arkadiy-Garber/FeGenie
  
  Garber AI, Nealson KH, Okamoto A, McAllister SM, Chan CS, Barco RA et al. FeGenie: a Comprehensive Tool for the identification of Iron genes and Iron Gene neighborhoods in Genome and Metagenome assemblies. Front Microbiol. 2020;11.

2. DiSCo: Программа для поиска генов цикла серы:

  DiSCo: Dsr-dependent dIssimilatory Sulfur metabolism Classification tOol - Automatic detection and prediction of enzyme type of proteins involved in Dsr-dependent dissimilatory sulfur metabolism.

  https://github.com/Genome-Evolution-and-Ecology-Group-GEEG/DiSCo

  Neukirchen, Sinje, and Filipa L. Sousa. "DiSCo: a sequence-based type-specific predictor of Dsr-dependent dissimilatory sulphur metabolism in microbial data." Microbial Genomics 7.7 (2021): 000603.

3. METABOLIC: Программа для поиска генов циклов серы, азота, углерода и "других" от Karthik Anantharaman, очень известного автора, исследователя и биоинформатика в области микробной экологии:

  METABOLIC: This software enables the prediction of metabolic and biogeochemical functional trait profiles to any given genome datasets. These genome datasets can either be metagenome-assembled genomes (MAGs), single-cell amplified genomes (SAGs)   or pure culture sequenced genomes. It can also calculate the genome coverage. The information is parsed and diagrams for elemental/biogeochemical cycling pathways (currently Nitrogen, Carbon, Sulfur and "other") are produced.

  https://github.com/AnantharamanLab/METABOLIC

  Zhou, Zhichao, et al. "METABOLIC: high-throughput profiling of microbial genomes for functional traits, metabolism, biogeochemistry, and community-scale functional networks." Microbiome 10.1 (2022): 33.

4. Metascan: Программа для поиска в метагеномах более сотни экологически значимых генов из восьми категорий. Тоже на основе HMM-профилей. 

  Metascan: Metascan works on a basis of ~180 different metabolic genes, that are key-genes or important genes in metabolic processes. McrA for instance, is needed for the conversion of methyl-CoM into methane. Without mcrA, there is no       methanogenesis. Therefore, the amount of mcrA in a sample can be seen as a measure of the potential for Methanogenesis. The complete key-gene set is divided into 8 main subsets:

  1. Methane cycle
  2. Nitrogen cycle
  3. Sulphur cycle
  4. Oxygen respiration
  5. C1 compounds
  6. Carbon fixation
  7. Hydrogen
  8. Miscellaneous metal cycling

  https://github.com/gcremers/metascan

  Cremers, Geert, et al. "Metascan: METabolic analysis, SCreening and annotation of metagenomes." Frontiers in Bioinformatics 2 (2022): 861505.
