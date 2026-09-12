# RNA-seq Analysis of Heat Stress-Induced Transposon Activation Correlates with 3D Chromatin Organization Rearrangement in Arabidopsis

## Group Information

### Group Number
**Group:** Group 1  
**Assigned Topic:** Heat stress

### Group Members and Roles

| Group Member | Assigned Role |
|---|---|
| Gedden D. Estrevillo | Literature lead  |
| Eugene Kim Ansag     | Data lead        |
| Ray Gee J. Lisondra  | Galaxy lead      |
| Jen Marie A. Martinez  | Documentation lead      |
| Jerson Lloyd Ortega  | Interpretation lead|


## Selected Paper

**Citation:**

Sun, L., Jing, Y., Liu, X., Li, Q., Xue, Z., Cheng, Z., Wang, D., He, H., & Qian, W. (2020). Heat stress-induced transposon activation correlates with 3D chromatin organization rearrangement in Arabidopsis. Nature Communications, 11(1), 1886. https://doi.org/10.1038/s41467-020-15809-5



## Research Question

The researchers wanted to know whether heat stress changes how DNA is physically organized inside the nucleus and whether these changes are connected to the activation of normally silenced transposable elements.

## Organism and Tissue

| Information | Description |
|---|---|
| **Organism** | *Arabidopsis thaliana* (Col‑0 ecotype)|
| **Tissue/Material** | Whole seedlings |
| **Experimental material** | 7-day-old Arabidopsis thaliana seedlings |

---

## Experimental Conditions

### Control

Wild-type *Arabidopsis thaliana* Col-0 seedlings were grown under normal growth conditions at a constant 22 °C with a 12-hour photoperiod. The plants were grown on ½ Murashige and Skoog (MS) medium containing 1% sucrose and 0.7% agar.

### Treatment

For the heat-stress treatment, 7-day-old Col-0 seedlings were exposed to alternating temperatures of 37 °C and 22 °C, with each temperature maintained for 12 hours, for a total of 3 days under a 12-hour photoperiod.

| Condition | Temperature | Duration | Photoperiod |
|---|---|---|---|
| **Control** | Constant 22 °C | Normal growth | 12 h |
| **Heat** | Alternating 37 °C / 22 °C | 3 days | 12 h |
| **Recovery** | Constant 22 °C after heat treatment | 3 days | 12 h |

## RNA-seq Accession Numbers

| Sample | Accession Number | Description |
|---|---|---|
| Sample 1 | SRR9257060 | Control-Rep1 |
| Sample 2 | SRR9257061 | Control-Rep2 |
| Sample 3 | SRR9257062 | Heat-Rep1    |
| Sample 4 | SRR9257062 | Heat-Rep2    |
---

## 7. Reference Genome and Annotation

| Component | Version |
|---|---|
| **Reference genome** | *Arabidopsis thaliana* TAIR10 |
| **Genome accession** | GCA_000001735.1 |
| **Gene annotation** | TAIR10.57 |
| **Annotation file** | `Arabidopsis_thaliana.TAIR10.57.gtf.gz` |


## 8. Original Authors' Analysis Pipeline

The original study used the following RNA-seq analysis pipeline:

                 RNA-seq Samples
                       │
                       ▼
               Illumina HiSeq 4000
               Paired-end, 150 bp
                       │
                       ▼
                  Trim Galore
            Adapter + quality trimming
                paired length 70
                       │
                       ▼
                  Clean Reads
                       │
                       ▼
                   TopHat2
                Read alignment to
               Arabidopsis TAIR10
           (Araport11-guided annotation)
                       │
                       ▼
                    SAMtools
            ┌──────────┬──────────┐
            │          │          │
          Sort       Index      Compress
            │          │          │
            └──────────┴──────────┘
                       │
                       ▼
             Unique-read filtering
           Multi-mapped reads removed
                       │
                       ▼
              ┌───────────────┐
              │ featureCounts │
              │ Gene/TE counts│
              └───────┬───────┘
                      │
                      ▼
                    DESeq2
             Differential Expression
                      │
                      ▼
                Differentially
            Expressed Genes / TEs

## Differences between the authors' pipeline and the group's pipeline
The group followed the original authors' RNA-seq workflow as closely as possible using the available resources in Galaxy. The authors used the Arabidopsis thaliana TAIR10 reference genome with Araport11 annotations, while the group obtained the reference genome from NCBI and used the available TAIR10.57 GTF annotation. For read alignment, the authors used TopHat2, but the group used TopHat because TopHat2 was not available among the Galaxy tools accessible to the group. The remaining steps, including read trimming, SAMtools processing, and featureCounts, were performed using the available Galaxy tools and settings that most closely matched the original workflow.

