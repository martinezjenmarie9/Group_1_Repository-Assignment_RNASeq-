# RNA-seq Analysis of Heat Stress-Induced Transposon Activation Correlates with 3D Chromatin Organization Rearrangement in Arabidopsis

## 1. Group Information

### Group Number
**Group:** Group 1  
**Assigned Topic:** Heat stress

### Group Members and Roles

| Group Member | Assigned Role |
|---|---|
| Gedden D. Estrevillo | Literature lead  |
| Eugene Kim Ansag     | Data lead        |
| Ray Gee J. Lisondra  | Galaxy lead      |
| Jerson Lloyd Ortega  | Interpretation lead|


## Selected Paper

**Citation:**

Sun, L., Jing, Y., Liu, X., Li, Q., Xue, Z., Cheng, Z., Wang, D., He, H., & Qian, W. (2020). Heat stress-induced transposon activation correlates with 3D chromatin organization rearrangement in Arabidopsis. Nature Communications, 11(1), 1886. https://doi.org/10.1038/s41467-020-15809-5



## 3. Research Question

The researchers wanted to know whether heat stress changes how DNA is physically organized inside the nucleus and whether these changes are connected to the activation of normally silenced transposable elements.

## 4. Organism and Tissue

| Information | Description |
|---|---|
| **Organism** | *Arabidopsis thaliana* (Col‑0 ecotype)|
| **Tissue/Material** | Whole seedlings |
| **Experimental material** | 7-day-old Arabidopsis thaliana seedlings |

---

## 5. Experimental Conditions

### Control

Wild-type *Arabidopsis thaliana* Col-0 seedlings were grown under normal growth conditions at a constant **22 °C** with a **12-hour photoperiod**. The plants were grown on **½ Murashige and Skoog (MS) medium containing 1% sucrose and 0.7% agar**.

### Treatment

For the heat-stress treatment, **7-day-old Col-0 seedlings** were exposed to alternating temperatures of **37 °C and 22 °C**, with each temperature maintained for **12 hours**, for a total of **3 days** under a **12-hour photoperiod**.

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
        --paired --length 70
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
              │  featureCounts │
              │ Gene/TE counts │
              └───────┬───────┘
                      │
                      ▼
                  DESeq2
          Differential Expression
                      │
                      ▼
             Differentially
             Expressed Genes
                    / TEs

## Differences between the authors' pipeline and the group's pipeline
The group followed the authors' RNA-seq workflow as closely as possible using Galaxy. Both pipelines used Trim Galore, TAIR10, 
TopHat2, SAMtools, and featureCounts. The main difference was the annotation: the authors used Araport11 annotations with the TAIR10 genome, while the group used the TAIR10.57 GTF available in Galaxy.

