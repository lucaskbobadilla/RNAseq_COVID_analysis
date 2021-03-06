# Differentiating diseased and healthy human gene expression for MERS and COVID-19 using published data from 2 experiments.
This Repository shows my analysis comparing expression of SARS and COVID-19

# Main purpose

This analysis was done as a Bioinformatics course at the University of Illinois. The goal of this project was to apply an RNA-seq analysis to compare
the expression patterns between SARS and COVID-19. We also applied a simple machine learning algothim to differentiate the diseases based on expression profile.

# People involved

Lucas Kopecky Bobadilla - RNA-seq analysis
Yuanxi Fu, Shiwei Fu - Text, introduction and references
Christine Atkinson, Brendan Alexander - Machine learning analysis

# Introduction

A patient’s fight against a Coronavirus is largely dependent on the tenacity of the immune system hardcoded
in their genome. A major challenge is determining how the virus will interact with the human immune
system and influence gene expression. Identification of changes in gene expression during infection may focus
research efforts toward looking for gene expression patterns in patients suffering from the virus.
MERS and SARS are both large positive-sense RNA viruses, part of the beta coronavirus group and fall into
a highly pathogenic group that settles in the lower part of the respiratory tract. Rate of person to person
transmissibility is a major difference between MERS and SARS, with SARS-CoV-2 (COVID from here on)
being more infectious. Rabaan et al. (2020) compared the disease characteristics of MERS and SARS groups.
COVID incubation period of 7-14 days is the longest, followed by SARS-CoV (2-7 days) and MERS (5-6
days). MERS includes symptoms of fever, nonproductive cough, sore throat and diarrhea has a high mortality
rate of 34.4%. SARS has a lower fatality rate and more symptoms like fever, fatigue, nonproductive cough,
myalgia, dyspnea, expectoration, sore throat, diarrhea, dizziness, headache, nausea or vomiting.
Coronaviruses are large RNA viruses that have their positive strand RNA contained within a nucleocapsid
and outer envelope covered in glycoprotein spikes. Upon entry to the host cell, the host’s RNA polymerase
can synthesize the virus’ mRNA that codes for spike (S), membrane (M), envelope (E), nucleocapsid (N),
and possibly hemagglutinin-esterase (HE) proteins. MERS and SARS enter the cell by different mechanisms.
COVID enters a cell when the S-protein of the virus binds to the metalloprotease angiotensin-converting
enzyme 2 (ACE2) receptor on the host endothelial cells as a result of the action of protease (suggested to
be TMPRSS2) that cleaves the S-protein of SARS and allow the virus to enter the cell (Rabi et al. 2020;
Bassendine et al. 2020). ACE2 receptors are also on the surface of cells throughout the body allowing the
virus to invade many organ systems. MERS binds to dipeptidyl-peptidase 4 (DPP4) to enter human cells,
where DPP4 is a glycoprotein expressed on a variety of cells, implicated in disease states of inflammation and
diabetes and involved in glucose homeostasis, signaling and immune cell activation (Röhrborn, Wronkowitz,
and Eckel 2015). Bassendine et al. (2020) notes that modeling studies of COVID suggest that it may bind to
both ACE2 and DPP4.
Endothelial cells line the surface of blood vessels and lymphatic vessel and manage blood or lymph movement
into the tissue. Phenotypic change may increase production of by producing signaling molecules like cytokines
to communicate with other cells or by expressing adhesion molecules to allow attachment of pathogen fighting
leukocytes (Pober and Sessa 2007). Channappanavar and Perlman (2017) noted MERS and SARs present
high serum levels of pro-inflammatory cytokines and chemokines yet lack anti-inflammatory cytokines.
Cell culture experiments help define the time course of gene expression early in the stage of infection. The
Calu-3 cell is a lung epithelial cell used for viral respiratory illness studies. It is an epithelial cell derived from
a metastatic site lung adenocarcinoma of a 25-year-old male who had received prior therapy with cytoxan,
bleomycin and adriamycin. The Calu-3 cells express angiotensin-converting enzyme 2 (ACE-2), the functional
receptor of SARS-CoV, on their apical surface and form monolayers in culture (Tseng et al. 2005).
Diagnostic tools are available to diagnose SARS and MERS infections but have limitations. PCR tests may
not be able to detect the viral RNA if the viral load is low or if sample handling errors occur (Zainol Rashid et al. 2020). Rashid et al evaluated 9 rapid detection tests (RDTs) which all used detection of IgG and
IgM antibodies (Zainol Rashid et al. 2020) and noted a predictable pattern with IgM appearing before IgG,
an antibody that signals the activation of the acquired immunity system. However, serology tests are not
ideal test systems as cross-reactivity with other coronaviruses can occur. Large scale testing platforms using
CRISPR-based nucleic acid detection in microarray technologies like CARMEN hold potential for low-cost
testing for presence of pathogens from one sample (Ackerman et al. 2020).
The challenge to understand COVID-19 and develop treatment rapidly have spurred data sharing. The
types of COVID-19 related data made open include scholarly articles, de-identified patient records, digital
pathology image and genomics data. For scholarly articles, many scientific publishers have made articles
on COVID-19 free of charge. The data analytics platform Kaggle initiated a COVID-19 Open research
dataset challenge (CORD-19) (https://kaggle.com/allen-institute-for-ai/CORD-19-research-challenge). It
posted a dataset with over 59,000 scholarly articles and 10 tasks to guide the participants’ effort. The
COVID-19 research database project opened a collection of de-identified medical and pharmacy claims,
electronic health record, and mortality data(https://covid19researchdatabase.org/). However, users must
register with institutional email and go through an approval process. In terms of genomics data, NCBI’s virus
repository has accumulated more than 2000 SRAS-Cov-2 sequences from all over the world. In comparison,
the number of RNA-seq and expression counts datasets is relevantly small. Only 14 datasets are available as
of May 5th. However, with intensive research activities around the world, we expect to see more RNA-seq
data deposited in the future.
Having open data encourages data reuse. NextStrain’s analyses of the combined 2000+ virus sequence data
has helped users to track the spread around the world(https://nextstrain.org/). The website also actively
disputes misinformation with narratives in multiple languages. On the other hand, analysis of combined
COVID-19 gene expression data has not been seen, due to the scarcity of the RNA-seq data deposited
so far. Potential benefits from such analysis include detecting signals that are too weak to be detected
in one experiment(Shah, Balakrishnan, and Wainwright 2016), discovering most consistently differentially
expressed genes(Rung and Brazma 2013), and establishing unified theory across disease types(Baschal et
al. 2020). When combining RNA-seq datasets for analysis, one key step is to remove the batch effect from
different studies, and the ComBat function in SVA package has been the most commonly used tool for such
purpose(Wang et al. 2018; Danielsson et al. 2015).
In this study we took samples from two GEO datasets (GSE147507 and GSE122876). Both datasets were
single read RNA-seq files from Calu-3 cells infected with the virus after 24 hours, one infected with MERS
and the other infected with COVID. We plan to investigate the difference between their gene expression
profile and build a machine learning model to automatically classify disease types by gene expression profile.


# Material and methods


## Data source and pre-processing

Data for this comparison were extracted from two GEO datasets (GSE147507 and GSE122876). Both datasets were single read RNA-seq files from Calu-3 cells infected with the virus after 24h. Both experiments were conducted using triplicates for each condition. Raw fastq files from both datasets were downloaded from NCBI using the SRA Toolkit and data quality was accessed using fastQC reports. All raw fastq files were trimmed using Trimmomatic1 set for LEADING:28, TRAILING:28, SLIDINGWINDOW:4:30 and MINLEN:50. After trimming low quality reads, libraries we pseudo-aligned to the homo sapiens genome GRCh38 using Kallisto without bootstrapping to get the transcript abundance2.



# Analysis

## Packages


```{r message=FALSE, warning=FALSE}
library(sva)
library(edgeR)
library(tximport)
library(tidyverse)
library(biomaRt)
library(DESeq2)
library(RColorBrewer)
library(pheatmap)
library(ggVennDiagram)
library(goseq)
library(kableExtra)
```



## metadata

```{r meta data covid}
# sample information - meta data
samples <-read.table("samples.txt", header=TRUE)
samples$condition <- factor(samples$condition, levels = c("Control","COVID19", "MERS"))
samples$batch <- factor(samples$batch)
rownames(samples) <- samples$sample
samples <- samples[,-1]

kable(samples)
```

## Load biomart query

```{r}
#biomart query
   
ensembl <- useMart("ensembl", dataset = "hsapiens_gene_ensembl")
tx2gene <- getBM(attributes = c("ensembl_transcript_id_version", "ensembl_gene_id","hgnc_symbol", "chromosome_name"), mart = ensembl) 


```

## Load Abundance reads


```{r get  data}

#get abundance files path
files <- file.path("data/all_data/", rownames(samples), "abundance.tsv")
names(files) <- rownames(samples)
files

# Load files using tximport - transcript level
txi.kallisto.covid <- tximport(files, type = "kallisto", tx2gene = tx2gene, txOut = TRUE)

#change to gene level

gene.kallisto.covid <- summarizeToGene(txi.kallisto.covid,tx2gene)

```

## Apply model matrix and Combat_seq function

```{r}

# matrix design
full.mat <- model.matrix(~condition, data = samples)

null.mat <- model.matrix(~1, data = samples)

#solving batch effect
batch <- samples$batch
group <- samples$condition
adjusted <- ComBat_seq(gene.kallisto.covid$counts, batch=batch, group=group)

# transforming data to integer
adj <- sapply(data.frame(adjusted), as.integer)
rownames(adj) <- rownames(adjusted)


dds <- DESeqDataSetFromMatrix(countData = adj,
                              colData = samples,
                              design = ~ condition)

rld <- rlog(dds)
plotPCA(rld, intgroup = "condition")
#ggsave(file = "PCA.jpeg", dpi = 300, units = "cm", height = 10, width = 24)
```

## Apply EdgeR model and plot dispersion

```{r}

dgList <- DGEList(counts=adjusted, genes=rownames(adjusted), group=samples$condition)

countsPerMillion <- cpm(dgList) #get counts
countCheck <- countsPerMillion > 1 # create a conditional matrix for values > 1
keep <- which(rowSums(countCheck) >= 1) #filter values
dgList <- dgList[keep,]

dgList_norm <- calcNormFactors(dgList, method="TMM")
?calcNormFactors
#dispersion
disp <- estimateDisp(dgList_norm, design=full.mat, robust=TRUE)

## plot dispersions
plotBCV(disp)



```

## volcano plot and DEG for COVID

```{r DEG analysis covid}
# DEG analysis

fit <- glmFit(disp, full.mat)
lrt <- glmLRT(fit, coef=2) # fit only for covid vs control

DEG_genes_covid <- topTags(lrt, adjust.method = "BH", p.value = 0.001, n = 400) # get genes significant at FDR < 0.001


# get all genes results
result_EDGER_covid <- topTags(lrt, n=nrow(lrt$table), adjust.method = "BH")

# get gene IDs from transcripts
FDR_genes_covid <- result_EDGER_covid$table # convert to dataframe

FDR_genes_significant_covid <- DEG_genes_covid$table # convert to dataframe

plotMD(lrt) # all significant ones

FDR_genes_covid %>% 
  ggplot(aes(y = -log10(FDR), x = logFC)) +
  geom_point() +
  geom_point(aes(y = -log10(FDR), x = logFC), col ="red", data = FDR_genes_significant_covid) + theme_light() +
  labs(title = "Volcano plot - COVID vs Control")
#ggsave("volcano_COVID.jpeg", dpi = 300)



```

## Volcano plot for MERS

```{r DEG results mers}
# DEG analysis


lrt <- glmLRT(fit, coef=3) # fit model for MERS vs control
DEG_genes_mers <- topTags(lrt, adjust.method = "BH", p.value = 0.001, n = 400)
result_EDGER_mers <- topTags(lrt, n=nrow(lrt$table), adjust.method = "BH")

# get gene IDs from transcripts
FDR_genes_mers <- result_EDGER_mers$table

FDR_genes_significant_mers <- DEG_genes_mers$table 

#plotMD(lrt) # all significant ones

FDR_genes_mers %>% 
  ggplot(aes(y = -log10(FDR), x = logFC)) +
  geom_point() +
  geom_point(aes(y = -log10(FDR), x = logFC), col ="red", data = FDR_genes_significant_mers) + theme_light() +
  labs(title = "Volcano plot - MERS vs Control")

#ggsave("volcano_MERS.jpeg", dpi = 300)

```


# Find genes in common between comparison with control

```{r find common genes}

# find genes in top common genes between disease when compared to control
common_disease <- FDR_genes_significant_covid %>% 
  dplyr::select(genes, logFC_covid = logFC,FDR_covid = FDR) %>% 
  inner_join(FDR_genes_significant_mers %>% 
              dplyr::select(genes, logFC_mers= logFC,FDR_mers = FDR),
             by ="genes")

write.csv(common_disease, "top100_common_genes.csv")

common_disease_tidy <- common_disease %>% 
  dplyr::select(genes, covid=FDR_covid,mers=FDR_mers) %>% 
  gather(covid:mers, key = "condition", value = "FDR") %>% 
  left_join(common_disease %>% 
  dplyr::select(genes, covid=logFC_covid,mers=logFC_mers) %>% 
  gather(covid:mers, key = "condition", value = "logFC"))


common_genes <- common_disease %>% 
  dplyr::select(ensembl_gene_id=genes,everything() ) %>% 
  inner_join(tx2gene %>% dplyr::select(-ensembl_transcript_id_version)) %>%
  distinct() %>% 
  dplyr::select(hgnc_symbol, ensembl_gene_id,
                chromosome_name, logFC_covid,
                logFC_mers) %>% 
  arrange(chromosome_name, desc(logFC_covid))


all_genes <- FDR_genes_significant_covid %>%
  mutate(condition = "COVID") %>% 
  full_join(FDR_genes_significant_covid %>% 
              mutate(condition = "MERS"))

#write_csv(all_genes,"top400_genes.csv")

# get all significant genes that were common

common_disease_all <- FDR_genes_covid %>% 
  filter(FDR <=0.001) %>% 
  dplyr::select(genes, logFC_covid = logFC,FDR_covid = FDR) %>% 
  inner_join(FDR_genes_mers %>% 
  filter(FDR <=0.001) %>% 
              dplyr::select(genes, logFC_mers= logFC,FDR_mers = FDR),
             by ="genes")


common_disease_all <- common_disease_all %>% 
  dplyr::select(ensembl_gene_id=genes,everything() ) %>% 
  inner_join(tx2gene %>% 
               dplyr::select(-ensembl_transcript_id_version)) %>%
  distinct() %>% 
  dplyr::select(hgnc_symbol, ensembl_gene_id,
                chromosome_name, logFC_covid,
                logFC_mers) %>% 
  arrange(chromosome_name, desc(logFC_covid))

#write_csv(common_disease_all, "common_genes.csv")


#cytokine genes plot
common_disease_all %>% arrange(desc(logFC_covid), desc(logFC_mers)) %>% 
  filter(str_detect(hgnc_symbol, "^IL")) %>% 
  gather(logFC_covid:logFC_mers, key = "Disease", value = "LogFC") %>% 
  separate(Disease, into = c("disc", "Disease"), sep = "_") %>% 
  ggplot(aes(x = hgnc_symbol, y = LogFC, fill = Disease)) +
  geom_col(position = position_dodge(.5), col = "black",width = 0.5) +
  geom_hline(yintercept = 0) +
  theme_light() +
  scale_fill_brewer(palette="Dark2") +
  labs(x = "Gene", title = "Differentially expressed genes involved with cytokine response")

#ggsave("IL_genes.jpeg", dpi = 300, units = "cm", width = 24, height = 12)

#GBP genes
common_disease_all %>% arrange(desc(logFC_covid), desc(logFC_mers)) %>% 
  filter(str_detect(hgnc_symbol, "^GBP")) %>% 
  gather(logFC_covid:logFC_mers, key = "Disease", value = "LogFC") %>% 
  separate(Disease, into = c("disc", "Disease"), sep = "_") %>% 
  ggplot(aes(x = hgnc_symbol, y = LogFC, fill = Disease)) +
  geom_col(position = position_dodge(.5), col = "black",width = 0.5) +
  geom_hline(yintercept = 0) +
  theme_light() +
  scale_fill_brewer(palette="Dark2") +
  labs(x = "Gene", title = "Differentially expressed Guanylate-binding proteins (GBP) genes")

#ggsave("GBP_genes.jpeg", dpi = 300, units = "cm", width = 24, height = 12)


#TNF genes

common_disease_all %>% arrange(desc(logFC_covid), desc(logFC_mers)) %>% 
  filter(str_detect(hgnc_symbol, "^TNF")) %>% 
  gather(logFC_covid:logFC_mers, key = "Disease", value = "LogFC") %>% 
  separate(Disease, into = c("disc", "Disease"), sep = "_") %>% 
  ggplot(aes(x = hgnc_symbol, y = LogFC, fill = Disease)) +
  geom_col(position = position_dodge(.5), col = "black",width = 0.5) +
  geom_hline(yintercept = 0) +
  theme_light() +
  scale_fill_brewer(palette="Dark2") +
  labs(x = "Gene", title = "Differentially expressed tumour necrosis factor (TNF) genes")

#ggsave("TNF_genes.jpeg", dpi = 300, units = "cm", width = 24, height = 12)

```

## Venn diagram

```{r}
#venn diagram


venn_mers <- FDR_genes_mers %>% 
  filter(FDR <=0.001)

rownames(venn_mers) <- venn_mers$genes

venn_covid <- FDR_genes_covid %>% 
  filter(FDR <=0.001)

rownames(venn_covid) <- venn_covid$genes

venn_plot <- list(COVID = rownames(venn_covid), 
          MERS = rownames(venn_mers))


ggVennDiagram(venn_plot)
#ggsave(file = "venn_diagram.jpeg", dpi = 300, height = 10, width = 20, units = "cm")

```


## list of genes up and down regulated

```{r}
# covid

FDR_genes_significant_covid %>% 
  mutate(DEG = if_else(logFC < 0, "Down-regulated", "Up-regulated")) %>% 
  group_by(DEG) %>% 
  summarize(DEG_count = n())

FDR_genes_significant_mers %>% 
  mutate(DEG = if_else(logFC < 0, "Down-regulated", "Up-regulated")) %>% 
  group_by(DEG) %>% 
  summarize(DEG_count = n())

  
```

## GO term annotation

```{r}

# get GO terms

query <- common_disease_all %>% 
   mutate(DEG_covid = if_else(logFC_covid < 0, "Down-regulated", "Up-regulated"),
          DEG_mers = if_else(logFC_covid < 0, "Down-regulated", "Up-regulated")) %>% 
  dplyr::select(hgnc_symbol, DEG_covid, DEG_mers,chromosome_name)

common_disease_all %>% 
  arrange(desc(logFC_covid),desc(logFC_mers))



listAttributes(ensembl)

query_result <- getBM(attributes = c("hgnc_symbol", "go_id",
                     "name_1006","definition_1006","namespace_1003"),
      filters = "hgnc_symbol",
      values = query$hgnc_symbol,
      mart = ensembl)


Enrichment_analysis <- query %>% 
  left_join(query_result) %>% 
  dplyr::select(-chromosome_name) %>% 
  filter(namespace_1003 == "biological_process") %>% 
  dplyr::select(-namespace_1003)

colnames(Enrichment_analysis) <- c("gene", "COVID", "MERS",
                                   "go_ID", "Biological_process",
                                   "Biological_description")

write.csv(Enrichment_analysis,"Enrichment_analysis.csv")

```

## GO-seq enrichment analysis

```{r}
library("org.Hs.eg.db")
deg_genes <- as.vector(common_disease_all$ensembl_gene_id)
measure_genes <- as.vector(FDR_genes_mers$genes)

gene_vector <- as.integer(measure_genes%in%deg_genes)
names(gene_vector) <- measure_genes


pwf <- nullp(gene_vector,"hg19","ensGene")
head(pwf)

GO.wall <- goseq(pwf,"hg19","ensGene",test.cats=c("GO:BP"))

GO.wall %>% 
    top_n(30, wt=-over_represented_pvalue) %>% 
    mutate(hitsPerc=numDEInCat*100/numInCat) %>% 
    ggplot(aes(x=hitsPerc, 
               y=term, 
               colour=over_represented_pvalue, 
               size=numDEInCat)) +
        geom_point() +
        expand_limits(x=0) +
        labs(x="Hits (%)", y="GO term", colour="p-value", size="Count", title = "GO terms - top 30")

#ggsave("GO-terms.jpeg", dpi = 300)


```