## Quality Control Results

Quality control of the RNA-seq reads was assessed using FastQC, and the results from all samples were summarized using MultiQC.

The main quality metrics obtained from the MultiQC report were sequence duplication, GC content, average sequence length, median sequence length, and FastQC module failures.

**MultiQC Summary**

| QC Metric | Forward Reads | Reverse Reads |
|---|---:|---:|
| % Duplicates | 59.45% | 56.40% |
| % GC | 45.02% | 45.01% |
| Average Sequence Length | 150 bp | 150 bp |
| Median Sequence Length | 150 bp | 150 bp |
| % FastQC Modules Failed | 20.0% | 20.0% |

**Interpretation**

The RNA-seq reads had an average and median sequence length of 150 bp, which is consistent with the paired-end 150-bp sequencing used in the original study. The GC content was approximately 45% for both forward and reverse reads.

The sequence duplication levels were 59.45% for forward reads** and 56.40% for reverse reads. These values indicate a relatively high level of sequence duplication, which should be considered when interpreting the sequencing quality.

The MultiQC report also indicated that 20% of the FastQC modules were marked as failed. These results were reviewed together with the other QC metrics rather than using the failure percentage alone to determine whether the data were suitable for further analysis.

> **Note:** The MultiQC values reported here summarize the available FastQC results for the RNA-seq datasets analyzed in this study.

## RNA-seq Mapping Results

The RNA-seq reads were mapped to the *Arabidopsis thaliana* reference genome using TopHat in Galaxy. The mapping results were evaluated based on the total number of input read pairs, overall mapping percentage, and percentage of uniquely mapped reads.

**Mapping Statistics** 

| Sample | Total Reads | Overall Mapped (%) | Uniquely Mapped (%) | Unusually Low Mapping |
|---|---:|---:|---:|---|
| Control-Rep1 | 32,997,552 read pairs | 90.8% | 96.2% | None |
| Control-Rep2 | 32,818,658 read pairs | 89.4% | 96.1% | None |
| Heat-Rep1 | 33,399,259 read pairs | 92.0% | 94.6% | None |
| Heat-Rep2 | 25,815,822 read pairs | 91.8% | 94.5% | None |

**Mapping Result Interpretation**

The overall mapping rates ranged from 89.4% to 92.0% across the four samples. The percentage of uniquely mapped reads ranged from 94.5% to 96.2% among the mapped reads. Overall, the samples showed good mapping performance, and none of the samples had an unusually low mapping rate.

The high mapping percentages indicate that most of the sequencing reads were successfully aligned to the *Arabidopsis thaliana* reference genome, allowing the samples to proceed to downstream read-counting analysis using featureCounts.

> **Note:** The uniquely mapped percentage represents the proportion of mapped aligned reads classified as unique and should not be interpreted as the percentage of all input reads.

## Differential Gene Expression

### DESeq2 Results

| Category | Observation |
|---|---|
| **Number of genes tested** | 32,833 |
| **Number of significantly differentially expressed genes** | 541 genes |
| **Genes with positive log2 fold change** | AT4G26530, AT1G54000, AT3G05730 |
| **Genes with negative log2 fold change** | AT1G09140, AT1G80130, AT5G47600 |
| **Adjusted p-value / FDR threshold** | 0.05 |

## Simple Interpretation of DESeq2 Results

| Result | Simple Meaning |
|---|---|
| **Positive log2 fold change** | Gene expression is higher in the treatment/stress condition, depending on the comparison direction. |
| **Negative log2 fold change** | Gene expression is lower in the treatment/stress condition, depending on the comparison direction. |
| **Adjusted p-value < 0.05** | The expression difference is considered statistically significant. |
| **Adjusted p-value ≥ 0.05** | The analysis does not provide strong statistical evidence of differential expression. |

---

## Selected Genes for Biological Interpretation

