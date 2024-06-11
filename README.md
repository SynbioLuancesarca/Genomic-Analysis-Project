# Bioinformatic Genomic Analysis Project 
Analysis of Purinergic Pathway Overload Due to the Use of Cannabidiol in the Treatment of SARS-CoV-2\
The chosen article is available in this repository under the name ***Cannabidiol inhibits SARS-CoV-2 replication through***\
The software used were:
- [Galaxy](https://usegalaxy.org)
- [DAVID](https://ngdc.cncb.ac.cn/databasecommons/database/id/3061)
- [KEGG](https://www.genome.jp/kegg/)

  
## Overview
SARS-CoV-2 is responsible for COVID-19, with a range of symptoms ranging from mild to severe, highlighting the need for studies on alternative treatments due to the high rate of virus transmission. A recent study suggests that cannabidiol (CBD) may reduce cytokine activation; however, the purinergic system also plays a crucial role in inflammation. Furthermore, enzymes such as purine nucleoside phosphorylase (PNP) and AMP deaminase are implicated in purine metabolism and may have a significant influence on the body's response. The hypothesis is that CBD treatment could overload the purinergic system, potentially masking symptoms of SARS-CoV-2.

## Files
For this project, the files used were: 
- ***[Human.GRCh38.p13.annot.tsv.gz].gtf***, to use the human genome as the basis for the project
- ***[GSE168797_Raw_gene_counts_matrix.txt.gz].tabular***, how the table of genes used in the article
- ***[GSE168797_cortados].tabular***, how the table of selected genes is prepared for analysis

  
## Methodology
High-throughput RNA sequencing was conducted on the Illumina NovaSeq 6000 platform, with paired-end reads of 100 bases, using a cDNA library and transcriptomic library source. The reads underwent processing to ensure quality and adapter removal. Subsequently, they were mapped to the human genome (hg19 version) and SARS-CoV-2.

For differential gene expression analysis from RNA-Seq data, tags were added to identify treatments and sequencing, crucial for analysis with DESeq2. DESeq2 returns relevant statistics such as the table of Differentially Expressed Genes (DEGs), including information like log2-fold change (a measure of gene expression difference between two conditions on a logarithmic scale) and adjusted p-value (correction of p-value to control false positives in gene expression analysis) for each Ensembl ID. Annotation data from the human genome were then added to the table. Genes significantly differentially expressed between treatments were selected based on criteria of p-value < 0.05 and abs(log2FC) > 1.

Volcano plots and heatmaps were generated based on Z-scores, which express data deviation from the sample mean in terms of standard deviation, for better visualization.

In the functional enrichment step, only positively differentially expressed genes were input into the DAVID platform. This approach enabled a detailed understanding of biological functions and processes, utilizing gene ontology for categorization and the KEGG database to explore associated metabolic pathways.



## Results
- The PCA plot reveals the variability between treatment groups (cannabidiol or vehicle), showing that they cluster according to treatment type. The distance between the groups indicates that treatment has a significant impact on the samples.
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/c9291b5e-22ff-4229-9291-d5b5a0bd729b" width=600 height=200>

- The scatter plot calculates a final value representing the variability of the studied genes based on raw data, shown in blue. Most genes, represented by black points, are close to the final value, indicating consistent and predictable variation, suggesting data quality.
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/e19fd9bb-6b94-4e49-8bb8-00ec6102acaa" width=400 height=400>
  
- In the frequency histogram, the higher concentration of p-values equal to zero indicates significant differences in gene expressions evaluated between samples treated with cannabidiol and those treated with the vehicle.
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/f092a8df-1bb2-4557-84fe-9894f91271d2" width=400 height=400>

- The MA-plot indicates differences in gene expression between sample groups, highlighting genes with increased expression (points above the x-axis) or reduced expression (points below the x-axis). This raises questions about which genes might be more highly expressed, considering the significant reduction in cytokines indicated in the article during the inflammatory immune response.
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/9418c34d-a1f1-4ecc-b945-fb4ca3adfff7" width=400 height=400>
  
- In the Volcano plot, genes that surpass the thresholds of False Discovery Rate (FDR) and log FoldChange are highlighted, showing those positively regulated (in red) and negatively regulated (in blue). "Up" genes are significantly increased in expression under the condition of infection with cannabidiol compared to infection with the vehicle, while "Down" genes are decreased.
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/afc873c4-7d0c-42fc-a8bc-4d83e061a369" width=400 height=400>
  
- In the heatmap analysis, samples are displayed on the X-axis, with a dendrogram highlighting the similarity between their gene expression profiles. The Y-axis presents 1591 positively expressed genes, also accompanied by a dendrogram showing similarity between their expression levels. Samples are organized in the heatmap according to treatment type, divided into six columns representing distinct experimental conditions, including treatments with cannabidiol and vehicle. This indicates there are three replicates per treatment, organized into two main groups in the heatmap, each corresponding to an experimental condition.
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/ec4991ff-9303-4265-a169-1c1b13fd91ed" width=400 height=400>
  
  <img src="https://github.com/SynbioLuancesarca/Genomic-Analysis-Project/assets/168687335/b543847f-01f9-418d-80fe-5cc3ed489b29" width=400 height=400>


## Conclusions
Based on this information, it is believed that by analyzing only cytokine expression as a source of inflammation, the article may overlook other pathways that could also be involved. In this case, the purinergic pathway, which is associated with inflammatory responses, shows overexpression, indicating potential overload due to cannabidiol use. Instead of acting as an anti-inflammatory component as proposed, cannabidiol might be masking the effects of a specific pathway related to immune system cytokines. Consequently, to maintain organismal homeostasis, there could be an overload on another pathway.
