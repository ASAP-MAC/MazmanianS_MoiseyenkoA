 - [OneDrive link to data and results](https://cuny907-my.sharepoint.com/:f:/g/personal/giacomo_antonello53_login_cuny_edu/EqYK-hqjR19Eg86ruPfCmDUBfJQDmHs1pOVXIozT3el-OA?e=l2DHdg)

 - Zenodo link, once available
 
 - SRA: PRJNA1259538
 
 - preprint link, once available
 
 - paper link, once available
 
# *Faecalibacterium prausnitzii*, depleted in the Parkinson’s disease microbiome, improves motor deficits in $\alpha$-synuclein overexpressing mice

Anastasiya Moiseyenko, Giacomo Antonello, Aubrey M. Schonhoff, Joseph C. Boktor, Kaelyn Long, Blake Dirks, Anastasiya D. Oguienko, Alexander Viloria Winnett, Patrick Simpson, Dorsa Daeizadeh, Rustem F. Ismagilov, Rosa Krajmalnik-Brown, Nicola Segata, Levi D. Waldron, and Sarkis K. Mazmanian

Abstract: Gut microbiome composition is altered in Parkinson’s disease (PD), a neurodegenerative disorder characterized by motor dysfunction and frequently accompanied by gastrointestinal (GI) symptoms. Notably, microbial taxa with anti-inflammatory properties are consistently depleted in PD patients compared to controls. To explore whether specific gut bacteria may be disease-protective, we assembled a microbial consortium of 8 human-associated taxa that are reduced in individuals with PD across multiple cohorts and geographies. Treatment of a-synuclein overexpressing (Thy1-ASO) mice, an animal model of PD, with this consortium improved motor and GI deficits. A single bacterial species from this consortium, Faecalibacterium prausnitzii, was sufficient to correct gut microbiome deviations in Thy1-ASO mice, induce anti-inflammatory immune responses, and promote protective colonic gene expression profiles. Accordingly, oral treatment with F. prausnitzii robustly ameliorated motor and GI symptoms, and reduced a-synuclein aggregates in the brain. These findings support the emerging hypothesis for functional contributions by the microbiome to PD and embolden development of potential probiotic therapies.

## Objective

Determine whether *F. prausnitzii* supplementation has an  impact on the 
microbiome composition in ASO mice compared to controls
  
## Experimental design

### Animal Models and treatment groups

- **WT Control**: Lab mice with specific pathogen free microbiomes administered
a control gavage consisting of phosphate-buffered saline (PBS) with sodium bicarbonate.

- **Thy1-ASO Control**: Lab mice overexpressing human $\alpha$-synuclein 
administered the same control gavage administered to **WT Control**

- **Thy1-ASO *F. prausnitzii***: Lab mice overexpressing human $\alpha$-synuclein 
administered a saline solution containing live *Faecalibacterium prausnitzii* 
cells.

All mice were administered the gavage $\frac{2}{week}$ between week 5 and 22.

### Metagenomics data

At week 22, mice underwent gastrointestinal and motor assessments, along with 
fecal pellet collection. DNA was extracted from the pellets to perform deep
shotgun sequencing.

Demultiplexed reads were uniformly processed with 
[curatedMetagenomicsNextflow](https://github.com/seandavi/curatedMetagenomicsNextflow).

Data analyzed in this repository are:
  
  - Taxonomic profiles (Species Genome Bin level) with [MetaPhlan 4.1.1](https://github.com/biobakery/MetaPhlAn/releases/tag/4.1.1)
  
  - Predicted MetaCyc pathways abundances with [HUMAnN 3.9](https://github.com/biobakery/humann/releases/tag/v3.9)

## Scripts overview
  
  - **01-data-preparation.Rmd**: Used to download `curatedMetagenomicsNextflow`
  output data and save it as human-readable files that can be re-imported into 
  R to generate a `TreeSummarizedExperiment` object. **IMPORTANT:** The script 
  stops with an error if there is an output directory with the same name. To 
  fully reproduce the data generation, you should delete the *.tse directories 
  in Data.
  
    - Input: 1 file
      - `Data/metadata.tsv`:
    - Output: 3 directories and 1 file
      - Data/MetaPhlAn.tse
      - Data/HUMAnN_pathways_unstratified.tse
      - Data/HUMAnN_genefamilies_unstratified.tse
      - `Data/GTDB_202403.tsv`
  
  - **Main-Analysis_SGB.Rmd** Generates the figures and tables related to 
  MetaPhlAn taxonomic data, both main and supplementary
    - Input: 2 files and 1 broken down TreeSummarizedExperiment object directory
      - Data/MetaPhlAn.tse
      - `Data/GTDB_202403.tsv`
      - `Data/Fp7_GI_motor_assessment.xlsx`
    - Output:
      - Everything contained in `results/SGB`, notably:
        - `Microbiome_Main_Figure.svg`
        - `Supplementary Figure 1 - alpha diversities and FB Ratio.svg`
        - `Supplementary Table {1-3}.tsv`

  - **Main-Analysis_pathway.Rmd** Generates the supplementary figures and tables
  related to HUMAnN 3.9 predicted pathways.
     - Input: 1 file and 1 broken down TreeSummarizedExperiment object directory
      - Data/HUMAnN_pathways_unstratified.tse
      - `Data/Fp7_GI_motor_assessment.xlsx`
    - Output:
      - Everything contained in results/pathway, notably:
        - `Suppelementary Figure 2.{svg,pdf,png}`
        
## Running scripts

Analyses were done on RStudio (version used: RStudio 2025.05.0+496, 
release f0b76cc00df96fe7f0ee687d4bed0423bc3de1f8) with R version 4.5.1. 

`sessionInfo()` is always shown at the end of each script

### In Rstudio (works on Windows as well)
  - point and click:
    - Open the script
    - install requested packages as suggested by RStudio
    - click on "knit"
  - from the R Console (example with 01-data-preaparation.Rmd):
    - `rmarkdown::render("01-data-preparation.Rmd")`
    
### Rscript from command line (not tested on Windows)

```
cd /path/to/repository
Rscript -e 'rmarkdown::render("01-data-preparation.Rmd")'
Rscript -e 'rmarkdown::render(Main-Analysis_SGB.Rmd")'
Rscript -e 'rmarkdown::render(Main-Analysis_pathway.Rmd")'
```

# Acknowledgements

Metagenomic analysis and figure creation was executed by G.A., while data processing was done by K.L., with supervision from N.S. and L.D.W.

This research was funded in part by Aligning Science Across Parkinson’s (ASAP-020495 and ASAP-000375) through the Michael J. Fox Foundation for Parkinson’s Research (MJFF), as well as the Heritage Medical Research Institute to S.K.M.