| Gene ID | Log2 Fold Change | Adjusted p-value | Regulation Status | Known or Predicted Function | Connection to Stress |
|---|---:|---:|---|---|---|
| **AT5G59720** | -11.42 | 0 | Downregulated | Low molecular weight heat shock protein / chaperone | **Heat / Osmotic Stress:** Typically acts as a molecular chaperone to protect proteins from heat denaturation. Its strong downregulation may indicate cellular shutdown or reprioritization under prolonged stress conditions. |
| **AT5G48570** | -6.77 | 0 | Downregulated | Purple acid phosphatase superfamily protein; dual-localized to mitochondria and chloroplasts and involved in carbon metabolism | **Salinity / Metabolic Stress:** Downregulation may be associated with reduced phosphate recycling and changes in organellar carbon metabolism under adverse environmental conditions. |
| **AT2G29500** | -10.17 | 0 | Downregulated | Class I small heat shock protein (17.6 kDa molecular chaperone) | **Heat / Oxidative Stress:** Functions in preventing protein aggregation and helping manage cellular damage associated with heat and oxidative stress. |
| **AT1G70850** | 4.32 | 5.25 × 10^-115 | Upregulated | Major Latex Protein (MLP)-like protein 34 | **Infection / Pathogen Defense:** Associated with defense signaling responses, pathogen invasion, and cross-talk between biotic and abiotic stress responses. |
| **AT2G42530** | 4.37 | 3.91 × 10^-151 | Upregulated | Cold-regulated 15B protein; LEA-like chaperone | **Salinity / Osmotic / Temperature Stress:** Associated with protection of chloroplast stromal membranes against dehydration, osmotic stress, and abiotic membrane damage. |

## Overall Interpretation

The DESeq2 analysis identified 541 significantly differentially expressed genes using an adjusted p-value threshold of 0.05. Both upregulated and downregulated genes were observed. The selected genes show changes in expression associated with heat, osmotic, metabolic, oxidative, and pathogen-related stress responses, suggesting that environmental stress can affect several cellular processes, including protein protection, metabolism, membrane stability, and defense signaling.


# Comparison with the Published Results

| Analysis Step | Original Authors | Our Galaxy Re-analysis |
|---|---|---|
| **Highlighted genes** | Heat-shock genes such as **HSP70, HSP101, HSP21, and HSP18.2** | The same specific highlighted genes were not confirmed. Other heat-shock and stress-related genes, such as **AT5G59720** and **AT2G29500**, were identified |
| **Overall biological response** | Heat stress caused major changes in gene expression, including activation of heat-shock-related genes | Heat stress also caused changes in gene expression, with **541 significant DEGs**, including heat- and stress-related genes |
| **Mapping results** | RNA-seq reads were mapped to the reference genome using the authors' workflow | High overall mapping rates of approximately **89–92%** were obtained |
| **Gene counting** | **featureCounts** was used to obtain gene counts | **featureCounts** was used to obtain gene counts |
| **Differential expression** | **DESeq2** identified **4,767 significant genes** under heat stress: 2,711 upregulated and 2,056 downregulated | **DESeq2** identified **541 significant DEGs**, including both upregulated and downregulated genes |
| **RNA-seq aligner** | **TopHat2** | **TopHat**, because TopHat2 was not available in our Galaxy tools |
| **Reference genome** | **TAIR10** | *Arabidopsis thaliana* reference genome obtained from **NCBI** |
| **Annotation** | **Araport11** | **NCBI annotation** |
| **Samples analyzed** | Control, Heat, and Recovery samples were included in the original study | **4 samples available in our assigned dataset:** 2 Control and 2 Heat |

## Limitations

One limitation of our re-analysis was that we could not reproduce some parts of the authors' workflow exactly. The authors used TopHat2 for RNA-seq alignment, but we used TopHat because TopHat2 was not available in our Galaxy tools. We also could not obtain the same TAIR10 reference genome and Araport11 annotation used in the study because access to the original resources required a subscription. Instead, we obtained the Arabidopsis thaliana reference genome and annotation from NCBI. These differences may have affected read alignment, gene assignment, and differential expression results. Therefore, our analysis reproduced the general workflow, but differences in the software and reference files may have contributed to why we identified 541 significant DEGs, compared with the 4,767 significant genes reported by the authors.

## Group Conclusion 

Overall, this activity helped us understand how RNA-seq can be used to study gene expression by sequencing RNA-derived fragments and measuring the number of reads associated with each gene. We learned that the genome FASTA provides the organism's DNA sequence, while RNA-seq FASTQ files contain the actual sequencing reads with quality information. We also learned that genome annotation is important because it provides the locations and identities of genes and other genomic features, allowing reads to be assigned and counted correctly.

Through the analysis, we understood the importance of biological replicates, normalization, and adjusted p-values in making reliable comparisons between samples. We also learned how to interpret upregulated and downregulated genes using changes in transcript abundance and log2 fold change. Changes in gene expression can help organisms respond to environmental stress by altering genes involved in protection, metabolism, and defense. However, we also learned that increased RNA abundance does not always mean increased functional protein because protein production and regulation can occur at different levels.

Finally, this activity showed us that RNA-seq results may differ between analyses because of differences in reference genomes, annotations, read processing, filtering, software, and analysis parameters. Therefore, careful documentation and consistent methods are important for reproducibility. Overall, RNA-seq provides a powerful way to examine how gene expression changes under different biological conditions and helps us better understand how organisms respond to stress.
