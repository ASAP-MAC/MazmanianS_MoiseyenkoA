[OneDrive link to data and results](https://cuny907-my.sharepoint.com/:f:/g/personal/giacomo_antonello53_login_cuny_edu/EqYK-hqjR19Eg86ruPfCmDUBfJQDmHs1pOVXIozT3el-OA?e=l2DHdg)

# *Faecalibacterium prausnitzii*, depleted in the Parkinson’s disease microbiome, improves motor deficits in $\alpha$-synuclein overexpressing mice

Anastasiya Moiseyenko, Giacomo Antonello, Aubrey Schonhoff, Kaelyn Long, 
Joseph Boktor, Blake Dirks, Anastasiya Oguienko, Alex Villoria-Winnett, 
Rustem Ismagilov, Rosa Krajmalnik-Brown, Nicola Segata, Levi Waldron, 
Sarkis K. Mazmanian

## Experimental Design

**The Objective** is to determine whether *F. prausnitzii* supplementation has an 
  impact on the microbiome composition in ASO mice compared to controls
  
### Animal Models

- **Wildtype (WT)** mice and **alpha-synuclein overexpressing (ASO)** mice, which model PD-like symptoms.  
- Treatment duration: **5 to 22 weeks of age**, with gavage administered twice per week.  

### Treatment Groups

| Cohort             | Treatment                                                  | Sample label |  
|--------------------|------------------------------------------------------------|--------------|  
| **Wild type (WT)** | Vehicle (phosphate-buffered saline [PBS] with sodium bicarbonate)      | W    |
| **Alpha-synuclein overexpression Control (ASO-C)**        | Vehicle (phosphate-buffered saline [PBS] with sodium bicarbonate) | C          |  
| **Alpha-synuclein overexpression + F. prausnitzii (ASO-FP)**             | *Faecalibacterium prausnitzii* (Fp)  | F          |  

### Metagenomics data
  
  - **Data generated:** Deep shotgun metagenomics followed by uniform processing
  with [curatedMetagenomicsNextflow](https://github.com/seandavi/curatedMetagenomicsNextflow).
  The main data output are [MetaPhlan 4.1.1](https://github.com/biobakery/MetaPhlAn/releases/tag/4.1.1) taxonomic profiles
  and [HUMAnN 3.9](https://github.com/biobakery/humann/releases/tag/v3.9) predicted functional UniRef90 gene families and MetaCyc 
  pathways

## Metagenomic Analyses

### Scripts overview
  
  - **01-data-preparation.Rmd** takes the `Data/metadata.tsv` as input, and
  uses it to download, prepare and store necessary data as human-readable files
  that can be re-imported to generate a `TreeSummarizedExperiment` object.
  
  - **Main-Analysis_SGB.Rmd** Generates the figures and tables related to 
  MetaPhlAn taxonomic data, both main and supplementary
  
  - **Main-Analysis_pathway.Rmd** Generates the supplementary figures and tables
  related to HUMAnN 3.9 predicted pathways.

### Running a script in Rstudio

The easiest way run these scripts is to install RStudio 
(version used: RStudio 2025.05.0+496, 
release f0b76cc00df96fe7f0ee687d4bed0423bc3de1f8).
Then open the script of interest and install necessary package in the `setup`
chunk. You can then knit the document by pressing the "knit" button

### Running a script from the command line

```
cd /path/to/repository
Rscript -e 'rmarkdown::render("01-data-preparation.Rmd")'
Rscript -e 'rmarkdown::render(Main-Analysis_SGB.Rmd")'
Rscript -e 'rmarkdown::render(Main-Analysis_pathway.Rmd")'
```
